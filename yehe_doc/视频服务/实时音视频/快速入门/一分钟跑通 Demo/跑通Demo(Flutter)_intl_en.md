This document describes how to quickly run the TRTC demo for Flutter.

## Environment Requirements
- Flutter 2.0 or above
- Developing for Android:
  - Android Studio 3.5 or above
  - Devices with Android 4.1 or above
- Developing for iOS:
  - Xcode 11.0 or above
  - Your project has a valid developer signature.

## Prerequisites

You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions

[](id:step1)

### Step 1. Create an application.
1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name, e.g. `TestTRTC`, and click **Create**.

[](id:step2)
### Step 2. Download the SDK and demo source code.
1. Download the SDK and demo source code for your platform.
2. Click **Next step**.


[](id:step3)
### Step 3. Configure demo project files.
1. In the **Modify Configuration** step, select the platform in line with the source package downloaded.
2. Find and open `/example/lib/debug/GenerateTestUserSig.dart`.
3. Set parameters in `GenerateTestUserSig.dart` as follows.
<ul><li/>SDKAPPID: `PLACEHOLDER` by default. Set it to the actual `SDKAppID`.
	<li/>SECRETKEY: `PLACEHOLDER` by default. Set it to the actual key.</ul>
4. Click **Next step** to complete the creation.
5. After compilation, click **Return to Overview Page**.

>!
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for the local execution and debugging of the demo**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

### Step 4. Compile and run the project.
1. Run `flutter pub get`.
2. Compile, run, and debug the project.

#### Android
1. Run `flutter run`.
2. Open the demo project with Android Studio (3.5 or above).
3. Run the project.

#### iOS
1. Open `\ios project` in the source code directory with Xcode (11.0 or above).
2. Compile and run the demo project.



## FAQs

- [The demo is running on two mobile phones, but why can't they display the images of each other?](https://intl.cloud.tencent.com/document/product/647/39242)
- [What firewall restrictions does TRTC face?](https://intl.cloud.tencent.com/document/product/647/39242)
- [What should I do if the iOS app crashes when I build and run it?](https://intl.cloud.tencent.com/document/product/647/39242)
- [What should I do if videos do not show on iOS but do on Android?](https://intl.cloud.tencent.com/document/product/647/39242)
- [What should I do if an error occurs when I run CocoaPods on iOS after updating to the latest version of the SDK?](https://intl.cloud.tencent.com/document/product/647/39242)
- [What should I do if I Android Studio fails to build my project with the error “Manifest merge failed”?](https://intl.cloud.tencent.com/document/product/647/39242)
- [What should I do if an error occurs due to the absence of signatures when I debug my project on a real device?](https://intl.cloud.tencent.com/document/product/647/39242)
- [After deleting/adding content in the swift file of the plugin, why can’t I find the corresponding file when building my project?](https://intl.cloud.tencent.com/document/product/647/39242)
- [What should I do if the error “Info.plist, error: No value at that key path or invalid key path: NSBonjourServices” occurs when I run my project?](https://intl.cloud.tencent.com/document/product/647/39242)
- [What should I do if an error occurs when I run `pod install`?](https://intl.cloud.tencent.com/document/product/647/39242)
- [What should I do if a dependency error occurs when I run my iOS project?](https://intl.cloud.tencent.com/document/product/647/39242)



