---
description: A primer into the working of the LDAP protocol
---

# LDAP Working

## Structure of LDAP directory

An LDAP directory is organized in a simple "tree" hierarchy consisting of the following levels:

* The root directory
* Countries
* Organizations
* Organizational units
* Individuals



<img src="../../.gitbook/assets/file.excalidraw (5).svg" alt="The LDAP Tree" class="gitbook-drawing">

## Data Transfer

LDIF (LDAP Data Interchange Format) defines the directory content as a set of records. It can also represent update requests (Add, Modify, Delete, Rename).

For the dump given below:

* Lines 1-3: define the top-level domain local
* Lines 5-8: define the first level domain. Here we use moneycorp as an example (moneycorp.local)
* Lines 10-16: define 2 organizational units: dev and sales
* Lines 18-26: create an object of the domain and assign attributes with values

```
dn: dc=local
dc: local
objectClass: dcObject

dn: dc=moneycorp,dc=local
dc: moneycorp
objectClass: dcObject
objectClass: organization

dn ou=it,dc=moneycorp,dc=local
objectClass: organizationalUnit
ou: dev

dn: ou=marketing,dc=moneycorp,dc=local
objectClass: organizationalUnit
Ou: sales

dn: cn= ,ou= ,dc=moneycorp,dc=local
objectClass: personalData
cn:
sn:
gn:
uid:
ou:
mail: pepe@hacktricks.xyz
phone: 23627387495
```

The **Basic Encoding Rules (BER)** format is used to transmit information between the client and server.
