# FTP (File Transfer Protocol)

File Transfer Protocol (FTP) is, as the name suggests, a protocol used to allow remote transfer of files over a network. It uses a client-server model to do this, and- as we'll come on to later- relays commands and data in a very efficient way.

### FTP runs on TCP port 21

### How does FTP work?

A typical FTP session operates using two channels:

* a command (sometimes called the control) channel - is used for transmitting commands as well as replies to those commands.
* a data channel - is used for transferring data.

FTP operates using a client-server protocol. The client initiates a connection with the server, the server validates whatever login credentials are provided and then opens the session. While the session is open, the client may execute FTP commands on the server.

FTP servers and FTP clients use the FTP protocol. There are various FTP server software that you can select from if you want to host your FTP file server. Examples of FTP server software include:

* [vsftpd](https://security.appspot.com/vsftpd.html)
* [ProFTPD](http://www.proftpd.org/)
* [uFTP](https://www.uftpserver.com/)

For FTP clients, in addition to the console FTP client commonly found on Linux systems, you can use an FTP client with GUI such as [FileZilla](https://filezilla-project.org/). Some web browsers also support FTP protocol.

Because FTP sends the login credentials along with the commands and files in cleartext, FTP traffic can be an easy target for attackers.

### Enumerating FTP

```
nmap -sV [ip] -p 21
```

### Exploiting FTP

#### FTP anonymous Login

username: anonymous\
password: \<blank>&#x20;

#### Password cracking with Hydra

Let's say we have a user Dale, whose password we wanna find on a particular ftp server. We use the sample command as shown below:

```awk
hydra -t 4 -l "dale" -P /usr/share/wordlists/rockyou.txt -vV 10.10.10.6 ftp
```

