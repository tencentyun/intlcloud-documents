This document shows how to integrate the TRTC SDK in Unity to enable audio/video calls in games.

The demo includes the following features:
- Room entry/exit
- Custom video rendering
- Device management and music/voice effects

>?
>
>- For details about API features and parameters, please see [Client APIs > Unity > Overview](https://intl.cloud.tencent.com/document/product/647/40139).
- Unity 2020.2.1f1c1 is recommended.
- Supported platforms: Android, iOS, Windows, macOS (alpha testing)
- Modules required: `Android Build Support`, `iOS Build Support`, `Windows Build Support`, `MacOS Build Support`
- If you are developing for iOS, you also need:
  - Xcode 11.0 or above
  - A valid developer signature for your project

## Directions
[](id:step1)
### Step 1. Create an application
1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name such as `TestTRTC` and click **Create**.
![](https://main.qcloudimg.com/raw/7178fb5203b8c1ad9eb4a3b7a3c008d7.png)

[](id:step2)
### Step 2. Download the SDK and source code
1. Download the SDK and [demo source code](https://github.com/tencentyun/TRTCUnitySDK).
2. Click **Next**. You can open the project with Unity, or copy `TRTCUnitySDK/Assets/TRTCSDK/SDK` in the SDK ZIP file to the `Assets` directory of your project.

3. Find and open `Assets/TRTCSDK/Demo/Tools/GenerateTestUserSig.cs`.
4. Set parameters in `GenerateTestUserSig.cs` as follows:
  <ul><li>SDKAPPID: `0` by default. Set it to the actual `SDKAppID`.</li>
  <li>SECRETKEY: left empty by default. Set it to the actual key.</li></ul> 
	<img src="https://main.qcloudimg.com/raw/4dad4541a4a0d400441e9cd75c07ba1e.png"/>

[](id:step3)
### Step 3. Compile and run
<dx-tabs>
::: Android\s
1. Open Unity Editor, go to **File** > **Build Settings**, and select **Android** for **Platform**.
![](https://main.qcloudimg.com/raw/4464eb891829e3505a59c8ec00cc2414.png)
2. Connect to a real Android device and click **Build And Run** to run the demo.
3. Call `enterRoom` first and go on to test other APIs. The data display window shows whether the call is successful, and the other window displays the callback information.
:::
::: iOS\s
1. Open Unity Editor, go to **File** > **Build Settings**, and select **iOS** for **Platform**.
![](https://main.qcloudimg.com/raw/3a0ef43000fe53e8e7ff58b6cc243785.png)
2. Connect to a real iPhone, and click **Build And Run**. You need to select a new folder to save your iOS build. When the build is completed, the folder containing the Xcode project will open in a new window.
:::
::: Windows\s
1. Open Unity Editor, go to **File** > **Build Settings**, and select **PC, Mac & Linux Standalone** for **Platform** and **Windows** for **Target Platform**.
![](https://main.qcloudimg.com/raw/580764f661c06cf71c4952727c409c5e.png)
2. Click **Build And Run** to run the demo.
:::
::: macOS\s
1. Open Unity Editor, go to **File** > **Build Settings**, and select **PC, Mac & Linux Standalone** for **Platform**, and **macOS** for **Target Platform**.
![](https://main.qcloudimg.com/raw/6f3f9c21aa9eeadd7a4e3be377b2a6b3.png)
2. Click **Build And Run** to run the demo.
3. To use the simulator feature of Unity Editor, you must install `Device Simulator Package`.
4. Click **Windows** > **General** > **Device Simulator**.
![](https://main.qcloudimg.com/raw/79f707b89553528956a888f48b4d4d6d.png)
:::
</dx-tabs>


[](id:demo)
## Demo
The demo integrates most of the APIs launched so far, which can be used for testing and as reference for API calls. For more information about APIs, see [Client APIs > Unity > Overview](https://intl.cloud.tencent.com/document/product/647/40139).
>? The UI of the latest version of the demo may look different.

![](https://main.qcloudimg.com/raw/2ce3ab51c6fdc843c1e8b086b55840c0.png)

## Directory Structure
```
├─Assets
├── Editor                        // Unity Editor script
│   ├── BuildScript.cs            // Unity Editor build menu
│   ├── IosPostProcess.cs         // Script for building iOS application in Unity Editor
├── Plugins
│   ├── Android                   
│   │   ├── AndroidManifest.xml   //Android configuration file
├── StreamingAssets               // Audio/video stream files for the Unity demo
├── TRTCSDK
    ├── Demo                      // Unity demo
    ├── SDK                       // TRTC SDK for Unity
        ├── Implement             // Implementation of TRTC SDK for Unity
        ├── Include               // Header files of TRTC SDK for Unity
        └── Plugins               // Underlying implementation of TRTC SDK for Unity for different platforms
            
```
