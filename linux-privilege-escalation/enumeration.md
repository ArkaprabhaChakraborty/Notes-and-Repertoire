---
description: A good enumeration helps in finding the right escalation technique
---

# Enumeration

After gaining access to the system, enumeration is key to know the right exploitation/privilege escalation technique.

### Finding host names

Using the `hostname` command, we can find the host name associated with the target system.

```bash
hostname
```

```
$ hostname
wade7363
```

Although this value can easily be changed or have a relatively meaningless string (e.g. Ubuntu-3487340239), in some cases, it can provide information about the target system’s role within the corporate network (e.g. SQL-PROD-01 for a production SQL server).

### Kernel details using uname

The `uname` command will print system information giving us additional detail about the kernel used by the system. This will be useful when searching for any potential kernel vulnerabilities that could lead to privilege escalation.

```bash
uname -a
```

{% code overflow="wrap" %}
```
Linux wade7363 3.13.0-24-generic #46-Ubuntu SMP Thu Apr 10 19:11:08 UTC 2014 x86_64 x86_64 x86_64 GNU/Linux
```
{% endcode %}

### Information from the proc file system

The proc file system (procfs) provides information about the target system processes.&#x20;

```bash
cat /proc/version
```

{% code overflow="wrap" %}
```
Linux version 3.13.0-24-generic (buildd@panlong) (gcc version 4.8.2 (Ubuntu 4.8.2-19ubuntu1) ) #46-Ubuntu SMP Thu Apr 10 19:11:08 UTC 2014
```
{% endcode %}

### Finding system information from /etc/issue

Systems can also be identified by looking at the `/etc/issue` file. This file usually contains some information about the operating system but can easily be customized or changed.&#x20;

```bash
cat /etc/issue
```

```
Ubuntu 14.04 LTS \n \l
```

### Using the ps command

The `ps` command is an effective way to see the running processes on a Linux system.&#x20;

```bash
ps -el       # View all running processes with all identifiers
```

```
ps -el
F S   UID   PID  PPID  C PRI  NI ADDR SZ WCHAN  TTY          TIME CMD
4 S     0     1     0  0  80   0 -  8411 poll_s ?        00:00:01 init
1 S     0     2     0  0  80   0 -     0 kthrea ?        00:00:00 kthreadd
1 S     0     3     2  0  80   0 -     0 smpboo ?        00:00:00 ksoftirqd/0
1 S     0     5     2  0  60 -20 -     0 worker ?        00:00:00 kworker/0:0H
1 S     0     6     2  0  80   0 -     0 worker ?        00:00:00 kworker/u30:0
1 S     0     7     2  0  80   0 -     0 rcu_gp ?        00:00:00 rcu_sched
```

```bash
ps -A       # View all running processes
```

```
  PID TTY          TIME CMD
    1 ?        00:00:01 init
    2 ?        00:00:00 kthreadd
    3 ?        00:00:00 ksoftirqd/0
    5 ?        00:00:00 kworker/0:0H
    6 ?        00:00:00 kworker/u30:0
    7 ?        00:00:00 rcu_sched
```

```bash
ps axjf    # View process tree
```

```
PPID   PID  PGID   SID TTY      TPGID STAT   UID   TIME COMMAND
   1   914   914   914 tty2       914 Ss+      0   0:00 /sbin/getty -8 38400 tty2
    1   915   915   915 tty3       915 Ss+      0   0:00 /sbin/getty -8 38400 tty3
    1   917   917   917 ?           -1 Ssl      0   0:00 /usr/bin/amazon-ssm-agent
  917  1184  1184   917 ?           -1 Sl       0   0:00  \_ /usr/bin/ssm-agent-wrkr
    1   918   918   918 ?           -1 Ssl      0   0:00 NetworkManager
    1   920   920   920 tty6       920 Ss+      0   0:00 /sbin/getty -8 38400 tty6
    1   953   953   953 ?           -1 Ss     106   0:00 /usr/sbin/kerneloops
    1   974   974   974 ?           -1 Ss       0   0:00 /usr/sbin/sshd -D
  974  1540  1540  1540 ?           -1 Ss       0   0:00  \_ sshd: karen [priv]  
 1540  1641  1540  1540 ?           -1 R     1001   0:00      \_ sshd: karen@pts/4
```

The `aux` option will show processes for all users (a), display the user that launched the process (u), and show processes that are not attached to a terminal (x).

```bash
ps aux
```

