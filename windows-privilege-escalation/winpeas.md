---
description: WinPEAS Enumeration
---

# WinPEAS

```
C:\PrivEsc>.\winPEASany.exe
```

{% code fullWidth="true" %}
```html
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<!-- This file was created with the aha Ansi HTML Adapter. https://github.com/theZiz/aha -->
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta http-equiv="Content-Type" content="application/xml+xhtml; charset=UTF-8" />
<title>stdin</title>
</head>
<body>
<pre>
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   Creating Dynamic lists, this could take a while, please wait...</span>
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   - Checking if domain...</span>
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   - Getting Win32_UserAccount info...</span>
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   - Creating current user groups list...</span>
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   - Creating active users list...</span>
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   - Creating disabled users list...</span>
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   - Admin users list...</span>
<span style="color:blue;">     
             </span><span style="font-weight:bold;color:green;">*((,.,/((((((((((((((((((((/,  */               
      ,/*,..*((((((((((((((((((((((((((((((((((,           
    ,*/((((((((((((((((((/,  .*//((//**, .*(((((((*       
    ((((((((((((((((</span><span style="font-weight:bold;color:blue;">**********/</span><span style="font-weight:bold;color:green;">########## .(* ,(((((((   
    (((((((((((/</span><span style="font-weight:bold;color:blue;">********************/</span><span style="font-weight:bold;color:green;">####### .(. (((((((
    ((((((..</span><span style="font-weight:bold;color:blue;">******************</span>/@@@@@/<span style="color:blue;">***/</span><span style="font-weight:bold;color:green;">###### ./(((((((
    ,,....</span><span style="font-weight:bold;color:blue;">********************</span>@@@@@@@@@@<span style="color:blue;">(***,</span><span style="font-weight:bold;color:green;">#### .//((((((
    , ,..</span><span style="font-weight:bold;color:blue;">********************</span>/@@@@@%@@@@<span style="color:blue;">/********</span><span style="font-weight:bold;color:green;">##((/ /((((
    ..((###########</span><span style="font-weight:bold;color:blue;">*********</span>/%@@@@@@@@@<span style="color:blue;">/************</span><span style="font-weight:bold;color:green;">,,..((((
    .(##################(/</span><span style="font-weight:bold;color:blue;">******</span>/@@@@@<span style="color:blue;">/***************</span><span style="font-weight:bold;color:green;">.. /((
    .(#########################(/</span><span style="font-weight:bold;color:blue;">**********************</span><span style="font-weight:bold;color:green;">..*((
    .(##############################(/</span><span style="font-weight:bold;color:blue;">*****************</span><span style="font-weight:bold;color:green;">.,(((
    .(###################################(/</span><span style="font-weight:bold;color:blue;">************</span><span style="font-weight:bold;color:green;">..(((
    .(#######################################(</span><span style="font-weight:bold;color:blue;">*********</span><span style="font-weight:bold;color:green;">..(((
    .(#######(,.***.,(###################(..***.</span><span style="font-weight:bold;color:blue;">*******</span><span style="font-weight:bold;color:green;">..(((
    .(#######*(#####((##################((######/(</span><span style="font-weight:bold;color:blue;">*****</span><span style="font-weight:bold;color:green;">..(((
    .(###################(/***********(##############(...(((
    .((#####################/*******(################.((((((
    .(((############################################(..((((
    ..(((##########################################(..(((((
    ....((########################################( .(((((
    ......((####################################( .((((((
    (((((((((#################################(../((((((
        (((((((((/##########################(/..((((((
              (((((((((/,.  ,*//////*,. ./(((((((((((((((.
                 (((((((((((((((((((((((((((((/</span>

<span style="font-weight:bold;color:olive;">ADVISORY: </span><span style="font-weight:bold;color:blue;">winpeas should be used for authorized penetration testing and/or educational purposes only.Any misuse of this software will not be the responsibility of the author or of any other collaborator. Use it at your own networks and/or with the network owner's permission.

</span><span style="font-weight:bold;color:olive;">  WinPEAS </span><span style="font-weight:bold;color:green;">vBETA VERSION, Please if you find any issue let me know in https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/issues</span><span style="color:olive;"> by carlospolop</span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Leyend:</span>
<span style="font-weight:bold;color:red;">         Red</span><span style="font-weight:bold;color:gray;">                Indicates a special privilege over an object or something is misconfigured</span>
<span style="font-weight:bold;color:green;">         Green</span><span style="font-weight:bold;color:gray;">              Indicates that some protection is enabled or something is well configured</span>
<span style="color:teal;">         Cyan</span><span style="font-weight:bold;color:gray;">               Indicates active users</span>
<span style="color:blue;">         Blue</span><span style="font-weight:bold;color:gray;">               Indicates disabled users</span>
<span style="font-weight:bold;color:olive;">         LightYellow</span><span style="font-weight:bold;color:gray;">        Indicates links</span>

<span style="color:olive;">   [?] </span><span style="font-weight:bold;color:blue;">You can find a Windows local PE Checklist here: </span><span style="font-weight:bold;color:olive;">https://book.hacktricks.xyz/windows/checklist-windows-privilege-escalation</span>


<span style="font-weight:bold;color:teal;">  ==========================================(</span><span style="color:olive;">System Information</span><span style="font-weight:bold;color:teal;">)==========================================</span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Basic System Information</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">T1082&amp;T1124&amp;T1012&amp;T1497&amp;T1212</span><span style="font-weight:bold;color:olive;">)</span>
<span style="color:olive;">   [?] </span><span style="font-weight:bold;color:blue;">Check if the Windows versions is vulnerable to some known exploit </span><span style="font-weight:bold;color:olive;">https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#kernel-exploits</span>
<span style="font-weight:bold;color:gray;">    Hostname: </span>WIN-QBA94KB3IOF
<span style="font-weight:bold;color:gray;">    ProductName: </span>Windows Server 2019 Standard Evaluation
<span style="font-weight:bold;color:gray;">    EditionID: </span>ServerStandardEval
<span style="font-weight:bold;color:gray;">    ReleaseId: </span>1809
<span style="font-weight:bold;color:gray;">    BuildBranch: </span>rs5_release
<span style="font-weight:bold;color:gray;">    CurrentMajorVersionNumber: </span>10
<span style="font-weight:bold;color:gray;">    CurrentVersion: </span>6.3
<span style="font-weight:bold;color:gray;">    Architecture: </span>AMD64
<span style="font-weight:bold;color:gray;">    ProcessorCount: </span>1
<span style="font-weight:bold;color:gray;">    SystemLang: </span>en-US
<span style="font-weight:bold;color:gray;">    KeyboardLang: </span>English (United States)
<span style="font-weight:bold;color:gray;">    TimeZone: </span>(UTC-08:00) Pacific Time (US &amp; Canada)
<span style="font-weight:bold;color:gray;">    IsVirtualMachine: </span>False
<span style="font-weight:bold;color:gray;">    Current Time: </span>7/20/2025 7:22:14 AM
<span style="font-weight:bold;color:gray;">    HighIntegrity: </span>False
<span style="font-weight:bold;color:gray;">    PartOfDomain: </span>False
<span style="font-weight:bold;color:gray;">    Hotfixes: </span><span style="font-weight:bold;color:green;">KB4514366, KB4512577, KB4512578, </span>

<span style="color:olive;">  [?] </span><span style="font-weight:bold;color:blue;">Windows vulns search powered by </span><span style="font-weight:bold;color:red;">Watson</span><span style="font-weight:bold;color:blue;">(https://github.com/rasta-mouse/Watson)</span>
    OS Build Number: 17763
<span style="font-weight:bold;color:red;">       [!] CVE-2019-1315 : VULNERABLE</span>
<span style="font-weight:bold;color:red;">        [&gt;] https://offsec.almond.consulting/windows-error-reporting-arbitrary-file-move-eop.html</span>

<span style="font-weight:bold;color:red;">       [!] CVE-2019-1385 : VULNERABLE</span>
<span style="font-weight:bold;color:red;">        [&gt;] https://www.youtube.com/watch?v=K6gHnr-VkAg</span>

<span style="font-weight:bold;color:red;">       [!] CVE-2019-1388 : VULNERABLE</span>
<span style="font-weight:bold;color:red;">        [&gt;] https://github.com/jas502n/CVE-2019-1388</span>

<span style="font-weight:bold;color:red;">       [!] CVE-2019-1405 : VULNERABLE</span>
<span style="font-weight:bold;color:red;">        [&gt;] https://www.nccgroup.trust/uk/about-us/newsroom-and-events/blogs/2019/november/cve-2019-1405-and-cve-2019-1322-elevation-to-system-via-the-upnp-device-host-service-and-the-update-orchestrator-service/</span>

<span style="font-weight:bold;color:gray;">    Finished. Found </span><span style="font-weight:bold;color:red;">4</span><span style="font-weight:bold;color:gray;"> potential vulnerabilities.</span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">PowerShell Settings</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;"></span><span style="font-weight:bold;color:olive;">)</span>
<span style="font-weight:bold;color:gray;">    PowerShell v2 Version: </span>2.0
<span style="font-weight:bold;color:gray;">    PowerShell v5 Version: </span>5.1.17763.1
<span style="font-weight:bold;color:gray;">    Transcription Settings: </span>
<span style="font-weight:bold;color:gray;">    Module Logging Settings: </span>
<span style="font-weight:bold;color:gray;">    Scriptblock Logging Settings: </span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Audit Settings</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">T1012</span><span style="font-weight:bold;color:olive;">)</span>
<span style="color:olive;">   [?] </span><span style="font-weight:bold;color:blue;">Check what is being logged </span><span style="font-weight:bold;color:olive;"></span>
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">    Not Found</span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">WEF Settings</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">T1012</span><span style="font-weight:bold;color:olive;">)</span>
<span style="color:olive;">   [?] </span><span style="font-weight:bold;color:blue;">Windows Event Forwarding, is interesting to know were are sent the logs </span><span style="font-weight:bold;color:olive;"></span>
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">    Not Found</span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">LAPS Settings</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">T1012</span><span style="font-weight:bold;color:olive;">)</span>
<span style="color:olive;">   [?] </span><span style="font-weight:bold;color:blue;">If installed, local administrator password is changed frequently and is restricted by ACL </span><span style="font-weight:bold;color:olive;"></span>
<span style="font-weight:bold;color:gray;">    LAPS Enabled: </span><span style="font-weight:bold;color:red;">LAPS not installed</span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Wdigest</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;"></span><span style="font-weight:bold;color:olive;">)</span>
<span style="color:olive;">   [?] </span><span style="font-weight:bold;color:blue;">If enabled, plain-text crds could be stored in LSASS </span><span style="font-weight:bold;color:olive;">https://book.hacktricks.xyz/windows/stealing-credentials/credentials-protections#wdigest</span>
<span style="font-weight:bold;color:green;">    Wdigest is not enabled</span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">LSA Protection</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;"></span><span style="font-weight:bold;color:olive;">)</span>
<span style="color:olive;">   [?] </span><span style="font-weight:bold;color:blue;">If enabled, a driver is needed to read LSASS memory (If Secure Boot or UEFI, RunAsPPL cannot be disabled by deleting the registry key) </span><span style="font-weight:bold;color:olive;">https://book.hacktricks.xyz/windows/stealing-credentials/credentials-protections#lsa-protection</span>
<span style="font-weight:bold;color:red;">    LSA Protection is not enabled</span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Credentials Guard</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;"></span><span style="font-weight:bold;color:olive;">)</span>
<span style="color:olive;">   [?] </span><span style="font-weight:bold;color:blue;">If enabled, a driver is needed to read LSASS memory </span><span style="font-weight:bold;color:olive;">https://book.hacktricks.xyz/windows/stealing-credentials/credentials-protections#credential-guard</span>
<span style="font-weight:bold;color:red;">    CredentialGuard is not enabled</span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Cached Creds</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;"></span><span style="font-weight:bold;color:olive;">)</span>
<span style="color:olive;">   [?] </span><span style="font-weight:bold;color:blue;">If &gt; 0, credentials will be cached in the registry and accessible by SYSTEM user </span><span style="font-weight:bold;color:olive;">https://book.hacktricks.xyz/windows/stealing-credentials/credentials-protections#cached-credentials</span>
<span style="font-weight:bold;color:red;">    cachedlogonscount is 10</span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">User Environment Variables</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;"></span><span style="font-weight:bold;color:olive;">)</span>
<span style="color:olive;">   [?] </span><span style="font-weight:bold;color:blue;">Check for some passwords or keys in the env variables </span><span style="font-weight:bold;color:olive;"></span>
<span style="font-weight:bold;color:gray;">    COMPUTER</span><span style="font-weight:bold;color:red;">NAME</span>: WIN-QBA94KB3IOF
<span style="font-weight:bold;color:gray;">    USERPROFILE: </span>C:\Users\user
<span style="font-weight:bold;color:gray;">    HOMEPATH: </span>\Users\user
<span style="font-weight:bold;color:gray;">    LOCALAPPDATA: </span>C:\Users\user\AppData\Local
<span style="font-weight:bold;color:gray;">    PSModulePath: </span>C:\Program Files\WindowsPowerShell\Modules;C:\Windows\system32\WindowsPowerShell\v1.0\Modules
<span style="font-weight:bold;color:gray;">    PROCESSOR_ARCHITECTURE: </span>AMD64
<span style="font-weight:bold;color:gray;">    Path: </span>C:\Windows\system32;C:\Windows;C:\Windows\System32\Wbem;C:\Windows\System32\WindowsPowerShell\v1.0\;C:\Windows\System32\OpenSSH\;C:\Users\Administrator\AppData\Local\Microsoft\WindowsApps;;C:\Temp;C:\Users\user\AppData\Local\Microsoft\WindowsApps;
<span style="font-weight:bold;color:gray;">    CommonProgramFiles(x86): </span>C:\Program Files (x86)\Common Files
<span style="font-weight:bold;color:gray;">    ProgramFiles(x86): </span>C:\Program Files (x86)
<span style="font-weight:bold;color:gray;">    PROCESSOR_LEVEL: </span>6
<span style="font-weight:bold;color:gray;">    LOGONSERVER: </span>\\WIN-QBA94KB3IOF
<span style="font-weight:bold;color:gray;">    PATHEXT: </span>.COM;.EXE;.BAT;.CMD;.VBS;.VBE;.JS;.JSE;.WSF;.WSH;.MSC
<span style="font-weight:bold;color:gray;">    HOMEDRIVE: </span>C:
<span style="font-weight:bold;color:gray;">    SystemRoot: </span>C:\Windows
<span style="font-weight:bold;color:gray;">    </span><span style="font-weight:bold;color:red;">SESSIONNAME</span>: RDP-Tcp#0
<span style="font-weight:bold;color:gray;">    ALLUSERSPROFILE: </span>C:\ProgramData
<span style="font-weight:bold;color:gray;">    DriverData: </span>C:\Windows\System32\Drivers\DriverData
<span style="font-weight:bold;color:gray;">    APPDATA: </span>C:\Users\user\AppData\Roaming
<span style="font-weight:bold;color:gray;">    PROCESSOR_REVISION: </span>4f01
<span style="font-weight:bold;color:gray;">    USER</span><span style="font-weight:bold;color:red;">NAME</span>: user
<span style="font-weight:bold;color:gray;">    CommonProgramW6432: </span>C:\Program Files\Common Files
<span style="font-weight:bold;color:gray;">    CommonProgramFiles: </span>C:\Program Files\Common Files
<span style="font-weight:bold;color:gray;">    CLIENT</span><span style="font-weight:bold;color:red;">NAME</span>: ip-10-10-92-199
<span style="font-weight:bold;color:gray;">    OS: </span>Windows_NT
<span style="font-weight:bold;color:gray;">    USERDOMAIN_ROAMINGPROFILE: </span>WIN-QBA94KB3IOF
<span style="font-weight:bold;color:gray;">    PROCESSOR_IDENTIFIER: </span>Intel64 Family 6 Model 79 Stepping 1, GenuineIntel
<span style="font-weight:bold;color:gray;">    ComSpec: </span>C:\Windows\system32\cmd.exe
<span style="font-weight:bold;color:gray;">    PROMPT: </span>$P$G
<span style="font-weight:bold;color:gray;">    SystemDrive: </span>C:
<span style="font-weight:bold;color:gray;">    TEMP: </span>C:\Users\user\AppData\Local\Temp\2
<span style="font-weight:bold;color:gray;">    ProgramFiles: </span>C:\Program Files
<span style="font-weight:bold;color:gray;">    NUMBER_OF_PROCESSORS: </span>1
<span style="font-weight:bold;color:gray;">    TMP: </span>C:\Users\user\AppData\Local\Temp\2
<span style="font-weight:bold;color:gray;">    ProgramData: </span>C:\ProgramData
<span style="font-weight:bold;color:gray;">    ProgramW6432: </span>C:\Program Files
<span style="font-weight:bold;color:gray;">    windir: </span>C:\Windows
<span style="font-weight:bold;color:gray;">    USERDOMAIN: </span>WIN-QBA94KB3IOF
<span style="font-weight:bold;color:gray;">    PUBLIC: </span>C:\Users\Public

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">System Environment Variables</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;"></span><span style="font-weight:bold;color:olive;">)</span>
<span style="color:olive;">   [?] </span><span style="font-weight:bold;color:blue;">Check for some passwords or keys in the env variables </span><span style="font-weight:bold;color:olive;"></span>
<span style="font-weight:bold;color:gray;">    ComSpec: </span>C:\Windows\system32\cmd.exe
<span style="font-weight:bold;color:gray;">    DriverData: </span>C:\Windows\System32\Drivers\DriverData
<span style="font-weight:bold;color:gray;">    OS: </span>Windows_NT
<span style="font-weight:bold;color:gray;">    Path: </span>C:\Windows\system32;C:\Windows;C:\Windows\System32\Wbem;C:\Windows\System32\WindowsPowerShell\v1.0\;C:\Windows\System32\OpenSSH\;C:\Users\Administrator\AppData\Local\Microsoft\WindowsApps;;C:\Temp
<span style="font-weight:bold;color:gray;">    PATHEXT: </span>.COM;.EXE;.BAT;.CMD;.VBS;.VBE;.JS;.JSE;.WSF;.WSH;.MSC
<span style="font-weight:bold;color:gray;">    PROCESSOR_ARCHITECTURE: </span>AMD64
<span style="font-weight:bold;color:gray;">    PSModulePath: </span>C:\Program Files\WindowsPowerShell\Modules;C:\Windows\system32\WindowsPowerShell\v1.0\Modules
<span style="font-weight:bold;color:gray;">    TEMP: </span>C:\Windows\TEMP
<span style="font-weight:bold;color:gray;">    TMP: </span>C:\Windows\TEMP
<span style="font-weight:bold;color:gray;">    USER</span><span style="font-weight:bold;color:red;">NAME</span>: SYSTEM
<span style="font-weight:bold;color:gray;">    windir: </span>C:\Windows
<span style="font-weight:bold;color:gray;">    NUMBER_OF_PROCESSORS: </span>1
<span style="font-weight:bold;color:gray;">    PROCESSOR_LEVEL: </span>6
<span style="font-weight:bold;color:gray;">    PROCESSOR_IDENTIFIER: </span>Intel64 Family 6 Model 79 Stepping 1, GenuineIntel
<span style="font-weight:bold;color:gray;">    PROCESSOR_REVISION: </span>4f01

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">HKCU Internet Settings</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">T1012</span><span style="font-weight:bold;color:olive;">)</span>
<span style="font-weight:bold;color:gray;">    DisableCachingOfSSLPages: </span>1
<span style="font-weight:bold;color:gray;">    IE5_UA_Backup_Flag: </span>5.0
<span style="font-weight:bold;color:gray;">    PrivacyAdvanced: </span>1
<span style="font-weight:bold;color:gray;">    SecureProtocols: </span>2688
<span style="font-weight:bold;color:gray;">    User Agent: </span>Mozilla/4.0 (compatible; MSIE 8.0; Win32)
<span style="font-weight:bold;color:gray;">    CertificateRevocation: </span>1
<span style="font-weight:bold;color:gray;">    ZonesSecurityUpgrade: </span>System.Byte[]
<span style="font-weight:bold;color:gray;">    WarnonZoneCrossing: </span>1
<span style="font-weight:bold;color:gray;">    EnableNegotiate: </span>1
<span style="font-weight:bold;color:gray;">    MigrateProxy: </span>1
<span style="font-weight:bold;color:gray;">    ProxyEnable: </span>0

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">HKLM Internet Settings</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">T1012</span><span style="font-weight:bold;color:olive;">)</span>
<span style="font-weight:bold;color:gray;">    ActiveXCache: </span>C:\Windows\Downloaded Program Files
<span style="font-weight:bold;color:gray;">    CodeBaseSearchPath: </span>CODEBASE
<span style="font-weight:bold;color:gray;">    EnablePunycode: </span>1
<span style="font-weight:bold;color:gray;">    MinorVersion: </span>0
<span style="font-weight:bold;color:gray;">    WarnOnIntranet: </span>1

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Drives Information</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">T1120</span><span style="font-weight:bold;color:olive;">)</span>
<span style="color:olive;">   [?] </span><span style="font-weight:bold;color:blue;">Remember that you should search more info inside the other drives </span><span style="font-weight:bold;color:olive;"></span>
    C:\ (Type: Fixed)(Filesystem: NTFS)(Available space: 28 GB)(<span style="font-weight:bold;color:red;">Permissions: Users [AppendData/CreateDirectories])</span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">AV Information</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">T1063</span><span style="font-weight:bold;color:olive;">)</span>
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">  [X] Exception: Invalid namespace </span>
<span style="font-weight:bold;color:red;">    No AV was detected!!</span>
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">    Not Found</span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">UAC Status</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">T1012</span><span style="font-weight:bold;color:olive;">)</span>
<span style="color:olive;">   [?] </span><span style="font-weight:bold;color:blue;">If you are in the Administrators group check how to bypass the UAC </span><span style="font-weight:bold;color:olive;">https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#basic-uac-bypass-full-file-system-access</span>
<span style="font-weight:bold;color:gray;">    ConsentPromptBehaviorAdmin: </span>5 - <span style="font-weight:bold;color:red;">PromptForNonWindowsBinaries</span>
<span style="font-weight:bold;color:gray;">    EnableLUA: </span>1
<span style="font-weight:bold;color:gray;">    LocalAccountTokenFilterPolicy: </span>1
<span style="font-weight:bold;color:gray;">    FilterAdministratorToken: </span>
<span style="font-weight:bold;color:red;">      [*] LocalAccountTokenFilterPolicy set to 1.
      [+] Any local account can be used for lateral movement.</span>


<span style="font-weight:bold;color:teal;">  ===========================================(</span><span style="color:olive;">Users Information</span><span style="font-weight:bold;color:teal;">)===========================================</span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Users</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">T1087&amp;T1069&amp;T1033</span><span style="font-weight:bold;color:olive;">)</span>
<span style="color:olive;">   [?] </span><span style="font-weight:bold;color:blue;">Check if you have some admin equivalent privileges </span><span style="font-weight:bold;color:olive;">https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#users-and-groups</span>
  Current <span style="color:teal;"></span><span style="color:teal;"></span><span style="font-weight:bold;color:purple;"></span><span style="font-weight:bold;color:purple;">user</span>: <span style="color:teal;"></span><span style="color:teal;"></span><span style="font-weight:bold;color:purple;"></span><span style="font-weight:bold;color:purple;">user</span>
  Current groups: Domain Users, Everyone, Users, Builtin\<span style="font-weight:bold;color:red;"></span><span style="font-weight:bold;color:red;">Remote </span>Desktop Users, <span style="font-weight:bold;color:red;"></span><span style="font-weight:bold;color:red;">Remote </span>Interactive Logon, Interactive, Authenticated Users, This Organization, Local account, Local, NTLM Authentication
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   =================================================================================================</span>

    <span style="font-weight:bold;color:purple;">WIN-QBA94KB3IOF</span>\<span style="color:teal;"></span><span style="font-weight:bold;color:red;">admin</span>
        |-&gt;Groups: <span style="font-weight:bold;color:red;">Administrator</span>s,Users
        |-&gt;Password: CanChange-Expi-Req

    <span style="font-weight:bold;color:purple;">WIN-QBA94KB3IOF</span>\<span style="font-weight:bold;color:red;">Administrator</span>(<span style="color:blue;">Disabled</span>): Built-in account for <span style="color:teal;"></span><span style="font-weight:bold;color:red;">admin</span>istering the computer/domain
        |-&gt;Groups: <span style="font-weight:bold;color:red;">Administrator</span>s
        |-&gt;Password: CanChange-<span style="font-weight:bold;color:red;">NotExpi</span>-Req

    <span style="font-weight:bold;color:purple;">WIN-QBA94KB3IOF</span>\<span style="color:blue;">DefaultAccount</span>(<span style="color:blue;">Disabled</span>): A <span style="color:teal;"></span><span style="font-weight:bold;color:purple;">user</span> account managed by the system.
        |-&gt;Groups: System Managed Accounts Group
        |-&gt;Password: CanChange-<span style="font-weight:bold;color:red;">NotExpi</span>-NotReq

    <span style="font-weight:bold;color:purple;">WIN-QBA94KB3IOF</span>\<span style="color:blue;">Guest</span>(<span style="color:blue;">Disabled</span>): Built-in account for guest access to the computer/domain
        |-&gt;Groups: <span style="color:blue;">Guest</span>s
        |-&gt;Password: <span style="font-weight:bold;color:red;">NotChange</span>-<span style="font-weight:bold;color:red;">NotExpi</span>-NotReq

    <span style="font-weight:bold;color:purple;">WIN-QBA94KB3IOF</span>\<span style="color:teal;"></span><span style="font-weight:bold;color:purple;">user</span>
        |-&gt;Groups: Users
        |-&gt;Password: CanChange-Expi-Req

    <span style="font-weight:bold;color:purple;">WIN-QBA94KB3IOF</span>\<span style="color:blue;">WDAGUtilityAccount</span>(<span style="color:blue;">Disabled</span>): A <span style="color:teal;"></span><span style="font-weight:bold;color:purple;">user</span> account managed and used by the system for Windows Defender Application Guard scenarios.
        |-&gt;Password: CanChange-Expi-Req


<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Current Token privileges</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">T1134</span><span style="font-weight:bold;color:olive;">)</span>
<span style="color:olive;">   [?] </span><span style="font-weight:bold;color:blue;">Check if you can escalate privilege using some enabled token </span><span style="font-weight:bold;color:olive;">https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#token-manipulation</span>
<span style="font-weight:bold;color:gray;">    SeShutdownPrivilege: </span>DISABLED
<span style="font-weight:bold;color:gray;">    SeChangeNotifyPrivilege: </span>SE_PRIVILEGE_ENABLED_BY_DEFAULT, SE_PRIVILEGE_ENABLED
<span style="font-weight:bold;color:gray;">    SeIncreaseWorkingSetPrivilege: </span>DISABLED

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Clipboard text</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">T1134</span><span style="font-weight:bold;color:olive;">)</span>
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">    Not Found</span>
<span style="color:olive;">    [i] </span><span style="font-weight:bold;color:blue;">    This C# implementation to capture the clipboard is not trustable in every Windows version</span>
<span style="color:olive;">    [i] </span><span style="font-weight:bold;color:blue;">    If you want to see what is inside the clipboard execute 'powershell -command &quot;Get - Clipboard&quot;'</span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Logged users</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">T1087&amp;T1033</span><span style="font-weight:bold;color:olive;">)</span>
    <span style="font-weight:bold;color:purple;">WIN-QBA94KB3IOF</span>\<span style="color:teal;"></span><span style="font-weight:bold;color:purple;">user</span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">RDP Sessions</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">T1087&amp;T1033</span><span style="font-weight:bold;color:olive;">)</span>
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">    SessID    pSessionName   pUserName      pDomainName              State     SourceIP</span>
    2         RDP-Tcp#0      <span style="color:teal;"></span><span style="font-weight:bold;color:purple;">user</span>           <span style="font-weight:bold;color:purple;">WIN-QBA94KB3IOF</span>          Active    10.10.92.199

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Ever logged users</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">T1087&amp;T1033</span><span style="font-weight:bold;color:olive;">)</span>
    <span style="font-weight:bold;color:purple;">WIN-QBA94KB3IOF</span>\<span style="font-weight:bold;color:red;">Administrator</span>
    <span style="font-weight:bold;color:purple;">WIN-QBA94KB3IOF</span>\<span style="color:teal;"></span><span style="font-weight:bold;color:red;">admin</span>
    <span style="font-weight:bold;color:purple;">WIN-QBA94KB3IOF</span>\<span style="color:teal;"></span><span style="font-weight:bold;color:purple;">user</span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Looking for AutoLogon credentials</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">T1012</span><span style="font-weight:bold;color:olive;">)</span>
<span style="font-weight:bold;color:red;">    Some AutoLogon credentials were found!!</span>
    DefaultUserName               :  <span style="color:teal;"></span><span style="font-weight:bold;color:red;">admin</span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Home folders found</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">T1087&amp;T1083&amp;T1033</span><span style="font-weight:bold;color:olive;">)</span>
<span style="font-weight:bold;color:green;">    C:\Users\admin</span>
<span style="font-weight:bold;color:green;">    C:\Users\Administrator</span>
<span style="font-weight:bold;color:green;">    C:\Users\All Users</span>
<span style="font-weight:bold;color:green;">    C:\Users\Default</span>
<span style="font-weight:bold;color:green;">    C:\Users\Default User</span>
<span style="font-weight:bold;color:red;">    C:\Users\Public : Interactive [WriteData/CreateFiles]</span>
<span style="font-weight:bold;color:green;">    C:\Users\user</span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Password Policies</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">T1201</span><span style="font-weight:bold;color:olive;">)</span>
<span style="color:olive;">   [?] </span><span style="font-weight:bold;color:blue;">Check for a possible brute-force </span><span style="font-weight:bold;color:olive;"></span>
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">  [X] Exception: System.OverflowException: Negating the minimum value of a twos complement number is invalid.
   at System.TimeSpan.op_UnaryNegation(TimeSpan t)
   at d7.d()</span>
<span style="font-weight:bold;color:gray;">    Domain: </span>Builtin
<span style="font-weight:bold;color:gray;">    SID: </span>S-1-5-32
<span style="font-weight:bold;color:gray;">    MaxPasswordAge: </span>42.22:47:31.7437440
<span style="font-weight:bold;color:gray;">    MinPasswordAge: </span>00:00:00
<span style="font-weight:bold;color:gray;">    MinPasswordLength: </span>0
<span style="font-weight:bold;color:gray;">    PasswordHistoryLength: </span>0
<span style="font-weight:bold;color:gray;">    PasswordProperties: </span>0
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   =================================================================================================</span>



<span style="font-weight:bold;color:teal;">  =======================================(</span><span style="color:olive;">Processes Information</span><span style="font-weight:bold;color:teal;">)=======================================</span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Interesting Processes -non Microsoft-</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">T1010&amp;T1057&amp;T1007</span><span style="font-weight:bold;color:olive;">)</span>
<span style="color:olive;">   [?] </span><span style="font-weight:bold;color:blue;">Check if any interesting proccesses for memmory dump or if you could overwrite some binary running </span><span style="font-weight:bold;color:olive;">https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#running-processes</span>
    winPEASany(4104)[<span style="font-weight:bold;color:red;">C:\PrivEsc\winPEASany.exe]</span> -- POwn:<span style="font-weight:bold;color:purple;"> user</span> -- isDotNet
    <span style="font-weight:bold;color:red;">Possible DLL Hijacking folder: C:\PrivEsc (Users [AppendData/CreateDirectories WriteData/CreateFiles])</span>
    <span style="font-weight:bold;color:gray;">Command Line: .\winPEASany.exe  
</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   =================================================================================================</span>

    RuntimeBroker(3276)[<span style="font-weight:bold;color:green;">C:\Windows\System32\RuntimeBroker.exe]</span> -- POwn:<span style="font-weight:bold;color:purple;"> user</span>
    <span style="font-weight:bold;color:gray;">Command Line: </span><span style="font-weight:bold;color:green;">C:\Windows\System32\RuntimeBroker.exe </span>-Embedding
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   =================================================================================================</span>

    conhost(4856)[<span style="font-weight:bold;color:green;">C:\Windows\system32\conhost.exe]</span> -- POwn:<span style="font-weight:bold;color:purple;"> user</span>
    <span style="font-weight:bold;color:gray;">Command Line: \??\</span><span style="font-weight:bold;color:green;">C:\Windows\system32\conhost.exe </span>0x4
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   =================================================================================================</span>

    cmd(4848)[<span style="font-weight:bold;color:green;">C:\Windows\System32\cmd.exe]</span> -- POwn:<span style="font-weight:bold;color:purple;"> user</span>
    <span style="font-weight:bold;color:gray;">Command Line: &quot;C:\Windows\System32\cmd.exe&quot; 
</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   =================================================================================================</span>

    cmd(3264)[<span style="font-weight:bold;color:green;">C:\Windows\System32\cmd.exe]</span> -- POwn:<span style="font-weight:bold;color:purple;"> user</span>
    <span style="font-weight:bold;color:gray;">Command Line: &quot;C:\Windows\System32\cmd.exe&quot; 
</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   =================================================================================================</span>

    conhost(5036)[<span style="font-weight:bold;color:green;">C:\Windows\system32\conhost.exe]</span> -- POwn:<span style="font-weight:bold;color:purple;"> user</span>
    <span style="font-weight:bold;color:gray;">Command Line: \??\</span><span style="font-weight:bold;color:green;">C:\Windows\system32\conhost.exe </span>0x4
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   =================================================================================================</span>

    RuntimeBroker(4048)[<span style="font-weight:bold;color:green;">C:\Windows\System32\RuntimeBroker.exe]</span> -- POwn:<span style="font-weight:bold;color:purple;"> user</span>
    <span style="font-weight:bold;color:gray;">Command Line: </span><span style="font-weight:bold;color:green;">C:\Windows\System32\RuntimeBroker.exe </span>-Embedding
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   =================================================================================================</span>

    taskhostw(3224)[<span style="font-weight:bold;color:green;">C:\Windows\system32\taskhostw.exe]</span> -- POwn:<span style="font-weight:bold;color:purple;"> user</span>
    <span style="font-weight:bold;color:gray;">Command Line: taskhostw.exe {222A245B-E637-4AE9-A93F-A59CA119A75E}
</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   =================================================================================================</span>

    svchost(3204)[<span style="font-weight:bold;color:green;">C:\Windows\system32\svchost.exe]</span> -- POwn:<span style="font-weight:bold;color:purple;"> user</span>
    <span style="font-weight:bold;color:gray;">Command Line: </span><span style="font-weight:bold;color:green;">C:\Windows\system32\svchost.exe </span>-k UnistackSvcGroup
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   =================================================================================================</span>

    smartscreen(4432)[<span style="font-weight:bold;color:green;">C:\Windows\System32\smartscreen.exe]</span> -- POwn:<span style="font-weight:bold;color:purple;"> user</span>
    <span style="font-weight:bold;color:gray;">Command Line: </span><span style="font-weight:bold;color:green;">C:\Windows\System32\smartscreen.exe </span>-Embedding
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   =================================================================================================</span>

    explorer(3592)[<span style="font-weight:bold;color:green;">C:\Windows\Explorer.EXE]</span> -- POwn:<span style="font-weight:bold;color:purple;"> user</span>
    <span style="font-weight:bold;color:gray;">Command Line: C:\Windows\Explorer.EXE
</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   =================================================================================================</span>

    SearchUI(632)[<span style="font-weight:bold;color:green;">C:\Windows\SystemApps\Microsoft.Windows.Cortana_cw5n1h2txyewy\SearchUI.exe]</span> -- POwn:<span style="font-weight:bold;color:purple;"> user</span>
    <span style="font-weight:bold;color:gray;">Command Line: &quot;C:\Windows\SystemApps\Microsoft.Windows.Cortana_cw5n1h2txyewy\SearchUI.exe&quot; -ServerName:CortanaUI.AppXa50dqqa5gqv4a428c9y1jjw7m3btvepj.mca
</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   =================================================================================================</span>

    sihost(3184)[<span style="font-weight:bold;color:green;">C:\Windows\system32\sihost.exe]</span> -- POwn:<span style="font-weight:bold;color:purple;"> user</span>
    <span style="font-weight:bold;color:gray;">Command Line: sihost.exe
</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   =================================================================================================</span>

    RuntimeBroker(1280)[<span style="font-weight:bold;color:green;">C:\Windows\System32\RuntimeBroker.exe]</span> -- POwn:<span style="font-weight:bold;color:purple;"> user</span>
    <span style="font-weight:bold;color:gray;">Command Line: </span><span style="font-weight:bold;color:green;">C:\Windows\System32\RuntimeBroker.exe </span>-Embedding
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   =================================================================================================</span>

    ShellExperienceHost(3952)[<span style="font-weight:bold;color:green;">C:\Windows\SystemApps\ShellExperienceHost_cw5n1h2txyewy\ShellExperienceHost.exe]</span> -- POwn:<span style="font-weight:bold;color:purple;"> user</span>
    <span style="font-weight:bold;color:gray;">Command Line: &quot;C:\Windows\SystemApps\ShellExperienceHost_cw5n1h2txyewy\ShellExperienceHost.exe&quot; -ServerName:App.AppXtk181tbxbce2qsex02s8tw7hfxa9xb3t.mca
</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   =================================================================================================</span>

    rdpclip(3160)[<span style="font-weight:bold;color:green;">C:\Windows\System32\rdpclip.exe]</span> -- POwn:<span style="font-weight:bold;color:purple;"> user</span>
    <span style="font-weight:bold;color:gray;">Command Line: rdpclip
</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   =================================================================================================</span>



<span style="font-weight:bold;color:teal;">  ========================================(</span><span style="color:olive;">Services Information</span><span style="font-weight:bold;color:teal;">)========================================</span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Interesting Services -non Microsoft-</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">T1007</span><span style="font-weight:bold;color:olive;">)</span>
<span style="color:olive;">   [?] </span><span style="font-weight:bold;color:blue;">Check if you can overwrite some service binary or perform a DLL hijacking, also check for unquoted paths </span><span style="font-weight:bold;color:olive;">https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#services</span>
    AmazonSSMAgent(Amazon SSM Agent)[<span style="font-weight:bold;color:green;">&quot;C:\Program Files\Amazon\SSM\amazon-ssm-agent.exe&quot;</span>] - Auto - Running
    <span style="font-weight:bold;color:gray;">Amazon SSM Agent
</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   =================================================================================================</span>

    AWSLiteAgent(Amazon Inc. - AWS Lite Guest Agent)[<span style="font-weight:bold;color:red;">C:\Program Files\Amazon\XenTools\LiteAgent.exe</span>] - Auto - Running - <span style="font-weight:bold;color:red;">No quotes and Space detected</span>
    <span style="font-weight:bold;color:gray;">AWS Lite Guest Agent
</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   =================================================================================================</span>

    daclsvc(DACL Service)[<span style="font-weight:bold;color:green;">&quot;C:\Program Files\DACL Service\daclservice.exe&quot;</span>] - Manual - Stopped
    <span style="font-weight:bold;color:red;">YOU CAN MODIFY THIS SERVICE: WriteData/CreateFiles</span>
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   =================================================================================================</span>

    dllsvc(DLL Hijack Service)[<span style="font-weight:bold;color:green;">&quot;C:\Program Files\DLL Hijack Service\dllhijackservice.exe&quot;</span>] - Manual - Stopped
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   =================================================================================================</span>

    filepermsvc(File Permissions Service)[<span style="font-weight:bold;color:red;">&quot;C:\Program Files\File Permissions Service\filepermservice.exe&quot;</span>] - Manual - Stopped
    <span style="font-weight:bold;color:red;">File Permissions: Everyone [AllAccess]</span>
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   =================================================================================================</span>

    PsShutdownSvc(Systems Internals - PsShutdown)[<span style="font-weight:bold;color:green;">C:\Windows\PSSDNSVC.EXE</span>] - Manual - Stopped
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   =================================================================================================</span>

    regsvc(Insecure Registry Service)[<span style="font-weight:bold;color:green;">&quot;C:\Program Files\Insecure Registry Service\insecureregistryservice.exe&quot;</span>] - Manual - Stopped
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   =================================================================================================</span>

    ssh-agent(OpenSSH Authentication Agent)[<span style="font-weight:bold;color:green;">C:\Windows\System32\OpenSSH\ssh-agent.exe</span>] - Disabled - Stopped
    <span style="font-weight:bold;color:gray;">Agent to hold private keys used for public key authentication.
</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   =================================================================================================</span>

    unquotedsvc(Unquoted Path Service)[<span style="font-weight:bold;color:red;">C:\Program Files\Unquoted Path Service\Common Files\unquotedpathservice.exe</span>] - Manual - Stopped - <span style="font-weight:bold;color:red;">No quotes and Space detected</span>
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   =================================================================================================</span>

    winexesvc(winexesvc)[<span style="font-weight:bold;color:green;">winexesvc.exe</span>] - Manual - Stopped
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   =================================================================================================</span>


<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Modifiable Services</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">T1007</span><span style="font-weight:bold;color:olive;">)</span>
<span style="color:olive;">   [?] </span><span style="font-weight:bold;color:blue;">Check if you can modify any service </span><span style="font-weight:bold;color:olive;">https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#services</span>
<span style="font-weight:bold;color:red;">    LOOKS LIKE YOU CAN MODIFY SOME SERVICE/s:</span>
<span style="font-weight:bold;color:red;">    daclsvc: WriteData/CreateFiles</span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Looking if you can modify any service registry</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;"></span><span style="font-weight:bold;color:olive;">)</span>
<span style="color:olive;">   [?] </span><span style="font-weight:bold;color:blue;">Check if you can modify the registry of a service </span><span style="font-weight:bold;color:olive;">https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#services-registry-permissions</span>
    HKLM\system\currentcontrolset\services\regsvc <span style="font-weight:bold;color:red;">(Interactive [TakeOwnership])</span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Checking write permissions in PATH folders (DLL Hijacking)</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;"></span><span style="font-weight:bold;color:olive;">)</span>
<span style="color:olive;">   [?] </span><span style="font-weight:bold;color:blue;">Check for DLL Hijacking in PATH folders </span><span style="font-weight:bold;color:olive;">https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#dll-hijacking</span>
<span style="font-weight:bold;color:green;">    C:\Windows\system32</span>
<span style="font-weight:bold;color:green;">    C:\Windows</span>
<span style="font-weight:bold;color:green;">    C:\Windows\System32\Wbem</span>
<span style="font-weight:bold;color:green;">    C:\Windows\System32\WindowsPowerShell\v1.0\</span>
<span style="font-weight:bold;color:green;">    C:\Windows\System32\OpenSSH\</span>
<span style="font-weight:bold;color:green;">    C:\Users\Administrator\AppData\Local\Microsoft\WindowsApps</span>
<span style="font-weight:bold;color:green;">    </span>
<span style="font-weight:bold;color:red;">    (DLL Hijacking) C:\Temp: Users [AppendData/CreateDirectories WriteData/CreateFiles]</span>


<span style="font-weight:bold;color:teal;">  ====================================(</span><span style="color:olive;">Applications Information</span><span style="font-weight:bold;color:teal;">)====================================</span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Current Active Window Application</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">T1010&amp;T1518</span><span style="font-weight:bold;color:olive;">)</span>
<span style="font-weight:bold;color:green;">    C:\Windows\System32\cmd.exe - .\winPEASany.exe  </span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Installed Applications --Via Program Files/Uninstall registry--</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">T1083&amp;T1012&amp;T1010&amp;T1518</span><span style="font-weight:bold;color:olive;">)</span>
<span style="color:olive;">   [?] </span><span style="font-weight:bold;color:blue;">Check if you can modify installed software </span><span style="font-weight:bold;color:olive;">https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#software</span>
<span style="font-weight:bold;color:green;">    C:\Program Files\Amazon</span>
<span style="font-weight:bold;color:green;">    C:\Program Files\Autorun Program</span>
<span style="font-weight:bold;color:green;">    C:\Program Files\Common Files</span>
<span style="font-weight:bold;color:green;">    C:\Program Files\DACL Service</span>
<span style="font-weight:bold;color:green;">    C:\Program Files\desktop.ini</span>
<span style="font-weight:bold;color:green;">    C:\Program Files\DLL Hijack Service</span>
<span style="font-weight:bold;color:green;">    C:\Program Files\File Permissions Service</span>
<span style="font-weight:bold;color:green;">    C:\Program Files\Insecure Registry Service</span>
<span style="font-weight:bold;color:green;">    C:\Program Files\internet explorer</span>
<span style="font-weight:bold;color:green;">    C:\Program Files\Uninstall Information</span>
<span style="font-weight:bold;color:red;">    C:\Program Files\Unquoted Path Service(Users [AllAccess])</span>
<span style="font-weight:bold;color:green;">    C:\Program Files\Windows Defender</span>
<span style="font-weight:bold;color:green;">    C:\Program Files\Windows Defender Advanced Threat Protection</span>
<span style="font-weight:bold;color:green;">    C:\Program Files\Windows Mail</span>
<span style="font-weight:bold;color:green;">    C:\Program Files\Windows Media Player</span>
<span style="font-weight:bold;color:green;">    C:\Program Files\Windows Multimedia Platform</span>
<span style="font-weight:bold;color:green;">    C:\Program Files\windows nt</span>
<span style="font-weight:bold;color:green;">    C:\Program Files\Windows Photo Viewer</span>
<span style="font-weight:bold;color:green;">    C:\Program Files\Windows Portable Devices</span>
<span style="font-weight:bold;color:green;">    C:\Program Files\Windows Security</span>
<span style="font-weight:bold;color:green;">    C:\Program Files\Windows Sidebar</span>
<span style="font-weight:bold;color:green;">    C:\Program Files\WindowsApps</span>
<span style="font-weight:bold;color:green;">    C:\Program Files\WindowsPowerShell</span>


<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Autorun Applications</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">T1010</span><span style="font-weight:bold;color:olive;">)</span>
<span style="color:olive;">   [?] </span><span style="font-weight:bold;color:blue;">Check if you can modify other users AutoRuns binaries </span><span style="font-weight:bold;color:olive;">https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#run-at-startup</span>
    Folder: <span style="font-weight:bold;color:green;">C:\Windows\system32</span>
    File: <span style="font-weight:bold;color:green;">C:\Windows\system32</span>\SecurityHealthSystray.exe
    RegPath: <span style="font-weight:bold;color:green;">HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run</span>
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   =================================================================================================</span>

    Folder: <span style="font-weight:bold;color:green;">C:\Program Files\Autorun Program</span>
    File: <span style="font-weight:bold;color:green;">C:\Program Files\Autorun Program</span>\program.exe
    <span style="font-weight:bold;color:red;">FilePerms: Everyone [AllAccess]</span>
    RegPath: <span style="font-weight:bold;color:green;">HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run</span>
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   =================================================================================================</span>

<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">System.Collections.Generic.KeyNotFoundException: The given key was not present in the dictionary.
   at System.ThrowHelper.ThrowKeyNotFoundException()
   at System.Collections.Generic.Dictionary`2.get_Item(TKey key)
   at d4.ap()</span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Scheduled Applications --Non Microsoft--</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">T1010</span><span style="font-weight:bold;color:olive;">)</span>
