---
description: Different ways in which a domain can be named...
---

# Naming Conventions

The domain name consists of the labels of each node in the domain name space concatenated together using the  `.` symbol.

&#x20;The hierarchy of domains is from right to left, each label to the left specifies a subdivision, or [subdomain](https://en.wikipedia.org/wiki/Subdomain) of the domain to the right.&#x20;

The root level being the extreme right, represented by a empty label is reserved for the root node and when fully qualified is expressed as the empty label terminated by a`.` at the right end. Generally, we do not type this in browser or curl or any tool we use to interact with a website or "domain".

The rightmost "label" is the name of the top level domain. Following that we have the second order domain. Generally, the organization name is chosen to be the second order domain label.

Each label may contain from 1 to 63 [octets](https://en.wikipedia.org/wiki/Octet\_\(computing\)). The full domain name cannot exceed beyond 253 ASCII characters.

<img alt="" class="gitbook-drawing">
