---
description: A primer on NTP enumeration and exploitation
---

# NTP

Network Time Protocol (NTP) is designed to synchronize the clocks of networked computers.&#x20;

It uses **UDP port 123** as its primary means of communication.

The following are some pieces of information an attacker can obtain by querying an NTP server:&#x20;

▪ List of hosts connected to the NTP server.&#x20;

▪ Clients IP addresses in the network, their system names, and OSs.&#x20;

▪ Internal IPs, if the NTP server is in the demilitarized zone (DMZ).

## Enumeration

NTP enumeration commands such as `ntpdate`, `ntptrace`, `ntpdc`, and `ntpq` are used to query an NTP server for valuable information.

* **ntpdate**: This command collects the number of time samples from a number of time sources
* **ntptrace**: This command determines from where the NTP server gets time and follows the chain of NTP servers back to its prime time source
* **ntpdc**: This command queries the ntpd daemon about its current state and requests changes in that state
* **ntpq**: This command monitors NTP daemon ntpd operations and determine performance

### Using ntpdate

The `ntpdate` command collects the number of time samples from several time sources. Its syntax is as follows:

{% code overflow="wrap" %}
```
ntpdate [-46bBdqsuv] [-a key] [-e authdelay] [-k keyfile] [-o version] [-p samples] [-t timeout] [ -U user_name] server
```
{% endcode %}

More Options:

<table><thead><tr><th width="185">Flag</th><th>Function</th></tr></thead><tbody><tr><td><code>-4</code></td><td>Force DNS resolution of given host names to the IPv4 namespace</td></tr><tr><td><code>-6</code></td><td>Force DNS resolution of given host names to the IPv6 namespace</td></tr><tr><td><code>-a key</code></td><td>Enable the authentication function/specify the key identifier to be used for authentication</td></tr><tr><td><code>-B</code></td><td>Force the time to always be slewed</td></tr><tr><td><code>-b</code></td><td>Force the time to be stepped</td></tr><tr><td><code>-d</code></td><td>Enable debugging mode</td></tr><tr><td><code>-e authdelay</code></td><td>Specify the processing delay to perform an authentication function</td></tr><tr><td><code>-k keyfile</code></td><td>Specify the path for the authentication key file as the string "keyfile"; the default is /etc/ntp/keys</td></tr><tr><td><code>-O version</code></td><td>Specify the NTP version for outgoing packets as an integer version, which can be 1 or 2; the default is 4.</td></tr><tr><td><code>-p samples</code></td><td>Specify the number of samples to be acquired from each server, with values ranging from 1-8; the default is 4</td></tr><tr><td><code>-q</code></td><td>Query only; do not set the clock</td></tr><tr><td><code>-s</code></td><td>Divert logging output from the standard output (default) to the system syslog facility</td></tr><tr><td><code>-t timeout</code></td><td>Specify the maximum wait time for a server response; the default is 1 S</td></tr><tr><td><code>-u</code></td><td>Use an unprivileged port for outgoing packets</td></tr><tr><td><code>-V</code></td><td>Be verbose; logs ntpdate's version identification string</td></tr></tbody></table>

### Using ntptrace

The `ntptrace` command determines where the NTP server obtains the time from and follows the chain of NTP servers back to its primary time source. Attackers use this command to trace the list of NTP servers connected to the network.&#x20;

Its syntax is as follows:

```
ntptrace [-n] [-m maxhosts] [servername/IP_address]
```

More options

<table><thead><tr><th width="175">Flag</th><th>Function</th></tr></thead><tbody><tr><td><code>-n</code> </td><td>Do not print host names and show only IP addresses; may be useful if a name server is down.</td></tr><tr><td><code>-m maxhosts</code></td><td>Set the maximum number of levels up the chain to be followed.</td></tr></tbody></table>

{% code overflow="wrap" %}
```
ntptrace

localhost: stratum 4, offset 0.0019529, synch distance 0.143235 
10.10.0.1: stratum 2, offset 0.01142 73, synch distance 0.115554 
10.10.1.1: stratum 1, offset 0.0017698, synch distance 0.011193
```
{% endcode %}

### Using ntpq

The `ntpq` command monitors the operations of the NTP daemon ntpd and determines its performance.&#x20;

Its syntax is as follows:

```
ntpq [-46dinp] [-c command] [host/IP_address]
```

More options:



Example commands:

```bash
ntpq -c readlist <IP_ADDRESS>
ntpq -c readvar <IP_ADDRESS>
ntpq -c peers <IP_ADDRESS>
ntpq -c associations <IP_ADDRESS>
```

```
ntpq> version 
ntpq 4.2.8p15@1.3728-o 

ntpq> host
current host is localhost
```

### Using ntpdc

The `ntpdc` command queries the ntpd daemon regarding its current state and requests changes in that state. Attackers use this command to retrieve the state and statistics of each NTP server connected to the target network.&#x20;

Its syntax is as follows:&#x20;

```
ntpdc [ -46dilnps ] [ -c command] [hostname/IP_address]
```

More Options:

<table><thead><tr><th width="162">Flag</th><th>Function</th></tr></thead><tbody><tr><td><code>-4</code></td><td>Force DNS resolution of the given hostname to the IPv4 namespace </td></tr><tr><td><code>-6</code> </td><td>Force DNS resolution of the given hostname to the IPv6 namespace </td></tr><tr><td><code>-d</code> </td><td>Set the debugging mode to on </td></tr><tr><td><code>-c</code> </td><td>The following argument is interpreted as an interactive format command; multiple <code>-c</code> options may be given</td></tr><tr><td><code>-i</code> </td><td>Force ntpdc to operate in the interactive mode </td></tr><tr><td><code>-l</code> </td><td>Obtain a list of peers known to the server(s); this switch is equivalent to <code>-c</code> listpeers</td></tr><tr><td><code>-n</code></td><td>Output all host addresses in the dotted-quad numeric format, rather than host names </td></tr><tr><td><code>-p</code></td><td>Print a list of the peers as well as a summary of their states; this is equivalent to <code>-c</code> peers</td></tr><tr><td><code>-s F</code></td><td>Print a list of the peers as well as a summary of their states, but in a slightly different format from that for the <code>-p</code> switch; this is equivalent to <code>-c dmpeers</code>.</td></tr></tbody></table>

Usage examples:

```
ntpdc -c monlist <IP_ADDRESS>
ntpdc -c listpeers <IP_ADDRESS>
ntpdc -c sysinfo <IP_ADDRESS>
```

### Using nmap

```bash
nmap -sU -sV --script "ntp* and (discovery or vuln) and not (dos or brute)" -p 123 <IP>
```
