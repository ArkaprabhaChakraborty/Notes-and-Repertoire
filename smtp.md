---
description: A primer on how SMTP enumeration and common exploitation techniques
---

# SMTP

Mail systems commonly use SMTP with POP3 and IMAP, which enable users to save messages in the server mailbox and download them from the server when necessary.&#x20;

SMTP uses mail exchange (MX) servers to direct mail via DNS.&#x20;

SMTP runs on **TCP port 25 but can also run on TCP ports 465**, **2525, or 587.**

### **Banner Grabbing/Basic connection**

**SMTP:**

**Using netcat**

```bash
nc -vn <IP> 25
```

**Using telnet**

```
telnet <IP> 25
```

After receiving the following:

```
Trying 192.168.168.1... 
Connected to 192.168.168.1. 
Escape character is '^]'.
220 NYmailserver ESMTP Sendmail 8.9.3 
```

We can type in the HELO command to get the greeting message from the mail server.

```
HELO
```

A sample greeting is as follows:

```
250 NYmailserver Hello [10.0.0.86], pleased to meet you.
```

**SMTPS**:

```bash
openssl s_client -crlf -connect smtp.mailgun.org:465 #SSL/TLS without starttls command
openssl s_client -starttls smtp -crlf -connect smtp.mailgun.org:587
```

### Finding MX servers of an organisation

```bash
dig +short mx google.com
```

## Enumeration

### Using SMTP commands

SMTP has three commands which can be used for enumeration:

* **VRFY**: Validates users

```
VRFY Jonathan 
250 Super-User <Jonathan@NYmailserver> 

VRFY Smith
550 Smith... User unknown
```

* **EXPN**: Displays the actual delivery addresses of aliases and mailing lists.

```
EXPN Jonathan 
250 Super-User <Jonathan@NYmailserver> 

EXPN Smith
550 Smith... User unknown
```

* **RCPT TO**: Defines the recipients of the message

```
RCPT TO: Ryder250 
Ryder... Recipient ok 

RCPT TO: Smith
550 Smith... User unknown
```

### Using nmap

#### Lists all the SMTP commands available in the Nmap directory

```
nmap -p 25, 365, 587 -script=smtp-commands <Target IP Address >
```

#### Identify SMTP open relays

```
nmap -p 25 -script=smtp-open-relay <Target IP Address>
```

#### Enumerate all the mail users on the SMTP server

```
nmap -p 25 –script=smtp-enum-users <Target IP Address>
```

### Using metasploit

Launch Metasploit msfconsole and switch to the relevant auxiliary scanner to initiate the process `auxiliary/scanner/smtp/smtp_enum`.&#x20;

```
msf> use auxiliary/scanner/smtp/smtp_enum msf 
auxiliary(smtp_enum)>
```

### Using smtp-user-enum

The `smtp-user-enum` is a tool for enumerating OS-level user accounts on Solaris via the SMTP service (sendmail). Enumeration is performed by inspecting the responses to VRFY, EXPN, and RCPT TO commands.

{% code overflow="wrap" %}
```
smtp-user-enum.pl [options] (-u username|-U file-of-usernames) (-t host|-T file-of-targets)
```
{% endcode %}

The smtp-user-enum has the following options:&#x20;

{% code overflow="wrap" %}
```
-m n: Maximum number of processes (default: 5) 
-M mode: Specify the SMTP command to use for username guessing from among EXPN, VRFY, and RCPT TO (default: VRFY) 
-u user: Check if a user exists on the remote system 
-f addr: Specify the from email address to use for "RCPT TO" guessing (default: user@example.com)
-D dom: Specify the domain to append to the supplied user list to create email addresses (default: none) 
-U file: Select the file containing usernames to check via the SMTP service 
-t host: Specify the server host running the SMTP service 
-T file: Select the file containing hostnames running the SMTP service 
-p port: Specify the TCP port on which the SMTP service runs (default: 25) 
-d: Debugging output 
-t n: Wait for a maximum of n seconds for the reply (default: 5) 
-v: Verbose -h: Help message
```
{% endcode %}

### Hacktricks: [https://book.hacktricks.xyz/network-services-pentesting/pentesting-smtp#username-bruteforce-enumeration](https://book.hacktricks.xyz/network-services-pentesting/pentesting-smtp#username-bruteforce-enumeration)

###



