
This document describes how to quickly integrate the MLVB SDK (iOS) of Tencent Video Cloud Toolkit into your project. The directions below use the full-featured [MLVB Professional Edition](https://intl.cloud.tencent.com/document/product/1071/38150) as an example.

## Environment Requirements
- Xcode 9.0 or above
- iPhone or iPad with iOS 9.0 or above
- A valid developer signature for your project

## Integrating the SDK
You can use CocoaPods to automatically load the SDK or manually download the SDK and import it into your project.

[](id:cocoapods)
### CocoaPods
#### 1. Install CocoaPods
Enter the following command in a terminal window (you need to install Ruby on your macOS first):
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
- Method 1: use the path of the PODSPEC file of LiteAVSDK
<dx-codeblock>
:::  podspec
  platform :ios, '9.0'
  
  target 'App' do
  pod 'TXLiteAVSDK_Professional', :podspec => 'https://liteav.sdk.qcloud.com/pod/liteavsdkspec/TXLiteAVSDK_Professional.podspec'
  end
:::
</dx-codeblock>
- Method 2: use CocoaPod’s official source, which allows version selection
<dx-codeblock>
COCOAPOD
   platform :ios, '9.0'
   source 'https://github.com/CocoaPods/Specs.git'
  
   target 'App' do
   pod 'TXLiteAVSDK_Professional'
   end
:::
</dx-codeblock>

#### 4. Update the local repository and install the SDK
Enter the following command in a terminal window to update the local repository file and install LiteAVSDK:
```
pod install
```
Or, run the following command to update the local repository:
```
pod update
```

An XCWORKSPACE project file integrated with LiteAVSDK will be generated. Double-click to open the file.

[](id:manual)
### Manual integration
1. Download [LiveAVSDK](https://intl.cloud.tencent.com/document/product/1071/38150) and decompress the file.
2. Open your Xcode project, select the target you want to run, and select **Build Phases**.
![](https://main.qcloudimg.com/raw/d78299d12be0f6c3255eabec91941e7a.jpg)
3. Expand **Link Binary with Libraries** and click **+** at the bottom to add the libraries to depend on.
![](https://main.qcloudimg.com/raw/dffd804d78d3e5765add218cb228c842.png)
4. Add the downloaded `TXLiteAVSDK_Professional.framework`、`TXFFmpeg.xcframework`、`TXSoundTouch.xcframework` and the libraries it depends on.
```
AVFoundation.framework
VideoToolbox.framework
libz.tbd
OpenGLES.framework
Accelerate.framework
libsqlite3.0.tbd
MetalKit.framework
CoreTelephony.framework
libresolv.tbd
GLKit.framework
Foundation.framework
SystemConfiguration.framework
AssetsLibrary.framework
libc++.tbd
CoreServices.framework
CoreMedia.framework
```
![](https://qcloudimg.tencent-cloud.cn/raw/2cad68ebf4de0faba9fad17c8cf769e7.png)
5. Click **Build Settings**, search for `Other Linker Flags`, and add `-ObjC`.
![](https://qcloudimg.tencent-cloud.cn/raw/c4709ea5f04ab51f6f2ce454ba1c1275.png)

## Granting Camera and Mic Permissions
To use the audio/video features of the SDK, you need to grant it mic and camera permissions. Add the two items below to `Info.plist` of your application to display pop-up messages asking for mic and camera permissions.
- **Privacy - Microphone Usage Description**, plus a statement specifying why mic access is needed
- **Privacy - Camera Usage Description**, plus a statement specifying why camera access is needed

![](https://main.qcloudimg.com/raw/aedd6bd1fb5821de41002f028c616661.png)

## Importing the SDK
There are two ways to import the SDK in your project code.
- **Method 1:** import the SDK module in the files that need to use the SDK’s APIs in your project
```
@import TXLiteAVSDK_Professional;
```
- **Method 2:** import a specific header file in the files that need to use the SDK’s APIs in your project
```
#import "TXLiteAVSDK_Professional/TXLiteAVSDK.h"
```

## Configuring License

Click [Get License](https://console.cloud.tencent.com/live/license) to obtain a trial license. You will get two strings: a license URL and a decryption key.

Before you use LiteAVSDK features in your application, complete the following configurations (preferably in `- [AppDelegate application:didFinishLaunchingWithOptions:]`):

```objc
@import TXLiteAVSDK_Professional;
@implementation AppDelegate
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    NSString * const licenceURL = @"<The license URL obtained>";
    NSString * const licenceKey = @"<The key obtained>";
    
    //V2TXLivePremier can be found in the "V2TXLivePremier.h" header file
    [V2TXLivePremier setEnvironment:@"GDPR"];
    [V2TXLivePremier setLicence:licenceURL key:licenceKey];
    [V2TXLivePremier setObserver:self];
    NSLog(@"SDK Version = %@", [V2TXLivePremier getSDKVersionStr]);
}
@end
```

## FAQs
### 1. Can I run LiteAVSDK in the background?
**Yes, you can**. If you want the SDK to run in the background, the operation is as follows:
1. Select the current project, select **Signing&Capabilities** , click **+** in the upper left corner, as shown in the figure:
![](https://qcloudimg.tencent-cloud.cn/raw/d06bbd6669a4d60bbf2c217b0a8cc961.png)
2. Select **Background Modes**.
![](https://qcloudimg.tencent-cloud.cn/raw/d43e735cb3450fe10c3327803904c0b2.png)
3. Check **Audio, AirPlay and Picture in Picture** in **Background Modes**, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/e37c5de253b07f27de0a6554ba3a6311.png)

### 2. How to solve the problem of symbol conflict between multiple SDKs of LiteAVSDK series such as live SDK/real-time audio/video/player integrated in the project?
If you integrate 2 or more LiteAVSDK products (live broadcast, player, TRTC, short video), there will be a library conflict problem when compiling, because some SDK underlying libraries have the same symbol files, it is recommended to integrate only one full-featured version of the SDK. Live broadcast, player, TRTC, and short video are all included in one SDK.For details, please refer to [SDK Download](https://www.tencentcloud.com/document/product/1071/38150).