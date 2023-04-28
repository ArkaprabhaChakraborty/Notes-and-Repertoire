---
description: Network Basic Input/Output system
---

# NetBIOS

NetBIOS is **NOT** a networking protocol, **rather an API**.&#x20;

Originally developed by IBM and later adapted by Microsoft for their NT kernels (Microsoft implemented SMB in [Windows NT 3.1](https://en.wikipedia.org/wiki/Windows\_NT\_3.1)), **NetBIOS is a naming system for devices in LAN** (Kinda like DNS). &#x20;

It is an API that allows communication of files and printers through the **Session Layer (Layer 5) of the OSI Model** in a LAN.

In modern networks, NetBIOS normally runs over [TCP/IP](https://en.wikipedia.org/wiki/TCP/IP) via the [NetBIOS over TCP/IP](https://en.wikipedia.org/wiki/NetBIOS\_over\_TCP/IP) (NBT) protocol. This results in each computer in the network having both an [IP address](https://en.wikipedia.org/wiki/IP\_address) and a NetBIOS name corresponding to a (possibly different) host name.&#x20;

NetBIOS is also used for identifying system names in Windows.&#x20;

### NetBIOS over TCP/IP (NBT or NetBT)

NetBIOS over TCP/IP is a **protocol** based on the NetBIOS API.  The [RFC 1001](https://datatracker.ietf.org/doc/html/rfc1001) deals with the NBT protocol.&#x20;

NetBIOS is not routable and hence scalable on it's own. But it can become so by relying on underlying TCP/IP stack for that. Hence NetBIOS over TCP/IP is used.&#x20;

NetBT can use both NTLM and Kerberos for Authentication.

NetBIOS has three integral service components:

1. NetBIOS Name Service (NetBIOS-NS)
2. NetBIOS Datagram Distribution Service (NetBIOS-DGM)
3. NetBIOS Session Service (NetBIOS-SSN)

