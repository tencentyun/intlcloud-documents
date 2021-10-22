
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
4. Add the downloaded `TXLiteAVSDK_Professional.framework` and the libraries it depends on.
```
libz.tbd
libc++.tbd
libresolv.tbd
libsqlite3.tbd
Accelerate.framework
OpenAL.framework
```
![](https://main.qcloudimg.com/raw/899f02c77d58f6e3b9a5d94995c767f8.png)
5. Click **Build Settings**, search for `Other Linker Flags`, and add `-ObjC`.
![](https://main.qcloudimg.com/raw/818eedfb17f50f6041e84126fe4d76ed.png)

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
    
    //TXLiveBase can be found in the "TXLiveBase.h" header file
    [TXLiveBase setLicenceURL:licenceURL key:licenceKey]; 
    NSLog(@"SDK Version = %@", [TXLiveBase getSDKVersionStr]);
}
@end
```

## FAQs
### Can I run LiteAVSDK in the background?
**Yes, you can**. If you want the SDK to run in the background, select your project, under the **Capabilities** tab, set **Background Modes** to **ON**, and check **Audio, AirPlay and Picture in Picture**, as shown below:
![](https://main.qcloudimg.com/raw/ee8a9e445c6af84b5d1cec3869ed7a3a.jpg)
