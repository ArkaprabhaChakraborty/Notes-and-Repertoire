# SNMP Basics

## Parts of an SNMP Network

An SNMP-managed network consists of three key components:

* Managed devices.
* [Agent](https://en.wikipedia.org/wiki/Software\_agent) – software which runs on managed devices.
* [Network management station](https://en.wikipedia.org/wiki/Network\_management\_station) (NMS) – software which runs on the manager.

SNMP consists of a manager and an agent. Agents are embedded on every network device, and the manager is installed on a separate computer.

## How does SNMP work?

Working of SNMP SNMP uses a disturbed architecture comprising SNMP managers, SNMP agents, and several related components.&#x20;

The following are some commands associated with SNMP:

▪ **GetRequest**: Used by the SNMP manager to request information from an SNMP agent.

▪ **GetNextRequest**: Used by the SNMP manager continuously to retrieve all the data stored in an array or table.

▪ **GetResponse**: Used by an SNMP agent to satisfy a request made by the SNMP manager.&#x20;

▪ **SetRequest**: Used by the SNMP manager to modify the value of a parameter within an SNMP agent’s management information base (MIB).&#x20;

▪ **Trap**: Used by an SNMP agent to inform the pre-configured SNMP manager of a certain event.

## Connection Strings Primer

SNMP contains the following two passwords for configuring and accessing the SNMP agent from the management station.&#x20;

▪ **Read Community String**: The configuration of the device or system can be viewed with the help of this password.  These strings are public.&#x20;

▪ **Read/Write Community String**:  The device configuration can be changed or edited using this password. These strings are private.

When administrators leave the community strings at the default setting, attackers can use these default community strings (passwords) for changing or viewing the configuration of the device or system.&#x20;

&#x20;