```
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.2  33644  2800 ?        Ss   14:31   0:01 /sbin/init
root         2  0.0  0.0      0     0 ?        S    14:31   0:00 [kthreadd]
root         3  0.0  0.0      0     0 ?        S    14:31   0:00 [ksoftirqd/0]
root       918  0.0  0.7 361536  7604 ?        Ssl  14:31   0:00 NetworkManager
kernoops   953  0.0  0.0  37144  1008 ?        Ss   14:31   0:00 /usr/sbin/kerneloops
root       974  0.0  0.2  61364  3028 ?        Ss   14:31   0:00 /usr/sbin/sshd -D
whoopsie  1107  0.0  0.5 371672  5312 ?        Ssl  14:31   0:00 whoopsie
```

### Dumping Environment variables

The `env` command dumps all the environment variables available in the current shell session.

```bash
env
```

{% code overflow="wrap" %}
```
MAIL=/var/mail/karen
USER=karen
SSH_CLIENT=10.17.30.161 38138 22
HOME=/home/karen
SSH_TTY=/dev/pts/4
QT_QPA_PLATFORMTHEME=appmenu-qt5
LOGNAME=karen
TERM=xterm-256color
XDG_SESSION_ID=1
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games
XDG_RUNTIME_DIR=/run/user/1001
LANG=en_US.UTF-8
SHELL=/bin/sh
PWD=/
SSH_CONNECTION=10.17.30.161 38138 10.10.14.143 22
```
{% endcode %}

The `PATH` variable may have a compiler or a scripting language (e.g. Python) that could be used to run code on the target system or leveraged for privilege escalation.

### The sudo -l for Finding commands that the user can run with root privileges

The target system may be configured to allow users to run some (or all) commands with root privileges. The `sudo -l` command can be used to list all commands your user can run using `sudo`.

```bash
sudo -l
```

```
Matching Defaults entries for fvalkyrie on faraday:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin, use_pty

User fvalkyrie may run the following commands on faraday:
    (ALL : ALL) ALL
```

#### Finding User Id and Group Id&#x20;

The `id` command will provide a general overview of the user’s privilege level and group memberships. The `id` command can also be used to obtain the same information for another user.

```bash
id
```

```
uid=1001(karen) gid=1001(karen) groups=1001(karen)
```

```bash
id matt
```

```
uid=1000(matt) gid=1000(matt) groups=1000(matt),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),108(lpadmin),124(sambashare)
```

### Infamous /etc/passwd

The `/etc/passwd` can be use to dump out user information and their access levels.

```bash
cat /etc/passwd
```

```
speech-dispatcher:x:110:29:Speech Dispatcher,,,:/var/run/speech-dispatcher:/bin/sh
avahi:x:111:117:Avahi mDNS daemon,,,:/var/run/avahi-daemon:/bin/false
lightdm:x:112:118:Light Display Manager:/var/lib/lightdm:/bin/false
colord:x:113:121:colord colour management daemon,,,:/var/lib/colord:/bin/false
hplip:x:114:7:HPLIP system user,,,:/var/run/hplip:/bin/false
pulse:x:115:122:PulseAudio daemon,,,:/var/run/pulse:/bin/false
matt:x:1000:1000:matt,,,:/home/matt:/bin/bash
karen:x:1001:1001::/home/karen:
sshd:x:116:65534::/var/run/sshd:/usr/sbin/nologin
```

This can be refined to find just the user names using:

```bash
cat /etc/passwd | cut -d ":" -f 1
```

```
saned
whoopsie
speech-dispatcher
avahi
lightdm
colord
hplip
pulse
matt
karen
sshd
```

Another approach is to grep for `home` in the results.

```
cat /etc/passwd | grep home
```

```
matt:x:1000:1000:matt,,,:/home/matt:/bin/bash
karen:x:1001:1001::/home/karen:
```

### Dumping Session history

The history command can be useful for finding secret keys and useful credentials within the shell session.

```bash
history
```

```
history
    5  sudo apt-get upgrade
    7  $ sudo add-apt-repository ppa:yannubuntu/boot-repair && sudo apt update\n$ sudo apt install -y boot-repair && boot-repair\n$ sudo reboot
    9  lscpu
   10  nvidia-smi
```

### Confirm target as pivoting point and find adjacent machines&#x20;

The target system may be a pivoting point to another network. The `ifconfig` command will give us information about the network interfaces of the system.

```bash
ifconfig
```

```
eth0      Link encap:Ethernet  HWaddr 02:4b:e9:0b:4c:63  
          inet addr:10.10.14.143  Bcast:10.10.255.255  Mask:255.255.0.0
          inet6 addr: fe80::4b:e9ff:fe0b:4c63/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:9001  Metric:1
          RX packets:776 errors:0 dropped:0 overruns:0 frame:0
          TX packets:767 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:66352 (66.3 KB)  TX bytes:153955 (153.9 KB)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:133 errors:0 dropped:0 overruns:0 frame:0
          TX packets:133 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:9505 (9.5 KB)  TX bytes:9505 (9.5 KB)
```

Use the `ip route` command to see which network routes exist.

```bash
ip route
```

