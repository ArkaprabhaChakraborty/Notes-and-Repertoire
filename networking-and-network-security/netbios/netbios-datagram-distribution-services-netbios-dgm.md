# NetBIOS Datagram Distribution Services (NetBIOS-DGM)

The NetBIOS datagram service provides connectionless, unreliable transport for unicast, multicast, and [broadcast](https://learn.microsoft.com/en-us/openspecs/windows\_protocols/ms-cifs/760f8b7f-9a8a-4f0c-a044-1501a83a933b#gt\_7f275cc2-a1c5-47d7-83ae-9a84178f2481) messages (datagrams).

Datagram mode is [connectionless](https://en.wikipedia.org/wiki/Connectionless); the application is responsible for error detection and recovery.&#x20;

### **In** [**NBT**](https://en.wikipedia.org/wiki/NetBIOS\_over\_TCP/IP)**, the datagram service runs on UDP port 138, but it can run on TCP port 138 as well.**

The datagram service primitives offered by NetBIOS are:

* Send Datagram – send a datagram to a remote NetBIOS name.
* Send Broadcast Datagram – send a datagram to all NetBIOS names on the network.
* Receive Datagram – wait for a packet to arrive from a Send Datagram operation.
* Receive Broadcast Datagram – wait for a packet to arrive from a Send Broadcast Datagram operation.