<span style="color:olive;">   [?] </span><span style="font-weight:bold;color:blue;">Check if you can modify other users scheduled binaries </span><span style="font-weight:bold;color:olive;">https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#run-at-startup</span>
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">System.IO.FileNotFoundException: Could not load file or assembly 'Microsoft.Win32.TaskScheduler, Version=2.8.16.0, Culture=neutral, PublicKeyToken=c416bc1b32d97233' or one of its dependencies. The system cannot find the file specified.
File name: 'Microsoft.Win32.TaskScheduler, Version=2.8.16.0, Culture=neutral, PublicKeyToken=c416bc1b32d97233'
   at dx.a()
   at d4.ao()

WRN: Assembly binding logging is turned OFF.
To enable assembly bind failure logging, set the registry value [HKLM\Software\Microsoft\Fusion!EnableLog] (DWORD) to 1.
Note: There is some performance penalty associated with assembly bind failure logging.
To turn this feature off, remove the registry value [HKLM\Software\Microsoft\Fusion!EnableLog].
</span>


<span style="font-weight:bold;color:teal;">  =========================================(</span><span style="color:olive;">Network Information</span><span style="font-weight:bold;color:teal;">)=========================================</span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Network Shares</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">T1135</span><span style="font-weight:bold;color:olive;">)</span>
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">  [X] Exception: System.Runtime.InteropServices.COMException (0x80070006): The handle is invalid. (Exception from HRESULT: 0x80070006 (E_HANDLE))
   at System.Runtime.InteropServices.Marshal.ThrowExceptionForHRInternal(Int32 errorCode, IntPtr errorInfo)
   at System.Runtime.InteropServices.Marshal.FreeHGlobal(IntPtr hglobal)
   at winPEAS.SamServer.c.d(Boolean A_0)</span>
    <span style="font-weight:bold;color:green;">ADMIN$</span> (<span style="font-weight:bold;color:gray;">Path: C:\Windows</span>)
    <span style="font-weight:bold;color:green;">C$</span> (<span style="font-weight:bold;color:gray;">Path: C:\</span>)
    <span style="font-weight:bold;color:green;">IPC$</span> (<span style="font-weight:bold;color:gray;">Path: </span>)

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Host File</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">T1016</span><span style="font-weight:bold;color:olive;">)</span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Network Ifaces and known hosts</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">T1016</span><span style="font-weight:bold;color:olive;">)</span>
<span style="color:olive;">   [?] </span><span style="font-weight:bold;color:blue;">The masks are only for the IPv4 addresses </span><span style="font-weight:bold;color:olive;"></span>
    Ethernet[02:4A:5A:4D:C6:21]: 10.10.244.66, fe80::a56f:ac0b:4d07:e305%15 / 255.255.0.0
        <span style="font-weight:bold;color:gray;">Gateways: </span>10.10.0.1
        <span style="font-weight:bold;color:gray;">DNSs: </span>10.0.0.2
        <span style="font-weight:bold;color:gray;">Known hosts:</span>
          10.10.0.1             02-C8-85-B5-5A-AA     Dynamic
          10.10.92.199          02-B1-55-C3-45-D1     Dynamic
          10.10.255.255         FF-FF-FF-FF-FF-FF     Static
          224.0.0.22            01-00-5E-00-00-16     Static
          224.0.0.251           01-00-5E-00-00-FB     Static
          224.0.0.252           01-00-5E-00-00-FC     Static
          255.255.255.255       FF-FF-FF-FF-FF-FF     Static

    Loopback Pseudo-Interface 1[]: 127.0.0.1, ::1 / 255.0.0.0
        <span style="font-weight:bold;color:gray;">DNSs: </span>fec0:0:0:ffff::1%1, fec0:0:0:ffff::2%1, fec0:0:0:ffff::3%1
        <span style="font-weight:bold;color:gray;">Known hosts:</span>
          224.0.0.22            00-00-00-00-00-00     Static


