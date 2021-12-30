This document describes how to quickly run the TRTC demo for Unreal Engine.

>! Currently, the demo can be run on Windows, macOS, iOS, and Android.

## Environment Requirements
- Unreal Engine 4.27.1 or above
- **Developing for Android:**
  - Android Studio 4.0 or above
  - Visual Studio 2017 15.6 or above
  - A real device for testing
- **Developing for iOS and macOS:**
  - Xcode 11.0 or above
  - OS X 10.11 or above
  - A valid developer signature for your project
- **Developing for Windows:**
    - OS: Windows 7 SP1 or above (64-bit based on x86-64)
    - Disk space: at least 1.64 GB of space after the IDE and relevant tools are installed
    - [Visual Studio 2019](https://visualstudio.microsoft.com/zh-hans/downloads/)

## Prerequisites
You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com) and verified your identity.

## Directions
[](id:step1)
### Step 1. Create an application
1. In the TRTC console, select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name such as `TestTRTC`. If you have already created an application, click **Existing** to select it.
3. Add or edit tags according to your actual business needs and click **Create**.
![](https://qcloudimg.tencent-cloud.cn/raw/f5fbbe70b7139531600e763846051a54.png)

>?
>- An application name can contain up to 15 characters. Only digits, letters, Chinese characters, and underscores are allowed.
>- Tags are used to identify and organize your Tencent Cloud resources. For example, an enterprise may have multiple business units, each of which has one or more TRTC applications. In this case, the enterprise can tag TRTC applications to mark out the unit information. Tags are optional and can be added or edited according to your actual business needs.

[](id:step2)
### Step 2. Download the SDK and demo source code
1. Download the SDK and [demo source code](https://comm.qq.com/sdk/trtc/UE4/TRTC_Demo.zip). If you have any questions, create an issue [here](https://github.com/tencentyun/TRTCUnrealEngine/issues).
2. Click **Next**.

[](id:step3)
### Step 3. Configure the demo project file
1. In the **Modify Configuration** step, select your platform.
2. Find and open `/TRTC_Demo/Source/debug/include/DebugDefs.h`.
3. Set parameters in `DebugDefs.h` as follows:
<ul><li/>SDKAPPID: `0` by default. Set it to the actual `SDKAppID`.
	<li/>SECRETKEY: left empty by default. Set it to the actual key.</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png"/>

4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.

>?
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for the local execution and debugging of the demo**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, please see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166#Server).

[](id:step4)
### Step 4. Compile, package, and run the project
1. Open `/TRTC_Demo/TRTC_Demo.uproject`.
2. Compile, run, and test the project.
<dx-tabs>
::: macOS\s
1. Go to **File > Package Project > Mac**.
2. Configure permissions. Right-click the `xxx.app` file compiled in the previous step and select **Show Package Contents**. 
![](https://qcloudimg.tencent-cloud.cn/raw/3eb106ee3307c206dff5314a43920132.png)
3. Go to **Contents > Info.plist**.
4. Select **Information Property List** and add the following two permissions:
```
<key>NSCameraUsageDescription</key>
<string>Video calls are possible only with camera permission.</string>
<key>NSMicrophoneUsageDescription</key>
<string>Audio calls are possible only with mic access.</string>
```
5. If you use UE4 Editor, add the above permissions to the **UE4Editor.app** file.
:::
::: Windows\s
1. Go to **File > Package Project > Windows > Windows(64-bit)**.
![](https://imgcache.qq.com/operation/dianshi/other/win.ba79ccce59ae58718e6c35c16cdef55531456a70.png)
:::
::: iOS\s
1. The following permissions are required on iOS.
```
Privacy - Camera Usage Description
Privacy - Microphone Usage Description
```
To add the permissions to `info.plist`, go to **Edit > Project Settings > Platforms: iOS** and add  
```
<key>NSCameraUsageDescription</key>
<string>Video calls are possible only with camera permission.</string>
<key>NSMicrophoneUsageDescription</key>
<string>Audio calls are possible only with mic access.</string>
```
to `Additional Plist Data`.
2. Go to **File > Package Project > iOS** to package your project.
:::
::: Android\s
1. For development and testing, see [Android Quick Start](https://docs.unrealengine.com/4.27/en-US/SharingAndReleasing/Mobile/Android/GettingStarted/).
2. For packaging, see [Packaging Android Projects](https://docs.unrealengine.com/4.27/en-US/SharingAndReleasing/Mobile/Android/PackagingAndroidProject/).
:::
</dx-tabs>
## Running the Demo
The demo offers implementation code for one-to-one video calls, which you can use for testing or as reference for API calls. For more information about APIs, see [All Platforms (C++) > Overview](https://intl.cloud.tencent.com/document/product/647/35131).
>? The UI of the latest version of the demo may look different.

![](https://qcloudimg.tencent-cloud.cn/raw/e81338b3f3cf22c73744bcfbcf8955d2.png)

## TRTC Cross-Platform (C++) APIs
[API Documentation (Chinese)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/md_introduction_trtc_zh_Cplusplus_Brief.html)

[API Documentation (English)](https://liteav.sdk.qcloud.com/doc/api/en/md_introduction_trtc_en_Cplusplus_Brief.html)

## FAQs
### How do I view TRTC logs?
TRTC logs are compressed and encrypted by default with the `.xlog` extension. You can view them via the following paths:
- **iOS**: `Documents/log` of the application sandbox
- **Android**:
	- 6.7 or below: `/sdcard/log/tencent/liteav`
	- 6.8 or above: `/sdcard/Android/data/package name/files/log/tencent/liteav/`

### What should I do if UE4 Editor crashes on macOS?
Make sure you have added the following audio/video permissions to `info.plist` of **UE4Editor.app**.
```
<key>NSCameraUsageDescription</key>
<string>Video calls are possible only with camera permission.</string>
<key>NSMicrophoneUsageDescription</key>
<string>Audio calls are possible only with mic access.</string>
```

### What should I do if the error "Attempt to construct staged filesystem reference from absolute path" occurs on Android?
Close the UE4 project, open Command Prompt, and type the following strings:
>adb shell
>cd sdcard
>ls (you should see the UE4Game directory listed)
>rm -r UE4Game
Compile your project again.