```
default via 10.10.0.1 dev eth0 
10.10.0.0/16 dev eth0  proto kernel  scope link  src 10.10.14.143 
169.254.0.0/16 dev eth0  scope link  metric 1000 
```

### Looking into existing communications

Using the `netstat` command we can have information about the existing communications.&#x20;

```bash
netstat -a
```

```
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State      
tcp        0      0 *:ssh                   *:*                     LISTEN     
tcp        0      0 localhost:ipp           *:*                     LISTEN     
tcp        0      1 ip-10-10-81-154.e:37517 ubuntu-mirror-2.ps:http SYN_SEN
```

```bash
netstat -at     # t is for TCP. Can be used with u to show UDP connections
```

```
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State      
tcp        0      0 *:ssh                   *:*                     LISTEN     
tcp        0      0 localhost:ipp           *:*                     LISTEN   
```

To find all the listening ports we can use `-l` which list ports in “listening” mode. These ports are open and ready to accept incoming connections. This can be used with the `t` option to list only ports that are listening using the TCP protocol.

```bash
netstat -l    # lists all listening processes
```

```
netstat -l
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State      
tcp        0      0 *:ssh                   *:*                     LISTEN     
tcp        0      0 localhost:ipp           *:*                     LISTEN     
tcp6       0      0 [::]:ssh                [::]:*                  LISTEN     
tcp6       0      0 ip6-localhost:ipp       [::]:*                  LISTEN
Active UNIX domain sockets (only servers)
Proto RefCnt Flags       Type       State         I-Node   Path
unix  2      [ ACC ]     STREAM     LISTENING     10074    /tmp/.X11-unix/X0
unix  2      [ ACC ]     STREAM     LISTENING     10513    /var/run/cups/cups.sock
unix  2      [ ACC ]     STREAM     LISTENING     10073    @/tmp/.X11-unix/X0
unix  2      [ ACC ]     STREAM     LISTENING     11311    /run/user/112/puls
```

To get the network usage statistics we can use the `-s` flag with `-t` or `-u`

```bash
netstat -st
```

```
Tcp:
    97 active connections openings
    3 passive connection openings
    52 failed connection attempts
    0 connection resets received
    1 connections established
    538 segments received
    469 segments send out
    70 segments retransmited
    0 bad segments received.
    52 resets sent
UdpLite:
TcpExt:
    2 TCP sockets finished time wait in fast timer
    5 delayed acks sent
    Quick ack mode was activated 1 times
    17 packet headers predicted
    82 acknowledgments not containing data payload received
    142 predicted acknowledgments
    13 other TCP timeouts
    1 DSACKs sent for old packets
    TCPRcvCoalesce: 3
```

To know about the interface statistics, like `eth0` or `tun0`, we can use the `-i` flag.

```bash
netstat -i
```

```bash
Kernel Interface table
Iface   MTU Met   RX-OK RX-ERR RX-DRP RX-OVR    TX-OK TX-ERR TX-DRP TX-OVR Flg
eth0       9001 0       683      0      0 0           699      0      0      0 BMRU
lo        65536 0       125      0      0 0           125      0      0      0 LRU
```

The super command used by most is `-ano` which means `-a` Display all sockets `-n` Do not resolve names `-o` Display timers and `-p` to show the PID.

```bash
netstat -anop
```

### Using the Find command&#x20;

The `find` command can be used to find some fascinating files.

#### Find development tools or languages of help

```bash
find / -name perl*
find / -name python*
find / -name gcc*
```

#### Find a simple file in current directory

```bash
find . -name flag*.txt 2>/dev/null
```

#### Search the entire target for a file&#x20;

```bash
find / -name flag*.txt 2>/dev/null
```

#### Find a directory in the target

```bash
find / -type d -name config 2>/dev/null
```

#### Find files that are readable, writable, and executable by all users

```bash
find / -type f -perm 0777 2>/dev/null
```

#### Find executables

```bash
find / -perm a=x 2>/dev/null
```

#### Find all files under /home directory for a particular user

```bash
find /home -user frank 2>/dev/null
```

#### Find files modified by time index and size

```bash
find / -mtime 10             # find files that were modified in the last 10 days
find / -atime 10             # find files that were accessed in the last 10 day
find / -cmin -60             # find files changed within the last hour (60 minutes)
find / -amin -60             # find files accesses within the last hour (60 minutes)
find / -size 50M             # find files with a 50 MB size
```

#### Find world writable folders

```bash
find / -writable -type d 2>/dev/null
find / -perm -222 -type d 2>/dev/null
find / -perm -o w -type d 2>/dev/null
```

#### Find world executable folders

```bash
find / -perm -o x -type d 2>/dev/null
```

#### Find Files with SUID set&#x20;

```bash
find / -perm -u=s -type f 2>/dev/null
```
