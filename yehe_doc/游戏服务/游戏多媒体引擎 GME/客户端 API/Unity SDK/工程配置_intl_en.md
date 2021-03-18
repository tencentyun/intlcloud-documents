## Overview
This document provides a detailed description that makes it easy for Unity developers to debug and integrate the APIs for Game Multimedia Engine (GME).


## Downloading SDK
1. Download the applicable demo and SDK. For more information, please see [SDK Download Guide](https://intl.cloud.tencent.com/document/product/607/18521).
2. Locate the SDK resources for Unity on the page.
3. Click **Download**. After decompression, the downloaded SDK resources include the following files:

| File Name | Description | Role |
| ------------- |:-------------:|------|
| Plugins | SDK library files | Stores library files for each platform |
| GMESDK | SDK code files | Provides APIs |

## Project Configuration Steps
#### Importing `Plugins` files
Copy the files from the `Plugins` folder in the SDK to the `Plugins` folder under `Assets` of your Unity project as shown below:  
<img src="https://main.qcloudimg.com/raw/1221a25f62cedd3831cf2bb27bb1ea45.png"  width="30%" /></img>
>?If you don't need to export executables in the Win32 architecture, delete the `x86` folder under the `Plugins` folder.


#### Importing code files
Copy the files in the `Scripts` folder in the SDK to the folder used to store code in your Unity project as shown below:  
<img src="https://main.qcloudimg.com/raw/8904a83c6173fa7c5b04ddb0e48138ca.png"  width="30%" /></img>

#### Audio settings
In the Unity editor, go to **Edit > Project Settings > Audio** and use the default system settings. If you make a change to the settings, Unity playback sound effect will be affected due to the hardware buffer set on the iOS device, as shown below:

<img src="https://main.qcloudimg.com/raw/db8975fcaefa3dc71732ede1b5f979db.png"  width="40%" /></img>

If the settings are as follows, Unity playback sound effect will be interrupted due to the hardware buffer set on the iOS device:

<img src="https://main.qcloudimg.com/raw/60fcc1ec0bd58cc1e0de5403392c1955.png"  width="40%" /></img>

#### Operations on macOS
If you use Unity to access the GME SDK on macOS 10.15.x, an error will be displayed for file corruption during the execution. This error is caused by the `com.apple.quarantine` attribute, and the most direct solution is to delete this attribute.

1. Run the `cd` command in terminal to go to the `Unity_OpenSDK_Audio/Assets/Plugins/` folder in the project.
2. Run the following command:
```
$ xattr -d com.apple.quarantine gmesdk.bundle
```

>?This operation is risky. It is recommended to use a lower version of macOS for access.

## Project Export Configuration
Project configuration is required before you can export executables from the Unity engine for different platforms:

>?The GME SDK for Unity supports IL2CPP compilation.

#### Exporting for iOS
1. Make sure that your Xcode version is above 10.0. Xcode 11.3 is used here as an example.
<img src="https://main.qcloudimg.com/raw/068f239e04fd6748a92a57c320e8e72e.png"  width="40%" /></img>

2. If the following error is displayed during compilation, please disable Bitcode.
   To disable this feature, search for Bitcode under **Targets** > **Build Settings** and set the corresponding option to `NO`.
<img src="https://main.qcloudimg.com/raw/bcc77d7574e2d1861ca408cdd77dff00.png"  width="60%" /></img>

3. If the following error occurs during compilation, please complete the library files.  
<img src="https://main.qcloudimg.com/raw/335c9d806cd2d5fe11b5f6a04a6fad80.png"  width="25%" /></img>

	Sample list of library files:
<img src="https://main.qcloudimg.com/raw/5950ab3af7fceb6b58e7510f274fffe6.png"  width="25%" /></img>

4. An error occurs, as shown below:
<img src="https://main.qcloudimg.com/raw/b8e40f601d9e8c1a62cf88bd10bdd241.png"  width="60%" /></img>
	
	Please add `libresolv9.tbd` to the `UnityFramework`.
<img src="https://main.qcloudimg.com/raw/ee0a20a0b0ad99f30fa87855d1b17f0f.jpg"  width="60%" /></img>


#### Exporting for Android
1. The GME SDK for Unity provides lib files for arm64-v8a, armeabi-v7a, and x86 by default. Please delete unnecessary files as appropriate.
2. To export an Android executable, you need to configure relevant permissions in `AndroidManifest.xml` to avoid audio or permission errors. For required permissions, please see [Android Project Configuration](https://intl.cloud.tencent.com/document/product/607/15203).
3. After the executable `apk` file is exported, if there is a black screen or crash when opening it, it is generally due to the lacking of corresponding architecture `lib` file, please add or delete it according to the project.
