
## Development Environment Requirements

- Xcode 10 or later
- iOS 8.0 or later


## Integration Description


### CocoaPods integration (recommended)

You can automatically or manually integrate TUIKit by using CocoaPods. We recommend that you use CocoaPods integration to update to the latest version when it is available.

1. Add the following code to Podfile.
```
pod 'TXIMSDK_TUIKit_iOS'
```
2. Run the following command to install TUIKit.
```bash
pod install
```
 If you fail to install the latest version of the SDK, run the following command to update the local CocoaPods repository list.
```bash
 pod repo update
```


### Manual integration (not recommended)

1. Add the ImSDK file path to Framework Search Path to manually add the TUIKit and ImSDK directories to your project.
2. Manually add third-party libraries used by TUIKit to your project:
 - [MMLayout](https://github.com/annidy/MMLayout)
 - [SDWebImage](https://github.com/SDWebImage/SDWebImage)
 - [ReactiveObjC](https://github.com/ReactiveCocoa/ReactiveObjC.git)
 - [Toast](https://github.com/scalessec/Toast)
 - [ISVImageScrollView](https://github.com/yuriiik/ISVImageScrollView)

**Use the latest library tags to integrate the preceding dependent libraries.**

## Referencing TUIKit

<ol><li>Import TUIKit to the AppDelegate.m file and initialize it.

```objectivec
#import "TUIKit.h"

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
	[[TUIKit sharedInstance] setupWithAppId:sdkAppid]; // The SDKAppID can be obtained in the IM console.
}
```
</li>
<li>Save and compile.<br>
  Successful compilation indicates that the integration is completed. If compilation fails, check the cause of the error or integrate again according to the instructions in this document.
</li></ol>
