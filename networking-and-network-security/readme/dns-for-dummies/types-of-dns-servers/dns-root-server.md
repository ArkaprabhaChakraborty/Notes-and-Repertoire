---
description: Also called as root name server
---

# DNS Root Server

Root servers are DNS nameservers that operate in the root zone. These servers can directly answer queries for records stored or cached within the root zone, and they can also refer other requests to the appropriate Top Level Domain (TLD) server.

During an uncached DNS query, whenever a user enters a web address into their browser, this action triggers a DNS lookup, and all DNS lookups start at the root zone.

Since the DNS root zone is at the top of the DNS hierarchy, recursive resolvers cannot be directed to them in a DNS lookup. Because of this, every DNS resolver has a list of the 13 IP root server addresses built into its software. Whenever a DNS lookup is initiated, the recursor’s first communication is with one of those 13 IP addresses.

A common misconception is that there are only 13 root servers in the world. In reality there are many more, but still only 13 IP addresses used to query the different root server networks. Limitations in the original architecture of DNS require there to be a maximum of 13 server addresses in the root zone. In the early days of the Internet, there was only one server for each of the 13 IP addresses, most of which were located in the United States.

Today each of the 13 IP addresses has several servers, which use [Anycast routing](https://www.cloudflare.com/learning/cdn/glossary/anycast-network/) to distribute requests based on load and proximity. Right now there are over 600 different DNS root servers distributed across every populated continent on earth.

Thanks to the use of Anycast routing and heavy redundancy, the root servers are very reliable. But on rare occasions a root server will have to update its IP address. In this case, recursive resolvers can continue using the other 12 IP addresses in the root zone to perform DNS lookups until their software is updated with the correct addresses of all 13 servers. Since resolvers will retry until they reach a working root server, there is no disruption to the normal operations of the Internet when one root server is down.
