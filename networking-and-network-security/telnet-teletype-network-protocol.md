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

To quit a telnet session, use `ctrl + ]` . To quit the telnet prompt use the keyword `quit`.

#### Nmap scripts for telnet

```
nmap -n -sV -Pn --script "*telnet*" -p 23 {IP}
```

#### &#x20;

