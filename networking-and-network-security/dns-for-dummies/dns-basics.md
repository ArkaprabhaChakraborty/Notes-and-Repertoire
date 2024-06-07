---
description: Some key concepts about DNS
---

# DNS Basics

## Domain Name Space

The **domain name space** is a "[tree](https://en.wikipedia.org/wiki/Tree\_\(data\_structure\))" data structure, where every node has a "label" and zero or more RRs.  The tree or domain name space subdivides into zones, beginning at the root zone - the first zone in a DNS namespace (like the root of a "[tree](https://en.wikipedia.org/wiki/Tree\_\(data\_structure\))").&#x20;

**`Root Zone`** refers to the highest level of the [Domain Name System](https://icannwiki.org/DNS) (DNS) structure. It contains the names and the numeric IP addresses for all the top-level domain names - stored in a root zone file or [root zone database](https://www.iana.org/domains/root/db). The root zone is serviced by several servers (around 600+ servers) in different countries.

<img src="../../.gitbook/assets/file.excalidraw (3).svg" alt="Schematic of a domain name space" class="gitbook-drawing">

There are `13 root name server addresses` (limitation due to the unfragmented UDP packet size) which can be `accommodated` in one "name-resolution-query". Each of the 13 addresses has several servers (also sometimes called root server clusters), which use `Anycast routing` to distribute requests based on load and proximity.&#x20;

## Naming Convention

The domain name consists of the labels of each node in the domain name space concatenated together using the  `.` symbol.  The hierarchy of domains go from right to left, each label to the left specifies a subdivision, or [subdomain](https://en.wikipedia.org/wiki/Subdomain) of the domain to the right.&#x20;

<img src="../../.gitbook/assets/file.excalidraw (4).svg" alt="A breakdown of a Fully Qualified Domain Name " class="gitbook-drawing">

The maximum length of a DNS name is 255 octets. This is spelled out in [RFC 1035](http://tools.ietf.org/html/rfc1035) [section 2.3.4](http://www.freesoft.org/CIE/RFC/1035/9.htm). he readable maximum length of an ASCII DNS name is 253 characters.

## Resource Records

DNS uses a special database called a DNS Zone database. Each such databases have a collection of "Resource Records" (also called RRs or zone files) to respond to "name resolution" queries from a user/client.

RRs are the basic building blocks of host-name and IP information and are used to resolve all DNS queries.

Before DNS the name resolution was done using hosts file by the Operating System of the user/client. For unix/linux systems its the `/etc/hosts` whereas for windows its the `C:\Windows\System32\drivers\etc\hosts.`

<figure><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/59/All_active_dns_record_types.png/1280px-All_active_dns_record_types.png" alt=""><figcaption><p>A graphical overview of all active DNS record types (Credits Wikipedia)</p></figcaption></figure>

The most interesting DNS records for us would be the AXFR, MX, AAAA, DHCID, DNSKEY and TXT records.

Common DNS records include

* **`A`**
  * Points a domain to an IPv4 address, such as `11.22.33.44`.
* **`AAAA`**
  * Points a domain to an IPv6 address, such as `FE80::0202:B3FF:FE1E:8329`.
* **`CNAME`**
  * Link a subdomain to a domain's existing A or AAAA record. A Canonical Name (CNAME) record is a type of [resource record](https://en.wikipedia.org/wiki/Resource\_record) in the [Domain Name System](https://en.wikipedia.org/wiki/Domain\_Name\_System) (DNS) that maps one domain name (an alias) to another (the [canonical](https://en.wikipedia.org/wiki/Canonical\_form) name).
  * E.g. `www.cloudarchitecture.io` to `cloudarchitecture.io`
* **`MX`**
  * Mail eXchange records are used to direct emails sent to domain
  * See also [MX records | Whois, GeoIpLocation and DNS interrogation](https://github.com/undergroundwires/CEH-in-bullet-points/blob/master/chapters/02-footprinting/whois-geoiplocation-and-dns-interrogation.md#mx-records)
* **`NS`**
  * Used to delegate a domain or subdomain to a set of name servers
* **`SOA`**
  * Contains data to control the zone transfer.
  * Includes serial number, timestamps, mail address of zone responsible..
  *   E.g.

      ```
        $TTL 86400
        @   IN  SOA     ns.icann.org. noc.dns.icann.org. (
                2020080302  ;Serial
                7200        ;Refresh
                3600        ;Retry
                1209600     ;Expire
                3600        ;Minimum TTL
        )
      ```
* **`PTR`**
  * Opposite of `A`, points an IP to domain
  * Commonly used for spam verification for e-mail programs
* **`HINFO`**
  * System information including CPU and OS type.

## Types of DNS servers

A fundamental component of DNS are DNS servers or name servers. There are four types of DNS servers.

### **1. DNS Recursor or Recursive DNS Server**&#x20;

This is the first server the browser contacts to resolve a domain name to its IP address. It acts as an intermediary between a DNS nameserver and a client, checking its cache before making requests to various nameservers. Once it obtains the IP address from an Authoritative nameserver, it responds to the client and caches information for future requests.

### **2. DNS Root Server**

These are essential DNS nameservers operating in the root zone. They directly handle queries for records in the root zone and can refer other requests to the appropriate Top Level Domain (TLD) server. DNS lookups begin at the root zone, with recursive resolvers having a list of the 13 IP root server addresses. These addresses use Anycast routing, providing high reliability with over 600 servers distributed worldwide. Updates to a root server's IP address do not disrupt the Internet, as other IP addresses are available for DNS lookups until resolvers are updated.

### 3. Top Level Domain DNS Server

A top-level domain (TLD) is one of the [domains](./#what-is-a-domain-name) at the highest level in the hierarchical [Domain Name System](./#so-what-is-a-dns), after the root domain. The top-level domain names are installed in the root zone of the namespace. For all domains in lower levels, it is the last part of the domain name, the last non-empty label of a fully qualified domain name.&#x20;

For example, in the domain name www.example.com, the top-level domain is .com.&#x20;

There are 5 official types of TLDs:

1. **Infrastructure Top-Level Domain (ARPA):** This special category contains only one TLD, the [Address and Routing Parameter Area (ARPA)](https://en.wikipedia.org/wiki/.arpa). The .arpa domain extension is managed directly by the IANA for the [Internet Engineering Task Force (IETF)](https://en.wikipedia.org/wiki/Internet\_Engineering\_Task\_Force) under the guidance of the Internet Architecture Board (IAB) and is only used for technical infrastructure purposes and [RFCs](https://en.wikipedia.org/wiki/Request\_for\_Comments) publications.
2. **Generic Top-level Domains (gTLD): These** are the most popular and familiar types of domain extensions. These have two subcategories:&#x20;
   * Top-level domains with three or more characters.&#x20;
   * Generic restricted top-level domains (grTLD) - managed under official ICANN accredited registrars.
3. **Sponsored Top-level Domains (sTLD):** These domains are proposed and sponsored by private agencies or organizations that establish and enforce rules restricting the eligibility to use the TLD.
4. **Country Code Top-level Domains (ccTLD):** Two-letter domains established for [countries](https://en.wikipedia.org/wiki/Country) or [territories](https://en.wikipedia.org/wiki/List\_of\_dependent\_territories). With some historical exceptions, the code for any territory is the same as its two-letter [ISO 3166](https://en.wikipedia.org/wiki/ISO\_3166) code. There are 312 country code top-level domains established for specific countries and territories, identifying them with a two-letter string. These domain extensions have dedicated managers who ensure each ccTLD is operated according to local policies and meets the cultural, linguistic and legal standards of the region.
5.  **Test Top-Level Domains (tTLD):** These domains are reserved for documentation purposes and local testing, and cannot be installed into the root zone of the domain name system. According to the IETF, the reason for reserving these specific domain extensions is to reduce the possibility of conflict and confusion.

    There are four tTLDs:

    * **.example** - for place holding
    * **.invalid** - for invalid domain names
    * **.localhost** - for usage in local networks
    * **.test** - for testing purposes

### 4. Authoritative DNS server&#x20;

An authoritative server for a zone is the name server that stores the IP addresses for the zone and holds the information about the zone’s domains in the text file known as the primary zone file. It queries and is queried by other name servers in the DNS. The data it receives in response from other name servers are cached. Authoritative servers are not authoritative for cached data.

Authoritative DNS nameservers are responsible for providing answers to recursive DNS nameservers about where specific websites can be found. These answers contain important information for each domain, like IP addresses.

#### Types of Authoritative DNS servers

There are two types of authoritative servers: master (primary) and slave (secondary).&#x20;

1. **Master server (primary name server)** – A master server stores the original master copies of all zone records. A hostmaster only makes changes to master server zone records.\
   &#x20;\
   A primary server for a zone is the server that stores the definitive versions of all records in that zone. It is identified in the **`Start-Of-Authority (SOA)`** resource record.  The [Start of Authority](https://en.wikipedia.org/wiki/SOA\_record) (SOA) is a DNS record with information about a zone. Normally DNS name servers are set up in clusters. The database within each cluster is synchronised through zone transfers. The SOA record for a zone contains data to control the zone transfer. This is the serial number and different time spans.\
   \
   Each slave server gets updates via a special automatic updating mechanism of the DNS protocol. All slave servers maintain an identical copy of the master records.\

2. **Slave server (secondary name server)** – A slave server is exact replica of the master server. It is used to share DNS server load and to improve DNS zone availability in case the master server fails. \
   \
   A secondary server for a zone uses an automatic updating mechanism to maintain an identical copy of the primary server's database for a zone. Examples of such mechanisms include [DNS zone transfers](https://en.wikipedia.org/wiki/DNS\_zone\_transfer) and file transfer protocols.\
   \
   DNS provides a mechanism whereby the primary for a zone can notify all the known secondaries for that zone when the contents of the zone have changed. The contents of a zone are either manually configured by an administrator or managed using [Dynamic DNS](https://en.wikipedia.org/wiki/Dynamic\_DNS).

Each zone must have only one master name server, and it should have at least one secondary name server for backup purposes to minimise dependency on a particular node.&#x20;

Calling a particular name server a master or secondary server is misleading. Any given name server can take on either or both roles, as defined by the conf file (DNS configuration file).

The zone data updates and maintenance are reflected in the master name server and the changes are then reflected in secondary name servers. Both master and secondary name servers are authoritative for a zone.

#### Tasks of an authoritative DNS server

An authoritative DNS server performs two important tasks.&#x20;

* It stores lists of domain names and their associated IP addresses.&#x20;
* It responds to requests from a recursive DNS server (the person who needs to look up a number) about the correct IP address assigned to a domain name.&#x20;

After getting the answer, the recursive DNS server sends that information back to the computer (and browser) that requested it.&#x20;

### 5. Other types of servers

| **Server Type**                | **Description**                                                                                                                                                                                            |
| ------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Non-authoritative Nameserver` | Non-authoritative name servers are not responsible for a particular DNS zone. Instead, they collect information on specific DNS zones themselves, which is done using recursive or iterative DNS querying. |
| `Caching DNS Server`           | Caching DNS servers cache information from other name servers for a specified period. The authoritative name server determines the duration of this storage.                                               |
| `Forwarding Server`            | Forwarding servers perform only one function: they forward DNS queries to another DNS server.                                                                                                              |
| `Resolver`                     | Resolvers are not authoritative DNS servers but perform name resolutions locally in the computer or router.                                                                                                |

## How DNS works?

Now that we know what DNS is, components of domain name, what name servers are, their types, what are zone resource records, etc, let's now see how DNS works.

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption><p>This is how DNS works</p></figcaption></figure>

## DNS Security Mechanisms

**Domain Keys Identified Mail (DKIM)** provides a cryptographic authentication mechanism. This can replace or supplement SPF. To configure DKIM, the organization uploads a public key as a TXT record in the DNS server.&#x20;

**Sender Policy Framework (SPF)** uses a DNS record published by an organization hosting an email service. The SPF record identifies the hosts authorized to send email from that domain, and there must be only one per domain. SPF does not provide a cryptographic authentication mechanism like DKIM does, though.&#x20;

The **Domain-Based Message Authentication, Reporting, and Conformance (DMARC)** framework ensures that SPF and DKIM are being utilized effectively. DMARC relies on DKMI for the cryptographic authentication mechanism.
