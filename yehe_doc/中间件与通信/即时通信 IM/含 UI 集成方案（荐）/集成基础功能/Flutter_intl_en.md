## TUIKit Overview
Flutter TUIKit is a set of TUI components based on Flutter IM SDKs. It provides features such as the conversation, chat, relationship chain, and group features. You can use these TUI components to quickly build your own business logic. The architecture of Flutter TUIKit is as follows.
![](https://qcloudimg.tencent-cloud.cn/raw/b336c1a482129254682d405e008fec01.png)

This TUIKit component library and the matching business logic code [im-flutter-uikit](https://github.com/tencentyun/TIMSDK/tree/master/Flutter/Demo/im-flutter-uikit) are open source. You can import the online version of TUIKit or import TUIKit locally after forking it.

Currently, Flutter TUIKit contains the following components:

- [TIMUIKitCore](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitCore/): core
- [TIMUIKitConversation](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitConversation/): conversation list
- [TIMUIKitChat](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitChat/): chat area that lists sent and historical messages
- [TIMUIKitContact](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitContact/): contacts
- [TIMUIKitProfile](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitProfile/): user profile viewing and relationship management
- [TIMUIKitGroupProfile](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitGroupProfile/): group profile display and management
- [TIMUIKitGroup](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitGroup/): my group chats
- [TIMUIKitBlackList](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitBlackList/): blocklist
- [TIMUIKitNewContact](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitNewContact/): new contact requests
- [TIMUIKitSearch](https://intl.cloud.tencent.com/document/product/1047/50036): local search

![](https://qcloudimg.tencent-cloud.cn/raw/f140dd76be01a65abfb7e6ba2bf50ed5.png)

>?
>
> The TUIKit interfaces listed in the above figure support automatic or manual language switching between **Simplified Chinese, Traditional Chinese, and English**. For multilingual inquiries, please [contact us](#contact).

## Directions
The following describes how to use Flutter TUIKit to quickly build a simple IM app.

### Step 1. Create a Flutter app and configure permissions
Quickly create a Flutter app. For details, see [Flutter documentation](https://flutter.cn/docs/get-started/test-drive?tab=terminal).
#### Configuring permissions[](id:permission)

As TUIKit running requires the camera, album, recording, and network permissions, you need to manually declare them in the `Native` file.

**Android**

Open `android/app/src/main/AndroidManifest.xml` and add the following permissions to `<manifest></manifest>`:
```xml
    <uses-permission
        android:name="android.permission.INTERNET"/>
    <uses-permission
        android:name="android.permission.RECORD_AUDIO"/>
    <uses-permission
        android:name="android.permission.FOREGROUND_SERVICE"/>
    <uses-permission
        android:name="android.permission.ACCESS_NETWORK_STATE"/>
    <uses-permission
        android:name="android.permission.VIBRATE"/>
    <uses-permission
        android:name="android.permission.ACCESS_BACKGROUND_LOCATION"/>
    <uses-permission
        android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
    <uses-permission
        android:name="android.permission.READ_EXTERNAL_STORAGE"/>
    <uses-permission
        android:name="android.permission.CAMERA"/>
```

**iOS**

Open `ios/Podfile` and add the following permission code at the end of the file.
```
post_install do |installer|
  installer.pods_project.targets.each do |target|
    flutter_additional_ios_build_settings(target)
    target.build_configurations.each do |config|
          config.build_settings['GCC_PREPROCESSOR_DEFINITIONS'] ||= [
            '$(inherited)',
            'PERMISSION_MICROPHONE=1',
            'PERMISSION_CAMERA=1',
            'PERMISSION_PHOTOS=1',
          ]
        end
  end
end
```

>?
> 
> If you want to use the push capability, you also need to add push permissions. For more information, see [Vendor Message Push Plugin Integration Guide for Flutter](https://intl.cloud.tencent.com/document/product/1047/48566).

#### Installing the IM TUIKit

TUIKit contains the IM SDK, so you only need to install `tim_ui_kit`.

```shell
# Run the following command:
flutter pub add tim_ui_kit
```

If your project requires web support, import JS files by referring to [the web compatibility description section](#web) before performing subsequent steps.

### Step 2. Initialization

1. Initialize the TUIKit upon application start.
2. Run [`TIMUIKitCore.getInstance()`](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitCore/getInstance.html) first and then call the initialization function [`init()`](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitCore/init.html). Remember to pass in your `sdkAppID`.
```dart
/// main.dart
import 'package:tim_ui_kit/tim_ui_kit.dart';

final CoreServicesImpl _coreInstance = TIMUIKitCore.getInstance();
  @override
 void initState() {
   _coreInstance.init(
     sdkAppID: 0, // Replace 0 with the SDKAppID of your IM application when integrating
     loglevel: LogLevelEnum.V2TIM_LOG_DEBUG,
     listener: V2TimSDKListener());    
   super.initState();
 }
}
```

>?
>
> Do not perform subsequent steps before the initialization in this step is completed.

#### Logging in with a test account
1. Log in with a test account initially generated in the console for verification.
2. Call the [`_coreInstance.login`](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitCore/login.html) method to log in with a test account.
```dart
import 'package:tim_ui_kit/tim_ui_kit.dart';

final CoreServicesImpl _coreInstance = TIMUIKitCore.getInstance();
_coreInstance.login(userID: userID, userSig: userSig);
```

>? This account is for development and testing only. Before the application is launched, the correct `UserSig` distribution method is to use the server to generate `UserSig` and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).

### Step 3. Implementation - Conversion list page

You can use the conversation list as the IM homepage, which contains all the one-to-one and group conversations.

<img style="width:300px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/279da6d5d41ec1ce0b0cf7fca9a697b8.jpg" />

Create a `Conversation` class and use the [`TIMUIKitConversation`](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitConversation/) component in `body` to render the conversation list.

You only need to pass in an `onTapItem` event processing function to redirect users to the specific chat page. The `Chat` class is as detailed in the next step.

```dart
import 'package:flutter/material.dart';
import 'package:tim_ui_kit/tim_ui_kit.dart';

class Conversation extends StatelessWidget {
const Conversation({Key? key}) : super(key: key);
@override
Widget build(BuildContext context) {
return Scaffold(
  appBar: AppBar(
    title: const Text(
      "Message",
      style: TextStyle(color: Colors.black),
    ),
  ),
  body: TIMUIKitConversation(
    onTapItem: (selectedConv) {
      Navigator.push(
          context,
          MaterialPageRoute(
            builder: (context) => Chat(
              selectedConversation: selectedConv,
            ),
          ));
    },
  ),
);
}
}
```

### Step 4. Implementation - Chat page

This page consists of the message history and message sending modules.
<img style="width:300px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/0c361254fa5117f7580f39e8b523e472.png" />

Create a `Chat` class and use the [`TIMUIKitChat`](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitChat/) component in `body` to render the chat page.

You'd better pass in an `onTapAvatar` event processing function to redirect users to the contact details page. The `UserProfile` class is as detailed in the next step.

```dart
import 'package:flutter/material.dart';
import 'package:tim_ui_kit/tim_ui_kit.dart';

class Chat extends StatelessWidget {
final V2TimConversation selectedConversation;
const Chat({Key? key, required this.selectedConversation}) : super(key: key);
String? _getConvID() {
return selectedConversation.type == 1
    ? selectedConversation.userID
    : selectedConversation.groupID;
}
@override
Widget build(BuildContext context) {
return TIMUIKitChat(
  conversationID: _getConvID() ?? '', // groupID or UserID
  conversationType: selectedConversation.type ?? 1, // Conversation type
  conversationShowName: selectedConversation.showName ?? "", // Conversation display name
  onTapAvatar: (_) {
        Navigator.push(
            context,
            MaterialPageRoute(
             builder: (context) => UserProfile(userID: userID),
        ));
  }, // Callback for the clicking of the message sender profile photo. This callback can be used with `TIMUIKitProfile`.
);
}
```

### Step 5. Implementation - User details page

By default, this page determines whether a user is a friend and generates the user details page after only one `userID` is passed in.

Create a `UserProfile` class and use the [`TIMUIKitProfile`](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitProfile/) component in `body` to render the user details and relationship chain page.

>? If you want to customize this page, first consider using [`profileWidgetBuilder`](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitProfile/ProfileWidgetBuilder.html) to pass in the profile component to be customized and use `profileWidgetsOrder` to determine the vertical display order. If the requirements cannot be met, use `builder` instead.

<img style="width:300px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/5f2e67ffb31adc738165e2c4ce58218c.jpg" />

```dart
import 'package:flutter/material.dart';
import 'package:tim_ui_kit/tim_ui_kit.dart';

class UserProfile extends StatelessWidget {
    final String userID;
    const UserProfile({required this.userID, Key? key}) : super(key: key);

    @override
    Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
       title: const Text(
         "Message",
         style: TextStyle(color: Colors.black),
       ),
     ),
     body: TIMUIKitProfile(
          userID: widget.userID,
     ),
    );
  }
}
```

At this point, your app supports messaging, friend relationship management, user details display, and conversation list display.

### More capabilities

You can also use the following TUIKit plugins to quickly implement complete IM features.

[TIMUIKitContact](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitContact/): contact list page

[TIMUIKitGroupProfile](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitGroupProfile/): group profile page, whose usage mode is basically the same as that of `TIMUIKitProfile`

[TIMUIKitGroup](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitGroup/): group list page

[TIMUIKitBlackList](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitBlackList/): blocklist page

[TIMUIKitNewContact](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitNewContact/): Friend request list. If you want to display a badge, you can use the `TIMUIKitUnreadCount` badge component, which can mount listeners automatically.

[Local search](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitSearch/): `TIMUIKitSearch` is a global search component, which supports the global search of contacts, groups, and chat records. You can also use `TIMUIKitSearchMsgDetail` to search for chat records in a specific conversation. You can choose whether to pass in `conversation` to choose between the two search modes.

For the full view of the UI components, see the [overview document](https://intl.cloud.tencent.com/document/product/1047/46297) or [detailed document](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/).

## Support for the Flutter for Web[](id:web)

TUIKit (tim_ui_kit) 0.1.4 or later version provides full compatibility with web.

To enable support for web, you need to perform the following extra steps, compared with the steps to enable support for Android and iOS:

### Importing JS

>?
>
> If your existing Flutter project does not support web, run `flutter create .` in the root directory of the project to add web support.

Download the following two JS files from GitHub and place them in the `web` directory under the project:

- [tim-js-friendship.js](https://github.com/TencentCloud/TIMSDK/blob/master/Web/IMSDK/tim-js-friendship.js)
- [Rename this file to tim-upload-plugin.js](https://github.com/TencentCloud/TIMSDK/blob/master/Web/IMSDK/tim-upload-plugin/index.js)

Open `web/index.html` and import the two JS files in `<head> </head>`. See below:

```html
<script src='./tim-upload-plugin.js'></script>
<script src="./tim-js-friendship.js"></script>
```
![](https://qcloudimg.tencent-cloud.cn/raw/f88ddfbdc79fb7492f3ce00c2c583246.png)

## FAQs

### What platforms are supported?
- [The IM SDK (tencent_im_sdk_plugin)](https://intl.cloud.tencent.com/document/product/1047/46264) supports iOS, Android, and web. (Web is supported starting from tencent_im_sdk_plugin 4.1.1+2.)
- [TUIKit](https://intl.cloud.tencent.com/document/product/1047/46576) and the [matching interactive TUIKit demo](https://github.com/TencentCloud/TIMSDK/tree/master/Flutter/Demo/im-flutter-uikit) support iOS, Android, and web. (Web is supported starting from tim_ui_kit 0.1.4.)
In addition, the editions for Windows and macOS are under development. Please stay tuned.

### What should I do if clicking **Build And Run** for an Android device triggers an error, stating no available device is found?

Check that the device is not occupied by other resources. Alternatively, click **Build** to generate an APK package, drag it to the simulator, and run it.

### What should I do if an error occurs during the first run for an iOS device?

If an error occurs after the configuration, click **Product** > **Clean Build Folder**, clear the product, and run `pod install` or `flutter run` again.

![](https://qcloudimg.tencent-cloud.cn/raw/d495b2e8be86dac4b430e8f46a15cef4.png)

### What should I do if an error occurs during debugging on a real iOS device when I am wearing an Apple Watch?

![](https://qcloudimg.tencent-cloud.cn/raw/1ffcfe39a18329c86849d7d3b34b9a0e.png)

Turn on Airplane Mode on your Apple Watch and go to **Settings > Bluetooth** on your iPhone to turn off Bluetooth.

Restart Xcode (if opened) and run `flutter run` again.

### Flutter environment

If you want to check the Flutter environment, run `Flutter doctor` to detect whether the Flutter environment is ready.

### What should I do if an error occurs on an Android device after TUIKit is imported into the app automatically generated by Flutter?

![](https://qcloudimg.tencent-cloud.cn/raw/d95efdd4ae50f13f38f4c383ca755ae7.png)

1. Open `android\app\src\main\AndroidManifest.xml` and complete `xmlns:tools="http://schemas.android.com/tools"` / `android:label="@string/android_label"` / `tools:replace="android:label"` as follows:
```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="your Android package name"
    xmlns:tools="http://schemas.android.com/tools">
    <application
        android:label="@string/android_label"
        tools:replace="android:label"
        android:icon="@mipmap/ic_launcher" // Specify an icon path
        android:usesCleartextTraffic="true"
        android:requestLegacyExternalStorage="true">
```

2. Open `android\app\build.gradle` and complete `minSdkVersion` and `targetSdkVersion` in `defaultConfig`.
```gradle
defaultConfig {
  applicationId "" // Replace it with your Android package name
  minSdkVersion 21
  targetSdkVersion 30
}
```

### How do I set up a live room?

See [Live Room Setup Guide](https://intl.cloud.tencent.com/document/product/1047/49589#.E7.BE.A4.E7.B1.BB.E5.9E.8B.E9.80.89.E6.8B.A9) to set up a complete live room system based on Tencent Cloud IM/TRTC/CSS.

### How do I query error codes?

- For IM SDK API error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
- TUIKit scenario codes are used for pop-up prompts and can be obtained through [onTUIKitCallbackListener](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitCore/init.html). For details, see [here](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitCore/TIMCallback.html#inforecommendtext).


