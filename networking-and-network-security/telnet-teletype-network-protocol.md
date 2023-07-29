---
description: If you see it... Disable it
---

# Telnet (Teletype Network Protocol)

### Telnet runs on **TCP port 23.**

Telnet is an application protocol which allows you, with the use of a telnet client, to connect to and execute commands on a remote machine that's hosting a telnet server.

The telnet client will establish a connection with the server. The client will then become a virtual terminal- allowing you to interact with the remote host.

**Problem**: Telnet sends all messages in clear text and has no specific security mechanisms.&#x20;

**Solution**: Telnet has been replaced by SSH in most implementations.

### How does Telnet work?

The user connects to the server by using the Telnet protocol, which means entering "telnet" into a command prompt. The user then executes commands on the server by using specific Telnet commands in the Telnet prompt. You can connect to a telnet server with the following syntax:

```
telnet [ip] [port]
```

### Enumeration

```
nmap -sV 10.10.10.3 -p 23
```

### Exploiting Telnet

Telnet, being a protocol, is in and of itself insecure for the reasons we talked about earlier. It lacks encryption, so sends all communication over plain text, and for the most part, has poor access control.

After connecting to a telnet session, we can run commands using `.RUN` prefix.

To quit a telnet session, use `Ctrl + ]` . To quit the telnet prompt use the keyword `quit`.

#### Nmap scripts for telnet

```
nmap -n -sV -Pn --script "*telnet*" -p 23 {IP} 
```

#### Banner Grabbing with Telnet

Telnet can be used for active reconnaissance. We can use telnet for banner grabbing purposes.

```
telnet 10.10.143.75 80
```

After this we get the prompt like shown below:

```
Trying 10.10.143.75...
Connected to 10.10.143.75.
Escape character is '^]'.
```

We can use:

```
GET / HTTP/1.1
host: telnet
```

A sample response is as follows:

```
HTTP/1.1 408 Request Timeout
Date: Sat, 29 Jul 2023 13:49:10 GMT
Server: Apache/2.4.10 (Debian)
Content-Length: 303
Connection: close
Content-Type: text/html; charset=iso-8859-1

<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>408 Request Timeout</title>
</head><body>
<h1>Request Timeout</h1>
<p>Server timeout waiting for the HTTP request from the client.</p>
<hr>
<address>Apache/2.4.10 (Debian) Server at debra2.thm.local Port 80</address>
</body></html>
Connection closed by foreign host.
```
