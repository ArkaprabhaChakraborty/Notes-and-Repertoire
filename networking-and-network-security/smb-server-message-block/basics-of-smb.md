# Basics of SMB

The SMB protocol is known as a response-request protocol, meaning that it transmits multiple messages between the client and server to establish a connection.&#x20;

Clients connect to servers using TCP/IP (actually NetBIOS over TCP/IP as specified in RFC1001 and RFC1002), NetBEUI, or IPX/SPX).

For systems running SMB using NetBIOS, ports 137,138,139 along with port 445 should be open. Otherwise, if just port 445 it's just using SMB over TCP/IP directly.

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption><p>SMB Packet Structure</p></figcaption></figure>

### SMB Services

As a client-server protocol, SMB requires a **server service (**_**LanmanServer**_**)** and a **client service (**_**LanmanWorkstation**_**)**. Every Windows computer, whether it is running a server OS (like Server 2016 or Server 2019) or a client OS (like Windows 10 or Windows 11), has both the _LanmanServer_ and _LanmanWorkstation_ services.

To check for the status of the services we can use:

```powershell
Get-Service Lanman*
```

#### LanmanServer

The LanmanServer service makes sure that your computer can act as a _server_ for hosting SMB shares. Some default shares are made available by the LanmanServer, these are:

* IPC$ (IPC Share)
* C$
* admin$

The $ character at the end of the name of any share indicates it's an administrative share, aka, it can be accessed by the administrator user.

The SMB shares available in a system can be listed using:&#x20;

```powershell
Get-SmbShare
```

The LanmanServer service is using the `srvsvc.dll` file that is located in the `C:\Windows\system32` directory.

The registry key name for the LanmanServer is `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer.`

#### LanmanWorkstation

The LanmanWorkstation is the client service, which makes sure that it can utilize SMB shares and shared printers from remote computers or servers.&#x20;

The information about this service is stored in the following registry location: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation`.

