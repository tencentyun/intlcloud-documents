This document describes how to quickly run the demo for TRTC SDK for Flutter.

## Environment Requirements
- Flutter 1.12 or above
- Developing for Android:
  - Android Studio 3.5 or above.
  - Devices with Android 4.1 or above
- Developing for iOS:
  - Xcode 11.0 or above
  - Your project has a valid developer signature.

## Prerequisites

You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions

<span id="step1"></span> 
### Step 1. Create an application.
1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Click **Start Now**, enter an application name, e.g. `TestTRTC`, and click **Create Application**.

<span id="step2"></span> 
### Step 2. Download the SDK and demo source code.
1. Click **[GitHub](https://github.com/c1avie/trtc_demo)** to download the SDK and demo source code.
2. After the download, return to the TRTC console and click **Downloaded and Next** to view your `SDKAppID` and secret key.


<span id="step3"></span> 
### Step 3. Configure demo project files.
1. Decompress the source package downloaded in [step 2](#step2).
2. Find and open `Web/js/debug/GenerateTestUserSig.js`.
3. Set parameters in `GenerateTestUserSig.java` as follows.
  - SDKAPPID: `PLACEHOLDER` by default. Set it to the actual `SDKAppID`.
	SECRETKEY: `PLACEHOLDER` by default. Set it to the actual key.
  - Return to the TRTC console and click **Pasted and Next**.
  - Click **Close Guide and Enter Console**.

>!
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for the local execution and debugging of the demo**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

### Step 4. Compile and run the project.
1. Run `flutter pub get`.
2. Compile, run, and debug the project.

###  Android
1. Run `flutter run`.
2. Open the demo project with Android Studio (3.5 or above).
3. Run the project.

### iOS
1. Open the demo project in the `\ios` folder with Xcode (11.0 or above).
2. Compile and run the demo project.



## FAQs

- [The demo is running on two mobile phones, but why can't they display the images of each other?](https://intl.cloud.tencent.com/zh/document/product/647/39242#que1)
- [What firewall restrictions does TRTC face?](hhttps://intl.cloud.tencent.com/zh/document/product/647/39242#que2)
- [What should I do if the iOS app crashes when I build and run it?](https://intl.cloud.tencent.com/zh/document/product/647/39242#que3)
- [What should I do if videos do not show on iOS but do on Android?](https://intl.cloud.tencent.com/zh/document/product/647/39242#que4)
- [What should I do if an error occurs when I run CocoaPods on iOS after updating to the latest version of the SDK?](https://intl.cloud.tencent.com/zh/document/product/647/39242#que5)
- [What should I do if Android Studio fails to build my project with the error “Manifest merge failed”?](https://intl.cloud.tencent.com/zh/document/product/647/39242#que6)
- [What should I do if an error occurs due to the absence of signatures when I debug my project on a real device?](https://intl.cloud.tencent.com/zh/document/product/647/39242#que7)
- [Why can’t I find the corresponding file after deleting/adding content in the swift file of the plugin?](https://intl.cloud.tencent.com/zh/document/product/647/39242#que8)
- [What should I do if the error “Info.plist, error: No value at that key path or invalid key path: NSBonjourServices” occurs when I run my project?](https://intl.cloud.tencent.com/zh/document/product/647/39242#que9)
- [What should I do if an error occurs when I run pod install?](https://intl.cloud.tencent.com/zh/document/product/647/39242#que10)
- [What should I do if a dependency error occurs when I run my project on iOS?](https://intl.cloud.tencent.com/zh/document/product/647/39242#que11)



