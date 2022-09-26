## Introduction to TUIKit
Flutter TUIKit is a set of UI components based on Flutter IM SDKs. It provides features such as the conversation, chat, relationship chain, and group features. You can use these UI components to quickly build your own business logic. The architecture of Flutter TUIKit is as follows.
![](https://qcloudimg.tencent-cloud.cn/raw/b336c1a482129254682d405e008fec01.png)

The TUIKit component library and supportive business logic code [im-flutter-uikit](https://github.com/tencentyun/TIMSDK/tree/master/Flutter/Demo/im-flutter-uikit) are open source. You can integrate the online version or fork it before local integration.

Currently, Flutter TUIKit contains the following components:

- [TIMUIKitCore](https://intl.cloud.tencent.com/document/product/1047/46297) (core)
- [TIMUIKitConversation](https://intl.cloud.tencent.com/document/product/1047/46297) (conversations)
- [TIMUIKitChat](https://intl.cloud.tencent.com/document/product/1047/46297) (chats)
- [TIMUIKitContact](https://intl.cloud.tencent.com/document/product/1047/46297) (contacts)
- [TIMUIKitProfile](https://intl.cloud.tencent.com/document/product/1047/46297) (friend management)
- [TIMUIKitGroupProfile](https://intl.cloud.tencent.com/document/product/1047/46297) (group management)
- [TIMUIKitGroup](https://intl.cloud.tencent.com/document/product/1047/46297) (my group chats)
- [TIMUIKitBlackList](https://intl.cloud.tencent.com/document/product/1047/46297) (blocklist)
- [TIMUIKitNewContact](https://intl.cloud.tencent.com/document/product/1047/46297) (new contacts)
- [TIMUIKitSearch](https://pub.dev/documentation/tim_ui_kit/latest/ui_views_TIMUIKitSearch_tim_uikit_search/TIMUIKitSearch-class.html) (local search)

![](https://qcloudimg.tencent-cloud.cn/raw/f140dd76be01a65abfb7e6ba2bf50ed5.png)

>?
>
> The UI language of TUIKit can be automatically or manually switched between **Simplified Chinese/Traditional Chinese/English**. If you have more questions, [contact us](#contact).

## Directions
The following describes how to use Flutter TUIKit to quickly build a simple IM app.

### Step 1. Create a Flutter app and configure permissions
Quickly create a Flutter app. For details, see [Flutter documentation](https://flutter.cn/docs/get-started/test-drive?tab=terminal).

#### Configuring permissions[](id:permission)

The TUIKit requires permissions such as camera, album, mic, and network, so you need to manually declare them in the native file first.

**Android**

Open `android/app/src/main/AndroidManifest.xml` and add the following permissions in `<manifest></manifest>`:

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

Open `ios/Podfile` and add the following permission code at the end of the file:
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

### Step 2. Install dependencies
Add `tim_ui_kit` under `dependencies` in the `pubspec.yaml` file, or run the following command:
```
// Step 1:
flutter pub add tim_ui_kit

// Step 2:
flutter pub get
```

### Step 3. Initialize TUIKit

Initialize `TIMUIKit` in `initState`. You only need to perform the initialization once for the project to start.
```dart
/// main.dart
import 'package:flutter/material.dart';
import 'package:tim_ui_kit/tim_ui_kit.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'TIMUIKit Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(title: 'TIMUIKit Demo'),
    );
  }
}

class MyHomePage extends StatefulWidget {
  MyHomePage({Key? key, required this.title}) : super(key: key);
  final String title;

  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  final CoreServicesImpl _coreInstance = TIMUIKitCore.getInstance();

  @override
  void initState() {
    _coreInstance.init(
      sdkAppID: 0, // SDKAppID obtained from the console
      loglevel: LogLevelEnum.V2TIM_LOG_DEBUG,
      listener: V2TimSDKListener());    
    super.initState();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      body: Container(),
    );
  }
}
```
### Step 4. Get the signature and log in
>?The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).

Add two `TextField` fields to pass in `UserID` and `UserSig`. Click **Login** to call the login API.
```dart
/// main.dart
/// Omitted
class _MyHomePageState extends State<MyHomePage> {
  /// Get the TIMUIKitCore instance
  final CoreServicesImpl _coreInstance = TIMUIKitCore.getInstance();
  String userID = "";
  String userSig = "";

  /// Omitted

  void _login() {
    // Log in
    _coreInstance.login(userID: userID, userSig: userSig);
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            TextField(
              onChanged: ((value) {
                setState(() {
                  userID = value;
                });
              }),
              decoration: InputDecoration(hintText: "userID"),
            ),
            TextField(
              onChanged: ((value) {
                setState(() {
                  userSig = value;
                });
              }),
              decoration: InputDecoration(hintText: "userSig"),
            ),
            ElevatedButton(
                onPressed: (() {
                  _login();
                }),
                child: const Text("Login"))
          ],
        ),
      ),
    );
  }
}

```



### Step 5. Integrate desired components
- Create the `message.dart` file to integrate `TIMUIKitConversation`, `TIMUIKitChat`, and more components as needed.
- Modify the code in `main.dart` to enable redirection to the specified page upon successful login. 
```dart
/// message.dart
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
      conversationType: selectedConversation.type ?? 0, // Conversation type
      conversationShowName: selectedConversation.showName ?? "", // Conversation display name
      onTapAvatar: (_) {}, // Callback for the clicking of the message sender profile photo. This callback can be used with `TIMUIKitProfile`.
      appBarActions: [
        IconButton(
            onPressed: () {}, icon: const Icon(Icons.more_horiz_outlined))
      ],
    );
  }
}


/// main.dart

/// Some code is omitted
void _login() async {
    final res = await _coreInstance.login(userID: userID, userSig: userSig);
    if (res.code == 0) {
      Navigator.of(context).pushAndRemoveUntil(
        MaterialPageRoute(
            builder: (BuildContext context) => const Conversation()),
        (route) => false,
      );
    }
  }
```
## FAQs

### Do I need to integrate the IM SDK after integrating TUIKit?
No. You don't need to integrate IM SDK again. If you want to use IM SDK related APIs, you can get them via `TIMUIKitCore.getSDKInstance()`. This method is recommended to ensure IM SDK version consistency.
### Why did forced quit occur when I sent audio, image, file, or other messages?
Check whether you have enabled the [camera, mic, album, or other related permission](#permission).

### What platforms are supported?
- Currently, [IM SDK (tencent_im_sdk_plugin)](https://intl.cloud.tencent.com/document/product/1047/46264) supports iOS, Android, and web. Windows and macOS will be supported in the future.
- [TUIKit](https://intl.cloud.tencent.com/document/product/1047/46576) and [the supportive interaction demo](https://github.com/TencentCloud/TIMSDK/tree/master/Flutter/Demo/im-flutter-uikit) support iOS and Android.

### What should I do if clicking **Build And Run** for an Android device triggers an error, stating no available device is found?

Check that the device is not occupied by other resources. Alternatively, click **Build** to generate an APK package, drag it to the simulator, and run it.

### What should I do if an error occurs during the first run for an iOS device?

If an error occurs after the configuration, click **Product** > **Clean Build Folder**, clean the product, and run `pod install` or `flutter run` again.

![](https://qcloudimg.tencent-cloud.cn/raw/d495b2e8be86dac4b430e8f46a15cef4.png)

### What should I do if an error occurs during debugging on a real iOS device when I am wearing an Apple Watch?

![](https://qcloudimg.tencent-cloud.cn/raw/1ffcfe39a18329c86849d7d3b34b9a0e.png)

Turn on Airplane Mode on your Apple Watch, and go to **Settings > Bluetooth** on your iPhone to turn off Bluetooth.

Restart Xcode (if opened) and run `flutter run` again.

### What should I do if the Flutter environment becomes abnormal?

If you want to check the Flutter environment, run `Flutter doctor` to detect whether the Flutter environment is ready.

### What should I do if an error occurs on an Android device after TUIKit is integrated into the application automatically generated by Flutter?

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