<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Current Listening Ports</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">T1049&amp;T1049</span><span style="font-weight:bold;color:olive;">)</span>
<span style="color:olive;">   [?] </span><span style="font-weight:bold;color:blue;">Check for services restricted from the outside </span><span style="font-weight:bold;color:olive;"></span>
    Proto     Local Address          Foreing Address        State
    TCP       0.0.0.0:135                                   Listening
    TCP       0.0.0.0:445                                   Listening
    TCP       0.0.0.0:3389                                  Listening
    TCP       0.0.0.0:5985                                  Listening
    TCP       0.0.0.0:47001                                 Listening
    TCP       0.0.0.0:49664                                 Listening
    TCP       0.0.0.0:49665                                 Listening
    TCP       0.0.0.0:49666                                 Listening
    TCP       0.0.0.0:49667                                 Listening
    TCP       0.0.0.0:49668                                 Listening
    TCP       0.0.0.0:49669                                 Listening
    TCP       0.0.0.0:49671                                 Listening
    TCP       10.10.244.66:139                              Listening
    TCP       [::]:135                                      Listening
    TCP       [::]:445                                      Listening
    TCP       [::]:3389                                     Listening
    TCP       [::]:5985                                     Listening
    TCP       [::]:47001                                    Listening
    TCP       [::]:49664                                    Listening
    TCP       [::]:49665                                    Listening
    TCP       [::]:49666                                    Listening
    TCP       [::]:49667                                    Listening
    TCP       [::]:49668                                    Listening
    TCP       [::]:49669                                    Listening
    TCP       [::]:49671                                    Listening
    UDP       0.0.0.0:123                                   Listening
    UDP       0.0.0.0:500                                   Listening
    UDP       0.0.0.0:3389                                  Listening
    UDP       0.0.0.0:4500                                  Listening
    UDP       0.0.0.0:5353                                  Listening
    UDP       0.0.0.0:5355                                  Listening
    UDP       10.10.244.66:137                              Listening
    UDP       10.10.244.66:138                              Listening
    UDP       <span style="font-weight:bold;color:red;">127.0.0.1</span>:56720                               Listening
    UDP       [::]:123                                      Listening
    UDP       [::]:500                                      Listening

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Firewall Rules</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">T1016</span><span style="font-weight:bold;color:olive;">)</span>
<span style="color:olive;">   [?] </span><span style="font-weight:bold;color:blue;">Showing only DENY rules (too many ALLOW rules always) </span><span style="font-weight:bold;color:olive;"></span>
    Current Profiles: PUBLIC
    FirewallEnabled (Domain):    <span style="font-weight:bold;color:red;">False</span>
    FirewallEnabled (Private):    <span style="font-weight:bold;color:red;">False</span>
    FirewallEnabled (Public):    <span style="font-weight:bold;color:red;">False</span>
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">    DENY rules:</span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">DNS cached --limit 70--</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">T1016</span><span style="font-weight:bold;color:olive;">)</span>
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">    Entry                                 Name                                  Data</span>
    activation-v2.sls.microsoft.com       activation-v2.sls.microsoft.com       ...vation-v2.sls.trafficmanager.net
    activation-v2.sls.microsoft.com       ...vation-v2.sls.trafficmanager.net   40.91.76.224
    sls.update.microsoft.com              sls.update.microsoft.com              ...prod.dcat.dsp.trafficmanager.net
    sls.update.microsoft.com              ...prod.dcat.dsp.trafficmanager.net   74.178.76.128
    time.windows.com                      time.windows.com                      twc.trafficmanager.net
    time.windows.com                      twc.trafficmanager.net                51.137.137.111


