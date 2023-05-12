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

### The portmapper runs on port 111 (TCP and UDP).

### The NFS server runs on port 2049 (TCP and UDP).

### The NFS Lock Manager runs on 3004 (TCP and UDP).

