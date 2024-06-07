---
description: >-
  A primer on one of the most used protocol that can be encountered in a network
  pentest
---

# LDAP (Lightweight Directory Access Protocol)

## What is LDAP?

Lightweight directory access protocol (LDAP) is an Internet protocol for accessing distributed directory services.

LDAP is an Internet protocol for accessing distributed directory services. LDAP accesses directory listings within Active Directory or from other directory services.&#x20;

LDAP is a hierarchical or logical form of a directory, similar to a company’s organizational chart. Directory services may provide any organized set of records, often in a hierarchical and logical structure, such as a corporate email directory.

A client starts an LDAP session by connecting to a **Directory System Agent (DSA)**, typically on TCP port **389**, and sends an operation request to the DSA.

#### **LDAP with SSL or LDAPS runs on TCP port 636**.&#x20;

**Global Catalog** (LDAP in ActiveDirectory) is available by default on **TCP ports 3268**, and **3269 for LDAPS**.
