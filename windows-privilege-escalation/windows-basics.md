---
description: Bare bones basics about windows management
---

# Windows Basics

## Permissions in Windows

### User Accounts

User accounts are used to log into a Windows System.  User accounts are basically a collection of settings bound to a particular unique identity.

There are several default user accounts like **Guest** and **Administrator**.

#### Managing user accounts

**The net user command**

The `net user` command is used to manage Windows user accounts.&#x20;

*   To list all users:

    {% code fullWidth="false" %}
    ```
    net user
    ```
    {% endcode %}
*   To add a user named "John" with password "Pass123":

    ```
    net user John Pass123 /add
    ```
*   To disable user "John":

    ```
    net user John /active:no
    ```
*   To delete user "John":

    ```
    net user John /delete
    ```

**Using wmic**&#x20;

List users

```
wmic useraccount get name,sid
```

```
wmic useraccount list full
```

```
wmic useraccount where name='username' get /all
```

Create user

{% code overflow="wrap" %}
```
wmic useraccount create name='NewUserName',password='Password',fullname='Full Name',description='Description'
```
{% endcode %}

Unlock user&#x20;

```
wmic useraccount where name='username' set PasswordRequired=false
```

```
wmic useraccount where name='username' set disabled=false
```

**Using PowerShell**

Create user

{% code overflow="wrap" fullWidth="false" %}
```
New-LocalUser -Name "John" -Password (ConvertTo-SecureString "P@ssw0rd" -AsPlainText -Force) -FullName "John Doe" -Description "Test User"
```
{% endcode %}

Add to group

```
Add-LocalGroupMember -Group "Administrators" -Member "John"
```

List all local groups

```
Get-LocalGroup
```

### Service Accounts

Windows service accounts are special user accounts that allow Windows services and applications to run with specific permissions, independently of users who log into the system. These accounts help control what resources a service can access and are crucial for security and manageability.

| Service Account                           | Description                                                                                   | Typical Responsibilities                                       |
| ----------------------------------------- | --------------------------------------------------------------------------------------------- | -------------------------------------------------------------- |
| **LocalSystem**                           | Highly privileged; full access to the local computer and acts as the computer on the network. | Runs core operating system services; powerful, use cautiously. |
| **NetworkService**                        | Limited local privileges; presents the computer's credentials to remote systems.              | Services needing limited local access and network access.      |
| **LocalService**                          | Minimal privileges; presents anonymous credentials to remote systems.                         | Services needing minimal local and no network resources.       |
| **Managed Service Accounts (MSA)**        | Automatically managed, single-service accounts for better security.                           | Used for services needing unique identities and isolation.     |
| **Group Managed Service Accounts (gMSA)** | Managed service accounts that can be used by multiple servers.                                | Ideal for load-balanced and clustered services.                |



* **LocalSystem**: Can access almost all resources on the machine and act as any user, but using it increases risk because if compromised, attackers gain maximum control.
* **NetworkService**: Suitable for services needing to interact with other computers under the machine's identity without exposing high privileges locally.
* **LocalService**: Ideal for services that don’t require any elevated privileges or network access.
* **MSA/gMSA**: Enhance security for applications/services by automatically managing strong, complex passwords and facilitating identity isolation and delegation for services, especially in domain environments.

### Groups

**Windows groups** are collections of user accounts (and sometimes other groups) that are managed as a single unit to simplify the assignment of permissions and access rights in Windows operating systems.

By using groups, administrators can efficiently manage users’ access to resources and assign roles without configuring each user individually.

#### Types of Windows Groups

* **Local Groups**
  * Defined on a specific computer or server.
  * Used to assign permissions to resources such as files, folders, and printers on that device.
  * Can include local users, domain users, and global groups.
  * Common local groups: Administrators, Users, Backup Operators.
* **Global Groups**
  * Exist within a domain and can contain accounts from that same domain.
  * Used to organize users who share similar access needs, like employees in a department.
  * Can be members of domain local groups to gain access to resources.
* **Domain Local Groups**
  * Used in Active Directory environments.
  * Can contain users, global groups, and other domain local groups from any domain in the forest.
  * Best for managing permissions to domain-specific resources, such as printers or shared folders.
* **Universal Groups (AD only)**
  * Can include users and groups from any domain in a forest.
  * Useful for assigning permissions across multiple domains.

### Resources

**Windows resources** are elements within the operating system that can be managed, secured, and accessed by users or applications. Proper management of these resources is fundamental for both security and functionality.

#### Common Resource Types

