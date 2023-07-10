---
description: A deep dive into how permissions in Linux work
---

# Permissions in Linux

Permissions in Linux are just relationships between users, groups, files and directories. Each user is a part of a group. Each group can have multiple users. Every files and directories define their permission based on a user, a group and "others"(all other users).

## Users

User accounts are configured in `/etc/passwd` file.

User password hashes are stored in `/etc/shadow` file.

The root user account is a special type of account with a UID `0` and has access to all resources of the machine. The system grants this user access to every files.

## Groups

Groups are configured in `/etc/group` file.

Users have a primary group and can be a part of multiple secondary groups. By default every user's primary group has the same name as that of their username in user account.

## Files and Directories

All files and directories have a `single owner` and a group. Permissions are defined in terms of read, write and execute operations.&#x20;

There are three sets of permissions, one for the owner, one for the group and one for all "other" users, also called as "`world`".

Only the owner can change the permissions.

File permissions are simple and self explanatory:

* **`Read(r)`** means when set, the file contents can be read.&#x20;
* **`Write(w)`** means content can be changed/written.
* **`Execute(e)`** means when set, it can be executed (run as a process).

Directory permissions are a bit complex.&#x20;

* **`Execute(e)`** when set, the directory can be entered. Without execute permission, neither read or write permissions over the directory will work.&#x20;
* **`Read(r)`** when set, means that the directory contents can be listed.&#x20;
* **`Write(w)`** when set, means that new sub directories and files can be created in the directory.

## Special permissions

#### Set user id (SUID) bit

When this is set, files will get executed with the privileges of the owner of the file.

#### Set group id (SGID) bit

When this is set, files will get executed with the privileges of the file group. When this is set on a directory, the files created within that directory will inherit the group and it's id of the directory itself.

## Viewing permissions



