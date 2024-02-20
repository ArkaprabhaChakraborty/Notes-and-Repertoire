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

### List all build tools and system images

```
sdkmanager --list --sdk_root=$ANDROID_HOME
```

The output for the above command will be like:

```
Available Packages:
  Path                                                                                     | Version       | Description                                                         
  -------                                                                                  | -------       | -------                                                             
  add-ons;addon-google_apis-google-15                                                      | 3             | Google APIs                                                         
  add-ons;addon-google_apis-google-16                                                      | 4             | Google APIs                                                         
  add-ons;addon-google_apis-google-17                                                      | 4             | Google APIs                                      
  build-tools;27.0.0                                                                       | 27.0.0        | Android SDK Build-Tools 27                                          
  build-tools;27.0.1                                                                       | 27.0.1        | Android SDK Build-Tools 27.0.1                                      
  build-tools;27.0.2                                                                       | 27.0.2        | Android SDK Build-Tools 27.0.2                                      
  build-tools;27.0.3                                                                       | 27.0.3        | Android SDK Build-Tools 27.0.3               
  cmake;3.10.2.4988404                                                                     | 3.10.2        | CMake 3.10.2.4988404                                                
  cmake;3.18.1                                                                             | 3.18.1        | CMake 3.18.1                                                        
  cmake;3.22.1                                                                             | 3.22.1        | CMake 3.22.1                                                        
  cmake;3.6.4111459                                                                        | 3.6.4111459   | CMake 3.6.4111459                                                   
  cmdline-tools;1.0                                                                        | 1.0           | Android SDK Command-line Tools                                      
  cmdline-tools;10.0                                                                       | 10.0          | Android SDK Command-line Tools                                      
  cmdline-tools;11.0                                                                       | 11.0          | Android SDK Command-line Tools                                      
  cmdline-tools;12.0                                                                       | 12.0          | Android SDK Command-line Tools                                  
  ndk-bundle                                                                               | 22.1.7171670  | NDK                                                                                                  | 25.1.8937393  | NDK (Side by side) 25.1.8937393                                     
  ndk;25.2.9519653                                                                         | 25.2.9519653  | NDK (Side by side) 25.2.9519653                                     
  ndk;26.0.10792818                                                                        | 26.0.10792818 | NDK (Side by side) 26.0.10792818                                    
  ndk;26.1.10909125                                                                        | 26.1.10909125 | NDK (Side by side) 26.1.10909125                                    
  ndk;26.2.11394342                                                                        | 26.2.11394342 | NDK (Side by side) 26.2.11394342                                    
  platform-tools                                                                           | 35.0.0        | Android SDK Platform-Tools                                                
  platforms;android-27                                                                     | 3             | Android SDK Platform 27                                             
  platforms;android-28                                                                     | 6             | Android SDK Platform 28                                             
  platforms;android-29                                                                     | 5             | Android SDK Platform 29                                             
  platforms;android-30                                                                     | 3             | Android SDK Platform 30                                             
  platforms;android-31                                                                     | 1             | Android SDK Platform 31                                             
  platforms;android-32                                                                     | 1             | Android SDK Platform 32                                             
  platforms;android-33                                                                     | 3             | Android SDK Platform 33                                                 
  platforms;android-TiramisuPrivacySandbox                                                 | 9             | Android SDK Platform TiramisuPrivacySandbox                         
  platforms;android-UpsideDownCakePrivacySandbox                                           | 3             | Android SDK Platform UpsideDownCakePrivacySandbox                   
  platforms;android-VanillaIceCream                                                        | 1             | Android SDK Platform VanillaIceCream                                
  skiaparser;1                                                                             | 6             | Layout Inspector image server for API 29-30                         
  skiaparser;2                                                                             | 3             | Layout Inspector image server for API S                             
  skiaparser;3                                                                             | 3             | Layout Inspector image server for API 31-34                         
  sources;android-15                                                                       | 2             | Sources for Android 15                                              
  sources;android-27                                                                       | 1             | Sources for Android 27                                              
  sources;android-28                                                                       | 1             | Sources for Android 28                                              
  sources;android-29                                                                       | 1             | Sources for Android 29                                              
  sources;android-30                                                                       | 1             | Sources for Android 30                                              
  sources;android-31                                                                       | 1             | Sources for Android 31                                              
  sources;android-32                                                                       | 1             | Sources for Android 32                                              
  sources;android-33                                                                       | 1             | Sources for Android 33                                              
  sources;android-34                                                                       | 2             | Sources for Android 34                                              
  system-images;android-10;default;armeabi-v7a                                             | 5             | ARM EABI v7a System Image                                           
  system-images;android-10;default;x86                                                     | 5             | Intel x86 Atom System Image                                         
  system-images;android-10;google_apis;armeabi-v7a                                         | 6             | Google APIs ARM EABI v7a System Image                               
  system-images;android-10;google_apis;x86                                                 | 6             | Google APIs Intel x86 Atom System Image                             
  system-images;android-14;default;armeabi-v7a                                             | 2             | ARM EABI v7a System Image    
```

