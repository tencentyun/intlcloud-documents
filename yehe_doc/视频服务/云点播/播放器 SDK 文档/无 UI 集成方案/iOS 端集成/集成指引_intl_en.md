This document describes how to quickly integrate RT-Cube's LiteAVSDK_Player for iOS into your project.


## Environment Requirements
- Xcode 9.0 or later
- iPhone or iPad with iOS 9.0 or later
- A valid developer signature for your project

## Integrating the SDK
You can use CocoaPods to automatically load the SDK or manually download the SDK and import it into your project.

[](id:cocoapods)
### Integration via CocoaPods
1. **Install CocoaPods**
Enter the following command in a terminal window (you need to install Ruby on your Mac first):
```
sudo gem install cocoapods
```
2. **Create a Podfile**
Go to the directory of your project and enter the following command to create a Podfile in the directory.
```
pod init
```
3. **Edit the Podfile.**
	Use CocoaPod's official source, which allows version selection. Edit the Podfile:
	
	Directly integrate the latest version of `TXLiteAVSDK_Player_Premium` as a Pod:
```objective
platform :ios, '9.0'
source 'https://github.com/CocoaPods/Specs.git'

target 'App' do
pod 'TXLiteAVSDK_Player_Premium'
end
```
To specify a version, you can add the following dependency to the `podfile` file:
```objective-c
pod 'TXLiteAVSDK_Player', '~> 110.8.29000'
```

4. **Update the local repository and install the SDK**
  - Enter the following command in a terminal window to update the local repository file and install LiteAVSDK:
```
pod install
```

  - Or, run this command to update the local repository:
```
pod update
```
An XCWORKSPACE project file integrated with LiteAVSDK will be generated. Double-click to open the file.

[](id:manual)
### Manual SDK integration
1. Download the package of the SDK and demo on the latest version of [TXLiteAVSDK_Player_Premium](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Player_Premium_iOS_latest.zip).
2. Add `SDK/TXLiteAVSDK_Player_Premium.framework` to the project to be integrated and select **Do Not Embed**.
3. You need to configure `-ObjC` of the project target; otherwise, the SDK will crash as the SDK category cannot be loaded.

```objective-c
Open Xcode, select the target, select the **Build Settings** tab, search for "Other Link Flag", and enter "-ObjC".
```

4. Add library files (in the SDK directory)
   **TXFFmpeg.xcframework**: Add the .xcframework file to the project, set it to **Embed & Sign** in **General** > **Frameworks, Libraries, and Embedded Content**, and check whether **Code Sign On Copy** is selected in **Build Phases** > **Embed Frameworks** in your **project settings** as shown below:
    **TXSoundTouch.xcframework**: Add the .xcframework file to the project, set it to **Embed & Sign** in **General** > **Frameworks, Libraries, and Embedded Content**, and check whether **Code Sign On Copy** is selected in **Build Phases** > **Embed Frameworks** in your **project settings** as shown below:<br>
    <img style="width:400px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/b226decc76c33eff8c3f5b4cc4246bea.png" />
   <br>
   Then, select **Build Settings** > **Search Paths** in Xcode and add the path of the above frameworks in **Framework Search Paths**.
	
	 **MetalKit.framework**: Open Xcode, go to your **project settings**, select **Build Phases** > **Link Binary With Libraries**, click **+** in the bottom-left corner, and enter "MetalKit" to add it to the project as shown below:<br>
   <img style="width:400px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/8ab7576dcc8bbe7b36396955ca06b186.png" />
   <br>
   <img style="width:400px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/8480798e5ba897077ed3cef8ebc12f2e.png" />
   <br>

	 **ReplayKit.framework**: Open Xcode, go to your **project settings**, select **Build Phases** > **Link Binary With Libraries**, click **+** in the bottom-left corner, and enter "ReplayKit" to add it to the project as shown below:<br>
   <img style="width:400px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/aa07f3d4963ee703505a14a743f61a68.png" />
   <img style="width:400px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/12491d4a64aa6df44e6a966e80ca54de.png" />
   <br>
   Add the following system libraries in the same way:
   <br><b>System frameworks</b>: SystemConfiguration, CoreTelephony, VideoToolbox, CoreGraphics, AVFoundation, Accelerate, and MobileCoreServices<br>
   <b>System libraries:</b> libz, libresolv, libiconv, libc++, and libsqlite3

#### Picture-in-picture (PiP) feature

To use the PiP feature, configure as shown below. If you don’t need the PiP feature, skip this part.

1. To use the PiP feature of iOS, upgrade the SDK to 10.3 or later.
2. To use the PiP feature, you need to enable the background mode. In Xcode, select the target, click **Signing & Capabilities** > **Background Modes**, and select **Audio, AirPlay, and Picture in Picture** as shown below:
<img style="width:400px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/116e1e741f80d810502221fd143d8434.png" />

## Importing the SDK
There are two ways to import the SDK in your project code.
- **Method 1:** import the SDK module in the files that need to use the SDK’s APIs in your project
```
@import TXLiteAVSDK_Player_Premium;
```
- **Method 2:** import a specific header file in the files that need to use the SDK’s APIs in your project
```
#import "TXLiteAVSDK_Player_Premium/TXLiteAVSDK.h"
```

## Configuring License
1. Click [Apply for License](https://www.tencentcloud.com/document/product/266/51098) to apply for a trial license as instructed in [Adding and Renewing a License](https://www.tencentcloud.com/document/product/266/51098#.E7.94.B3.E8.AF.B7.E6.B5.8B.E8.AF.95.E7.89.88-license). If no license is configured, video playback will fail. You will get two strings: a license URL and a decryption key.
2. Before your application calls features of LiteAVSDK, complete the following configuration (preferably in `- [AppDelegate application:didFinishLaunchingWithOptions:]`):
```objc
@import TXLiteAVSDK_Player_Premium;
@implementation AppDelegate
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    NSString * const licenceURL = @"<The license URL obtained>";
    NSString * const licenceKey = @"<The key obtained>";
    
    //TXLiveBase can be found in the "TXLiveBase.h" header file
    [TXLiveBase setLicenceURL:licenceURL key:licenceKey]; 
    // TXLiveBase.delegate = self;
    NSLog(@"SDK Version = %@", [TXLiveBase getSDKVersionStr]);
}

#pragma mark - TXLiveBaseDelegate
- (void)onLicenceLoaded:(int)result Reason:(NSString *)reason {
    NSLog(@"onLicenceLoaded: result:%d reason:%@", result, reason);
}
@end
```

## Viewing License Information

After the license is successfully configured, you can call the API below to view the license information. Please note that it may take a while for the configuration to take effect. The exact time needed depends on your network conditions.

```swift
NSLog(@"%@", [TXLiveBase getLicenceInfo]);
```

[](id:faq)

## FAQs
1. What should I do if a duplicate symbol error occurs because my project integrates multiple editions of LiteAVSDK such as CSS, TRTC, and Player?

If you integrate two or more editions of LiteAVSDK (MLVB, Player, TRTC, UGSV), a library conflict error will occur when you build your project. This is because some symbol files are shared among the underlying libraries of the SDKs. To solve the problem, we recommend you integrate the All-in-One SDK, which includes the features of MLVB, Player, TRTC, and UGSV. For details, see [SDK Download](https://www.tencentcloud.com/document/product/266/50561).

