## TUIKit Overview

TUIKit for Flutter is a set of UI components based on Chat SDKs for Flutter. It provides features such as the conversation, chat, relationship chain, group, and local search features.

By leveraging these UI components and built-in Chat business logic, you can quickly import chat, user relationship chain management, and other modules into your app.

**Before integrating TUIKit, you can quickly try out its features online through the [demos](https://intl.cloud.tencent.com/document/product/1047/50059).**

>? The TUIKit `tencent_cloud_chat_uikit` package is open source. You can integrate the [online version](https://pub.dev/packages/tencent_cloud_chat_uikit) or fork it on [GitHub](https://github.com/TencentCloud/chat-uikit-flutter) before local integration.

Currently, TUIKit for Flutter contains the following primary components:

- [TIMUIKitCore](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitCore/readme.html): The core.
- [TIMUIKitConversation](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitConversation/TIMUIKitConversation-Implementation.html): The conversations.
- [TIMUIKitChat](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitChat/TIMUIKitChat-Implementation.html): The chat panel for message sending and historical message display.
- [TIMUIKitContact](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitContact/TIMUIKitContact-Implementation.html): The contacts.
- [TIMUIKitProfile](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitProfile/TIMUIKitProfile-Implementation.html): The component for viewing user profile and managing the relationship chain.
- [TIMUIKitGroupProfile](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitGroupProfile/TIMUIKitGroupProfile-Implementation.html): The component for group profile display and management.
- [TIMUIKitGroup](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitGroup/TIMUIKitGroup-Implementation.html): My group chats.
- [TIMUIKitBlackList](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitBlackList/TIMUIKitBlackList-Implementation.html): The blocklist.
- [TIMUIKitNewContact](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitNewContact/TIMUIKitNewContact-Implementation.html): New friend requests.
- [TIMUIKitSearch](https://intl.cloud.tencent.com/document/product/1047/50036): The local search component, which supports global search and in-conversation search.

![](https://qcloudimg.tencent-cloud.cn/raw/f140dd76be01a65abfb7e6ba2bf50ed5.png)

>?The TUIKit interfaces listed in the above figure support automatic or manual language switching among **Simplified Chinese, Traditional Chinese, English, Japanese, and Korean**. For more information about how to set the display language of the UI and add other languages, [click here](https://www.tencentcloud.com/document/product/1047/52154).

## Environment Requirements

|     Environment    | Version                                                               |
| ------- | ------------------------------------------------------------------ |
| Flutter | Flutter 2.10.0 or later.                                     |
| Android | Android Studio 3.5 or later; and devices with Android 4.1 or later for apps |
| iOS | Xcode 11.0 or later. Ensure that your project has a valid developer signature. |

## Supported Platforms

| Platform  | Supported or Not |
|---------|---------|
| iOS  | Supported |
| Android  | Supported |
| [Web](#web)  | Supported from version 0.1.5 |
| macOS  | Will be supported soon |
| Windows  | Will be supported soon |
| [Hybrid development](https://www.tencentcloud.com/document/product/1047/51456) (adding the SDK for Flutter to your existing native app) | Supported from version 1.0.0 |

>? A set of all-platform Chat SDKs for Flutter and TUIKit are provided to help you build apps for different platforms by using one set of code.

## Prerequisites

1. You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).
2. You have created an application as instructed in [Creating and Upgrading an Application](https://intl.cloud.tencent.com/document/product/1047/34577) and recorded the `SDKAppID`.
3. In the [Chat console](https://console.cloud.tencent.com/im), select your application and choose **Auxiliary Tools** > **UserSig Tools** in the left sidebar to go the **UserSig Generation & Verification** page. Create two `UserID` values and their `UserSig` values, and copy the `UserID`, `Key`, and `UserSig` values for subsequent logins.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/wXAk840_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_7462189b-a67c-4c6c-9948-962c763dc057.png)

## Access directions

The following describes how to use Flutter TUIKit to quickly build a simple Chat app.

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

>?To use push capabilities, you need to add push permissions as instructed in [Vendor Message Push Plugin Integration Guide for Flutter](https://www.tencentcloud.com/document/product/1047/46306).

#### Installing the Chat TUIKit

TUIKit contains the Chat SDK, so you only need to install `tencent_cloud_chat_uikit`.

```shell
# Run the following command:
flutter pub add tencent_cloud_chat_uikit
```

If your project requires web support, import JS files by referring to [the web compatibility description section](#web) before performing subsequent steps.

### Step 2. Initialize the Chat service[](id:init)

1. Initialize the Chat service upon application start.
2. Run [`TIMUIKitCore.getInstance()`](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitCore/getInstance.html) first and then call the initialization function [`init()`](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitCore/init.html). Remember to pass in your `sdkAppID`.
3. To help you get API errors and user prompts, we recommend you mount an `onTUIKitCallbackListener` instance. For more information, see [here](#callback).

Below is the sample code (for all initialization parameters, see [init](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitCore/init.html)):

```dart
/// main.dart
import 'package:tencent_cloud_chat_uikit/tencent_cloud_chat_uikit.dart';

final CoreServicesImpl _coreInstance = TIMUIKitCore.getInstance();
  @override
 void initState() {
   _coreInstance.init(
     sdkAppID: 0, // Replace 0 with the SDKAppID of your Chat application when integrating
     // language: LanguageEnum.en, // Configure the UI language; otherwise, the system language will be used.
     loglevel: LogLevelEnum.V2TIM_LOG_DEBUG,
     onTUIKitCallbackListener:  (TIMCallback callbackValue){}, // We recommend you configure it. For more information, see [Flutter](https://intl.cloud.tencent.com/document/product/1047/50054).
     listener: V2TimSDKListener());
   super.initState();
 }
}
```

>! Do not perform subsequent steps before the initialization in this step is completed.

#### Logging in with a test account

1. Log in with a test account initially generated in the console for verification.
2. Call the [`_coreInstance.login`](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitCore/login.html) method to log in with a test account.

```dart
import 'package:tencent_cloud_chat_uikit/tencent_cloud_chat_uikit.dart';

final CoreServicesImpl _coreInstance = TIMUIKitCore.getInstance();
_coreInstance.login(userID: userID, userSig: userSig);
```

>? This account is for development and testing only. Before the application is launched, the correct `UserSig` distribution method is to use the server to generate `UserSig` and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).

### Step 3. Implement the chats page

You can use the conversation list as the Chat app homepage, which contains all the one-to-one and group conversations.

<img style="width:300px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/279da6d5d41ec1ce0b0cf7fca9a697b8.jpg" />

Create a `Conversation` class and use the [`TIMUIKitConversation`](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitConversation/TIMUIKitConversation-Implementation.html) component in `body` to render the conversation list.

You only need to pass in an `onTapItem` event processing function to redirect users to the specific chat page. The `Chat` class is as detailed in the next step.

```dart
import 'package:flutter/material.dart';
import 'package:tencent_cloud_chat_uikit/tencent_cloud_chat_uikit.dart';

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

### Step 4. Implement the chat page

This page consists of the message history and message sending modules.
<img style="width:300px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/0c361254fa5117f7580f39e8b523e472.png" />

Create a `Chat` class and use the [`TIMUIKitChat`](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitChat/TIMUIKitChat-Implementation.html) component in `body` to render the chat page.

You'd better pass in an `onTapAvatar` event processing function to redirect users to the contact details page. The `UserProfile` class is as detailed in the next step.

```dart
import 'package:flutter/material.dart';
import 'package:tencent_cloud_chat_uikit/tencent_cloud_chat_uikit.dart';

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

### Step 5. Implement the profile page

By default, this page determines whether a user is a friend and generates the user profile page after only one `userID` is passed in.

Create a `UserProfile` class and use the [`TIMUIKitProfile`](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitProfile/TIMUIKitProfile-Implementation.html) component in `body` to render the user details and relationship chain page.

>? If you want to customize this page, first consider using [`profileWidgetBuilder`](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitProfile/ProfileWidgetBuilder.html) to pass in the profile component to be customized and use `profileWidgetsOrder` to determine the vertical display order. If the requirements cannot be met, use `builder` instead.

<img style="width:300px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/5f2e67ffb31adc738165e2c4ce58218c.jpg" />

```dart
import 'package:flutter/material.dart';
import 'package:tencent_cloud_chat_uikit/tencent_cloud_chat_uikit.dart';

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

At this point, your app supports messaging, friend relationship management, user profile display, and conversation list display.

### Addition 1. More TUIKit capabilities

You can also use the following TUIKit components to quickly implement Chat features:

- [TIMUIKitContact](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitContact/TIMUIKitContact-Implementation.html): The Contacts page.
- [TIMUIKitGroupProfile](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitGroupProfile/TIMUIKitGroupProfile-Implementation.html): The group profile page, whose usage mode is basically the same as that of `TIMUIKitProfile`.
- [TIMUIKitGroup](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitGroup/TIMUIKitGroup-Implementation.html): The group list page.
- [TIMUIKitBlackList](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitBlackList/TIMUIKitBlackList-Implementation.html): The blocklist page.
- [TIMUIKitNewContact](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitNewContact/TIMUIKitNewContact-Implementation.html): The contact (friend) request list. If you want to display a badge, you can use the `TIMUIKitUnreadCount` badge component, which can mount listeners automatically.
- [Local search](https://intl.cloud.tencent.com/document/product/1047/50036): The global search component `TIMUIKitSearch` supports the global search of contacts/groups/chat history and in-conversation search of chat history through `TIMUIKitSearchMsgDetail`. The two modes are distinguished by `conversation`.

For the full view of the UI components, see [TUIKit Overview](https://intl.cloud.tencent.com/document/product/1047/50059) or [Module overview](https://comm.qq.com/im/doc/flutter/zh/TUIKit/readme.html).

[](id:controller)

### Addition 2. (Optional) Using a controller to control TUIKit

>? We recommend you use this feature in `tencent_cloud_chat_uikit` 0.1.5 or later.

After quick integration in the above steps, you can now build a set of available Chat modules. If you have any additional control requirements, you can use the corresponding controllers.

In scenarios such as the conversation list page, you can customize the swipe action menu with conversation items to provide features such as pinning a conversation to the top, deleting a conversation, and deleting historical messages, or sending messages to meet your additional message sending requirements, for example, sending a gift message on the gift UI developed by you.

Currently, the following controllers are provided:

| Component                                                                                                                               | Controller                                                                                                                                  | Feature Description                                                                                                                                         |
| ---------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| [TIMUIKitChat](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitChat/TIMUIKitChat-Implementation.html)                         | [TIMUIKitChatController](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitChat/TIMUIKitChatController.html)                         | Refreshes the historical message list/Updates a single message/Sends additional messages/Sets custom fields for messages, etc.                                                                     |
| [TIMUIKitConversation](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitConversation/TIMUIKitConversation-Implementation.html) | [TIMUIKitConversationController](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitConversation/TIMUIKitConversationController.html) | Gets and refreshes the conversation list/Pins a conversation to the top/Sets a conversation draft/Clears all messages in a conversation/Deletes a conversation/Navigates to a specific conversation, etc.                                                                    |
| [TIMUIKitProfile](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitProfile/TIMUIKitProfile-Implementation.html)                | [TIMUIKitProfileController](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitProfile/TIMUIKitProfileController.html)                | Deletes a contact/Pins the conversation with the current contact/Adds a user to the blocklist/Changes the way of being added as a friend/Updates the alias of a contact/Mutes notifications of messages of contacts/Adds a contact/Updates the user profile, etc.|

These controllers are used in the same way, and [TIMUIKitChatController](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitChat/TIMUIKitChatController.html) is taken as an example. For the complete code, see the [demo](https://github.com/TencentCloud/tc-chat-demo-flutter/blob/main/lib/src/chat.dart).

1. Instantiate a [TIMUIKitChatController](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitChat/TIMUIKitChatController.html) object in a class that uses [TIMUIKitChat](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitChat/TIMUIKitChat-Implementation.html).
<dx-codeblock>
:::  dart
final TIMUIKitChatController _chatController = TIMUIKitChatController();
:::
</dx-codeblock>
2. Pass the object in to the `controller` parameter of [TIMUIKitChat](https://comm.qq.com/im/doc/flutter/zh/TUIKit/TIMUIKitChat/TIMUIKitChat-Implementation.html).
<dx-codeblock>
:::  dart
@override
Widget build(BuildContext context) {
    return TIMUIKitChat(
    controller: _chatController,
    // ... Other parameters
 );
}
:::
</dx-codeblock>
3. In the class, you can use the controller to customize operations such as sending a geographical location message:
<dx-codeblock>
:::  dart
_sendLocationMessage(String desc, double longitude, double latitude) async {
    final locationMessageInfo = await sdkInstance.v2TIMMessageManager
        .createLocationMessage(
        desc: desc,
        longitude: longitude,
        latitude: latitude);
    final messageInfo = locationMessageInfo.data!.messageInfo;
    _chatController.sendMessage(
        receiverID: _getConvID(),
groupID:_getConvID(),
        convType: _getConvType(),
        messageInfo: messageInfo);
}
:::
</dx-codeblock>

### Addition 3. (Optional) Using more plugins to gain a rich TUIKit user experience

In addition to the basic features of TUIKit, four optional plugins are provided for you to implement more Chat capabilities.

- [Message push plugin](https://intl.cloud.tencent.com/document/product/1047/50032): It provides vendor offline push capabilities, online push capabilities, and the push of your other business messages to help you increase the message deliverability.
- [Custom emoji plugin](https://www.tencentcloud.com/document/product/1047/52227): Starting from version 0.1.5, TUIKit comes with no stickers, and you need to use this plugin to quickly integrate emoji and sticker capabilities. The plugin supports emoji Unicode encoding and custom image stickers. For the integration process, see the [demo](https://github.com/TencentCloud/tc-chat-demo-flutter/blob/main/lib/src/pages/app.dart).

>?More practical plugins are on the way. If you have any good ideas and suggestions, feel free to [contact us](https://cloud.tencent.com/online-service?from=doc_269&source=PRESALE).

## Support for Flutter for Web[](id:web)

TUIKit (tencent_cloud_chat_uikit) 0.1.5 and later are perfectly compatible with the web.

To enable support for web, you need to perform the following extra steps, compared with the steps to enable support for Android and iOS:

### Importing JS

>?If your existing Flutter project does not support web, run `flutter create .` in the root directory of the project to add web support.

Go to the `web/` directory of your project and run `npm` or `yarn` to install relevant JS dependencies. Initialize the project as instructed.

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

![](https://qcloudimg.tencent-cloud.cn/raw/a4d25e02c546e0878ba59fcda87f9c76.png)

## FAQs

### What should I do if an error is reported on Android indicating that `compileSdkVersion` is not compatible?

1. Make sure that the following two plugin versions are specified in the `pubspec.yaml` file of your project.

```yaml
  video_thumbnail: ^0.5.3
  permission_handler: ^10.0.0
  flutter_local_notifications: 9.7.0
```

2. Modify the `android/app/build.gradle` file to ensure `android => compileSdkVersion 33`.

```gradle
android {
  compileSdkVersion 33
  ...
}
```

3. Run the following command to reinstall the dependencies on Android.

```shell
flutter pub cache clean
flutter pub get
```

### What should I do if the Android build error "Codepoint 984472 not found in font, aborting." occurs on Flutter 2.x?

![](https://qcloudimg.tencent-cloud.cn/raw/017362112bb49e5ac2d94d76699b068a.png)

Add `--no-tree-shake-icons` to your compilation command, for example:

```shell
flutter build apk --no-tree-shake-icons --dart-define=SDK_APPID={your `SDKAPPID`}
```

### What should I do if Pods dependencies fail to be installed on iOS?

#### **Solution 1:** If an error occurs after the configuration, click **Product** > **Clean Build Folder**, clear the product, and run `pod install` or `flutter run` again.

![](https://qcloudimg.tencent-cloud.cn/raw/d495b2e8be86dac4b430e8f46a15cef4.png)

#### **Solution 2:** Manually delete the `ios/Pods` folder and the `ios/Podfile.lock` file and run the following command to reinstall the dependencies

1. For macOS devices with Apple silicon, such as M1:

```shell
cd ios
sudo arch -x86_64 gem install ffi
arch -x86_64 pod install --repo-update
```

2. For macOS devices with Intel chips:

```shell
cd ios
sudo gem install ffi
pod install --repo-update
```

### What do I do if an error occurs during debugging on an iOS device when I am wearing an Apple Watch?

![](https://qcloudimg.tencent-cloud.cn/raw/1ffcfe39a18329c86849d7d3b34b9a0e.png)

Turn on Airplane Mode on your Apple Watch and go to **Settings > Bluetooth** on your iPhone to turn off Bluetooth.

Restart Xcode (if opened) and run `flutter run` again.

### How do I check a Flutter environment issue?

If you want to check the Flutter environment, run `Flutter doctor` to detect whether the Flutter environment is ready.

### What do I do if an error occurs on an Android device after TUIKit is imported into an app that is automatically generated by Flutter?

![](https://qcloudimg.tencent-cloud.cn/raw/d95efdd4ae50f13f38f4c383ca755ae7.png)

1. Open `android\app\src\main\AndroidManifest.xml` and complete `xmlns:tools="http://schemas.android.com/tools"` / `android:label="@string/android_label"` / `tools:replace="android:label"` as follows:
<dx-codeblock>
:::  xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="your Android package name"
    xmlns:tools="http://schemas.android.com/tools">
    <application
        android:label="@string/android_label"
        tools:replace="android:label"
        android:icon="@mipmap/ic_launcher" // Specify an icon path
        android:usesCleartextTraffic="true"
        android:requestLegacyExternalStorage="true">
:::
</dx-codeblock>
2. Open `android\app\build.gradle` and complete `minSdkVersion` and `targetSdkVersion` in `defaultConfig`.
<dx-codeblock>
:::  gradle
defaultConfig {
    applicationId "" // Replace it with your Android package name
    minSdkVersion 21
    targetSdkVersion 30
}
:::
</dx-codeblock>

### How do I switch the interface language?

For information about how to switch the interface language and add other interface languages, [click here](https://www.tencentcloud.com/document/product/1047/52154).

### How do I get an API call error/Flutter layer error/pop-up prompt message?[](id:callback)

Mount the `onTUIKitCallbackListener` listener when initializing TUIKit.

The listener is used to return SDK API errors/Flutter errors/information about scenarios where a pop-up prompt may need to be displayed to the user.

Determine the type through `TIMCallbackType`.

Below is the sample code. You can modify the following code based on your business needs to customize the logic for prompting the user, including but not limited to the pop-up and banner.

```dart
final CoreServicesImpl _coreInstance = TIMUIKitCore.getInstance();

final isInitSuccess = await _coreInstance.init(
  onTUIKitCallbackListener: (TIMCallback callbackValue){
    switch(callbackValue.type) {
      case TIMCallbackType.INFO:
        // Shows the recommend text for info callback directly
        Utils.toast(callbackValue.infoRecommendText!);
        break;
      case TIMCallbackType.API_ERROR:
        //Prints the API error to console, and shows the error message.
        print("Error from TUIKit: ${callbackValue.errorMsg}, Code: ${callbackValue.errorCode}");
        if (callbackValue.errorCode == 10004 && callbackValue.errorMsg!.contains("not support @all")) {
            Utils.toast(imt("The current group does not support @all members"));
        }else{
          Utils.toast(callbackValue.errorMsg ?? callbackValue.errorCode.toString());
        }
        break;
      case TIMCallbackType.FLUTTER_ERROR:
      default:
        // prints the stack trace to console or shows the catch error
        if(callbackValue.catchError != null){
          Utils.toast(callbackValue.catchError.toString());
        }else{
          print(callbackValue.stackTrace);
        }
    }
  },
);
```

The following describes the three types of callbacks respectively.

#### SDK API error (`TIMCallbackType.API_ERROR`)

In this scenario, native SDK API `errorMsg` and `errorCode` are provided.

For information about the error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).

#### Flutter error (`TIMCallbackType.FLUTTER_ERROR`)

This error is returned from Flutter. It provides the `stackTrace` (from `FlutterError.onError`) or `catchError` (from `try-catch`) when the error occurred.

#### Scenario information (`TIMCallbackType.INFO`)

We recommend you display the information to the user in the form of a pop-up when appropriate.

You can decide the prompt rule and pop-up style.

The scenario code `infoCode` is provided to help you identify the current scenario and the default prompt `infoRecommendText`.

You can directly pop up the default prompt or customize a prompt based on `infoCode`. The prompt will be displayed in the system language or the specified language. Do not determine the scenario based on the prompt.

**`infoCode` complies with the following rules:**

`infoCode` consists of seven digits, the first five of which determine the component where the scenario occurred, and the last two of which determine the specific scenario.

| Start of `infoCode` | Component             |
| ---------- | ---------------------- |
| 66601      | `TIMUIKitAddFriend`    |
| 66602      | `TIMUIKitAddGroup`     |
| 66603      | `TIMUIKitBlackList`    |
| 66604      | `TIMUIKitChat`         |
| 66605      | `TIMUIKitContact`      |
| 66606      | `TIMUIKitConversation` |
| 66607      | `TIMUIKitGroup`        |
| 66608      | `TIMUIKitGroupProfile` |
| 66609      | `TIMUIKitNewContact`   |
| 66610      | `TIMUIKitGroupProfile` |
| 66611      | `TIMUIKitNewContact`   |
| 66612      | `TIMUIKitProfile`      |
| 66613      | `TIMUIKitSearch`       |
| 66614      | Common component               |

**The complete list of `infoCode` values is as follows:**[](id:infoCode)

| `infoCode` | `infoRecommendText`                               | Scenario Description                                                                    |
| ----------------- | ------------------------------------------------------------ | --------------------------------------------------------------------------- |
| 6660101           | A friend request is sent successfully.                                               | The user requests to add another user to the contacts.                                                |
| 6660102           | The user is already a friend.                                               | The `onTapAlreadyFriendsItem` callback is triggered when the user requests to add an existing friend. |
| 6660201           | A group join request is sent.                                                 | The user requests to join a group requiring admin approval.                                             |
| 6660202           | You are already a group member.                                                 | The `onTapExistGroup` callback is triggered when the user sends a group join request and is identified as an existing group member.       |
| 6660401           | The original message cannot be located.                                             | The target message cannot be found in the message list when the user needs to be redirected to the @message or quote the message.             |
| 6660402           | The video is saved successfully.                                                 | The user selects **Save** after opening a video message in the message list.                                 |
| 6660403           | The video failed to be saved.                                                 | The user selects **Save** after opening a video message in the message list. |
| 6660404           | The recording is too short.                                                 | The user sends a too short audio message.                                                    |
| 6660405           | The video failed to be sent. Videos cannot be greater than 100 MB in size.                                  | The user attempts to send a video greater than 100 MB in size.                                               |
| 6660406           | The image is saved successfully.                                                 | The user selects **Save** after opening the large image in the message list.                                 |
| 6660407           | The image failed to be saved.                                                 | The user selects **Save** after opening the large image in the message list.                                |
| 6660408           | Copied                                                       | The user selects **Copy** to copy the text message in the pop-up window.                                 |
| 6660409           | Unavailable                                                     | The user selects a non-standard feature in the pop-up window.                                                     |
| 6660410           | Other files are being received.                                           | The previous download tasks have not been completed when the user clicks to download a file message.                                |
| 6660411           | Receiving                                                   | The user clicks to download a file message.                                                        |
| 6660412           | Video messages must be in MP4 format.                                        | The user sends a video message in non-MP4 format.                                          |
| 6660413           | The file has been added to the queue waiting to be downloaded. Other files are being downloaded.                                                   | The file has been added to the queue waiting to be downloaded. Other files are being downloaded.                                         |
| 6661001           | Modification failed in the absence of a network connection.                                         | The user attempts to modify the group profile in an environment without a network connection.                                        |
| 6661002           | You cannot view the group members in the absence of a network connection.                                   | The user attempts to view the group members in an environment without a network connection.                                        |
| 6661003           | The admin status is removed successfully.                                           | The user removes the admin status of another user in the group.                                                |
| 6661201           | Modification failed in the absence of a network connection.                                         | The user attempts to modify their own profile or that of a contact in an environment without a network connection.                                        |
| 6661202           | The friend is added successfully.                                                 | The user adds another user as a friend on the profile page, who is automatically added successfully without approval.                        |
| 6661203           | A friend request is sent.                                               | The user adds another user who requires approval as a friend on the profile page.                                 |
| 6661204           | The user is on the blocklist.                                             | The user adds another user who is on the blocklist as a friend on the profile page.                             |
| 6661205           | The friend failed to be added.                                                 | The user failed to add a friend, possibly because the latter forbids being added.                |
| 6661206           | The friend is deleted successfully.                                                 | The user successfully deleted a friend on the profile page.                                            |
| 6661207           | The friend failed to be deleted.                                                  | The user failed to delete a friend on the profile page.                                            |
| 6661401           | The input cannot be empty.                                                 | The user enters an empty string.                                           |
| 6661402           | Pass in a lifecycle function for leaving a group to provide the navigation method to return to the homepage or another page. | A method to return to the homepage is provided when the user leaves or disbands the group.                                    |
| 6661403           | The device's available storage space is insufficient. We recommend you free up some space to gain a better user experience.               | After the user is logged in successfully, the system will automatically check the device's available storage space. If the available space is less than 1 GB, a prompt will be displayed indicating that the available space is insufficient.        |
