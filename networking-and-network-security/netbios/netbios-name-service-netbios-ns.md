---
description: The un-routable nameservice
---

# NetBIOS Name Service (NetBIOS-NS)

On a NetBIOS network, applications locate and identify each other through their NetBIOS names. NetBIOS Name Service serves much the same purpose as DNS does: translate human-readable names to IP addresses.

In order to start sessions or distribute datagrams, an application must register its NetBIOS name using the name service.&#x20;

NetBIOS names are **16 octets** long (so 16\*8 or **48 characters** is the limit) and vary based on the particular implementation.&#x20;

The 16th octet, called the NetBIOS Suffix, frequently designates the **type of resource** and can be used to **tell other applications what type of services the system offers**.

So overall the name is at minimum 15 octets long if the 16th octet is reserved.

### **NetBIOS name service runs on UDP port 137, but it can run on TCP port 137 as well.**

NBT can implement a central repository or _Name Service_, that records all name registrations. An application wanting to register a name would therefore contact the name server (which has a known network address) and ask whether the name is already registered, using a "Name Query" packet.&#x20;

This is much faster, as the name server returns a negative response immediately if the name is not already in the database, meaning it is available.&#x20;

According to RFCs 1001 and 1002, the Name Service is called _NetBIOS Naming Service_ or NBNS.&#x20;

#### Microsoft [WINS](https://en.wikipedia.org/wiki/Windows\_Internet\_Name\_Service) is an implementation of NBNS.

The packet formats of the Name Service are identical to [DNS](https://en.wikipedia.org/wiki/Domain\_Name\_System). The key differences are the addition of NetBIOS **"Node Status" query, dynamic registration and conflict marking packets**. They are encapsulated in [UDP](https://en.wikipedia.org/wiki/User\_Datagram\_Protocol).&#x20;
