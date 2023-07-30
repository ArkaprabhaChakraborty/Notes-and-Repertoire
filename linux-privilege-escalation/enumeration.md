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
root         5  0.0  0.0      0     0 ?        S<   14:31   0:00 [kworker/0:0H]
root         6  0.0  0.0      0     0 ?        S    14:31   0:00 [kworker/u30:0]
root         7  0.0  0.0      0     0 ?        S    14:31   0:00 [rcu_sched]
root         8  0.0  0.0      0     0 ?        R    14:31   0:00 [rcuos/0]
root         9  0.0  0.0      0     0 ?        S    14:31   0:00 [rcuos/1]
root       918  0.0  0.7 361536  7604 ?        Ssl  14:31   0:00 NetworkManager
root       920  0.0  0.0  20016   968 tty6     Ss+  14:31   0:00 /sbin/getty -8 38400 tty6
kernoops   953  0.0  0.0  37144  1008 ?        Ss   14:31   0:00 /usr/sbin/kerneloops
root       974  0.0  0.2  61364  3028 ?        Ss   14:31   0:00 /usr/sbin/sshd -D
root      1011  0.0  0.0   4368   700 ?        Ss   14:31   0:00 acpid -c /etc/acpi/events -s /var/run/acpid.socket
root      1012  0.0  0.0  23656  1012 ?        Ss   14:31   0:00 cron
root      1082  0.0  0.0  20016   964 tty1     Ss+  14:31   0:00 /sbin/getty -8 38400 tty1
root      1087  0.0  0.3  75352  3396 ?        Ss   14:31   0:00 /usr/sbin/cups-browsed
root      1106  0.0  0.5 295864  5816 ?        Sl   14:31   0:00 /usr/lib/policykit-1/polkitd --no-debug
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







