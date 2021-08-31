## Environment Requirements

- Xcode 10 or later
- iOS 8.0 or later
## Integration Description
### CocoaPods integration (recommended)

TUIKit supports CocoaPods integration and manual integration. We recommend that you use CocoaPods integration to ensure that you can update to the latest version at any time.

<ol><li>Add the following content in the Podfile.

```

// TUIKit uses a third-party static library. This setting needs to be blocked.
#use_frameworks!

// TXIMSDK_TUIKit_live_iOS uses the *.xcassets resource file. You need to add this statement to prevent it from conflicting with other resource files in the project.
install! 'cocoapods', :disable_input_output_paths => true  

// Integrate the chat, relationship chain, and group features.
 pod 'TXIMSDK_TUIKit_iOS'  
 
// Integratevoice and video calls, group livestreaming and livestreaming plazas, using the TXLiteAVSDK_TRTC library as the default dependency.
pod 'TXIMSDK_TUIKit_live_iOS'	

// Integrate voice and video calls, group livestreaming, and livestreaming plazas, using the TXLiteAVSDK_Professional TRTC library as the default dependency.
// pod 'TXIMSDK_TUIKit_live_iOS_Professional' 

```
>! 1. `TXIMSDK_TUIKit_live_iOS` and `TXIMSDK_TUIKit_iOS` must have consistent versions. Otherwise, logic exceptions may occur.
2. Do not integrate different Tencent Cloud [audio and video libraries](https://intl.cloud.tencent.com/document/product/647/34615) at the same time to avoid symbol conflicts. If you use a library not of the [TRTC](https://intl.cloud.tencent.com/document/product/647/34615#TRTC) version, we recommend that you remove it and integrate the `TXIMSDK_TUIKit_iOS_Professional` version. The audio and video library of the [LiteAV_Professional](https://intl.cloud.tencent.com/document/product/647/34615#.E4.B8.93.E4.B8.9A.E7.89.88.EF.BC.88professional.EF.BC.89) version contains all basic audio and video capabilities.

<li> Run the following command to install TUIKit. <br>

```bash
pod install
```
 If the latest SDK version cannot be installed, run the following command to update the local CocoaPods repository list. <br>

```bash
 pod repo update
```
</ol></li>

### Manual integration (not recommended)

1. Add the ImSDK file path to Framework Search Path and manually add the TUIKit and ImSDK directories to your project.
2. Manually add the third-party library used by TUIKit to your project:
 - [MMLayout - Tag : 0.2.0](https://github.com/annidy/MMLayout)
 - [SDWebImage - Tag : 5.9.0](https://github.com/SDWebImage/SDWebImage/tree/5.9.0)
 - [ReactiveObjC - Tag  : 3.1.1](https://github.com/ReactiveCocoa/ReactiveObjC.git)
 - [Toast - Tag  : 4.0.0](https://github.com/scalessec/Toast)
 - [TXLiteAVSDK_TRTC](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/SDK)

## Importing TUIKit

<ol><li>Introduce TUIKit in the AppDelegate.m file and initialize it.

```objectivec
#import "TUIKit.h"

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
	[[TUIKit sharedInstance] setupWithAppId:sdkAppid]; // SDKAppID can be obtained from the IM console.
}
```
</li>
<li>Compile and save the file. <br>
  If compilation is successful, integration has been completed. If compilation fails, check the cause of the error or perform integration again based on this document.
</li></ol>

## FAQs

### 1 ** target has transitive dependencies that include statically linked binaries

If this error occurs during the pod process, this is because `TUIKit` is using a third-party static library. You need to comment out `use_frameworks!` in the podfile.

If you need to use `use_frameworks!`, use `cocoapods 1.9.0` or a later version for `pod install` and modify it as follows:

```
use_frameworks! :linkage => :static
```

If you use `swift`, change the reference of the header file to the reference format of @import module name.
