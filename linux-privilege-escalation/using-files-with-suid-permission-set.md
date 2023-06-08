# Using files with SUID permission set

## What is SUID?

Set owner User ID&#x20;

## Find files with SUID set

```
find / -user root -perm -4000 -exec ls -ldb {} \;
```

```
find / -perm -u=s -type f 2>/dev/null
```

## Abusing systemctl

#### Reverse shell to root user

