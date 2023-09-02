---
description: Find out what services are running on a particular target host.
---

# Port Scanning - Service and OS Discovery

Discovery of open ports and services can be performed via various port scanning techniques. Administrators often use port scanning techniques to verify the security policies of their networks, whereas attackers use them to identify open ports and running services on a host with the intent of compromising the network.

### Service Version Discovery: the -`sV` option is used to detect service versions.

## TCP Connect/Full-Open Scan

Sends in  SYN packets for request. If SYN+ACK packet response - Port is open. If RST packet response - Port is closed.&#x20;

Disadvantage: Easily detectable and filterable. The logs in the target system disclose the connection.

```bash
nmap –sT –v <Target IP Address>
```

## Stealth Scan (Half-Open Scan)

Sends in a single SYN packet. Bypasses firewall rules and logging mechanisms.

```
nmap –sS –v <Target IP Address>
```

## Inverse TCP Flag Scan

Sends in a probe packet (FIN/URG/PSH/NULL). If no response is received port is open. If RST packet response is received port is closed. Avoids many IDS and logging systems; highly stealthy.

Disadvantage: Not effective against Microsoft Windows hosts, in particular.

```
nmap –(-sF, -sN, -sX) –v <Target IP Address>
```

The `-sF` flag is used for FIN scan and `-sN` is for NULL scan.

## Xmas Scan

Avoids IDS and the TCP three-way handshake. Sends a probe packet (FIN + URG + PSH).  No response - Port is open. RST packet response - Port is closed. Works only when systems are compliant with the RFC 793–based TCP/IP implementation and the Unix platform only.&#x20;

```
nmap –sX –v <Target IP Address>
```

## ACK Scanning

Can evade IDS in most cases Helps in checking the filtering systems of target networks.  But it can be extremely slow and can exploit only older OSes with vulnerable BSD-derived TCP/IP stacks.

<table data-header-hidden><thead><tr><th width="142">Type</th><th width="165">Command</th><th width="150">Request</th><th width="237">Response</th></tr></thead><tbody><tr><td>ACK Flag Probe Scan</td><td><code>nmap -sA -V &#x3C;Target IP></code></td><td>ACK probe packets</td><td>No response Port is filtered (stateful firewall is present) RST packet response Port is not filtered (no firewall is present)</td></tr><tr><td>TTL-Based ACK Flag Probe Scan</td><td><code>nmap -sA -ttl 100 -v &#x3C;Target IP></code></td><td>ACK probe packets (several thousands) to different TCP ports</td><td>RST packet response Port is open (TTL value on a port &#x3C; 64) RST packet response - Port is closed (TTL value on a port > 64)</td></tr><tr><td>Window-Based ACK Flag Probe Scan</td><td><code>nmap -sA -sW &#x3C;Target IP></code></td><td>ACK probe packets (several thousands) to different TCP ports</td><td>RST packet response Port is open (WINDOW value on a port is non-zero) ICMP unreachable error response - Port is filtered RST packet response Port is closed (WINDOW value on a port is zero)</td></tr></tbody></table>

## UDP Scan

Less informal with regard to an open port because there is no overhead of a TCP handshake. Microsoft-based OSes do not usually implement any ICMP rate limiting; hence, this scan operates very efficiently on Windows-based devices.

```
nmap –sU –v <Target IP Address>
```

## SCTP Scans

### SCTP INIT Scan

Sends a INIT chunk. An INIT scan is performed quickly by scanning thousands of ports per second on a fast network not obstructed by a firewall, offering a strong sense of security. Can clearly differentiate between various ports such as open, closed, and filtered states.

INIT+ACK chunk - Port is open. ICMP unreachable exception - Port is filtered. ABORT chunk - Port is closed

```
nmap -SY -V <Target IP>
```

### SCTP Cookie ECHO Scan

Sends in a COOKIE ECHO chunk. The COOKIE ECHO chunk is not blocked by non-stateful firewall rule sets. Only an advanced IDS can detect an SCTP COOKIE ECHO scan.  No response Port is open ABORT chunk Port is closed.&#x20;

```
nmap -sZ -V <Target IP>
```

Cannot differentiate clearly between open and filtered ports, showing the output as open filtered in both cases.

## OS Discovery

### Based on TTL

| Operating System | Time To Live | TCP Window Size            |
| ---------------- | ------------ | -------------------------- |
| Linux            | 64           | 5840                       |
| FreeBSD          | 64           | 65535                      |
| OpenBSD          | 255          | 16384                      |
| Windows          | 128          | 65,535 bytes to 1 Gigabyte |
| Cisco Routers    | 255          | 4128                       |
| Solaris          | 255          | 8760                       |
| AIX              | 255          | 16384                      |

Wireshark or unicornscan can be used to find the TTL and derive the OS being used by the target.

### Nmap

In Nmap, the `-O` option is used to perform OS discovery, providing OS details of the target machine.

```
nmap -O <Target IP>
```

The nmap scripting engine can also be used to find OS versions based on certain services like SMB. For example, in Nmap, smb-os-discovery is an inbuilt script that can be used for collecting OS information on the target machine through the SMB protocol.

