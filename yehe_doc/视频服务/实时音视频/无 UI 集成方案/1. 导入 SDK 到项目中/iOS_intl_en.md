This document describes how to import the SDK into your project.
![](https://qcloudimg.tencent-cloud.cn/raw/f85f7ee54d462d85290fc6f50e5ed96a.png)
## Environment Requirements
- Xcode 9.0 or later 
- iPhone or iPad with iOS 9.0 or later
- A valid developer signature for your project

## Step 1. Import the SDK
You can use CocoaPods or download and import the SDK manually into your project.

### Method 1. Use CocoaPods
1. **Install CocoaPods.**
Enter the following command in a terminal window (you need to install Ruby on your Mac first):
```
sudo gem install cocoapods
```
2. **Create a Podfile.**
Go to the directory of your project and enter the following command to create a Podfile in the directory.
```
pod init
```
3. **Edit the Podfile.**
Choose an appropriate edition according to your project needs and edit the Podfile:
  - **Option 1: Lite**
The installation package is the smallest but only supports two features: real-time communication (TRTC) and live player (TXLivePlayer). To choose this version, edit the Podfile as follows:
```
 platform :ios, '8.0'
  
  target 'App' do
  pod 'TXLiteAVSDK_TRTC', :podspec => 'https://liteav.sdk.qcloud.com/pod/liteavsdkspec/TXLiteAVSDK_TRTC.podspec'
  end
```
   - **Option 2: Professional**
The installation package includes real-time communication (TRTC), live player (TXLivePlayer), RTMP streaming (TXLivePusher), VOD player (TXVodPlayer), short video recording and editing (UGSV), and many other features. To choose this edition, edit the Podfile as follows:
```
 platform :ios, '8.0'
  
  target 'App' do
  pod 'TXLiteAVSDK_Professional', :podspec => 'https://liteav.sdk.qcloud.com/pod/liteavsdkspec/TXLiteAVSDK_Professional.podspec'
  end
```
4. **Update the local repository and install the SDK**
  - Enter the following command in a terminal window to update the local repository and install the SDK:
```
pod install
```
   - Or, run this command to update the local repository:
```
pod update
```
An XCWORKSPACE project file integrated with the TRTC SDK will be generated. Double-click to open it.

### Method 2. Download the SDK and import it manually
1. Download and decompress the [SDK package](https://intl.cloud.tencent.com/document/product/647/34615).
2. Open your Xcode project, select the target you want to run, and click **Build Phases**.
![](https://qcloudimg.tencent-cloud.cn/raw/f57f1da3efefefe98a4b8c03c688fd17.png)
3. Expand **Link Binary With Libraries** and click the **+** icon at the bottom to add dependent libraries.
![](https://qcloudimg.tencent-cloud.cn/raw/25faf435d56c7c7df1f944a536dd8869.png)
4. Add the downloaded `TXLiteAVSDK_TRTC.Framework` (or `TXLiteAVSDK_Professional.Framework`), `TXFFmpeg.xcframework`, `TXSoundTouch.xcframework`, and the frameworks they depend on: `GLKit.framework`, `AssetsLibrary.framework`, `SystemConfiguration.framework`, `libsqlite3.0.tbd`, `CoreTelephony.framework`, `AVFoundation.framework`, `OpenGLES.framework`, `Accelerate.framework`, `MetalKit.framework`, `libresolv.tbd`, `MobileCoreServices.framework`, `libc++.tbd`, `CoreMedia.framework`.
![](https://qcloudimg.tencent-cloud.cn/raw/8f4b4dc4f794cd0bf4159cd5b0c2a507.png)
5. Click **General**, expand **Frameworks, Libraries, and Embedded Content**, and check if the dynamic libraries required by `TXLiteAVSDK_TRTC.framework` (**TXFFmpeg.xcframework** and **TXSoundTouch.xcframework**) have been added and set to **Embed & Sign**. If not, click **+** at the bottom to add them.
![](https://qcloudimg.tencent-cloud.cn/raw/a159c5fb799cf50611387bdae7275863.png)

## Step 2. Configure app permissions
1. To use the audio/video features of the SDK, you need to grant the application mic and camera permissions. Add the two items below to `Info.plist` of your application. Their content is what users see in the mic and camera access pop-up windows.
	- **Privacy - Microphone Usage Description**. Include a statement specifying why mic access is needed
	- **Privacy - Camera Usage Description**. Include a statement specifying why camera access is needed
![](https://main.qcloudimg.com/raw/7c483aae65f64cd2bf35b55d9c896a52.png)
2. If you want the SDK to run in the background, select your project, under the **Capabilities** tab, set **Background Modes** to **ON**, and select **Audio, AirPlay, and Picture in Picture**.
![](https://main.qcloudimg.com/raw/d960dfec88388936abce2d4cb77ac766.jpg)

## Step 3. Import the SDK into the project
After completing the first step of importing and the second step of granting device permissions, you can import the APIs provided by the SDK into your project.

### Using Objective-C or Swift APIs
There are two ways to use the SDK in Objective-C or Swift:
- **Import the module**: Import the SDK module in the files that will use the SDK APIs.
```
@import TXLiteAVSDK_TRTC;
```
- **Import the header file**: Import the header file in the files that will use the SDK APIs.
```
#import "TXLiteAVSDK_TRTC/TRTCCloud.h"
```

>? For more information on how to use Objective-C APIs, see [Overview](https://intl.cloud.tencent.com/document/product/647/35119).

[](id:using_cpp)
### Using C++ APIs (optional)
If your project imports the SDK through a cross-platform framework such as Qt or Electron, import the header files in the `TXLiteAVSDK_TRTC.framework/Headers/cpp_interface` directory:
```
#include "TXLiteAVSDK_TRTC/cpp_interface/ITRTCCloud.h"
```

>? For more information on how to use C++ APIs, see [Overview](https://intl.cloud.tencent.com/document/product/647/35131).

