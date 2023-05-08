---
description: Also called namespaces
---

# Domain name space

The **domain name space** is a "[tree](https://en.wikipedia.org/wiki/Tree\_\(data\_structure\))" data structure, where every node has a "label" and zero or more [RRs](dns-resource-records.md).&#x20;

The [Internet Corporation for Assigned Names and Numbers](https://en.wikipedia.org/wiki/Internet\_Corporation\_for\_Assigned\_Names\_and\_Numbers) (ICANN) is the organization that looks over the top-level development and the architecture of the Internet domain name space.  ICANN authorizes [domain name registrars](https://en.wikipedia.org/wiki/Domain\_name\_registrar), through which domain names may be registered and reassigned.

The tree or domain name space subdivides into zones, beginning at the root zone - the first zone in a DNS namespace (like the root of a "[tree](https://en.wikipedia.org/wiki/Tree\_\(data\_structure\))").&#x20;

## Root Zone vs Root Name Server

Now there is a stark difference between the root zone and the [root name server](types-of-dns-servers/dns-root-server.md).&#x20;

Root Zone refers to the highest level of the [Domain Name System](https://icannwiki.org/DNS) (DNS) structure. It contains the names and the numeric IP addresses for all the top-level domain names - stored in a root zone file or [root zone database](https://www.iana.org/domains/root/db).

There are `13 root name server addresses` (limitation due to the unfragmented UDP packet size) which can be `accommodated` in one "name-resolution-query". Note that I said **ADDRESSES** and not servers.&#x20;

The root zone is serviced by several servers (around 600+ servers) in different countries - each of the 13 addresses has several servers (also sometimes called root server clusters), which use [Anycast routing](../addressing-methods/anycast-addressing.md) to distribute requests based on load and proximity.&#x20;

<img src="../../.gitbook/assets/file.excalidraw (2).svg" alt="" class="gitbook-drawing">

