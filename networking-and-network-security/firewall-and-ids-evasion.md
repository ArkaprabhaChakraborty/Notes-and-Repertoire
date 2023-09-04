---
description: Various Techniques for Scanning Beyond IDS and Firewall
---

# Firewall and IDS Evasion

Intrusion detection systems (IDS) and firewalls are security mechanisms intended to prevent an attacker from accessing a network.

Though firewalls and IDSs can prevent malicious traffic (packets) from entering a network, attackers can manage to send intended packets to the target by evading an IDS or firewall through the following techniques:

## Packet Fragmentation

Packet fragmentation refers to the splitting of a probe packet into several smaller packets (fragments) while sending it to a network.  The TCP header is split into several packets so that the packet filters are not able to detect what the packets are intended to do.

The -f flag in nmap performs packet fragmentation. Once chosen, the IP data will be divided into 8 bytes or less. Adding another `-f` (`-f -f` or `-ff`) will split the data into 16 byte-fragments instead of 8.&#x20;

```
nmap -f 10.10.10.10
```

You can change the default value by using the `--mtu`; however, you should always choose a multiple of 8.&#x20;

```
nmap --mtu 24 223.23.23.12
```

## Source Routing

Source routing refers to sending a packet to the intended destination with a partially or completely specified route (without firewall-/IDS-configured routers) in order to evade an IDS or firewall.  In source routing, the attacker makes some or all of these decisions on the router.

Using the `--ip-options` flag in nmap we can use source routing.

Simply pass the letter `R`, `T`, or `U` to request record-route, record-timestamp, or both options together, respectively. Loose or strict source routing may be specified with an `L` or `S` followed by a space and then a space-separated list of IP addresses.

## Source Port Manipulation

Source port manipulation refers to manipulating actual port numbers with common port numbers in order to evade an IDS or firewall.  It occurs when a firewall is configured to allow packets from well-known ports like HTTP, DNS, FTP, etc..

In nmap we can use the `-g` flag or the `--source-port` flag to specify the port number.

```
nmap -g 80 10.10.10.10
```

## IP Address Decoy

The `-D` flag causes a decoy scan to be performed, which makes it appear to the remote host that the host(s) you specify as decoys are scanning the target network too. Thus their IDS might report 5–10 port scans from unique IP addresses, but they won't know which IP was scanning them and which were innocent decoys.

To Perform Decoy Scan and Generate Random non-reserved IP:

```
nmap -D RND:10 10.10.10.10
```

Manually specify the IP addresses of the decoys:

```
nmap -D decoy1,decoy2,decoy3
```

While this can be defeated through router path tracing, response-dropping, and other active mechanisms, it is generally an effective technique for hiding your IP address.

Decoys are used both in the initial host discovery scan (using ICMP, SYN, ACK, or whatever) and during the actual port scanning phase.&#x20;

Decoys are also used during remote OS detection (`-O`). Decoys do not work with version detection or TCP connect scan.&#x20;

When a scan delay is in effect, the delay is enforced between each batch of spoofed probes, not between each individual probe. Because decoys are sent as a batch all at once, they may temporarily violate congestion control limits.

## IP Address Spoofing

IP spoofing refers to changing the source IP addresses so that the attack appears to be coming from someone else. When the victim replies to the address, it goes back to the spoofed address rather than the attacker’s real address. Attackers modify the address information in the IP packet header and the source address bits field in order to bypass the IDS or firewall.

**Note: You will not be able to complete the three-way handshake and open a successful TCP connection with spoofed IP addresses. This is why you need to PIVOT on that IP using a SOCKS proxy or any other methods of proxy.**&#x20;

#### Using Hping3

```
hping3 www.certifiedhacker.com -a 7.7.7.7
```

#### Using nmap

The -S flag can spoof the IP address but you usually won't receive reply packets back (they will be addressed to the IP you are spoofing), so Nmap won't produce useful reports.&#x20;

```
nmap -S 7.7.7.7 10.10.10.10
```

The `-e` option and `-Pn` are generally required for this sort of usage.

## MAC Address Spoofing

The `--spoof-mac` asks Nmap to use the given MAC address for all of the raw ethernet frames it sends. This option implies `--send-eth` to ensure that Nmap actually sends ethernet-level packets.&#x20;

The MAC given can take several formats.&#x20;

* If it is simply the number `0`, Nmap chooses a completely random MAC address for the session.&#x20;
* If the given string is an even number of hex digits (with the pairs optionally separated by a colon), Nmap will use those as the MAC.&#x20;
* If fewer than 12 hex digits are provided, Nmap fills in the remainder of the six bytes with random values.&#x20;
* If the argument isn't a zero or hex string, Nmap looks through `nmap-mac-prefixes` to find a vendor name containing the given string (it is case insensitive).&#x20;
* If a match is found, Nmap uses the vendor's OUI (three-byte prefix) and fills out the remaining three bytes randomly.&#x20;

Valid `--spoof-mac` argument examples are `Apple`, `0`, `01:02:03:04:05:06`, `deadbeefcafe`, `0020F2`, and `Cisco`.&#x20;

This option only affects raw packet scans such as SYN scan or OS detection, not connection-oriented features such as version detection or the Nmap Scripting Engine.

```
nmap --spoof-mac Cisco 10.10.10.10
```

## Randomizing Host Order

Attackers scan the number of hosts in the target network in random order to scan an intended target that is behind a firewall.&#x20;

The flag `--randomize-hosts` can be used with nmap for this:

```
nmap --randomize-hosts 10.10.10.11
```

## Sending Bad Checksums

Attackers send packets with bad or bogus TCP/UDP checksums to the intended target to avoid certain firewall rule sets.

```
nmap --badsum 10.10.10.11
```

## Proxy Servers

A proxy server is an application that can serve as an intermediary for connecting with other computers.&#x20;

### Proxy with Nmap

For proxying with Nmap we can use `--proxies` flag. This option takes a list of proxies as argument, expressed as URLs in the format `proto://host:port`.&#x20;

Use commas to separate node URLs in a chain. No authentication is supported yet. Valid protocols are `HTTP` and `SOCKS4`.

```
nmap -sS -Pn --proxies PROXY_URL -F MACHINE_IP
```

Proxies can be chained in Nmap as follows:

```
nmap -sS -Pn --proxies PROXY_URL_1, PROXY_URL_2 -F MACHINE_IP
```

This means the final source would be PROXY\_URL\_2 before hitting the target. The target would respond back to PROXY\_URL\_2 which needs to be relayed back using a HTTP or a SOCKS4 proxy.

**Disadvantage:** It is implemented within the nsock library and thus has no effect on the ping, port scanning and OS discovery phases of a scan. Only NSE and version scan benefit from this option so far—other features may disclose your true address. SSL connections are not yet supported, nor is proxy-side DNS resolution (host names are always resolved by Nmap).

### Proxy chaining with proxychains

Proxychains can be used for proxying Nmap traffic and performing scans with little restrictions. Proxychains allows TCP and DNS tunnelling through proxies.

```
proxychains nmap -Pn -n -sT <target IP>
```

The above flags are the best way to the scans so that we don't leak out our actual source IP.

## Anonymizers

An anonymizer removes all identity information from the user’s computer while the user surfs the Internet Anonymizers make activity on the Internet untraceable Anonymizers allow you to bypass Internet censors

## Creating Custom Packets

Custom packets can be created using Scapy and python or tools like Colasoft Packet Builder.
