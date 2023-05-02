# Basics of SMB

The SMB protocol is known as a response-request protocol, meaning that it transmits multiple messages between the client and server to establish a connection.&#x20;

Clients connect to servers using TCP/IP (actually NetBIOS over TCP/IP as specified in RFC1001 and RFC1002), NetBEUI, or IPX/SPX.

For systems running SMB using NetBIOS, ports 137,138,139 along with port 445 should be open. Otherwise, if just port 445 it's just using SMB over TCP/IP directly.

### SMB Services

