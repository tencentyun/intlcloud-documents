
## Development Environment Requirements

- Xcode 10 or later
- iOS 8.0 or later


## Integration Description


### CocoaPods integration (recommended)

TUIKit supports CocoaPods integration and manual integration. We recommend CocoaPods integration because it enables upgrades to the latest version at any time.

1. Add the following content in Podfile.
```
#use_frameworks!   // This configuration needs to be shielded because TUIKit uses third-party static libraries.
pod 'TXIMSDK_TUIKit_iOS'                 // The TXLiteAVSDK_TRTC audio and video library is integrated by default.
// pod 'TXIMSDK_TUIKit_iOS_Professional' // The TXLiteAVSDK_Professional audio and video library is integrated by default.
```
The Tencent Cloud [audio and video library](https://intl.cloud.tencent.com/document/product/647/34615) cannot be integrated at the same time due to symbol conflicts. If you use a non-[TRTC](https://intl.cloud.tencent.com/document/product/647/34615#TRTC) version of an audio and video library, we recommend that you remove it first and then integrate the `TXIMSDK_TUIKit_iOS_Professional` version into the pod. This version of the [LiteAV_Professional](https://intl.cloud.tencent.com/document/product/647/34615#.E4.B8.93.E4.B8.9A.E7.89.88.EF.BC.88professional.EF.BC.89) audio and video library includes all basic audio and video capabilities.

2. Run the following command to install TUIKit.
```bash
pod install
```
 If installation of the latest SDK version fails, run the following command to update the local CocoaPods repository list:
```bash
 pod repo update
```


### Manual integration (not recommended)

1. In Framework Search Path, add the file path of ImSDK, and manually add the TUIKit and ImSDK directories to your project.
2. Manually add the third-party libraries used by TUIKit to your project:
 - [MMLayout - Tag : 0.2.0](https://github.com/annidy/MMLayout)
 - [SDWebImage - Tag : 5.9.0](https://github.com/SDWebImage/SDWebImage/tree/5.9.0)
 - [ReactiveObjC - Tag  : 3.1.1](https://github.com/ReactiveCocoa/ReactiveObjC.git)
 - [Toast - Tag  : 4.0.0](https://github.com/scalessec/Toast)
 - [TXLiteAVSDK_TRTC](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/SDK)

## Importing TUIKit

<ol><li>Import TUIKit to the AppDelegate.m file and initialize it.

```objectivec
#import "TUIKit.h"

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
	[[TUIKit sharedInstance] setupWithAppId:sdkAppid]; // SDKAppID can be obtained in the IM Console.
}
```
</li>
<li>Save and compile it.<br>
  If the compilation is successful, the integration is completed. If the compilation fails, check the failure cause or re-perform the integration according to the instructions in this document.
</li></ol>
