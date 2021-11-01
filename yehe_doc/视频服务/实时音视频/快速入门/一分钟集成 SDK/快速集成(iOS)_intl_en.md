This document describes how to quickly integrate the Tencent Cloud TRTC SDK for iOS into your project in the following steps.

## Environment Requirements
- Xcode 9.0+. 
- iPhone or iPad on iOS 9.0 or above.
- Your project has a valid developer signature.

## Integrating TRTC SDK
You can choose to use CocoaPods for automatic loading or download the SDK first and then import it into your current project.

### CocoaPods
#### 1. Install CocoaPods
Enter the following command in the terminal window (you need to install the Ruby environment on your macOS in advance):
```
sudo gem install cocoapods
```

#### 2. Create a Podfile
Go to the path to the project, and enter the following command to create a Podfile in the project path.
```
pod init
```

#### 3. Edit the Podfile
Edit the Podfile and select the appropriate SDK version as needed:
- [Lite](https://intl.cloud.tencent.com/document/product/647/34615): it has the smallest installation package but only supports TRTC and CDN playback (TXLivePlayer) features.
```
 platform :ios, '8.0'
  
  target 'App' do
  pod 'TXLiteAVSDK_TRTC', :podspec => 'http://pod-1252463788.cosgz.myqcloud.com/liteavsdkspec/TXLiteAVSDK_TRTC.podspec'
  end
```

- [Pro](https://intl.cloud.tencent.com/document/product/647/34615): in addition to TRTC, it also includes RTMP push (TXLivePusher), CDN playback (TXLivePlayer), VOD playback (TXVodPlayer), short video (UGSV), and other features.
```
 platform :ios, '8.0'
  
  target 'App' do
  pod 'TXLiteAVSDK_Professional', :podspec => 'http://pod-1252463788.cosgz.myqcloud.com/liteavsdkspec/TXLiteAVSDK_Professional.podspec'
  end
```

You can also use an official CocoaPods source, but the download may be slow:
```
   platform :ios, '8.0'
   source 'https://github.com/CocoaPods/Specs.git'
   
   target 'App' do
   pod 'TXLiteAVSDK_TRTC'
   end
```

#### 4. Update and install the SDK
Enter the following command in the terminal window to update the local library file and install the TRTC SDK:
```
pod install
```
Or, run the following command to update the local repository:
```
pod update
```

After the pod command is executed, an .xcworkspace project file integrated with the SDK will be generated. Double-click this file to open it.
>? You need to manually add the required system dependent library **Accelerate.framework**.

### Manual integration
1. Download [TRTC - SDK](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/SDK) and decompress it.
2. Open your Xcode project, select the target you want to run, and select **Build Phases**.
 ![](https://main.qcloudimg.com/raw/85509cc24bd958e7b9978e11937597c5.png)
3. Click to expand **Link Binary with Libraries** and then click the "+" icon at the bottom to add the dependent library.
 ![](https://main.qcloudimg.com/raw/54be71cc14ec79ce642216612544a8a4.png)
4. Add the downloaded TRTC SDK Framework and its required dependent libraries **libc++.tbd**, **Accelerate.framework**, **libresolv.tbd**, and **AVFoundation.framework** in sequence.
 ![](https://main.qcloudimg.com/raw/2fa94b7f81c7e9c4ac09733782e79c10.png)


## Granting Camera and Mic Access
To use the audio/video features of the SDK, you need to grant the microphone and camera permissions. Add the following two items to the `Info.plist` file of the application, which correspond to the microphone and camera prompt messages when the authorization dialog box pops up.
- **Privacy - Microphone Usage Description**. Enter the prompt that indicates the purpose of using the microphone.
- **Privacy - Camera Usage Description**. Enter the prompt that indicates the purpose of using the camera.

![](https://main.qcloudimg.com/raw/7c483aae65f64cd2bf35b55d9c896a52.png)


## Importing TRTC SDK
TRTC SDK supports two calling methods for your choice.
### Method 1. Import TRTC SDK through Objective-C or Swift APIs
There are two ways to use the SDK in Objective-C or Swift code:
- **Import module**: add an import module to the project's files that need to use the SDK APIs.
```
@import TXLiteAVSDK_TRTC;
```
- **Import header file**: use the following code to import specific header files into the project's files that need to use the SDK APIs.
```
#import TXLiteAVSDK_TRTC/TRTCCloud.h
```


[](id:using_cpp)
### Method 2. Import TRTC SDK through C++ APIs
1. **Import the header file**: if you want to use C++ APIs to develop iOS applications, please import the header files in the `TXLiteAVSDK_TRTC.framework/Headers/cpp_interface` directory.
```
#include TXLiteAVSDK_TRTC/cpp_interface/ITRTCCloud.h
```
2. **Use the namespace**: the methods and types of cross-platform C++ APIs are defined in the `trtc` namespace. To simplify your code, you are advised to use the `trtc` namespace.
```
using namespace trtc;
```

>? For more information on how to use C++ APIs, please see [Overview](https://intl.cloud.tencent.com/document/product/647/35131).

## FAQs
### 1. Does the TRTC SDK support running in the background?
Yes. If you want the SDK to run relevant features in the background, you can select the current project, set **Background Modes** under **Capabilities** to **ON**, and check **Audio, AirPlay and Picture in Picture** as shown below:
![](https://main.qcloudimg.com/raw/d960dfec88388936abce2d4cb77ac766.jpg)
