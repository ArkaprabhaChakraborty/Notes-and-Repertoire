# NFS (Network File System)

NFS stands for "Network File System" and allows a system to share directories and files with others over a network.&#x20;

By using NFS, users and programs can access files on remote systems almost as if they were local files. It does this by mounting all, or a portion of a file system on a server. The portion of the file system that is mounted can be accessed by clients with whatever privileges are assigned to each file.

### How does it work?

To access data stored on another machine (i.e. a server) the server would implement NFS daemon processes to make data available to clients. The server administrator determines what to make available and ensures it can recognize validated clients.

From the client's side, the machine requests access to exported data, typically by issuing a mount command. If successful, the client machine can then view and interact with the file systems within the decided parameters.

If someone wants to access a file using NFS, an RPC call is placed to NFSD (the NFS daemon) on the server. This call takes parameters such as:

* &#x20;The file handle
* &#x20;The name of the file to be accessed
* &#x20;The user's, user ID
* &#x20;The user's group ID

These are used in determining access rights to the specified file. This is what controls user permissions, I.E read and write of files.

NFS uses RPC (Remote Procedure Calls) to communicate between the client and the server.

#### The portmapper runs on port 111 (TCP and UDP).

#### The NFS server runs on port 2049 (TCP and UDP).

#### The NFS Lock Manager runs on 3004 (TCP and UDP).

### Enumeration of NFS

Required tools/dependencies/libs: `nfs-utils` or `nfs-common`.

#### Show available shares

```awk
showmount -e 10.10.75.141
```

#### Mount available shares

```awk
sudo mount -t nfs 10.10.75.141:home /tmp/mount/ -nolock
```

### Exploiting NFS

#### Root squashing disabled

By default, on NFS shares- Root Squashing is enabled and prevents anyone connecting to the NFS share from having root access to the NFS volume.&#x20;

Remote root users are assigned a user “nfsnobody” when connected, which has the least local privileges.&#x20;

However, if this is turned off, it can allow the creation of SUID bit files, allowing a remote user root access to the connected system.

#### What are files with the SUID bit set?&#x20;

Essentially, this means that the file or files can be run with the permissions of the file(s) owner/group. If there is a case in which the file has SUID set as the root user or as the super-user, we can leverage this to get a shell with these privileges.



\
