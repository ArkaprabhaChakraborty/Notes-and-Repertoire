---
description: Guided steps to install android SDK on any Ubuntu or Debian system
---

# Installing Android SDK and emulator

## Download the SDK tools&#x20;

Firstly download the CLI tools from the Command Line Tools Only section from [https://developer.android.com/studio](https://developer.android.com/studio). I have it saved in my `Downloads` section/directory.

## Move it to the Correct location

Now we need to unzip it. Remember to change the zip file name with your specific one.

```bash
cd Downloads                      # Or wherever you have downloaded the CLI tools zip
```

```bash
unzip commandlinetools-linux-10406996_latest.zip 
```

Now we need to copy the `cmdline-tools` to `/opt/android-sdk/` directory. This is going to be our system wide android SDK root.&#x20;

<pre class="language-bash"><code class="lang-bash"><strong>sudo mkdir /opt/android-sdk
</strong></code></pre>

```bash
sudo cp -r Downloads/cmdline-tools/ /opt/android-sdk/tools/
```

Yes this is going to throw warnings as we are using our custom directory, but since these opensource projects are maintained by Google, using custom directory configurations is much better as Google is shit and changes such configuration in almost every goddamn releases.

## Install platform-tools and emulator

We are going to use the sdkmanager to install the `platform-tools` and `emulator`. Now run:

```bash
cd /opt/android-sdk/tools/bin/
```

```bash
sudo ./sdkmanager platform-tools emulator --sdk_root=../../../android-sdk
```

## Add to `/etc/environment`&#x20;

Now that we have the three necessary components, we need to add them to the `/etc/environment` file.

Modify the `PATH` variable to have the following along with it's original content.

```
/opt/android-sdk/emulator:/opt/android-sdk/platform-tools:/opt/android-sdk/tools/bin:
```

Add the following variables:

```
ANDROID_SDK_ROOT="/opt/android-sdk"
ANDROID_HOME="/opt/android-sdk"
```

Save the changes, logout and log back in for the changes to take effect.

After this you will have access to commands like `sdkmanager`, `avdmanager`, `emulator` etc.&#x20;

## Install necessary platform, build-tools and system-images







