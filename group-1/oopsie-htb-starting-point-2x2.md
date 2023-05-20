# Oopsie (HTB Starting Point 2x2)

## Target Details

IP: 10.129.69.179

## Full Walk Through

### Port scan

```bash
naabu -host 10.129.69.179  -nmap-cli 'nmap -sV -sC nmap-output'
```

{% code overflow="wrap" %}
```
[INF] Current naabu version 2.1.6 (latest)
[INF] Running CONNECT scan with non root privileges
[INF] Found 2 ports on host 10.129.69.179 (10.129.69.179)
10.129.69.179:22
10.129.69.179:80
[INF] Running nmap command: nmap -sV -sC nmap-output -p 80,22 10.129.69.179
Starting Nmap 7.93 ( https://nmap.org ) at 2023-05-21 07:53 IST
Nmap scan report for 10.129.69.179
Host is up (0.32s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 61e43fd41ee2b2f10d3ced36283667c7 (RSA)
|   256 241da417d4e32a9c905c30588f60778d (ECDSA)
|_  256 78030eb4a1afe5c2f98d29053e29c9f2 (ED25519)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Welcome
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 18.01 seconds
```
{% endcode %}

So we have an SSH service and a HTTP service (website).&#x20;

### Directory Brute Force



**Probable Approaches** \
**SSH:** that we need to get access of, either, by getting the keys from the server or by uploading our forged keys.\
**Website**: should be our primary target to gain a foothold on the server.

### Login Panel allows unauthenticated guest access

Upon inspection we find `<script src="`[`/cdn-cgi/login/script.js`](http://10.129.69.179/cdn-cgi/login/script.js)`"></script>` almost at the end of the home page.&#x20;

This gives us the login panel at the `/cdn-cgi/login` endpoint:

<figure><img src="../.gitbook/assets/LOGIN_PANEL.png" alt=""><figcaption><p>Login Panel</p></figcaption></figure>

After clicking on `Login as Guest`, we are given guest access to the control panel, without any authentication.

<figure><img src="../.gitbook/assets/GUEST_UNAUTH_LOGIN.png" alt=""><figcaption><p>Guest Login</p></figcaption></figure>

### IDOR using guest login

We can modify the Id parameter in the URL to leak out information about other users.&#x20;

#### Leaking out client (john) information&#x20;

* Modify Id parameter to 4 to see john's information

<figure><img src="../.gitbook/assets/CLIENT_JOHN_INFO_LEAK.png" alt=""><figcaption><p>Access ID and email of John</p></figcaption></figure>

#### Leaking out admin information

* Similar approach like above, by setting Id parameter to 1.

<figure><img src="../.gitbook/assets/IDOR_TOADMIN_REVEAL_ADMIN_ID.png" alt=""><figcaption></figcaption></figure>



### File Upload Vulnerability





