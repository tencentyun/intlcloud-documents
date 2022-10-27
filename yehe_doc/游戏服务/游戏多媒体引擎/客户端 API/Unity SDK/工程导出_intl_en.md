This document describes how to configure a Unity project export for the GME APIs for Unity.

## Project Export Configuration

Project configuration is required before you can export executables from the Unity engine for different platforms:



<dx-alert infotype="explain" title="">
The GME SDK for Unity supports IL2CPP compilation.
</dx-alert>



### Export for iOS

#### 1. Determine the Xcode version

Make sure that the Xcode version is 10.0 or later.

#### 2. Disable Bitcode

If the following error occurs during the compilation, disable Bitcode. Search for Bitcode in **Targets** > **Build Settings** and set the corresponding option to `NO`.
<img src="https://main.qcloudimg.com/raw/bcc77d7574e2d1861ca408cdd77dff00.png"  width="60%" /></img>

#### 3. Add access to iOS

- Required background modes: allows running in the background (optional).
- Microphone Usage Description: allows access to microphone.

#### 4. Add the library file

If the following error occurs during compilation, please complete the library files.
<img src="https://main.qcloudimg.com/raw/335c9d806cd2d5fe11b5f6a04a6fad80.png"  width="25%" /></img>
The list of library files is as follows:
```
libc+.tbd
CoreMedia.framework
libresolv.tbd
AVFoundation.framework
Security.framework
CoreAudio.framework
AudioToolbox.framework
libiconv.tbd
libz.tbd
SystemConfiguration.framework
OpenAL.framework
```

#### 5. Add libresolv9.tbd

If the following error occurs:
<img src="https://main.qcloudimg.com/raw/b8e40f601d9e8c1a62cf88bd10bdd241.png"  width="60%" /></img>
Add `libresolv9.tbd` to **UnityFramework**.
<img src="https://main.qcloudimg.com/raw/ee0a20a0b0ad99f30fa87855d1b17f0f.jpg"  width="60%" /></img>

#### 6. FAQs about exporting
If you have any questions during exporting, please see [Exporting for iOS](https://intl.cloud.tencent.com/document/product/607/39522).



### Export for Android

#### 1. Delete unnecessary lib files

The GME SDK for Unity provides lib files for arm64-v8a, armeabi-v7a, and x86 by default. Please delete unnecessary files as needed.
<dx-alert infotype="alarm" title="Architecture loss">
A crash will occur if the exported Android executable file lacks the specified architecture.
</dx-alert>
After the executable `apk` file is exported, if a black screen or crash occurs when you open it, it is generally caused by the lack of corresponding architecture `lib` file. Please add or delete the corresponding architecture `lib` file according to the project.

#### 2. Configure permissions
**2.1 Required permissions**
You must add the following permissions in the `AndroidManifest.xml` file of the project:

```
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
```

**2.2 Adding permissions as needed**
Add the following permissions in the `AndroidManifest.xml` file of the project as needed:
<dx-tabs>
::: Read/Write permission
The read/write permission is not required. Determine whether to add it according to the following rules:

- If you use the default log path (/SDCARD/Android/Data/files), it means that you do not call SetLogPath, and do not need Write_External_Storage permission.
- If you call the setLogPath API to set the log path to an external storage device, and the storage path of the voice message recording is an external storage device, you need to apply for the Write_External_Storage permission to the user and get the user's approval.

```
 <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
```
:::
::: Bluetooth permission
Add the Bluetooth permission according to the following rules:

- If `targetSDKVersion` in the project is v30 or earlier:
```
<uses-permission android:name="android.permission.BLUETOOTH"/>
```

- If `targetSDKVersion` in the project is v31 or later:
```
<uses-permission android:name="android.permission.BLUETOOTH" android:maxSdkVersion="30" />
<uses-permission android:name="android.permission.BLUETOOTH_CONNECT" />
```
:::
</dx-tabs>


#### 3. FAQs about exporting
If you have any questions during exporting, please see [Exporting for Android](https://intl.cloud.tencent.com/document/product/607/39522).


### Export for Windows


If you have any questions during exporting, please see [Exporting for Windows](https://intl.cloud.tencent.com/document/product/607/39522).

