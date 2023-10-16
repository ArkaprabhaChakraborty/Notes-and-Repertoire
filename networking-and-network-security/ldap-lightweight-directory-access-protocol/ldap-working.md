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

## Schema

The contents of the entries in a subtree are governed by a [directory schema](https://en.wikipedia.org/wiki/Logical\_schema), a set of definitions and constraints concerning the structure of the directory information tree (DIT).

The schema of a Directory Server defines a set of rules that govern the kinds of information that the server can hold. It has a number of elements, including:

* Attribute Syntaxes—Provide information about the kind of information that can be stored in an attribute.
* Matching Rules—Provide information about how to make comparisons against attribute values.
* Matching Rule Uses—Indicate which attribute types may be used in conjunction with a particular matching rule.
* Attribute Types—Define an [object identifier](https://en.wikipedia.org/wiki/Object\_identifier) (OID) and a set of names that may refer to a given attribute, and associates that attribute with a syntax and set of matching rules.
* Object Classes—Define named collections of attributes and classify them into sets of required and optional attributes.
* Name Forms—Define rules for the set of attributes that should be included in the RDN for an entry.
* Content Rules—Define additional constraints about the object classes and attributes that may be used in conjunction with an entry.
* Structure Rule—Define rules that govern the kinds of subordinate entries that a given entry may have.

## Tasks that can be accomplished using LDAP

* **Add.** Enter a new file into the database.&#x20;
* **Delete.** Take out a file from the database.&#x20;
* **Search.** Start a query to find something within the database.&#x20;
* **Compare.** Examine two files for similarities or differences.&#x20;
* **Modify.** Make a change to an existing entry.

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

**DN (Distinguished Name)** - This refers to the name that uniquely identifies an entry in the directory.  This consists of its _Relative Distinguished Name_ (RDN), constructed from some attribute(s) in the entry, followed by the parent entry's DN. Think of the DN as the [full file path](https://en.wikipedia.org/wiki/Full\_path) and the RDN as its relative filename in its parent folder (e.g. if `/foo/bar/myfile.txt` were the DN, then `myfile.txt` would be the RDN). **Relative distinguished name (RDN)** is a way of tying DNs together while specifying the relative location.

**CN (Common Name)** -  This refers to the individual object (person's name; meeting room; recipe name; job title; etc.) for whom/which you are querying.

**DC (Domain Component)** - This refers to each component of the domain. For example www.mydomain.com would be written as DC=www,DC=mydomain,DC=com&#x20;

**OU (Organizational Unit)** - This refers to the organizational unit (or sometimes the user group) that the user is part of. If the user is part of more than one group, you may specify as such, e.g., OU= Lawyer,OU= Judge.

The **Basic Encoding Rules (BER)** format is used to transmit information between the client and server.

## LDAP Query

An LDAP query typically involves:

* **Session connection.** The user connects to the server via an LDAP port.&#x20;
* **Request.** The user submits a query, such as an email lookup, to the server.&#x20;
* **Response.** The LDAP protocol queries the directory, finds the information, and delivers it to the user.&#x20;
* **Completion.** The user disconnects from the LDAP port.

## URI scheme

An LDAP [uniform resource identifier (URI)](https://en.wikipedia.org/wiki/Uniform\_resource\_identifier) scheme exists, which clients support in varying degrees, and servers return in referrals and continuation references (see RFC 4516):

```
ldap://host:port/DN?attributes?scope?filter?extensions
```

Most of the components described below are optional.

* The `host` is the [FQDN](https://en.wikipedia.org/wiki/Fully\_qualified\_domain\_name) or IP address of the LDAP server to search.
* The `port` is the [network port](https://en.wikipedia.org/wiki/Network\_port) (default port 389) of the LDAP server.
* The `DN` is the distinguished name to use as the search base.
* The _`attributes`_ is a comma-separated list of attributes to retrieve.
* The `scope` specifies the search scope and can be "base" (the default), "one" or "sub".
* The `filter` is a search filter. For example, `(objectClass=*)` as defined in RFC 4515.
* The `extensions` are extensions to the LDAP URL format.



