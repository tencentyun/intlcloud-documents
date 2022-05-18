This document describes how to quickly integrate the TRTC iOS SDK into your project.

## Environment Requirements
- Xcode 9.0 or later 
- iPhone or iPad with iOS 9.0 or later
- A valid developer signature for your project

## Integrating the TRTC SDK
You can use CocoaPods to automatically load the SDK or download and import it manually into your project.

### CocoaPods
#### 1. Install CocoaPods
Enter the following command in a terminal window (you need to install Ruby on your Mac first):
```
sudo gem install cocoapods
```

#### 2. Create a Podfile
Go to the directory of your project and enter the following command to create a Podfile in the directory.
```
pod init
```

#### 3. Edit the Podfile
Edit the Podfile and select an SDK edition based on your needs:
- [TRTC Lite](https://intl.cloud.tencent.com/document/product/647/34615): This edition has the smallest installation package, but integrates only TRTC and CDN playback (TXLivePlayer) features.
```
 platform :ios, '8.0'
  
  target 'App' do
  pod 'TXLiteAVSDK_TRTC', :podspec => 'https://liteav.sdk.qcloud.com/pod/liteavsdkspec/TXLiteAVSDK_TRTC.podspec'
  end
```

- [TRTC Professional](https://intl.cloud.tencent.com/document/product/647/34615):This edition integrates RTMP push (TXLivePusher), CDN playback (TXLivePlayer), VOD playback (TXVodPlayer), short video (UGSV), and other features.
```
 platform :ios, '8.0'
  
  target 'App' do
  pod 'TXLiteAVSDK_Professional', :podspec => 'https://liteav.sdk.qcloud.com/pod/liteavsdkspec/TXLiteAVSDK_Professional.podspec'
  end
```

You can use the official CocoaPods source, but the download may be slow:
```
   platform :ios, '8.0'
   source 'https://github.com/CocoaPods/Specs.git'
   
   target 'App' do
   pod 'TXLiteAVSDK_TRTC'
   end
```

#### 4. Update the local repository and install the SDK
Enter the following command in a terminal window to update the local repository and install the SDK:
```
pod install
```
Or, run this command to update the local repository:
```
pod update
```

An XCWORKSPACE project file integrated with the TRTC SDK will be generated. Double-click to open it.
>? You need to manually add the dependent library **Accelerate.framework**.

### Manual integration
1. Download the [TRTC SDK](https://github.com/LiteAVSDK/TRTC_iOS/tree/main/SDK) and decompress the downloaded file.
2. Open your Xcode project, select the target you want to run, and click **Build Phases**.
 ![](https://main.qcloudimg.com/raw/85509cc24bd958e7b9978e11937597c5.png)
3. Expand **Link Binary With Libraries** and click the **+** icon at the bottom to add dependent libraries.
 ![](https://main.qcloudimg.com/raw/54be71cc14ec79ce642216612544a8a4.png)
4. Add the downloaded TRTC SDK framework and the libraries it depends on: **VideoToolBox.framework**, **MetalKit.framework**, **SystemConfiguration.framework**, **ReplayKit.framework**, **libc++.tbd**, **Accelerate.framework**, **CoreMedia.framework**, and **CoreTelephoney.framework**.
 ![](https://qcloudimg.tencent-cloud.cn/raw/c3a1b11bce036f654b747c7937edb709.png)
5. If you use **TRTC SDK v9.6 or a later version**, you need to manually add the dynamic libraries.
Click **General**, expand **Frameworks, Libraries, and Embedded Content**, and click the **+** icon at the bottom to add the dynamic libraries required by `TXLiteAVSDK_TRTC.framework`: **TXFFmpeg.xcframework** and **TXSoundTouch.xcframework**. Click **Embed & Sign**.
![](https://qcloudimg.tencent-cloud.cn/raw/4d3fa9093b49c73f96c114ace22abadb.png)

## Granting Camera and Mic Permissions
To use the audio/video features of the SDK, you need to grant it mic and camera permissions. Add the two items below to `Info.plist` of your application. Their content is what users see in the mic and camera access pop-up windows.
- **Privacy - Microphone Usage Description**, plus a statement specifying why mic access is needed
- **Privacy - Camera Usage Description**, plus a statement specifying why camera access is needed

![](https://main.qcloudimg.com/raw/7c483aae65f64cd2bf35b55d9c896a52.png)


## Importing the TRTC SDK
You can import the TRTC SDK in two ways.
### Method 1: Using Objective-C or Swift APIs
There are two ways to use the SDK in Objective-C or Swift:
- **Import the module**: Import the SDK module in the files that will use the SDK APIs.
```
@import TXLiteAVSDK_TRTC;
```
- **Import the header file**: Import the header file in the files that will use the SDK APIs.
```
#import TXLiteAVSDK_TRTC/TRTCCloud.h
```


[](id:using_cpp)
### Method 2: Using C++ APIs
1. **Import the header file**: If you want to use C++ APIs to develop your iOS application, import the header file in the `TXLiteAVSDK_TRTC.framework/Headers/cpp_interface` directory.
```
#include TXLiteAVSDK_TRTC/cpp_interface/ITRTCCloud.h
```
2. **Use the namespace**: The cross-platform C++ methods and types are all defined in the TRTC namespace, which you can use directly. This method can simplify your code and is recommended.
```
using namespace trtc;
```

>? For more information on how to use C++ APIs, see [Overview](https://intl.cloud.tencent.com/document/product/647/35131).

## FAQs
### Can the SDK run in the background?
Yes. If you want the SDK to run in the background, select your project, under the **Capabilities** tab, toggle on **Background Modes**, and select **Audio, AirPlay, and Picture in Picture**.
![](https://main.qcloudimg.com/raw/d960dfec88388936abce2d4cb77ac766.jpg)
