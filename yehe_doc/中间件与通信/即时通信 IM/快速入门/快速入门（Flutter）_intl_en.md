[](id:toc)
This document describes how to integrate the SDK for Flutter.

## Environment Requirements

|   | Version |
|---------|---------|
| Flutter | Flutter 2.2.0 or later for the IM SDK; Flutter 2.10.0 or later for the TUIKit integration component library. |
| Android | Android Studio 3.5 or later; devices with Android 4.1 or later for apps |
| iOS | Xcode 11.0 or later. Ensure that your project has a valid developer signature. |

## Preparation

1. You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).
2. You have created an application as instructed in [Creating and Upgrading an Application](https://intl.cloud.tencent.com/document/product/1047/34577) and recorded the `SDKAppID`.

[](id:part1)

## Part 1. Creating a Test Account

In the [IM console](https://console.cloud.tencent.com/im), select your application and click **Auxiliary Tools** > **UserSig Generation & Verification** on the left sidebar. Create two `UserID` and their corresponding `UserSig`, and copy the `UserID`, `Key`, and `UserSig` for subsequent logins.

>? The account is for development and testing only. Before the application release, the correct `UserSig` distribution method is to generate `UserSig` on the server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).

![](https://main.qcloudimg.com/raw/2286644d987d24caf565142ae30c4392.png)

[](id:part2)

## Part 2. Selecting a Proper Scheme to Integrate the SDK for Flutter


IM offers three integration schemes:

|   | Use Case |
|---------|---------|
| [Using the demo](#part3) | IM demo is a complete chat application with open-source code. If you need to implement chat scenarios, you can use the demo for secondary development. Try it out [here](https://intl.cloud.tencent.com/document/product/1047/34279). |
| [Using UI library](#part4) | The IM UI component library `TUIKit` provides common UI components, such as conversation list, chat page, and contact list. You can use the component library to quickly build a custom IM application as needed. **This scheme is recommended**. |
| [Self-implementing](#part5) | Use this scheme if `TUIKit` cannot meet your UI requirements or you need heavy customization. |


To better understand IM SDK APIs, see API examples [here](https://github.com/TencentCloud/TIMSDK/tree/master/Flutter/IMSDK/im-flutter-plugin/tencent_im_sdk_plugin/example), which shows how to call APIs and trigger listeners.


[](id:part3)

## Part 3. Using the Demo

### Running the demo

1. Download the source code and install dependencies:
```shell
# Clone the code
git clone https://github.com/TencentCloud/TIMSDK.git

# Enter the demo directory of Flutter
cd TIMSDK/Flutter/Demo/im-flutter-uikit

# Install dependencies
flutter pub get
```

2. Run the demo:
```shell
# Start the demo. Replace `SDK_APPID` and `KEY`
flutter run --dart-define=SDK_APPID={YOUR_SDKAPPID} --dart-define=ISPRODUCT_ENV=false --dart-define=KEY={YOUR_KEY}
```

>?
>
>- `--dart-define=SDK_APPID={YOUR_SDKAPPID}`. Here, `{YOUR_SDKAPPID}` needs to be replaced with the `SDKAppID` of your application.
>- `--dart-define=ISPRODUCT_ENV=false`. Set it to `false` for a development environment.
>- `--dart-define=KEY={YOUR_KEY}`. Here, `{YOUR_KEY}` needs to be replaced with the `Key` recorded in [Part 1. Creating a Test User](#part1).
>

#### (Optional) Using the IDE

<dx-tabs>
::: Android[](id:android)
1. Go to the discuss/android directory via Android Studio.
![](https://qcloudimg.tencent-cloud.cn/raw/6516f9b17c58915c4ebc93c5c8829831.png)
2. Start an Android simulator, tap **Build And Run** to run the demo. Enter a random UserID (a combination of digits and letters).
>? The UI of the latest version of the demo may look different after adjustments.
:::
::: iOS[](id:ios)
1. Open Xcode and the file discuss/ios/Runner.xcodeproj:
![](https://qcloudimg.tencent-cloud.cn/raw/6d74814ba9bce54c7439e8b3cea53e73.png)
2. Connect an iPhone, and click **Build And Run**. After the iOS project is built, the Xcode project will be displayed in a new pop-up window.
3. Open the iOS project, and set **Signing & Capabilities** (an iPhone developer account required) for the primary target to run the project on the iPhone.
4. Start the project and debug the demo on the iPhone device.
![](https://qcloudimg.tencent-cloud.cn/raw/3fe6bbac88bb21ad7a7822bb297793b3.png)
:::
</dx-tabs>

#### Demo code structure

>? The TUIKit for Flutter is used for the UI and business logic of the demo. The demo layer itself is only used to build the application, process navigation redirects, and call instantiated TUIKit components.


|  Folder  | Description |
|---------|---------|
| lib | Core application directory |
| lib/i18n | Internationalization code, excluding the internationalization capabilities and strings of TUIKit, which can be imported as needed. |
| lib/src | Main application directory |
| lib/src/pages | Important navigation pages of the demo. After the application is initialized, `app.dart` displays the loading animation, judges the login status, and redirects the user to `login.dart` or `home_page.dart`. After the user logs in, the login information will be stored locally through the `shared_preference` plugin and used for automatic login upon future application launch. If there is no such information or the login fails, the user will be redirected to the login page. During automatic login, the user is still on `app.dart` and can see the loading animation. `home_page.dart` has a bottom tab to switch between the four main feature pages of the demo. |
| lib/utils | Some tool function classes. |


Basically, a TUIKit component is imported into each `dart` file in `lib/src`. After the component is instantiated in the file, the page can be rendered.

Below are main files:


|  Main File in `lib/src`  | Description |
|---------|---------|
| add_friend.dart | Friend request page that uses the `TIMUIKitAddFriend` component. |
| add_group.dart | Group joining request page that uses the `TIMUIKitAddGroup` component.|
| blacklist.dart| Blocklist page that uses the `TIMUIKitBlackList` component. |
| chat.dart | Main chat page that uses all the chat capabilities of TUIKit and the `TIMUIKitChat` component. |
| chatv2.dart | Main chat page that uses atomic capabilities and the `TIMUIKitChat` component. |
| contact.dart | Contacts page that uses the `TIMUIKitContact` component. |
| conversation.dart | Conversation list page that uses the `TIMUIKitConversation` component. |
| create_group.dart | Group chat page that is implemented in the demo with no component used. |
| group_application_list.dart | Group application list page that uses the `TIMUIKitGroupApplicationList` component. |
| group_list.dart | Group list page that uses the `TIMUIKitGroup` component.  |
| group_profile.dart | Group profile and management page that uses the `TIMUIKitGroupProfile` component. |
| newContact.dart | New contact request page that uses the `TIMUIKitNewContact` component. |
| routes.dart | Demo route that navigates users to the login page `login.dart` or homepage `home_page.dart`. |
| search.dart | Global search and in-conversation search page that uses the `TIMUIKitSearch` (global search) and `TIMUIKitSearchMsgDetail` (in-conversation search) components. |
| user_profile.dart | User information and relationship chain maintenance page that uses the `TIMUIKitProfile` component. |

The navigation redirect method needs to be imported into most TUIKit components; therefore, the demo layer needs to process `Navigator`.

You can modify the above demo for secondary development or implement your business needs based on it.

[](id:part4)

## Part 4. Using TUIKit Component Library to Implant IM Capabilities in Half a Day

TUIKit is a UI component library of Tencent Cloud IM SDK. It provides common UI components, such as conversation list, chat page, and contact list. You can use the component library to quickly build a custom IM application as needed. For more information, see [Quick Integration Solution](https://intl.cloud.tencent.com/document/product/1047/46576).

### Prerequisites

You have created a Flutter application or have an application that can be based on Flutter.

### Directions

#### Installing the IM TUIKit

TUIKit already contains the IM SDK, so you only need to install `tim_ui_kit`.

```shell
# Run the following command:
flutter pub add tim_ui_kit
```

#### Initialization

1. Initialize the TUIKit when starting the application.
2. Run `TIMUIKitCore.getInstance()` and then call the `init()` function. Also, pass in your `sdkAppID`.
```dart
/// main.dart
import 'package:tim_ui_kit/tim_ui_kit.dart';

final CoreServicesImpl _coreInstance = TIMUIKitCore.getInstance();
  @override
 void initState() {
   _coreInstance.init(
     sdkAppID: 0, // Replace `0` with the `SDKAppID` of your IM application during integration
     loglevel: LogLevelEnum.V2TIM_LOG_DEBUG,
     listener: V2TimSDKListener());    
   super.initState();
 }
}
```

#### Logging in with the test account
1. Complete login verification using the test account created at the beginning.
2. Call the `_coreInstance.login` method to log in with the test account.
```dart
import 'package:tim_ui_kit/tim_ui_kit.dart';

final CoreServicesImpl _coreInstance = TIMUIKitCore.getInstance();
_coreInstance.login(userID: userID, userSig: userSig);
```

>? The account is for development and testing only. Before the application release, the correct `UserSig` distribution method is to generate `UserSig` on the server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).

#### Implementation: conversation list page

You can use the conversation list page as the IM homepage, which displays all the one-to-one and group chats.

<img style="width:300px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/279da6d5d41ec1ce0b0cf7fca9a697b8.jpg" />

Create a `Conversation` class and use the `TIMUIKitConversation` component in the `body` to render the conversation list.

You only need to pass in a processing function of the `onTapItem` event to redirect users to the specific chat page. The `Chat` class is as detailed in the next step.

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

#### Chat page

This page consists of the message history and message sending modules.
<img style="width:300px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/0c361254fa5117f7580f39e8b523e472.png" />

Create a `Chat` class and use the `TIMUIKitChat` component in the `body` to render the chat page.

You'd better pass in a processing function of the `onTapAvatar` event to redirect users to the contact details page. The `UserProfile` class is as detailed in the next step.

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

#### User details page

By default, this page determines whether a user is a friend and generates the user details page after only a `userID` is passed in.

Create a `UserProfile` class and use the `TIMUIKitProfile` component in the `body` to render the user details and relationship chain page.

>? To customize this page, preferably use `profileWidgetBuilder` to pass in the profile component that needs to be customized and use `profileWidgetsOrder` to determine the vertical display order; if requirements cannot be met, use `builder` instead.

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

At this point, your application supports messaging, friend relationship management, user details display, and conversation list display.

#### More capabilities

You can use the following TUIKit plugins to quickly implement complete IM features.

[TIMUIKitContact](https://intl.cloud.tencent.com/document/product/1047/46297#timuikitcontact): Contact list page.

[TIMUIKitGroupProfile](https://intl.cloud.tencent.com/document/product/1047/46297#timuikitgroupprofile): Group profile page, which can be basically used in the same way as `TIMUIKitProfile`.

[TIMUIKitGroup](https://intl.cloud.tencent.com/document/product/1047/46297#timuikitgroup): Group list page.

[TIMUIKitBlackList](https://intl.cloud.tencent.com/document/product/1047/46297#timuikitblacklist): Blocklist page.

[TIMUIKitNewContact](https://intl.cloud.tencent.com/document/product/1047/46297#timuikitnewcontact): New contact (friend) request list. If you need to display a red dot, use the `TIMUIKitUnreadCount` red dot component, which can mount listeners automatically.

[TIMUIKitSearch](https://pub.dev/documentation/tim_ui_kit/latest/ui_views_TIMUIKitSearch_tim_uikit_search/TIMUIKitSearch-class.html): Search component. It supports the global search of contacts/groups/chat history and in-conversation search of chat history. The two modes are distinguished by `conversation`.

For more information on UI plugins, see [UI Components](https://intl.cloud.tencent.com/document/product/1047/46297) or [Readme](https://pub.dev/packages/tim_ui_kit).

[](id:part5)

## Part 5. Self-Implementing Integration

### Prerequisites

You have created a Flutter application or have an application that can be based on Flutter.

### Directions

#### Installing the IM SDK

For detailed directions involved in this section, see [SDK Integration (Flutter)](https://intl.cloud.tencent.com/document/product/1047/46264).

Run the following command to install the latest IM SDK for Flutter.

Run the following command:

```shell
flutter pub add tencent_im_sdk_plugin
```

#### Initializing the SDK

For detailed directions involved in this section, see [here](https://intl.cloud.tencent.com/document/product/1047/47966).

Call `initSDK` to initialize the SDK.

Pass in your `sdkAppID`.

```Dart
import 'package:tencent_im_sdk_plugin/enum/V2TimSDKListener.dart';
import 'package:tencent_im_sdk_plugin/enum/log_level_enum.dart';
import 'package:tencent_im_sdk_plugin/tencent_im_sdk_plugin.dart';
    TencentImSDKPlugin.v2TIMManager.initSDK(
    sdkAppID: 0, // Replace `0` with the `SDKAppID` of your IM application during integration
    loglevel: LogLevelEnum.V2TIM_LOG_DEBUG, // Log
    listener: V2TimSDKListener(),
  );
```

In this step, you can mount some listeners to the IM SDK, mainly including those for network status and user information change. For more information, see [V2TimSDKListener class](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/enum_V2TimSDKListener/V2TimSDKListener-class.html).

#### Logging in with the test account

For detailed directions involved in this section, see [Flutter](https://cloud.tencent.com/document/product/269/75296).

Complete login verification using the test account created at the beginning.

Call the `TencentImSDKPlugin.v2TIMManager.login` method to log in with the test account.

If the returned `res.code` is `0`, the login is successful.

```dart
import 'package:tencent_im_sdk_plugin/tencent_im_sdk_plugin.dart';
 V2TimCallback res = await TencentImSDKPlugin.v2TIMManager.login (
    userID: userID,
    userSig: userSig, 
  );
```

>? The account is for development and testing only. Before the application release, the correct `UserSig` distribution method is to integrate the `UserSig` calculation code into the server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).

#### Sending a message

For detailed directions involved in this section, see [here](https://intl.cloud.tencent.com/document/product/1047/47992).

The following shows how to send a text message:

1. Call `createTextMessage(String)` to create a text message.
2. Get the message ID from the returned value.
3. Call `sendMessage()` to send the message with the ID. `receiver` can be the ID of the other test account created earlier. `groupID` doesn't need to be entered for sending one-to-one messages.

Sample code:

```dart
import 'package:tencent_im_sdk_plugin/tencent_im_sdk_plugin.dart';

V2TimValueCallback<V2TimMsgCreateInfoResult> createMessage =
      await TencentImSDKPlugin.v2TIMManager
          .getMessageManager()
          .createTextMessage(text: "The text to create");
          
String id = createMessage.data!.id!; // The message creation ID 

V2TimValueCallback<V2TimMessage> res = await TencentImSDKPlugin.v2TIMManager
      .getMessageManager()
      .sendMessage(
          id: id, // Pass in the message creation ID to
          receiver: "The userID of the destination user",
          groupID: "The groupID of the destination group",
          );
```

>?If sending fails, it may be that your `sdkAppID` doesn't support sending messages to strangers. In this case, enable the feature in the console for test.
>
> Disable the friend relationship chain check [here](https://console.cloud.tencent.com/im/login-message) .

#### Getting the conversation list

For detailed directions involved in this section, see [here](https://intl.cloud.tencent.com/document/product/1047/48321).

After sending the test message in the previous step, log in with the other test account to pull the conversation list.
<img style="width:300px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/e2fdd7632ebc0c5cde68c91afa914201.jpg" />


There are two methods to pull the conversation list:

1. Listen on the persistent connection callback to update the conversation list in real time.
2. Send a request through an API to get the paginated conversation list at one time.

Common use cases:

Get the conversation list upon application launch and listen on the persistent connection to update the conversation list in real time.

##### Requesting the conversation list at one time

To get the conversation list, you need to maintain `nextSeq` and record its current position.

```dart
import 'package:tencent_im_sdk_plugin/tencent_im_sdk_plugin.dart';

String nextSeq = "0";

getConversationList() async {
  V2TimValueCallback<V2TimConversationResult> res = await TencentImSDKPlugin
      .v2TIMManager
      .getConversationManager()
      .getConversationList(nextSeq: nextSeq, count: 10);
  
  nextSeq = res.data?.nextSeq ?? "0";
}
```

At this point, you can see the message sent by the other test account in the previous step.

##### Listening on the persistent connection to get the real-time conversation list

Mount listeners to the SDK, process the callback event, and update the UI.

1. Mount listeners.
```dart
await TencentImSDKPlugin.v2TIMManager
      .getConversationManager()
      .setConversationListener(
        listener: new V2TimConversationListener(
          onConversationChanged: (List<V2TimConversation> list){
            _onConversationListChanged(list);
    },
          onNewConversation:(List<V2TimConversation> list){
            _onConversationListChanged(list);
    },
```

2. Process the callback event to display the latest conversation list on the UI.
```dart
import 'package:tencent_im_sdk_plugin/tencent_im_sdk_plugin.dart';

List<V2TimConversation> _conversationList = [];

_onConversationListChanged(List<V2TimConversation> list) {
  for (int element = 0; element < list.length; element++) {
    int index = _conversationList.indexWhere(
        (item) => item!.conversationID == list[element].conversationID);
    if (index > -1) {
      _conversationList.setAll(index, [list[element]]);
    } else {
      _conversationList.add(list[element]);
    }
  }
```

#### Receiving a message

For detailed directions involved in this section, see [here](https://intl.cloud.tencent.com/document/product/1047/47997).

There are two methods to receive messages in the IM SDK for Flutter:

1. Listen on the persistent connection callback to get message changes and update and render the historical message list in real time.
2. Send a request through an API to get paginated message history at one time.

Common use cases:

1. When entering a new conversation, request a certain number of historical messages at one time to display the historical message list.
2. Listen on the persistent connection to receive messages in real time and add them to the historical message list.

##### Requesting the historical message list at one time

We recommend you limit the number of messages pulled per page to 20 to avoid affecting the speed.

Dynamically record the current number of pages for the next request.

The sample code is as follows:

```dart
import 'package:tencent_im_sdk_plugin/tencent_im_sdk_plugin.dart';

  V2TimValueCallback<List<V2TimMessage>> res = await TencentImSDKPlugin
      .v2TIMManager
      .getMessageManager()
      .getGroupHistoryMessageList(
        groupID: "groupID",
        count: 20,
        lastMsgID: "",
      );
      
  List<V2TimMessage> msgList = res.data ?? [];
  
  // here you can use msgList to render your message list
    }
```

##### Listening on the persistent connection to get new messages in real time

After the historical message list is initialized, new messages are from the persistent connection `V2TimAdvancedMsgListener.onRecvNewMessage`.

After the `onRecvNewMessage` callback is triggered, add new messages to the historical message list as needed.

Below is the sample code for binding a listener:

```dart
import 'package:tencent_im_sdk_plugin/tencent_im_sdk_plugin.dart';

final adVancesMsgListener = V2TimAdvancedMsgListener(
onRecvNewMessage: (V2TimMessage newMsg) {
  _onReceiveNewMsg(newMsg);
},
/// ... other listeners related to message
);

TencentImSDKPlugin.v2TIMManager
    .getMessageManager()
    .addAdvancedMsgListener(listener: adVancesMsgListener);
```

At this point, you have completed the IM module development. You can send and receive messages and enter different conversations.

You can develop more features, such as [group](https://intl.cloud.tencent.com/document/product/1047/48169), [user profile](https://intl.cloud.tencent.com/document/product/1047/48160), [relationship chain](https://intl.cloud.tencent.com/document/product/1047/48157), [offline push](https://intl.cloud.tencent.com/document/product/1047/46306), and [local search](https://intl.cloud.tencent.com/document/product/1047/48135).



## FAQs

### What platforms are supported?
- Currently, [IM SDK (tencent_im_sdk_plugin)](https://intl.cloud.tencent.com/document/product/1047/46264) supports iOS, Android, and web. Windows and macOS will be supported in the future.
- [TUIKit](https://intl.cloud.tencent.com/document/product/1047/46576) and [the supportive interaction demo](https://github.com/TencentCloud/TIMSDK/tree/master/Flutter/Demo/im-flutter-uikit) support iOS and Android.

### What should I do if clicking **Build And Run** for an Android device triggers an error, stating no available device is found?

Check that the device is not occupied by other resources. Alternatively, click **Build** to generate an APK package, drag it to the simulator, and run it.

### What should I do if an error occurs during the first run for an iOS device?

If an error occurs after the configuration, click **Product** > **Clean Build Folder**, clean the product, and run `pod install` or `flutter run` again.

![20220714152720](https://tuikit-1251787278.cos.ap-guangzhou.myqcloud.com/20220714152720.png)

### What should I do if an error occurs during debugging on a real iOS device when I am wearing an Apple Watch?

![20220714152340](https://tuikit-1251787278.cos.ap-guangzhou.myqcloud.com/20220714152340.png)

Turn on Airplane Mode on your Apple Watch, and go to **Settings > Bluetooth** on your iPhone to turn off Bluetooth.

Restart Xcode (if opened) and run `flutter run` again.

### Flutter environment

If you want to check the Flutter environment, run `Flutter doctor` to detect whether the Flutter environment is ready.

### What should I do when an error occurs on an Android device after TUIKit is imported into the application automatically generated by Flutter?

![](https://qcloudimg.tencent-cloud.cn/raw/d95efdd4ae50f13f38f4c383ca755ae7.png)

1. Open `android\app\src\main\AndroidManifest.xml` and complete `xmlns:tools="http://schemas.android.com/tools"` / `android:label="@string/android_label"` / `tools:replace="android:label"` as follows.
```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="Replace it with your Android package name"
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

## Contact Us
If you have any questions when using the service, join our QQ group (788910197) for consultation.
