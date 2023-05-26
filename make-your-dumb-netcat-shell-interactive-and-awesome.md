---
description: Reducing the pain of working with netcat reverse shells
---

# Make your dumb netcat shell interactive and awesome

Netcat shells can be a tough nut to crack and work with, so, you can make them interactive with auto completions and stuffs to make it easier for you to work with them.

Once you have the netcat shell back (it can be a simple bash reverse shell or a php-web-reverse-shell) check if python is available or not:

```
$  which python

/usr/bin/python3
```

If python exists, then you can run:

```bash
python3 -c 'import pty;pty.spawn("/bin/bash")'
```

Now you should have a better shell like the one below:

```
www-data@oopsie:/$ ls
ls
bin    dev   initrd.img      lib64       mnt   root  snap  tmp  vmlinuz
boot   etc   initrd.img.old  lost+found  opt   run   srv   usr  vmlinuz.old
cdrom  home  lib             media       proc  sbin  sys   var
```

Next you need to background the shell with `Ctrl + Z`.

Now you need some info on our terminal so we use:

```bash
echo $TERM
```

It should give you your terminal type like shown below:

```bash
xterm-256color
```

Now run:

```bash
stty raw -echo
```

Now, type **`fg`** to foreground our shell running in the background. You won't be able to see those letters on the screen as you type, but hit _Enter_ afterwards, and the Netcat command will appear automatically.&#x20;

Now type reset. The screen would look awkward while doing this:

```
~# nc -lvp 1234
               reset
```

Next in the prompt `terminal type?` set the type you obtained before.

Now just set the rows and columns using:&#x20;

```bash
stty rows 56 columns 213
```
