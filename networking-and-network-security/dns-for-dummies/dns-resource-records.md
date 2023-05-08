---
description: A dive into different resource records in a domain name space
---

# DNS Resource Records

DNS uses a special database called a  DNS Zone database. Each such databases have a collection of "Resource Records" (also called RRs or zone files) to respond to "name resolution" queries from a user/client.&#x20;

RRs are the basic building blocks of host-name and IP information and are used to resolve all DNS queries.

<figure><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/59/All_active_dns_record_types.png/1280px-All_active_dns_record_types.png" alt=""><figcaption><p>A graphical overview of all active DNS record types (Credits Wikipedia)</p></figcaption></figure>

Before DNS the name resolution was done using hosts file by the Operating System of the user/client.&#x20;

In fact the hosts file are still present to this date and the mechanism is still used. For unix/linux systems its the `/etc/hosts` whereas for windows its the `C:\Windows\System32\drivers\etc\hosts`
