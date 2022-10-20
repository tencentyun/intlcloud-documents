This document describes how to quickly integrate [live_flutter_plugin](https://pub.dev/packages/live_flutter_plugin) (Tencent Cloud RT-Cube MLVB Flutter plugin) into your project. For the demo project, visit [GitHub](https://github.com/LiteAVSDK/Live_Flutter).

## Environment Requirements
- Flutter 2.0 or later
- **Developing for Android:**
  - Android Studio 3.5 or later
  - Devices with Android 4.1 or later
- **Developing for iOS and macOS:**
  - Xcode 11.0 or later
  - OS X 10.11 or later
  - A valid developer signature for your project


## Quickly Integrating the SDK
The SDK for Flutter has been released to the Pub repository. You can configure `pubspec.yaml` to download the update automatically.

1. Add the following dependencies to `pubspec.yaml` of your project:
```dart
dependencies:
  live_flutter_plugin: latest version number
```
2. Get camera and mic permissions to enable the audio and video call features.
<dx-tabs>
:::  iOS
1. Add requests for camera and mic permissions in `Info.plist`:
```dart
<key>NSCameraUsageDescription</key>
<string>Video calls are possible only with camera permission.</string>
<key>NSMicrophoneUsageDescription</key>
<string>You can make audio calls only if you grant the app mic permission.</string>
```
2. Get camera and mic permissions to enable the audio and video call features.
:::
::: Android
1. Open `/android/app/src/main/AndroidManifest.xml`.
2. Add `xmlns:tools="http://schemas.android.com/tools"` to `manifest`.
3. Add `tools:replace="android:label"` to `application`.
>? Without the above steps, the "Android Manifest merge failed" error will occur and the compilation will fail.

![](https://main.qcloudimg.com/raw/7a37917112831488423c1744f370c883.png)
:::
</dx-tabs>


## Getting Started
1. Click [Apply for License](https://console.tencentcloud.com/live/license) to get a trial license. You will get two strings: a license URL and a decryption key.
2. Before your application calls features of `live_flutter_plugin`, complete the following configuration:
```dart
import 'package:live_flutter_plugin/v2_tx_live_premier.dart';

 /// Tencent Cloud license management page (https://console.tencentcloud.com/live/license)
setupLicense() {
  // The license URL of the current application
  var LICENSEURL = "";
  // The license key of the current application
  var LICENSEURLKEY = "";
  V2TXLivePremier.setLicence(LICENSEURL, LICENSEURLKEY);
}

```

## FAQs
For more FAQs, see [Flutter](https://intl.cloud.tencent.com/document/product/647/39242).

### How do I get a valid stream push URL?
Activate CSS. In the **CSS console**, go to **Auxiliary Tools** > [**Address Generator**](https://console.tencentcloud.com/live/addrgenerator/addrgenerator) to generate a stream push URL. For more information, see [Publishing/Playback URL](https://www.tencentcloud.com/document/product/1071/39359).

### What should I do if videos do not show on iOS but do on Android?

Check whether `io.flutter.embedded_views_preview` in `info.plist` is `YES`.

### What should I do if the "Manifest merge failed" error occurs in Android Studio?
1. Open `/example/android/app/src/main/AndroidManifest.xml`.
2. Add `xmlns:tools="http://schemas.android.com/tools"` to `manifest`.
3. Add `tools:replace="android:label"` to `application`.

![Illustration](https://main.qcloudimg.com/raw/7a37917112831488423c1744f370c883.png)
