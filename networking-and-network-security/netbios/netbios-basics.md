---
description: A deep dive into NetBIOS API and it's services
---

# NetBIOS Basics

NetBIOS has three integral service components:

## NetBIOS Name Service (NetBIOS-NS)

NetBIOS Name Service serves much the same purpose as DNS does: translate human-readable names to IP addresses. In order to start sessions or distribute datagrams, an application must register its NetBIOS name using the name service. Microsoft [WINS](https://en.wikipedia.org/wiki/Windows\_Internet\_Name\_Service) is an implementation of NBNS.

On a NetBIOS network, applications locate and identify each other through their NetBIOS names which are **16 octets** long (so 16\*8 or **48 characters** is the limit) and vary based on the particular implementation. The 16th octet, called the NetBIOS Suffix, frequently designates the **type of resource** and can be used to **tell other applications what type of services the system offers**.

### **NetBIOS name service runs on UDP port 137, but it can run on TCP port 137 as well.**&#x20;

The packet formats of the Name Service are identical to [DNS](https://en.wikipedia.org/wiki/Domain\_Name\_System). The key differences are the addition of NetBIOS **"Node Status" query, dynamic registration and conflict marking packets**. They are encapsulated in [UDP](https://en.wikipedia.org/wiki/User\_Datagram\_Protocol).&#x20;

## NetBIOS Datagram Distribution Service (NetBIOS-DGM)

The NetBIOS datagram service provides connectionless, unreliable transport for unicast, multicast, and [broadcast](https://learn.microsoft.com/en-us/openspecs/windows\_protocols/ms-cifs/760f8b7f-9a8a-4f0c-a044-1501a83a933b#gt\_7f275cc2-a1c5-47d7-83ae-9a84178f2481) messages (datagrams). Datagram mode is [connectionless](https://en.wikipedia.org/wiki/Connectionless); the application is responsible for error detection and recovery.&#x20;

### **In** [**NBT**](https://en.wikipedia.org/wiki/NetBIOS\_over\_TCP/IP)**, the datagram service runs on UDP port 138, but it can run on TCP port 138 as well.**

The datagram service primitives offered by NetBIOS are:

* Send Datagram – send a datagram to a remote NetBIOS name.
* Send Broadcast Datagram – send a datagram to all NetBIOS names on the network.
* Receive Datagram – wait for a packet to arrive from a Send Datagram operation.
* Receive Broadcast Datagram – wait for a packet to arrive from a Send Broadcast Datagram operation.

## NetBIOS Session Service (NetBIOS-SSN)

The NetBIOS session service provides reliable, point-to-point transport. Session mode lets two computers establish a connection, allows messages to span multiple packets, and provides error detection and recovery.&#x20;

### In [NBT](https://en.wikipedia.org/wiki/NetBIOS\_over\_TCP/IP), the session service runs on TCP port 139.

The session service primitives offered by NetBIOS are:

* Call – opens a session to a remote NetBIOS name.
* Listen – listen for attempts to open a session to a NetBIOS name.
* Hang Up – close a session.
* Send – sends a packet to the computer at the other end of a session.
* Send No Ack – like Send, but doesn't require an acknowledgment.
* Receive – wait for a packet to arrive from a Send on the other end of a session.

In the original protocol used to implement NetBIOS services on PC-Network, to establish a session, the initiating computer sends an Open request which is answered by an Open acknowledgment. The computer that started the session will then send a Session Request packet which will prompt either a Session Accept or Session Reject packet.

During an established session, each transmitted packet is answered by either a positive-acknowledgment (ACK) or a negative-acknowledgment (NAK) response. A NAK will prompt the retransmission of the data. Sessions are closed by the non-initiating computer by sending a close request. The computer that started the session will reply with a close response which prompts the final session closed packet.
