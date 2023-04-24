---
description: Also called a recursive DNS server
---

# DNS Recursor

**DNS recursor** is the first server that the browser hits after it has searched it's cache and the hosts file for resolving a domain name to its IP address. It's like a "librarian", who goes and "fetches" the particular book requested by the reader/user.

A recursive resolver serves as an intermediary between a DNS nameserver and a client.&#x20;

When a web client sends a DNS query, the recursive resolver checks if it has cached data to respond with, or else, it sends a request to a root nameserver, then to a TLD nameserver, and finally to an authoritative nameserver.&#x20;

Once the authoritative nameserver responds with the requested IP address, the recursive resolver sends a response to the client.

While going through the above process, the recursive resolver caches information from authoritative nameservers. This allows it to quickly serve a client's request for a domain's IP address without the need to communicate with nameservers again.

