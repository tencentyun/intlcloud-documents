This document describes how to quickly integrate the Tencent Cloud Chat SDK into your Flutter project.

## Environment Requirements

| Platform | Version                                                      |
| -------- | ------------------------------------------------------------ |
| Flutter  | 2.2.0 or later                                               |
| Android  | Android Studio 3.5 or later; devices with Android 4.1 or later for apps |
| iOS      | Xcode 11.0 or later. For testing with a real device, ensure that your project has a valid developer signature. |

## Supported Platforms

We are committed to building a set of Chat SDK and TUIKit for all Flutter platforms, allowing you to run one set of code across all platforms.

| Platform                                                     | Support or Not          |
| ------------------------------------------------------------ | ----------------------- |
| iOS                                                          | Supported               |
| Android                                                      | Supported               |
| [Web](#web)                                                  | Supported from v4.1.1+2 |
| [macOS](#pc)                                                 | Supported from v4.1.9   |
| [Windows](#pc)                                               | Supported from v4.1.9   |
| [Hybrid development](https://www.tencentcloud.com/document/product/1047/51456) (Adding SDK for Flutter to existing native applications) | Supported from v5.0.0   |

>? For web, macOS, and Windows platforms, you need to perform a few extra steps for SDK integration. For details, see [Support for the Flutter for Web](#web) and [Support for the Flutter for Desktop](#pc) in this document.

## Trying Out Demos

Before integration, you can try out our demos to quickly understand the capabilities of the Tencent Cloud Chat cross-platform SDK and TUIKit for Flutter.

**All of the following demos are packaged by the same Flutter project.** The Chat SDK for Flutter already supports desktop platforms (macOS/Windows), and the corresponding demo will be available soon.

<table style="text-align:center; vertical-align:middle; max-width: 800px">
  <tr>
    <th style="text-align:center;">Mobile App</th>
    <th style="text-align:center;">Web - HTML5</th>
  </tr>
  <tr>
    <td><div style="display: flex; justify-content: center; align-items: center; flex-direction: column; padding-top: 10px">iOS/Android app (automatically downloaded according to your platform)<img style="max-width:200px; margin: 20px 0 20px 0" src="https://qcloudimg.tencent-cloud.cn/raw/ca2aaff551410c74fce48008c771b9f6.png"/></div></td>
    <td><div style="display: flex; justify-content: center; align-items: center; flex-direction: column; padding-top: 10px">Scan the QR code with your mobile phone to try out<img style="max-width:200px; margin: 20px 0 20px 0" src="https://qcloudimg.tencent-cloud.cn/raw/3c79e8bb16dd0eeab35e894a690e0444.png"/></div></td>
  </tr>
</table>

## Integrating the Chat SDK

You can directly integrate the Chat SDK for Flutter through [pub add](https://pub.dev/packages/tencent_cloud_chat_sdk), or write the Chat SDK into `pubspec.yaml`.

### Installing the Chat SDK via `flutter pub add`

Enter the following command in the terminal window (the Flutter environment is ready):

```
flutter pub add tencent_cloud_chat_sdk
```

>?If your project also needs to be applied to [web](#web) or [desktop (macOS/Windows)](#pc) platforms, you need to perform a few extra steps for SDK integration. For details, see [Support for the Flutter for Web](#web) and [Support for the Flutter for Desktop](#pc) in this document.

### Writing the Chat SDK into `pubspec.yaml`

```
dependencies:
  tencent_cloud_chat_sdk: "Latest version" // You can check the latest version of the Chat SDK for Flutter on https://pub.dev/packages/tencent_cloud_chat_sdk
```

Here, your editor may automatically run `flutter pub get`. If not, enter the command `flutter pub get`.

If your project requires web support, import JS files by referring to [the web compatibility description section](#web) before performing subsequent steps.

### Importing and initializing the SDK

```
import 'package:tencent_cloud_chat_sdk/tencent_cloud_chat_sdk.dart';
```

## Support for the Flutter for Web[](id:web)

Chat SDK (tencent_cloud_chat_sdk) 4.1.1+2 or later provides full compatibility with web.

To enable support for web, you need to perform the following extra steps, compared with the steps to enable support for Android and iOS:

### Upgrading to Flutter 3.x

Flutter 3.x has been dramatically optimized for web performance and is highly recommended for Flutter web project development.

### Importing JS

>?If your existing Flutter project does not support web, run `flutter create .` in the root directory of the project to add web support.

Go to the `web/` directory of your project and use npm or Yarn to install related JS dependencies. To initialize the project, follow the on-screen instructions.

```shell
cd web

npm init

npm i tim-js-sdk

npm i tim-upload-plugin
```

Open `web/index.html` and import the JS files in `<head> </head>`. See below:

```html
<script src="./node_modules/tim-upload-plugin/index.js"></script>
<script src="./node_modules/tim-js-sdk/tim-js-friendship.js"></script>
```

![](https://staticintl.cloudcachetci.com/yehe/backend-news/AhQ9056_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_1672108602242.png)

### Importing the Flutter for Web supplement SDK

```dart
flutter pub add tencent_im_sdk_plugin_web
```

## Support for the Flutter for Desktop (PC)[](id:pc)

Our no-UI SDK (tencent_cloud_chat_sdk) v4.1.9 or later provides full compatibility with macOS and Windows clients.

To enable support for macOS and Windows, you need to perform the following extra steps, compared with the steps to enable support for Android and iOS:

### Upgrading to Flutter 3.x

Only Flutter 3.0 or later supports desktop clients. Therefore, if you need to use desktop clients, upgrade your Flutter to Flutter 3.x.

### Importing the Flutter for Desktop supplement SDK

```dart
flutter pub add tencent_im_sdk_plugin_desktop
```

#### Modifying macOS configuration

Open the `macos/Runner/DebugProfile.entitlements` file.

In `<dict></dict>`, add the following key-value pair:

```
<key>com.apple.security.app-sandbox</key>
<false/>
```

## FAQs

### What should I do if `flutter pub get/add` fails?

Configure Flutter to use a mirror site as instructed in [Flutter](https://flutter.cn/community/china).
