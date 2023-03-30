- [](id:toc)
  This document describes how to integrate the SDK for Flutter.

  ## Environment Requirements

  | Environment | Version                                                      |
  | ----------- | ------------------------------------------------------------ |
  | Flutter     | Flutter 2.2.0 or later for the Chat SDK; Flutter 2.10.0 or later for the TUIKit component library. |
  | Android     | Android Studio 3.5 or later; devices with Android 4.1 or later for apps |
  | iOS         | Xcode 11.0 or later. Ensure that your project has a valid developer signature. |

  ## Supported Platforms

  We are committed to building a set of Chat SDK and TUIKit for all Flutter platforms, allowing you to run one set of code on all platforms.

  | Platform                                                     | No-UI SDK ([tencent_cloud_chat_sdk](https://pub.dev/packages/tencent_cloud_chat_sdk)) | TUIKit with UI and Basic Business Logic ([tencent_cloud_chat_uikit](https://pub.dev/packages/tencent_cloud_chat_uikit)) |
  | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | iOS                                                          | Supported                                                    | Supported                                                    |
  | Android                                                      | Supported                                                    | Supported                                                    |
  | [Web](#web)                                                  | Supported from v4.1.1+2                                      | Supported from v0.1.5                                        |
  | [macOS](#pc)                                                 | Supported from v4.1.9                                        | Available soon                                               |
  | [Windows](#pc)                                               | Supported from v4.1.9                                        | Available soon                                               |
  | [Hybrid development](https://www.tencentcloud.com/document/product/1047/51456) (Adding Flutter SDK to Existing Native Applications) | Supported from v5.0.0                                        | Supported from v1.0.0                                        |

  >? For web, macOS, and Windows platforms, a few extra steps are needed for integration. For more information, see [Expanding to More Platforms](#more).

  ## Demos

  Before integration, you can try out our demos to quickly understand the capabilities of the Tencent Cloud Chat Flutter cross-platform SDK and TUIKit.

  **All of the following demos are packaged by the same Flutter project with TUIKit introduced.** The Chat SDK for Flutter already supports desktop platforms (macOS/Windows), and the corresponding demo will be available soon.

  <table style="text-align:center; vertical-align:middle; max-width: 800px">
    <tr>
      <th style="text-align:center;">Mobile App</th>
      <th style="text-align:center;">Web - HTML5</th>
    </tr>
    <tr>
      <td><div style="display: flex; justify-content: center; align-items: center; flex-direction: column; padding-top: 10px">iOS/Android app (automatically downloaded according to your platform)<img style="max-width:200px; margin: 20px 0 20px 0" src="https://qcloudimg.tencent-cloud.cn/raw/ca2aaff551410c74fce48008c771b9f6.png"/></div></td>
      <td><div style="display: flex; justify-content: center; align-items: center; flex-direction: column; padding-top: 10px">Use your phone to scan the QR code to try out<img style="max-width:200px; margin: 20px 0 20px 0" src="https://qcloudimg.tencent-cloud.cn/raw/3c79e8bb16dd0eeab35e894a690e0444.png"/></div></td>
    </tr>
  </table>

  ## Preparations

  1. You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).
  2. You have created an application as instructed in [Creating and Upgrading an Application](https://intl.cloud.tencent.com/document/product/1047/34577) and recorded the `SDKAppID`.
  3. In the [Chat console](https://console.cloud.tencent.com/im), select your application and click **Auxiliary Tools** > **UserSig Tools** on the left sidebar to open **UserSig Generation & Verification** page. Create two `UserID` values and their `UserSig` values, and copy the `UserID`, `Key`, and `UserSig` for subsequent logins.
  ![](https://main.qcloudimg.com/raw/2286644d987d24caf565142ae30c4392.png)

  >? This account is for development and testing only. Before the application is launched, the correct `UserSig` distribution method is to use the server to generate `UserSig` and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).

  [](id:part2)

  ## Selecting a Suitable Scheme to Integrate the SDK for Flutter

  Chat offers three integration schemes:

  | Integration Scheme                    | Applicable Scenario                                          |
  | ------------------------------------- | ------------------------------------------------------------ |
  | [Modifying the demo](#part3)          | The Chat demo is a complete chat application with open-source code. If you need to implement chat scenarios, you can use the demo for secondary development. Try it out [here](https://intl.cloud.tencent.com/document/product/1047/34279). |
  | [Using UI library](#part4)            | The Chat UI component library TUIKit provides common UI components, such as conversation list, chat UI, and contacts. You can use the component library to quickly build a custom Chat application as needed. **This scheme is recommended**. |
  | [Implementing UI on your own](#part5) | You can use this scheme if TUIKit cannot meet your UI requirements or you need heavy customization. |

  To help you better understand Chat SDK APIs, sample APIs are provided [here](https://github.com/TencentCloud/tc-chat-sdk-flutter/tree/main/example) to demonstrate how to call APIs and trigger listeners.

  [](id:part3)

  ## Scheme 1. Modifying the Demo

  ### Running demo

  1. Download the demo source code and install dependencies:
  ```shell
  # Clone the code
  git clone https://github.com/TencentCloud/tc-chat-demo-flutter.git
  
  # Install dependencies
  flutter pub get
  ```
  2. Run the demo:
  ```shell
  # Start the demo and replace `SDK_APPID` and `KEY`
  flutter run --dart-define=SDK_APPID={YOUR_SDKAPPID} --dart-define=ISPRODUCT_ENV=false --dart-define=KEY={YOUR_KEY}
  ```
  >?
  >
  >- `--dart-define=SDK_APPID={YOUR_SDKAPPID}`. Here, `{YOUR_SDKAPPID}` needs to be replaced with the `SDKAppID` of your application.
  >- Use `--dart-define=ISPRODUCT_ENV=false` to determine the environment (development or production). Enter `false` for a development environment.
  >- `--dart-define=KEY={YOUR_KEY}`. Here, `{YOUR_KEY}` needs to be replaced with the `Key` recorded in [Part 1. Creating Test Accounts](#part1).
  >

  #### (Optional) Using the IDE

  <dx-tabs>
  ::: Android[](id:android)
  1. Install the Flutter and Dart plugins in Android Studio.
   - macOS: Go to plugin settings (choose **Preferences** > **Plugins** in v3.6.3.0 or later). Select **Flutter** and click **Install**. When the Dart plugin installation prompt is displayed, click **Yes**. When the restart prompt is displayed, click **Restart**.
   - Linux or Windows: Go to plugin settings (**File** > **Settings** > **Plugins**). Select **Marketplace**, select **Flutter plugin**, and click **Install**.
  ![](https://qcloudimg.tencent-cloud.cn/raw/481bc19b55b40051daa8e669325cd123.png)
  2. Open the project and get dependencies.
  Open the `im-flutter-uikit` directory in Android Studio.
  Run the following command in the path to install dependencies:
  ```shell
  flutter pub get
  ```
  3. Configure environment variables.
  In the upper-right corner, hover over `main.dart` next to the run button and select `Edit Configurations`.
  ![](https://qcloudimg.tencent-cloud.cn/raw/e2db56849e86dab8f6f0ccb4d3374fce.png)
  In the pop-up window, configure `Additional run args` by entering environment variables (such as SDKAppID). For example:
  ```shell
  # Replace the SDK_APPID and KEY parameters
  --dart-define=SDK_APPID={YOUR_SDKAPPID} --dart-define=ISPRODUCT_ENV=false --dart-define=KEY={YOUR_KEY}
  ```
  ![](https://qcloudimg.tencent-cloud.cn/raw/f022441399d2d6057b86e489593768ad.png)
  4. Create an Android simulator.
  Start the simulator that you create and select it.
  ![](https://qcloudimg.tencent-cloud.cn/raw/e3aebdd2f6018c8f1fa10d5b5fb62c79.png)
  Click **Device Manager** in the upper-right corner, click **Create device**, and create a simulator. If the Google FCM push capability is required, you are advised to install devices that support Google Play Store.
  ![](https://qcloudimg.tencent-cloud.cn/raw/9db005b86f9ffa1052826fe5e11d219a.png)
  5. Run the project.
  Click the **Run** button on the left or the **Debug** button on the right as needed to run the project.
  ![](https://qcloudimg.tencent-cloud.cn/raw/7b0d4d008f71e1d0d805c9fb3a5de437.png)
  >? The UI of the latest version of the demo may look different.
  >:::
  >::: iOS[](id:ios)

  1. Open the `im-flutter-uikit/ios` directory in Xcode.
  2. Connect an iPhone, and tap **Build And Run**. After the iOS project is built, the Xcode project will be displayed in a new pop-up window.
  3. Open the iOS project, and set **Signing & Capabilities** (an iPhone developer account required) for the primary target to run the project on the iPhone.
  4. Start the project and debug the demo on the iPhone device.
  ![](https://qcloudimg.tencent-cloud.cn/raw/911935cf419e4298edb45cd93bf10852.png)
  :::
  </dx-tabs>

  #### Demo code structure

  >? The TUIKit for Flutter is used for the UI and business logic of the demo. The demo layer itself is only used to build an application, process navigation redirects, and call instantiated TUIKit components.

  | Folder        | Description                                                  |
  | ------------- | ------------------------------------------------------------ |
  | lib           | Core application directory                                   |
  | lib/i18n      | Internationalization code, excluding the internationalization capabilities and strings of TUIKit, which can be imported as needed. |
  | lib/src       | Main application directory                                   |
  | lib/src/pages | Important navigation pages of the demo. After the application is initialized, `app.dart` will display the loading animation, identify the login status, and redirect the user to `login.dart` or `home_page.dart`. After the user logs in, the login information will be stored locally through the `shared_preference` plugin and used for automatic login upon each application start. If there is no such information or the login fails, the user will be redirected to the login page. During automatic login, the user is still on `app.dart` and can see the loading animation. `home_page.dart` offers a bottom tab to support switch between the four main feature pages of the demo. |
  | lib/utils     | Some tool function classes                                   |

  Basically, a TUIKit component is imported into each `dart` file in `lib/src`. After the component is instantiated in the file, the page can be rendered.

  Below are the main files:

  | Main File in `lib/src`      | Description                                                  |
  | --------------------------- | ------------------------------------------------------------ |
  | add_friend.dart             | Friend request page, which uses the `TIMUIKitAddFriend` component |
  | add_group.dart              | Group join request page, which uses the `TIMUIKitAddGroup` component |
  | blacklist.dart              | Blocklist page, which uses the `TIMUIKitBlackList` component |
  | chat.dart                   | Main chat page, which uses all the chat capabilities of TUIKit and the `TIMUIKitChat` component |
  | chatv2.dart                 | Main chat page, which uses atomic capabilities and the `TIMUIKitChat` component |
  | contact.dart                | Contacts page, which uses the `TIMUIKitContact` component    |
  | conversation.dart           | Conversation list page, which uses the `TIMUIKitConversation` component |
  | create_group.dart           | Group chat start page, which is implemented in the demo with no components used |
  | group_application_list.dart | Group join request list page, which uses the `TIMUIKitGroupApplicationList` component |
  | group_list.dart             | Group list page, which uses the `TIMUIKitGroup` component    |
  | group_profile.dart          | Group profile and management page, which uses the `TIMUIKitGroupProfile` component |
  | newContact.dart             | Friend request page, which uses the `TIMUIKitNewContact` component |
  | routes.dart                 | Demo route, which navigates users to the login page `login.dart` or homepage `home_page.dart` |
  | search.dart                 | Global search and in-conversation search page, which uses the `TIMUIKitSearch` (global search) and `TIMUIKitSearchMsgDetail` (in-conversation search) components |
  | user_profile.dart           | User information and relationship chain maintenance page, which uses the `TIMUIKitProfile` component |

  As the navigation redirect method needs to be imported into most of the TUIKit components, the demo layer needs to process `Navigator`.

  You can modify the above demo for secondary development or implement your business needs based on it.

  [](id:part4)

  ## Scheme 2. Using UI library and the TUIKit Component Library to Implant Chat Capabilities in Half a Day

  TUIKit is a UI component library of the Chat SDK. It provides common UI components such as conversation list, chat UI, and contacts. You can use the component library to quickly build a custom Chat application as needed. For more information, see [here](https://intl.cloud.tencent.com/document/product/1047/50059).

  The following is a simple guide to help you get started with TUIKit. For detailed directions, see [here](https://intl.cloud.tencent.com/document/product/1047/50054).

  ![](https://qcloudimg.tencent-cloud.cn/raw/f140dd76be01a65abfb7e6ba2bf50ed5.png)

  ### Prerequisites

  You have created a Flutter application or have an application that can be based on Flutter.

  ### Directions

  #### Configure permissions

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

  #### Installing the Chat TUIKit

  TUIKit contains the Chat SDK, so you only need to install `tencent_cloud_chat_uikit`.

  ```shell
  # Run the following command:
  flutter pub add tencent_cloud_chat_uikit
  ```

  If your project requires web support, import JS files by referring to [the web compatibility description section](#web) before performing subsequent steps.

  #### Initialization API

  1. Initialize the TUIKit upon application start.
  2. Run [`TIMUIKitCore.getInstance()`](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitCore/getInstance.html) first and then call the initialization function [`init()`](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitCore/init.html). Remember to pass in your `sdkAppID`.
  3. You are advised to mount an `onTUIKitCallbackListener` listener to get API errors and prompts. For more information, see [here](https://intl.cloud.tencent.com/document/product/1047/50054#onTUIKitCallbackListener).

  ```dart
  /// main.dart
  import 'package:tencent_cloud_chat_uikit/tencent_cloud_chat_uikit.dart';
  
  final CoreServicesImpl _coreInstance = TIMUIKitCore.getInstance();
    @override
   void initState() {
     _coreInstance.init(
       sdkAppID: 0, // Replace 0 with the SDKAppID of your Chat application when integrating
       // language: LanguageEnum.en, // UI language. If no value is specified, the system language is used.
       loglevel: LogLevelEnum.V2TIM_LOG_DEBUG,
       onTUIKitCallbackListener:  (TIMCallback callbackValue){}, // [Configure a listener](https://intl.cloud.tencent.com/document/product/1047/50054#onTUIKitCallbackListener).
       listener: V2TimSDKListener());
     super.initState();
   }
  }
  ```

  >?Do not perform subsequent steps before the initialization in this step is completed.

  #### Logging in with a test account

  1. Log in with a test account initially generated in the console for verification.
  2. Call the [`_coreInstance.login`](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitCore/login.html) method to log in with a test account.

  ```dart
  import 'package:tencent_cloud_chat_uikit/tencent_cloud_chat_uikit.dart';
  
  final CoreServicesImpl _coreInstance = TIMUIKitCore.getInstance();
  _coreInstance.login(userID: userID, userSig: userSig);
  ```

  >? This account is for development and testing only. Before the application is launched, the correct `UserSig` distribution method is to use the server to generate `UserSig` and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).

  #### Implementation: conversation list page

  You can use the conversation list as the Chat homepage, which contains all the one-to-one and group conversations.

  <img style="width:300px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/279da6d5d41ec1ce0b0cf7fca9a697b8.jpg" />

  Create a `Conversation` class and use the [`TIMUIKitConversation`](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitConversation/) component in `body` to render the conversation list.

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

  #### Implementation: chat page

  This page consists of the message history and message sending modules.
  <img style="width:300px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/0c361254fa5117f7580f39e8b523e472.png" />

  Create a `Chat` class and use the [`TIMUIKitChat`](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitChat/) component in `body` to render the chat page.

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

  #### Implementation: user details page

  By default, this page determines whether a user is a friend and generates the user details page after only one `userID` is passed in.

  Create a `UserProfile` class and use the [`TIMUIKitProfile`](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitProfile/) component in `body` to render the user details and relationship chain page.

  >? If you want to customize this page, first consider using [`profileWidgetBuilder`](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitProfile/ProfileWidgetBuilder.html) to pass in the profile component to be customized and use `profileWidgetsOrder` to determine the vertical display order. If the requirements cannot be met, use `builder` instead.

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

  At this point, your app supports messaging, friend relationship management, user details display, and conversation list display.

  #### More capabilities

  You can also use the following TUIKit plugins to quickly implement Chat features:

  - [TIMUIKitContact](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitContact/): Contact list page
  - [TIMUIKitGroupProfile](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitGroupProfile/): Group profile page, whose usage mode is basically the same as that of `TIMUIKitProfile`
  - [TIMUIKitGroup](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitGroup/): Group list page
  - [TIMUIKitBlackList](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitBlackList/): Blocklist page
  - [TIMUIKitNewContact](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitNewContact/): Contact/Friend request list. If you want to display a badge, you can use the `TIMUIKitUnreadCount` badge component, which can mount listeners automatically.
  - [Local search](https://intl.cloud.tencent.com/document/product/1047/50036): `TIMUIKitSearch` is a global search component, which supports the global search of contacts, groups, and chat history. You can also use `TIMUIKitSearchMsgDetail` to search for chat records in a specific conversation. You can choose whether to pass in `conversation` to choose between the two search modes.

  For the full view of the UI components, see the [overview document](https://intl.cloud.tencent.com/document/product/1047/50059) or [detailed document](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/).

  [](id:part5)

  ## Scheme 3. Implementing UI on Your Own

  ### Prerequisites

  You have created a Flutter application or have an application that can be based on Flutter.

  ### Directions

  #### Installing the Chat SDK

  [Detailed documentation](https://intl.cloud.tencent.com/document/product/1047/46264)

  Run the following command to install the latest version of the Chat SDK for Flutter.

  Run the following command:

  ```shell
  flutter pub add tencent_cloud_chat_sdk
  ```

  >?
  >If your project also needs to be applied to [web](#web) or [desktop (macOS/Windows)](#pc) platforms, you need to perform a few extra steps for SDK integration. For details, see [Support for the Flutter for web](#web) and [Support for the Flutter for desktop](#pc) in this document.

  #### Initializing the SDK

  [Detailed documentation](https://intl.cloud.tencent.com/document/product/1047/47966)

  Call `initSDK` to initialize the SDK.

  Pass in your `sdkAppID`.

  ```Dart
  import 'package:tencent_cloud_chat_sdk/enum/V2TimSDKListener.dart';
  import 'package:tencent_cloud_chat_sdk/enum/log_level_enum.dart';
  import 'package:tencent_cloud_chat_sdk/tencent_cloud_chat_sdk.dart';
  TencentImSDKPlugin.v2TIMManager.initSDK(
    sdkAppID: 0, // Replace 0 with the SDKAppID of your Chat application when integrating
    loglevel: LogLevelEnum.V2TIM_LOG_DEBUG, // Log
    listener: V2TimSDKListener(),
  );
  ```

  In this step, you can mount some listeners to the Chat SDK, mainly including those for network status and user information changes. For more information, see [here](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/enum_V2TimSDKListener/V2TimSDKListener-class.html).

  #### Logging in with a test account

  [Detailed documentation](https://intl.cloud.tencent.com/document/product/1047/47969)

  Log in with a test account initially generated for verification.

  Call the `TencentImSDKPlugin.v2TIMManager.login` method to log in with the test account.

  If the returned `res.code` is `0`, the login is successful.

  ```dart
  import 'package:tencent_cloud_chat_sdk/tencent_cloud_chat_sdk.dart';
  V2TimCallback res = await TencentImSDKPlugin.v2TIMManager.login (
    userID: userID,
    userSig: userSig,
  );
  ```

  >?This account is for development and testing only. Before the application is launched, the correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).

  #### Sending messages

  [Detailed documentation](https://intl.cloud.tencent.com/document/product/1047/47992)

  The following shows how to send a text message:

  1. Call `createTextMessage(String)` to create a text message.
  2. Get the message ID from the returned value.
  3. Call `sendMessage()` to send the message with the ID. `receiver` can be the ID of the other test account created earlier. `groupID` is not required for sending a one-to-one message.

  Sample code:

  ```dart
  import 'package:tencent_cloud_chat_sdk/tencent_cloud_chat_sdk.dart';
  
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

  > ?If sending fails, it may be that your `sdkAppID` doesn't support sending messages to strangers. In this case, you can enable the feature in the console for testing.
  >
  > Disable the friend relationship chain check [here](https://console.cloud.tencent.com/im/login-message).

  #### Obtaining the conversation list

  [Detailed documentation](https://intl.cloud.tencent.com/document/product/1047/48324)

  Log in with the other test account to pull the conversation list.
  <img style="width:300px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/e2fdd7632ebc0c5cde68c91afa914201.jpg" />

  The conversation list can be obtained in two ways:

  1. Listen for the persistent connection callback to update the conversation list in real time.
  2. Call the API to get the paginated conversation list at a time.

  Common use cases include:

  Get the conversation list upon application start and listen for the persistent connection to update the conversation list in real time.

  ##### Requesting the conversation list at a time

  To get the conversation list, you need to maintain `nextSeq` and record its current position.

  ```dart
  import 'package:tencent_cloud_chat_sdk/tencent_cloud_chat_sdk.dart';
  
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

  ##### Listening for the persistent connection to get the conversation list in real time

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
  2. Process the callback event and display the latest conversation list on the UI.
  ```dart
  import 'package:tencent_cloud_chat_sdk/tencent_cloud_chat_sdk.dart';
  
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

  #### Receiving messages

  [Detailed documentation](https://intl.cloud.tencent.com/document/product/1047/47997)

  There are two methods to receive messages in the Chat SDK for Flutter:

  1. Listen for the persistent connection callback to get message changes and update and render the historical message list in real time.
  2. Call the API to get the paginated message history at a time.

  Common use cases include:

  1. After a new conversation is opened on the UI, request a certain number of historical messages at a time to display the historical message list.
  2. Listen for the persistent connection to receive messages in real time and add them to the historical message list.

  ##### Requesting the historical message list at a time

  To avoid affecting the pull speed, we recommend you limit the number of messages to be pulled per page to 20.

  You need to dynamically record the current number of pages for the next request.

  Sample code:

  ```dart
  import 'package:tencent_cloud_chat_sdk/tencent_cloud_chat_sdk.dart';
  
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

  ##### Listening for the persistent connection to get new messages in real time

  After the historical message list is initialized, new messages are from the persistent connection `V2TimAdvancedMsgListener.onRecvNewMessage`.

  After the `onRecvNewMessage` callback is triggered, you can add new messages to the historical message list as needed.

  Sample code for binding a listener:

  ```dart
  import 'package:tencent_cloud_chat_sdk/tencent_cloud_chat_sdk.dart';
  
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

  At this point, you have completed the Chat module development, and now users can send and receive messages and enter different conversations.

  You can develop more features, such as [group](https://intl.cloud.tencent.com/document/product/1047/48169), [user profile](https://intl.cloud.tencent.com/document/product/1047/48160), [relationship chain](https://intl.cloud.tencent.com/document/product/1047/48157) and [local search](https://intl.cloud.tencent.com/document/product/1047/48135).

  For more information, see [Integration Solution (No UI)](https://www.tencentcloud.com/document/product/1047/34299).

  ## Integrating Advanced Features

  ### Enriching your Flutter Chat experience with more plugins

  In addition to the SDK and TUIKit basic features, we provide four optional plugins to help you enrich Chat capabilities:

  - [Message push plugin](https://intl.cloud.tencent.com/document/product/1047/50032): Supports vendors' native offline push capabilities and supports pushing your other business messages to help you improve the message reach rate.
  - [Audio/Video call plugin](https://pub.dev/packages/tim_ui_kit_calling_plugin): Supports one-to-one and group audio/video calls.
  - [Geographical location message plugin](https://pub.dev/packages/tim_ui_kit_lbs_plugin): Provides the capabilities to select locations, send locations, and parse and display location messages.
  - [Custom emoji plugin](https://www.tencentcloud.com/document/product/1047/52227): TUIKit 0.1.5 or later does not provide an emoji package, and you can use this plugin to quickly integrate the emoji capability. This plugin supports emoji unicode encoding and custom image emojis. For the integration code, refer to our [demo](https://github.com/TencentCloud/tc-chat-demo-flutter/blob/main/lib/src/pages/app.dart).

  >?If you have any good ideas or suggestions, feel free to [contact us](https://www.tencentcloud.com/contact-us).

  [](id:more)

  ## Expanding to More Platforms

  Tencent Cloud Chat for Flutter SDKs support Android and iOS platforms by default. You can also expand to more platforms (web and desktop).

  ### Support for the Flutter for web[](id:web)

  Our SDKs, TUIKit (tencent_cloud_chat_uikit) 0.1.5 or later, and no-UI SDK (tencent_cloud_chat_sdk) 4.1.1+2 or later provide full compatibility with web.

  To enable support for web, you need to perform the following extra steps, compared with the steps to enable support for Android and iOS:

  #### Upgrading to Flutter 3.x

  Flutter 3.x has been dramatically optimized for web performance and is highly recommended for Flutter web project development.

  #### Importing the Flutter for Web plugin SDK

  ```dart
  flutter pub add tencent_im_sdk_plugin_web
  ```

  #### Importing JS

  >?If your existing Flutter project does not support web, run `flutter create .` in the root directory of the project to add web support.
  >

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

  ![](https://qcloudimg.tencent-cloud.cn/raw/a4d25e02c546e0878ba59fcda87f9c76.png)

  ### Support for the Flutter for desktop (PC)[](id:pc)

  Our no-UI SDK (tencent_cloud_chat_sdk) 4.1.9 or later provides full compatibility with macOS and Windows clients. To enable support for macOS and Windows, you need to perform the following extra steps, compared with the steps to enable support for Android and iOS:

  #### Upgrading to Flutter 3.x

  Only Flutter 3.0 or later supports desktop clients. Therefore, if you need to use desktop clients, upgrade your Flutter to Flutter 3.x.

  #### Importing the Flutter for Desktop plugin SDK

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

  ### What should I do if Pods dependency installation fails in iOS?

  #### **Solution 1:** If an error occurs after the configuration, click **Product** > **Clean Build Folder**, clear the product, and run `pod install` or `flutter run` again.

  ![](https://qcloudimg.tencent-cloud.cn/raw/d495b2e8be86dac4b430e8f46a15cef4.png)

  #### **Solution 2:** Manually delete the `ios/Pods` folder and the `ios/Podfile.lock` file, and run the following commands to install the dependencies again.

  1. For macOS devices with the latest series of Apple Silicon chips, such as M1:
  ![](https://staticintl.cloudcachetci.com/yehe/backend-news/vAsQ099_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_327a198c-bc61-433a-991f-0124e7b0d2e2.png)
  ```shell
  cd ios
  sudo arch -x86_64 gem install ffi
  arch -x86_64 pod install --repo-update
  ```
  2. For macOS devices with Intel chips of earlier versions:
  ```shell
  cd ios
  sudo gem install ffi
  pod install --repo-update
  ```

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

  ### How do I query error codes?

  - For Chat SDK API error codes, see [here](https://intl.cloud.tencent.com/document/product/1047/34348).
  - TUIKit scenario codes are used for pop-up prompts and can be obtained by listening for [onTUIKitCallbackListener](https://intl.cloud.tencent.com/document/product/1047/50054#callback). For the scenario code list, see [here](https://intl.cloud.tencent.com/document/product/1047/50054#infoCode).
