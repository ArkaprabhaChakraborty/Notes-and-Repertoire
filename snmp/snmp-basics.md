---
description: A primer on the protocol works
---

# SNMP Basics

## Parts of an SNMP Network

SNMP uses a disturbed architecture comprising SNMP managers, SNMP agents, and several related components.&#x20;

An SNMP-managed network consists of three key components:

* Managed devices.
* [Agent](https://en.wikipedia.org/wiki/Software\_agent) – software which runs on managed devices.
* [Network management station](https://en.wikipedia.org/wiki/Network\_management\_station) (NMS) – software which runs on the manager.

SNMP consists of a manager and an agent. Agents are embedded on every network device, and the manager is installed on a separate computer.

A _**managed device**_ is a network node that implements an SNMP interface that allows unidirectional (read-only) or bidirectional (read and write) access to node-specific information. Managed devices exchange node-specific information with the NMSs.&#x20;

An _**agent**_ is a network-management software module that resides on a managed device. An agent has local knowledge of management information and translates that information to or from an SNMP-specific form.

A _**network management** station_ executes applications that monitor and control managed devices. NMSs provide the bulk of the processing and memory resources required for network management. One or more NMSs may exist on any managed network.

## SNMP Commands

The following are some commands associated with SNMP:

▪ **GetRequest**: Used by the SNMP manager to request information from an SNMP agent.

▪ **GetNextRequest**: Used by the SNMP manager continuously to retrieve all the data stored in an array or table.

▪ **GetResponse**: Used by an SNMP agent to satisfy a request made by the SNMP manager.&#x20;

▪ **SetRequest**: Used by the SNMP manager to modify the value of a parameter within an SNMP agent’s management information base (MIB).&#x20;

▪ **Trap**: Used by an SNMP agent to inform the pre-configured SNMP manager of a certain event.

## How does SNMP work?

The SNMP communication process between the manager (Host X: 10.10.2.1) and agent (Host Y:  10.10.2.15), with a preconfigured host or trap destination for default errors (Host Z: 10.10.2.12) involves the following steps:

1. Host X sends a `GetRequest` command to request active session information from Host Y (SNMP agent) using an SNMP service library.
2. Host Y verifies the **community string** (Let's say in this case it's `Compinfo`) in its **MIB**, checks access permissions, and validates the source IP address.
3. If the SNMP agent does not find the community string or access permission in Host Y’s MIB database and the SNMP service is set to send an authentication **trap**, it sends an authentication failure trap to the specified trap destination, Host Z
4. The master agent component of the SNMP agent calls the appropriate extension agent to retrieve the requested session information from the MIB
5. Using the retrieved session data from the extension agent, the SNMP service creates a response message with active session count of Host Y and Host X's IP or the destination IP (10.10.2.1).
6. Host Y sends the response to Host X.

To perform a GetRquest on Windows, the SNMP manager uses an SNMP service library such as the Microsoft SNMP Management API library (Mgmtapi.dll) or Microsoft WinSNMP API library (Wsnmp32.dll).

## Connection Strings Primer

SNMP contains the following two passwords for configuring and accessing the SNMP agent from the management station.&#x20;

▪ **Read Community String**: The configuration of the device or system can be viewed with the help of this password.  These strings are public.&#x20;

▪ **Read/Write Community String**:  The device configuration can be changed or edited using this password. These strings are private.

When administrators leave the community strings at the default setting, attackers can use these default community strings (passwords) for changing or viewing the configuration of the device or system.&#x20;

### Management Information Base

To ensure that SNMP access works across manufacturers and with different client-server combinations, the **Management Information Base (MIB)** was created. MIB is a virtual database containing a formal description of all the network objects that SNMP manages. It is a collection of hierarchically organized information. It provides a standard representation of the SNMP agent’s information and storage. MIB elements are recognized using object identifiers (OIDs).&#x20;

MIB is an **independent format for storing device information**. A MIB is a **text** file in which all queryable **SNMP objects** of a device are listed in a **standardized** tree hierarchy. It contains at **least one `Object Identifier` (`OID`)**, which, in addition to the necessary **unique address** and a **name**, also provides information about the type, access rights, and a description of the respective object.

MIB-managed objects include scalar objects, which define a single object instance, and tabular objects, which define a group of related object instances. OIDs include the object's type (such as counter, string, or address), access level (such as read or read/write), size restrictions, and range information. **The SNMP manager converts the OIDs into a human-readable display using the MIB as a codebook**.

MIB files are written in the `Abstract Syntax Notation One` (`ASN.1`) based ASCII text format. The **MIBs do not contain data**, but they explain **where to find which information** and what it looks like, which returns values for the specific OID, or which data type is used.

A user can access the contents of the MIB by using a web browser either by entering the IP address and Lseries.mib or by entering the DNS library name and Lseries.mib. For example, `http://IP.Address/Lseries.mib` or `http://library_name/Lseries.mib`.&#x20;

Microsoft provides the list of MIBs that are installed with the SNMP service in the Windows resource kit.&#x20;

The major MIBs are as follows:&#x20;

▪ DHCP.MIB: Monitors network traffic between DHCP servers and remote hosts&#x20;

▪ HOSTMIB.MIB: Monitors and manages host resources&#x20;

▪ LNMIB2.MIB: Contains object types for workstation and server services&#x20;

▪ MIB\_II.MIB: Manages TCP/IP-based Internet using a simple architecture and system&#x20;

▪ WINS.MIB: For the Windows Internet Name Service (WINS)

&#x20;
