---
description: How to setup Frida Server on a rooted android device
---

# Setting up Frida-Server on Android Device

## Install Frida Tools

```
pip install frida-tools
```

## Setup Frida server

### Download Frida Server

1. Spin up your AVD.&#x20;

```
emulator @avdname -writable-system
```

2. Find your AVD architecture using:

```
adb shell getprop ro.product.cpu.abi
```

3. Download the correct version of Frida server from [release-page](https://github.com/frida/frida/releases). Click on show more options to get the entire list and download the version by matching the architecture.
4. Unpack the contents using:

```
unxz frida-server.xz        # Change the filename 
```

### Install Frida Server on Android Virtual Device

#### On non-production emulator (AVD without google-apis)

Use the following commands to push the frida server to the AVD.

```
adb root # might be required
adb push frida-server /data/local/tmp/                # Change the filename
adb shell "chmod 755 /data/local/tmp/frida-server"    # Change the filename
```

Start  Frida Server using the command:

```
adb shell "/data/local/tmp/frida-server &"            # Change the filename 
```

#### On production emulator (AVD with google-apis)

```
adb push frida-server /data/local/tmp/                # Change the filename
adb shell "su -c chmod 755 /data/local/tmp/frida-server"   # Change the filename
```

Start  Frida Server using the command:

```
adb shell "su -c /data/local/tmp/frida-server &"      # Change the filename
```

### Check Installation

The adb terminal will be stuck. Now to check if Frida server is running run the following on a separate terminal.

```
frida-ps -U
```

&#x20;This should list all running processes.