* **Files and Directories**
  * Basic units of storage in Windows, including individual files and folders.
  * Critical for user data and system operation.
* **Registry Entries**
  * Configuration database storing settings for the OS and applications.
  * Registry keys and values act as resources controlling system behavior.
* **Services**
  * Background programs or processes that provide essential OS functionalities (e.g., print spooler, Windows Update).
  * Managed through the Service Control Manager.
* **Printers and Print Queues**
  * Hardware and virtual printers, including their spooled print jobs.
* **Shared Resources**
  * Network shares (files/folders), printers, and devices accessible to multiple users.
* **Active Directory Objects (in domain environments)**
  * Users, computers, groups, and other entities managed centrally.

## Access Control: ACLs and ACEs

Managing who can access or modify Windows resources is accomplished through **Access Control Lists (ACLs)** and **Access Control Entries (ACEs)**.

### Access Control List (ACL)

* An **ACL** is attached to secured resources (such as files, registry keys, services, etc.).
* It contains a list of permissions, defining what actions users and groups may perform on the resource.
* There are two types of ACLs in Windows:
  * **Discretionary ACL (DACL):** Specifies permissions for users and groups (allow/deny).
  * **System ACL (SACL):** Specifies which access attempts should be audited.
* An ACL in Windows has the following structure:
  * **AclRevision:** Specifies the revision level of the ACL.
  * **AclSize:** Total size in bytes, including the ACL header and all ACEs.
  * **AceCount:** Number of ACEs in the list.
  * **ACEs:** An ordered list of ACEs, processed in order.

### Access Control Entry (ACE)

* Each **ACE** within an ACL describes an individual permission for a specific user or group.
* An ACE specifies:
  * The security principal (user, group, or computer).
  * Allowed or denied actions (e.g., Read, Write, Execute).
  * Inheritance flags (whether permissions propagate to sub-resources).
* An **Access Control Entry (ACE)** defines what access rights a specific user or group has. Each ACE includes:
  * A **type** (allow, deny, or audit)
  * **Flags** (inheritance, how it’s applied to children)
  * **Access mask** (which operations are allowed or denied)
  * **SID** (Security Identifier for the user or group)
  * Possible **object GUIDs** for object-specific permissions
* ACE types supported by all Windows objects include:
  * **Access-Allowed ACE:** Grants permissions
  * **Access-Denied ACE:** Denies permissions
  * **System-Audit ACE:** Specifies actions to log for auditing

### How ACLs and ACEs Apply to Resource Types

| Resource Type     | Where ACLs/ACEs Apply             | Example Permissions                                         |
| ----------------- | --------------------------------- | ----------------------------------------------------------- |
| Files/Directories | NTFS permissions on file/folder   | Read, Write, Execute, Modify, Full Control                  |
| Registry Entries  | Registry key security descriptors | Query Value, Set Value, Create Subkey, Delete, Full Control |
| Services          | Service DACLs (Discretionary ACL) | Start, Stop, Pause, Change Config, Read Permissions         |
| Printers          | Printer security descriptors      | Print, Manage Printers, Manage Documents                    |
| Active Directory  | Security on AD objects            | Read, Write, Create Child, Delete, Full Control             |

> The combination of ACLs and ACEs empowers administrators to implement _least privilege_ principles—ensuring users and applications have only the permissions needed for their tasks, which enhances both security and manageability.

### Command-Line Tools

**icacls**: The primary CLI tool for viewing and modifying file/folder ACLs.

* `icacls <filename>` — Shows the DACL for the specified file/folder.
* `icacls <filename> /save <outputfile>` — Saves ACLs to a file for viewing/editing.
* `icacls <filename> /verify` — Verifies the integrity of the ACLs

**Get-Acl** (PowerShell): Retrieves ACLs for files, folders, registry keys, or AD objects.

* `Get-Acl <filename> | Format-List`

### Key Points

* **Permissions are cumulative** unless explicitly denied by a "deny" ACE.
* **Inheritance** allows permissions to propagate from parent folders/keys to children.
* Most resources can be managed via properties dialogs (GUI) or command-line tools (like `icacls` for files, `sc sdshow` for services, and `regini` or PowerShell for registry keys).
* Principle of **least privilege**: always grant only necessary permissions to reduce risks.

### SDDL (Security Descriptor Definition Language) Representation

Advanced users may view ACL and ACE data as a single string using SDDL notation, which encodes the ACL/ACE data in a compact format. To display SDDL:

* `icacls <filename> /save <outputfile> /t`
* Or in PowerShell: `(Get-Acl <filename>).Sddl`

