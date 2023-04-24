# Authoritative DNS servers

Each domain must have one authoritative DNS server that publishes the information about the domain. **An authoritative server for a zone is the name server that stores the IP addresses for the zone and holds the information about the zone’s domains in the text file known as the primary zone file.**

It queries and is queried by other name servers in the DNS. The data it receives in response from other name servers are cached. Authoritative servers are not authoritative for cached data.

Authoritative DNS nameservers are responsible for providing answers to recursive DNS nameservers about where specific websites can be found. These answers contain important information for each domain, like IP addresses.

### Types of Authoritative DNS servers

There are two types of authoritative servers: master (primary) and slave (secondary).&#x20;

1. **Master server (primary name server)** – A master server stores the original master copies of all zone records. A hostmaster only makes changes to master server zone records.\
   &#x20;\
   A primary server for a zone is the server that stores the definitive versions of all records in that zone. It is identified in the [start-of-authority (SOA)](authoritative-dns-servers.md#start-of-authority) resource record. \
   \
   Each slave server gets updates via a special automatic updating mechanism of the DNS protocol. All slave servers maintain an identical copy of the master records.\

2. **Slave server (secondary name server)** – A slave server is exact replica of the master server. It is used to share DNS server load and to improve DNS zone availability in case the master server fails. \
   \
   A secondary server for a zone uses an automatic updating mechanism to maintain an identical copy of the primary server's database for a zone. Examples of such mechanisms include [DNS zone transfers](https://en.wikipedia.org/wiki/DNS\_zone\_transfer) and file transfer protocols.\
   \
   DNS provides a mechanism whereby the primary for a zone can notify all the known secondaries for that zone when the contents of the zone have changed. The contents of a zone are either manually configured by an administrator or managed using [Dynamic DNS](https://en.wikipedia.org/wiki/Dynamic\_DNS).

Each zone must have only one master name server, and it should have at least one secondary name server for backup purposes to minimize dependency on a particular node.&#x20;

Calling a particular name server a master or secondary server is misleading. Any given name server can take on either or both roles, as defined by the conf file (DNS configuration file).

The zone data updates and maintenance are reflected in the master name server and the changes are then reflected in secondary name servers. Both master and secondary name servers are authoritative for a zone.

### Tasks of an authoritative DNS server

An authoritative DNS server performs two important tasks.&#x20;

First, it stores lists of domain names and their associated IP addresses.&#x20;

Second, it responds to requests from a recursive DNS server (the person who needs to look up a number) about the correct IP address assigned to a domain name.&#x20;

After getting the answer, the recursive DNS server sends that information back to the computer (and browser) that requested it.&#x20;

### Start of Authority

&#x20;The [Start of Authority](https://en.wikipedia.org/wiki/SOA\_record) (SOA) is a DNS record with information about a zone. Normally DNS name servers are set up in clusters. The database within each cluster is synchronized through zone transfers. The SOA record for a zone contains data to control the zone transfer. This is the serial number and different timespans.

We can find the SOA record of a nameserver using nslookup. Consider google.com as an example:&#x20;

```bash
nslookup -type=soa google.com
```

We get a response specifying the primary name server and associated information:

```bash
Non-authoritative answer:
google.com
	origin = ns1.google.com
	mail addr = dns-admin.google.com
	serial = 526409246
	refresh = 900
	retry = 900
	expire = 1800
	minimum = 60
```

### Authoritative answer

**An authoritative answer is a response we get directly from the primary DNS server holding the master copy of the zone file.**  To find the authoritative answer for _google.com,_ we execute a new _nslookup_ query in which we specify the primary name server as _`ns1.google.com`._

```bash
nslookup ns1.google.com
```

Upon executing the command, we’ll get the following response, which gives us the addresses of the authoritative server for the specified domain.

```
Non-authoritative answer:
Name:	ns1.google.com
Address: 216.239.32.10
Name:	ns1.google.com
Address: 2001:4860:4802:32::a
```
