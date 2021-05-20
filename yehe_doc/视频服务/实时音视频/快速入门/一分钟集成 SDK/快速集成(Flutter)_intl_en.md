This document describes how to quickly integrate TRTC SDK for Flutter into your project.

## Environment Requirements
- Flutter 2.0or above
- Developing for Android:
  - Android Studio 3.5 or above
  - Devices with Android 4.1 or above
- Developing for iOS:
  - Xcode 11.0 or above
  - Your project has a valid developer signature.

### Integrating the SDK

The SDK for Flutter has been published on [Pub](https://pub.dev/packages/tencent_trtc_cloud). You can have the SDK downloaded and updated automatically by configuring `pubspec.yaml`.
1. Add the following dependency to `pubspec.yaml` of your project.
```
dependencies:
  tencent_trtc_cloud: latest version number
```
2. Grant **camera** and **mic** permissions to enable the audio and video call features.

#### iOS
1. Add requests for camera and mic permissions in `Info.plist`:
```
<key>NSCameraUsageDescription</key>
<string>Video calls are possible only with camera permission.</string>
<key>NSMicrophoneUsageDescription</key>
<string>Audio calls are possible only with mic permission.</string>
```
2. Add the field `io.flutter.embedded_views_preview` and set the value to `Yes`.

#### Android
1. Open `/android/app/src/main/AndroidManifest.xml`.
2. Add `xmlns:tools="http://schemas.android.com/tools"` to “manifest”.
3. Add `tools:replace="android:label"` to “application”.
>? Without the above steps, the [“Android Manifest merge failed”](https://intl.cloud.tencent.com/zh/document/product/647/39242#que6) error will occur and the compilation will fail.


![Illustration](https://main.qcloudimg.com/raw/7a37917112831488423c1744f370c883.png)





## FAQs
- [What should I do if the iOS app crashes when I build and run it?](https://intl.cloud.tencent.com/zh/document/product/647/39242#que3)
- [What should I do if videos do not show on iOS but do on Android?](https://intl.cloud.tencent.com/zh/document/product/647/39242#que4)
- [What should I do if an error occurs when I run CocoaPods on iOS after updating to the latest version of the SDK?](https://intl.cloud.tencent.com/zh/document/product/647/39242#que5)
- [What should I do if Android Studio fails to build my project with the error “Manifest merge failed”?](https://intl.cloud.tencent.com/zh/document/product/647/39242#que6)
- [What should I do if an error occurs due to the absence of signatures when I debug my project on a real device?](https://intl.cloud.tencent.com/zh/document/product/647/39242#que7)
- [Why can’t I find the corresponding file after deleting/adding content in the swift file of the plugin?](https://intl.cloud.tencent.com/zh/document/product/647/39242#que8)
- [What should I do if the error “Info.plist, error: No value at that key path or invalid key path: NSBonjourServices” occurs when I run my project?](https://intl.cloud.tencent.com/zh/document/product/647/39242#que9)
- [What should I do if an error occurs when I run pod install?](https://intl.cloud.tencent.com/zh/document/product/647/39242#que10)
- [What should I do if a dependency error occurs when I run my project on iOS?](https://intl.cloud.tencent.com/zh/document/product/647/39242#que11)