<span style="font-weight:bold;color:teal;">  =========================================(</span><span style="color:olive;">Windows Credentials</span><span style="font-weight:bold;color:teal;">)=========================================</span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Checking Windows Vault</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;"></span><span style="font-weight:bold;color:olive;">)</span>
<span style="color:olive;">   [?] </span><span style="font-weight:bold;color:blue;"> </span><span style="font-weight:bold;color:olive;">https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#credentials-manager-windows-vault</span>
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">  [X] Exception: Object reference not set to an instance of an object.</span>
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">    Not Found</span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Checking Credential manager</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;"></span><span style="font-weight:bold;color:olive;">)</span>
<span style="color:olive;">   [?] </span><span style="font-weight:bold;color:blue;"> </span><span style="font-weight:bold;color:olive;">https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#credentials-manager-windows-vault</span>
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">    This function is not yet implemented.</span>
<span style="color:olive;">    [i] </span><span style="font-weight:bold;color:blue;">If you want to list credentials inside Credential Manager use 'cmdkey /list'</span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Saved RDP connections</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;"></span><span style="font-weight:bold;color:olive;">)</span>
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">    Not Found</span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Recently run commands</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;"></span><span style="font-weight:bold;color:olive;">)</span>
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">    Not Found</span>

<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Checking for DPAPI Master Keys</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;"></span><span style="font-weight:bold;color:olive;">)</span>
<span style="color:olive;">   [?] </span><span style="font-weight:bold;color:blue;"> </span><span style="font-weight:bold;color:olive;">https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#dpapi</span>
<span style="font-weight:bold;color:gray;">    MasterKey: </span>C:\Users\user\AppData\Roaming\Microsoft\Protect\S-1-5-21-3025105784-3259396213-1915610826-1000\ced3b33f-849e-4587-8829-fbaf4cd747a7
<span style="font-weight:bold;color:gray;">    Accessed: </span>6/5/2020 8:38:04 AM
<span style="font-weight:bold;color:gray;">    Modified: </span>6/5/2020 8:38:04 AM
<span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;">   =================================================================================================</span>


<span style="color:olive;">  [+] </span><span style="font-weight:bold;color:green;">Checking for Credential Files</span><span style="font-weight:bold;color:olive;">(</span><span style="font-weight:bold;filter: contrast(70%) brightness(190%);color:dimgray;"></span><span style="font-weight:bold;color:olive;">)</span>
<span style="color:olive;">   [?] </span><span style="font-weight:bold;color:blue;"> </span><span style="font-weight:bold;color:olive;">https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#dpapi</span>
<span style="font-weight:bold;color:gray;">    CredFile: </span>C:\Users\user\AppData\Local\Microsoft\Credentials\DFBE70A7E5CC19A398EBF1B96859CE5D
<span style="font-weight:bold;color:gray;">    Description: </span>Local Credential Data

```
{% endcode %}
