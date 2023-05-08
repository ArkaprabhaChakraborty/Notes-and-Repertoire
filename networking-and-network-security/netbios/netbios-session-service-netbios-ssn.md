# NetBIOS Session Service (NetBIOS-SSN)

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

\
