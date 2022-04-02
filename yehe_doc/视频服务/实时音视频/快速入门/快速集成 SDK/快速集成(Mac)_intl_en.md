This document describes how to quickly integrate the TRTC macOS SDK into your project.


## Environment Requirements
- Xcode 9.0 or above
- A Mac computer with OS X 10.10 or above
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
There are two ways to edit the Podfile:
- Method 1: Use the pod path of the LiteAV SDK
<dx-codeblock>
::: pod path
	platform :osx, '10.10'
	
	target 'Your Target' do
	pod 'TXLiteAVSDK_TRTC_Mac', :podspec => 'http://pod-1252463788.cosgz.myqcloud.com/liteavsdkspec/TXLiteAVSDK_TRTC_Mac.podspec'
	end
:::
</dx-codeblock>
- Method 2: Use CocoaPod’s official source, which allows version selection
<dx-codeblock>
::: pod path
	platform :osx, '10.10'
	source 'https://github.com/CocoaPods/Specs.git'
	
	target 'Your Target' do
	pod 'TXLiteAVSDK_TRTC_Mac'
	end
:::
</dx-codeblock>

#### 4. Install and update the SDK
Enter the following command in a terminal window to install the SDK.
```
pod install
```
Or, run this command to update the local repository:
```
pod update
```

An XCWORKSPACE project file integrated with LiteAVSDK will be generated. Double-click to open the file.

### Manual integration
1. Download the [TRTC macOS SDK](https://github.com/LiteAVSDK/TRTC_Mac).
2. Open your Xcode project and import into it the framework downloaded in step 1.
3. Select the target you want to run and click **Build Phases**.
![](https://main.qcloudimg.com/raw/b5097f8ac4cbaa5044d92b2a96ea2b9e.jpg)
4. Expand **Link Binary With Libraries** and click the **+** icon at the bottom to add dependent libraries.
![](https://main.qcloudimg.com/raw/17046154417930f9d31b6452782df55d.jpg)
5. Add the downloaded SDK framework and the dependent libraries it requires: `AudioUnit.framework`, `libc++.tbd`, and `Accelerate.framework`.  
After that, you will see:
![](https://main.qcloudimg.com/raw/258ffc87c493d23cf591bb2ff9102677.png)

## Granting Camera and Mic Permissions
To use the audio/video features of the SDK, you need to grant it mic and camera permissions. Add the two items below to `Info.plist` of your application. Their content is what users see in the mic and camera access pop-up windows.
- **Privacy - Microphone Usage Description**, plus a statement specifying why mic access is needed
- **Privacy - Camera Usage Description**, plus a statement specifying why camera access is needed
As shown below:
![](https://main.qcloudimg.com/raw/ce02c335f1a6413fb37adb0ed20a9603.png) 

If **App Sandbox** or **Hardened Runtime** is enabled for your application, select `Network`, `Camera`, and `Audio Input`.
- For App Sandbox:
![](https://main.qcloudimg.com/raw/b77d2ab814e6e14e8bed17efdcbee1a6.png)
- For Hardened Runtime:
![](https://main.qcloudimg.com/raw/2b569e1c95bb4c97b7045112d6e3ce9c.png)

## Importing the TRTC SDK
You can import the TRTC SDK in two ways.
### Method 1: Using Objective-C or Swift APIs
There are two ways to use the SDK in Objective-C or Swift:
- **Import the module**: Import the SDK module in the files that will use the SDK APIs.
```
@import TXLiteAVSDK_TRTC_Mac;
```
- **Import the header file**: Import the header file in the files that will use the SDK APIs.
```
#import TXLiteAVSDK_TRTC_Mac/TRTCCloud.h
```

[](id:using_cpp)
### Method 2: Using C++ APIs
1. **Import the header file**: If you want to use C++ APIs to develop your macOS application, import the header file in the `TXLiteAVSDK_TRTC_Mac.framework/Headers/cpp_interface` directory.
```
#include TXLiteAVSDK_TRTC_Mac/cpp_interface/ITRTCCloud.h
```
2. **Use the namespace**: The cross-platform C++ APIs and types are all defined in the TRTC namespace, which you can use directly. This method can simplify your code and is recommended.
```
using namespace trtc;
```

>? For more information on how to use C++ APIs, please see [Overview](https://intl.cloud.tencent.com/document/product/647/35131).
