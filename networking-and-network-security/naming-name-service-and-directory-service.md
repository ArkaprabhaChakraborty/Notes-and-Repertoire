---
description: What on earth are these???
---

# Naming/Name Service and Directory Service

If you're into infosec or network engineering these two buzz words have to b e common to you. The terms Name service and directory service are often used interchangeably, but they do have some slight difference.&#x20;

### What is a Name/Naming Service?

Naming Service is an entity that **associates names with values**, also known as `bindings`.  It provides a facility to **find an object** **based on a name** that is known as `lookup` or `search` operation. &#x20;

Some of the naming services are:

* DNS (Domain Name System)
* NetBIOS (Network Basic Input/Output System)&#x20;

### What is a Directory Service?

Directory Service is **a special type of Naming Service** that allows storing and finding of “directory objects.”&#x20;

A directory object differs from generic objects in that it's possible to associate attributes to the object. A Directory Service, therefore offers extended functionality to operate on the object attributes.

#### All Directory services are name services but not all name services are directory services.

Directory services were part of an [Open Systems Interconnection](https://en.wikipedia.org/wiki/Open\_Systems\_Interconnection) (OSI) initiative for common network standards and multi-vendor interoperability. During the 1980s, the [ITU](https://en.wikipedia.org/wiki/International\_Telecommunication\_Union) and [ISO](https://en.wikipedia.org/wiki/International\_Organization\_for\_Standardization) created the [X.500 set of standards](https://en.wikipedia.org/wiki/X.500) for directory services, initially to support the requirements of inter-carrier electronic messaging and network-name lookup.

The X.500 introduced Directory Access Protocol (DAP).

Some of the famous directory services are:

* NIS (Network Information System - developed by Sun Microsystems).
* NT Domains (Developed by Microsoft to provide directory services for Windows machines before the release of the LDAP-based Active Directory in Windows 2000).
* LDAP/X.500 implementations like Microsoft **A**ctive **D**irectory \[**D**omain **S**ervices, **C**ertificate **S**ervices], OpenLDAP, Apache Directory Server and OpenDS (There are many like these).