### Choosing platform, build-tools and system-image

Choose the platform, build tools and system-image from the sdkmanager list. Make sure the versions are same. For ex:

* For android-27 we can choose:

```
platforms;android-27
sources;android-27
build-tools;27.0.3                  # The latest versions are more stable
system-images;android-27;google_apis;x86
```

#### Note: x86 and x86\_64 images are best for emulation. The arm64-v8a architecture is damn slow requires at least 32GB ram to emulate properly and can only be done up to android-27 only.

### Download and Installation

Download the 4 requirements using the commands given below. Make sure to replace the `<>` texts with proper versions by referring to the sdkmanager list.

```
sdkmanager "system-images;<ANDROID-VERSION>;<OPTIONAL-GOOGLE-APIS-FLAG>;<ARCH>" --sdk_root=$ANDROID_HOME
sdkmanager "platforms;<ANDROID-VERSION>" --sdk_root=$ANDROID_HOME
sdkmanager "sources;<ANDROID-VERSION>" --sdk_root=$ANDROID_HOME
sdkmanager "build-tools;<BUILD-TOOL-VERSION>" --sdk_root=$ANDROID_HOME
```

For eg:- for android-27 with google-apis we have:

<pre><code><strong>sdkmanager "system-images;android-27;google_apis;x86" --sdk_root=$ANDROID_HOME
</strong>sdkmanager "platforms;android-27" --sdk_root=$ANDROID_HOME
sdkmanager "sources;android-27" --sdk_root=$ANDROID_HOME
sdkmanager "build-tools;27.0.3" --sdk_root=$ANDROID_HOME
</code></pre>

Now create a device using avdmanager using:

{% code overflow="wrap" %}
```
avdmanager create avd -n <DEVICE-NAME> -k "system-images;<ANDROID-VERSION>;<OPTIONAL-GOOGLE-APIS-FLAG>;<ARCH>" --device "<DEVICE-SPEC" --force
```
{% endcode %}

For eg:

{% code overflow="wrap" %}
```
avdmanager create avd -n android27x86 -k "system-images;android-27;google_apis;x86" --device "pixel_4" --force
```
{% endcode %}

Now run the emulator using:

```
emulator @<DEVICE-NAME> -writable-system 
```

For eg:

```
emulator @android27x86 -writable-system 
```

### Troubleshoot

If you get errors like:

{% code overflow="wrap" %}
```
INFO    | Android emulator version 32.1.15.0 (build_id 10696886) (CL:N/A)
INFO    | AVD android27x86 has path /home/fvalkyrie/.android/avd/android27x86.avd
INFO    | trying to check whether /opt/android-sdk is a valid sdk root
WARNING | /opt/android-sdk/android-sdk/system-images/android-27/google_apis/x86/ is not a valid directory.
WARNING | emulator has searched the above paths but found no valid sdk root directory.
PANIC: Broken AVD system path. Check your ANDROID_SDK_ROOT value [/opt/android-sdk]!
```
{% endcode %}

This happens because of emulator configuration. To change this go to `/home/.android/avd/<DEVICE-NAME>.avd` and change the `config.ini` file as follows:

* Go to the line shown below and remove the `android/` portion.

```
image.sysdir.1=android-sdk/system-images/android-27/google_apis/x86/ #OLD
image.sysdir.1=android-sdk/system-images/android-27/google_apis/x86/ #NEW
```

this should fix your startup configuration.

