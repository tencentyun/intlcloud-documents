# LiteAVSDK Integration Document_iOS

[Original document URL](https://github.com/tencentyun/qcloud-documents/edit/master/product/%E8%A7%86%E9%A2%91%E6%9C%8D%E5%8A%A1/%E7%A7%BB%E5%8A%A8%E7%9B%B4%E6%92%AD/%E5%9F%BA%E7%A1%80%E5%8A%9F%E8%83%BD/SDK%20%E9%9B%86%E6%88%90/iOS.md)

This document describes how to quickly integrate the LiteAVSDK (iOS) into your project.

## Development Environment Requirements
- Xcode 9.0+.
- iPhone or iPad on iOS 9.0 or above.
- Your project has a valid developer signature.

## Integrating the LiteAVSDK
You can choose to use CocoaPods for automatic loading, or download the SDK first and then import it into your current project.

### CocoaPods
#### 1. Install CocoaPods
Enter the following command in the terminal window (you need to install the Ruby environment on your macOS in advance):
```
sudo gem install cocoapods
```

#### 2. Create a Podfile
Go to the path to the project, enter the following command, and a Podfile will appear in the project path.
```
pod init
```

#### 3. Edit the Podfile
There are two ways to edit the Podfile:
- Method 1: use the `podspec` file path of the Tencent Cloud LiteAV SDK.
/// Create TODO TXLiteAVSDK_International.podspec and change the repository URL. Alternatively, delete this mode and retain only [Manual integration](#Manual integration).
```
  platform :ios, '8.0'
  
  target 'App' do
  pod 'TXLiteAVSDK_International', :podspec => 'http://pod-1252463788.cosgz.myqcloud.com/liteavsdkspec/TXLiteAVSDK_International.podspec'
  end
```

- Method 2: use the official source of CocoaPod, which allows you to choose the version number.

```
   platform :ios, '8.0'
   source 'https://github.com/CocoaPods/Specs.git'
   
   target 'App' do
   pod 'TXLiteAVSDK_International'
   end
```

#### 4. Update and install the SDK
Enter the following command in the terminal window to update the local repository file and install the LiteAVSDK:
```
pod install
```
Or, run the following command to update the local repository:
```
pod update
```

After the pod command is executed, an `.xcworkspace` project file integrated with the SDK will be generated. Double-click this file to open it.


### Manual integration
1. Download the [LiveAVSDKV2](https://cloud.tencent.com/document/product/454/7873), and then decompress it.

2. Open your Xcode project, select the target you want to run, and select **Build Phases**.
![](https://main.qcloudimg.com/raw/81404ea4ae84f577941c0ede791eb205.png)

3. Click **Link Binary with Libraries** to expand it and then click the "+" icon at the bottom to add the dependent library.
![](https://main.qcloudimg.com/raw/940265f2e206619d249077db5f29800b.png)

4. Add the downloaded `TXLiteAVDemo_International.framework` and its dependent library.
/// For TODO, check whether the dependent libraries are as follows. If not, change the content and images.
```
libz.tbd
libc++.tbd
libresolv.tbd
libsqlite3.tbd
Accelerate.framework
OpenAL.framework
```
![](https://main.qcloudimg.com/raw/899f02c77d58f6e3b9a5d94995c767f8.png)

## Granting Camera and Microphone Permissions
To use the audio/video features of the SDK, you need to grant the microphone and camera permissions. Add the following two items to the `Info.plist` file of the application. The two items correspond to the microphone and camera prompt messages when the authorization dialog box pops up.
- **Privacy - Microphone Usage Description**. Enter the prompt that indicates the purpose of using the microphone.
- **Privacy - Camera Usage Description**. Enter the prompt that indicates the purpose of using the camera.

## Introducing the SDK to the Project
There are two ways to use the SDK in your project code:
- Method 1: add an import module to the project's files that need to use the SDK APIs.
```
@import TXLiteAVSDK_International;
```

- Method 2: import specific header files into the project's files that need to use the SDK APIs.
```
#import <TXLiteAVSDK.h>
```

## Configuring a License for the SDK

Click [Apply for a License](https://console.cloud.tencent.com/live/license) to obtain the license for testing. You will receive two strings. One is the license URL, and the other is the decryption key.

Before you call the LiteAVSDK features in your app, we recommend that you complete the following configurations in `- [AppDelegate application:didFinishLaunchingWithOptions:]`:

```objc
@import TXLiteAVSDK_Professional;
@implementation AppDelegate
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    NSString * const licenceURL = @"<Obtained license URL>";
    NSString * const licenceKey = @"<Obtained key>";
		
    //TXLiveBase is located in the "TXLiveBase.h" header file.
    [TXLiveBase setLicenceURL:licenceURL key:licenceKey]; 
    NSLog(@"SDK Version = %@", [TXLiveBase getSDKVersionStr]);
}
@end
```

## FAQs
### Can I run the LiteAVSDK in the background?
Yes. If you want the SDK to run relevant features in the background, you can select the current project, set **Background Modes** under **Capabilities** to **ON**, and check **Audio, AirPlay and Picture in Picture** as shown below:
![](https://main.qcloudimg.com/raw/9c8698d4fc563b7d0d70f415b7471572.png)


