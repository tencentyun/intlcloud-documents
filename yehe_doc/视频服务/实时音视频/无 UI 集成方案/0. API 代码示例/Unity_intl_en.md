This document shows you how to integrate the TRTC SDK in Unity to enable audio/video calls in games.

The demo includes the following features:
- Room entry/exit
- Custom video rendering
- Device management and music/audio effects

>?
>- For details about the APIs and their parameters, see [Overview](https://intl.cloud.tencent.com/document/product/647/40139).
>- Unity 2020.2.1f1c1 is recommended.
>- Supported platforms: Android, iOS, Windows, macOS (alpha testing)
>- Modules required: `Android Build Support`, `iOS Build Support`, `Windows Build Support`, `MacOS Build Support`
>- If you are developing for iOS, you also need:
   - Xcode 11.0 or later
   - A valid developer signature for your project

## Directions

### Step 1. Create an application

1. Log in to the TRTC console and select [Application Management](https://console.cloud.tencent.com/trtc/app) on the left sidebar.
2. Click **Create application**, enter an application name such as `APIExample`. If you already have an application, select **Existing** and click **Next**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/6704c9f7eb9e18e422c513cb9a2a3926.png)

### Step 2. Download the sample code

1. Select **No UI**, and go to [GitHub](https://github.com/LiteAVSDK/TRTC_Unity/tree/main/TRTC-Simple-Demo) to download the SDK and demo source code.
2. Click **Next**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/d28964ad85dddd85833a28310a62d514.png)

### Step 3. Configure the project

1. If you are running a demo project, select **Testing**. Note the `SDKAppID` and secret key.
   ![](https://qcloudimg.tencent-cloud.cn/raw/82a45972f2d12763a6dc80eee6c952c0.png)
2. Open the file downloaded previously, find and open `TRTC-Simple-Demo/Assets/TRTCSDK/Demo/Tools/GenerateTestUserSig.cs`, and set the following parameters:
  - `SDKAPPID`: A placeholder by default. Set it to the actual `SDKAppID`.
  - `SECRETKEY`: A placeholder by default. Set it to the actual key.
3. Click **Next**.

>?
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in the client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is disclosed, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for the local execution and debugging of TRTC-Simple-Demo**.
>- The best practice is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to your server for a dynamic `UserSig`. For more information, see [How do I calculate `UserSig` during production?](https://www.tencentcloud.com/document/product/647/35166).

### Step 4. Compile and run the demo

#### Android

1. Open Unity Editor, go to **File** > **Build Settings**, and select **Android** for **Platform**.
![](https://main.qcloudimg.com/raw/4464eb891829e3505a59c8ec00cc2414.png)
2. Connect to a real Android device and click **Build And Run** to run the demo.
3. Call `enterRoom` first and go on to test other APIs. The data display window shows whether the call is successful, and the other window displays the callback information.

#### iOS

1. Open the TRTC build and configuration tool (from the menu at the top).
2. Click **Build & Configure iOS** to generate a project.
   ![](https://qcloudimg.tencent-cloud.cn/raw/d7aa3153469c10b2dfe35db31bebbbf2.png)
3. Open the project generated (`Unity-iPhone.xcodeproj`) with Xcode.
4. Download the [underlying TRTC SDK](https://comm.qq.com/trtc/TRTC_9.7.0.11440_iOS.zip). Click **General**, select **Frameworks, Libraries, and Embedded Content**, click **+** at the bottom to add the dynamic libraries required – `FFmpeg.xcframework` and `SoundTouch.xcframework`, and click **Embed & Sign**.
   ![](https://imgcache.qq.com/operation/dianshi/other/unity.ca7b6e717bf7b34e4f08a7e688ff59bf49d92217.png)
5. Connect to a real iOS device to debug the project.

#### Windows

1. Open Unity Editor, go to **File** > **Build Settings**, and select **PC, Mac & Linux Standalone** for **Platform**, and **Windows** for **Target Platform**.
   ![](https://main.qcloudimg.com/raw/580764f661c06cf71c4952727c409c5e.png)
2. Click **Build And Run** to run the demo.

#### macOS

1. Open Unity Editor, go to **File** > **Build Settings**, and select **PC, Mac & Linux Standalone** for **Platform**, and **macOS** for **Target Platform**.
   ![](https://main.qcloudimg.com/raw/6f3f9c21aa9eeadd7a4e3be377b2a6b3.png)
2. Click **Build And Run** to run the demo.
3. To use the simulator feature of Unity Editor, you must install `Device Simulator Package`.
4. Click **Windows** > **General** > **Device Simulator**.
   ![](https://main.qcloudimg.com/raw/79f707b89553528956a888f48b4d4d6d.png)

[](id:demo)
## Demo
The demo integrates most of the APIs launched so far, which can be used for testing and as reference for API calls. For more information about APIs, see [Client APIs > Unity > Overview](https://intl.cloud.tencent.com/document/product/647/40139).
>? The UI of the latest version of the demo may look different.

## Directory Structure
```
├─Assets
├── Editor                        // Unity Editor script
│   ├── BuildScript.cs            // Unity Editor build menu
│   ├── IosPostProcess.cs         // Script for building iOS application in Unity Editor
├── Plugins
│   ├── Android                   
│   │   ├── AndroidManifest.xml   //Android configuration file
├── StreamingAssets               // Audio/Video stream files for the Unity demo
├── TRTCSDK
    ├── Demo                      // Unity demo
    ├── SDK                       // TRTC SDK for Unity
        ├── Implement             // Implementation of TRTC SDK for Unity
        ├── Include               // Header files of TRTC SDK for Unity
        └── Plugins               // Underlying implementation of TRTC SDK for Unity for different platforms
            
```