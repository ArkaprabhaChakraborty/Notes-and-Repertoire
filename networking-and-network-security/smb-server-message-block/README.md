---
description: Or how windows shares files and directories
---

# SMB (Server Message Block)

The Server Message Block protocol (SMB protocol) is common in enterprise networks where Windows services are running. It enables applications and users to transfer files to and from remote servers.

### **SMB runs on port 445.**

Microsoft Windows operating systems since Windows 95 have included client and server SMB protocol support.&#x20;

Samba, an open-source server that supports the SMB protocol, was released for Unix systems.&#x20;

Microsoft later released CIFS (Common Internet File System), a different "flavor" of SMB, to compete with open-source NFS(Network File System), but failed drastically. CIFS/SMB1.0 was used in older Windows operating systems such as Windows 2000, XP, Server 2003, and Server 2002 R2. The redesign to SMB 2.0 improved file-sharing capabilities, increased performance, enhanced security, and changed its signature to use HMACSHA-256 instead of MD5. Due to the significant changes, Microsoft decided to rename it SMB2 from CIFS.

Apart from regular resource sharing, SMB is also useful for inter-process communication (IPC), such as in mailslots.
