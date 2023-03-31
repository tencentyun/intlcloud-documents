Tencent Cloud IM terminal users need to obtain the latest messages at any time. However, considering the limited performance and battery SOC of mobile devices, Tencent Cloud IM recommends you use the system-grade push channels provided by vendors for message notifications when the app is running in the background to avoid excessive resource consumption caused by maintaining a persistent connection. Compared with third-party push channels, system-grade push channels provide more stable system-grade persistent connections, enabling users to receive push messages at any time and greatly reducing resource consumption.

>?
>- If you want users to receive IM message notifications when, without proactive logout, the app is switched to the background, the mobile phone screen is locked, or the app process is killed by a user, you can enable the IM offline push.
>- If the `logout` API is called to log out proactively or you are forced to log out due to multi-device login, you cannot receive offline push messages even though IM offline push is enabled.

IM for Flutter integrates a plugin to connect to the offline push of mainstream vendors such as Apple, Google, OPPO, vivo, Huawei, Mi, and Meizu.

This document describes how to connect to IM offline push. The plugin has been encapsulated with the SDKs of the vendors mentioned above, and you only need to reconstruct them a little before calling them.

If offline push is not required by your application or supported in your business scenarios, see [Online Push - Creating a Local Message Notification](#online_push).


If vendor offline push has been configured for your application, you only need to enter the vendor information in the console as instructed in [step 1](#step_1) and [step 5](#step_5) and report the certificate ID after logging in to the application.

## Plugin APIs

>? The following APIs are compatible with Android/iOS platforms and supported vendor devices unless otherwise specified. The platform and vendor are identified inside the plugin, which can be called directly.

| API                                  | Description                                                  |
| ------------------------------------ | ------------------------------------------------------------ |
| Constructor (TimUiKitPushPlugin)     | Instantiates a push plugin object and determines whether to use Google FCM. |
| init                                 | Binds the callback for the notification click event and passes in vendor channel information. |
| uploadToken                          | Automatically gets and uploads the device token and certificate ID to the IM server. |
| requireNotificationPermission        | Requests the push permission.                                |
| setBadgeNum                          | Sets the unread count badge (only supported by some Android devices. For more information, see API Code Parameter Description.) |
| clearAllNotification                 | Clears all the notifications of the current application from the notification bar. |
| getDevicePushConfig                  | Gets the push information of the current vendor, including model, certification ID, and token. |
| getDevicePushToken                   | Gets the push token of the current vendor.                   |
| getOtherPushType                     | Gets the vendor information.                                 |
| getBuzId                             | Gets the current vendor's certificate ID registered in the Tencent Cloud console. |
| createNotificationChannel            | Creates a notification channel for an Android model. For more information, see [Create and Manage Notification Channels](https://developer.android.com/training/notify-user/channels). |
| clearAllNotification                 | Clears all the notifications of the current application from the notification bar. |
| displayNotification                  | Manually creates a message notification on the client.       |
| displayDefaultNotificationForMessage | Automatically creates a message notification for a `V2TimMessage` object on the client according to the default rules. |

## Connection Preparations (Vendor Registration)[](id:firstone)

You need to apply for a vendor developer account (enterprise verification is usually required), create an application, request the push permission, and get the key information.

### Apple
#### iOS

1. [Apply for an Apple push certificate](https://intl.cloud.tencent.com/document/product/1047/34346).
2. Host the obtained production and development environment certificates in the IM console.
3. Go to the [IM console > Basic Configuration](https://console.cloud.tencent.com/im/detail) and click **Add iOS Certificate** on the right.


### Android
#### Google FCM
1. Go to the [Google Firebase console](https://console.firebase.google.com/) and create a project. You don't need to enable Google Analytics.

2. Click the **Your apps** card to enter the application configuration page.
3. Click <img src="https://main.qcloudimg.com/raw/0d062411405553c9fae29f8e0daf02ad.png"  style="margin:0;"> on the right of **Project Overview**, select **Project settings** > **Service accounts**, and click **Generate new private key** to download the private key file.

4. Host the private key file in the IM console. Go to the [IM console > Basic Configuration](https://console.cloud.tencent.com/im/detail) and click **Add Certificate** on the right to pop up the **Add Android Certificate** window. Then select **Google** and **Upload certificate**.


#### OPPO

##### Activating the service
Register a developer account, create an application, and activate the OPPO PUSH service. For operation details, see [How to enable OPPO PUSH](https://open.oppomobile.com/wiki/doc#id=10195).

On the [OPPO PUSH Platform](https://push.oppo.com/), select **Configuration Management** > **Application Configuration** to view the application details and record the `AppId`, `AppKey`, `AppSecret`, and `MasterSecret`.


##### Creating a message channel

The official OPPO documentation states that ChannelIDs are required for push messages on OPPO Android 8.0 and above. Therefore, create a ChannelID for your app. Below is a sample code that creates a ChannelID called `tuikit`.

Create a channel in **Configuration Management > Create Channel**. **ChannelID** is the ID of the channel.

>?OPPO imposes daily limits on public channels. For communication messages, we recommend you apply for private channels as instructed in [OPPO documentation](https://open.oppomobile.com/new/developmentDoc/info?id=11227).



##### Uploading a certificate to the console

1. Go to the [IM console > Basic Configuration](https://console.cloud.tencent.com/im/detail) and click **Add Certificate** on the right to pop up the **Add Android Certificate** window. Select **OPPO** and enter other information.
2. Enter the dedicated channel ID applied for communication in the OPPO console for `ChannelID`. A private channel is recommended to avoid exceeding the daily push limit.
3. Select **Open specified in-app page** > **activity** for the opening method and enter `com.tencent.flutter.tim_ui_kit_push_plugin.pushActivity.OPPOMessageActivity`.


#### Mi
##### Activating the service

Visit the [Mi open platform website](https://dev.mi.com/console/), register an account, and complete developer verification.
 >?The verification process takes about two days. Please read the [Mi Push Service Activation Guide](https://dev.mi.com/console/doc/detail?pId=68) in advance to avoid any effect on your connection progress.

On the Mi Developer platform, create an application and select **Application Services** > **PUSH Service**.


Once the app is created, you can view detailed app information under the app details.

Record the **primary package name**, **AppID**, **AppSecret** information.


##### Uploading a certificate to the console

Go to the [IM console > Basic Configuration](https://console.cloud.tencent.com/im/detail) and click **Add Certificate** on the right to pop up the **Add Android Certificate** window. Select **Mi**, enter other information, and set **Response after Click** to **Open application**.



#### vivo

##### Activating the service
Visit the [vivo open platform official website](https://dev.vivo.com.cn/home) and register for an account. Complete developer verification.

 >?The verification process takes about 3 days. You can read the [vivo Push description](https://dev.vivo.com.cn/documentCenter/doc/180) while you wait to get a head start.

1. Log in to the vivo Developers platform, go to the management center, click **Message Push** > **Create** > **Test Push**, and create a Vpush application.

2. View the application details and record the `APP ID`, `APP key`, and `App secret`.


>?Vpush can only be used after the application launch. If you need to debug vivo devices during development, enable the test mode as instructed in [Debugging on vivo](#vivotest).

##### Uploading a certificate to the console

Go to the [IM console > Basic Configuration](https://console.cloud.tencent.com/im/detail) and click **Add Certificate** on the right to pop up the **Add Android Certificate** window. Select **Vivo** and enter other information.

- **Response after Click**: Select **Open specified in-app page**.
- **In-app page**: Set it to `tencent_im_push://${your package name}/message?#Intent;scheme=tencent_im_push;launchFlags=0x4000000;end`.


#### Huawei

##### Obtaining a key

1. Go to the [Huawei Developer Platform](http://developer.huawei.com). Register a developer account and log in to the platform. For more information, see [Account Registration and Verification](https://developer.huawei.com/consumer/cn/devservice/doc/20300). If you are registering a new account, identity verification is required.
2. Create an application on the Huawei Push platform. For more information, see [Creating an App](https://developer.huawei.com/consumer/cn/doc/distribution/app/agc-create_app). Note down the **AppID** and **AppSecret**.



>?If you cannot find `SecretKey` in **App information** > **My apps**, go to **Project settings** > **General information** to view `Client secret`.


##### Configuring the SHA-256 certificate fingerprint

Get the SHA-256 certificate fingerprint as instructed in [Generating a Signing Certificate Fingerprint](https://developer.huawei.com/consumer/cn/doc/development/HMS-Guides/Preparations#generate_finger). Then configure the fingerprint on the Huawei Push platform, and **remember to click <img src="https://main.qcloudimg.com/raw/f74e3aa948316533ce91f9add4a81a29.png"></img> to save the configuration**.

> ?If your application needs to be compiled and released through a pipeline, and each compilation is performed on different build machines, you can create a local `keystore.jks` key file to get its SHA-256 value and enter it on the HUAWEI Push platform.
>
> When a script is built in a pipeline, you need to archive and align the final build and use the `keystore` signature, so that the SHA-256 value of the final build is consistent with the former value. The code is as follows:
> ```shell
> zipalign -v -p 4 built apk.apk packaged apk_aligned.apk 
> apksigner sign --ks keystore.jks --ks-pass pass: Your keystore password --out Final signature Completed apk.apk Packaged apk_aligned.apk
> ```

##### Getting the Huawei Push configuration file

Log in to the Huawei Developer platform, go to **My Projects** > select a project > **Project Settings**, and download the latest configuration file `agconnect-services.json` of your Huawei application to the `android/app` directory.



##### Enabling the push service

On the Huawei Push platform, choose **All services** > **Push Kit** to go to the **Push Kit** page.


On the **Push Kit** page, click **Enable now**. For more information, see [Enabling Services](https://developer.huawei.com/consumer/cn/doc/distribution/app/agc-enable_service#enable-service).


##### Uploading a certificate to the console

1. Go to the [IM console > Basic Configuration](https://console.cloud.tencent.com/im/detail) and click **Add Certificate** on the right to pop up the **Add Android Certificate** window.
2. Select **Huawei** and enter other information.

Set **Badge Parameter** to the `Activity` class of the Android application entry, for example, `com.tencent.flutter.tuikit` in the demo; otherwise, the badge settings of the Huawei channel notifications will not take effect.

Set **Response after Click** to **Open application**.



#### Meizu

##### Activating the service
1. Go to the [Meizu Flyme platform](https://open.flyme.cn) and perform registration and developer verification.
 >?The verification process takes about three days. Read the [Meizu Flyme Push Connection Document](https://open.flyme.cn/docs?id=129) in advance to avoid any effect on your connection progress.

2. Log in to the console of the Meizu Flyme platform, select **Service** > **Integrate Push Service** > **Push Backend**, and create a Meizu push application.
3. View the application details and record the `App package name`, `App ID`, and `App Secret`.



##### Uploading a certificate to the console
1. Go to the [IM console > Basic Configuration](https://console.cloud.tencent.com/im/detail) and click **Add Certificate** on the right to pop up the **Add Android Certificate** window.
2. Select **Meizu**, enter other information, and set **Response after Click** to **Open application**.


## Using the Plugin to Run the Offline Push (Overview + Android)
Install the IM for Flutter offline push plugin in your project:
```shell
flutter pub add tim_ui_kit_push_plugin
```

Enable the push plugin in the plugin marketplace.

### Step 1. Aggregate the class of constants[](id:step_1)
1. After configuring the [connection preparations (vendor registration)](#firstone), go to the IM console > **Basic Configuration** to view the certificate ID allocated for your vendor channel application on the backend on the right.

2. Instantiate the information and vendor channel account information into a static `PushAppInfo` class, which needs to be passed in later.
3. You can configure the information of all the vendor push models that need to be connected in the class. You don't need to enter a complete constructor field. If you want to use a vendor platform, you need to enter the relevant field of the platform.
 ```Dart
import 'package:tim_ui_kit_push_plugin/model/appInfo.dart';

static final PushAppInfo appInfo = PushAppInfo(
  hw_buz_id: , // Huawei certificate ID
  mi_app_id: , // Mi `APPID`
  mi_app_key: , // Mi `APPKey`
  mi_buz_id: , // Mi certificate ID
  mz_app_id: , // Meizu `APPID`
  mz_app_key: , // Meizu `APPKey`
  mz_buz_id: , // Meizu certificate ID
  vivo_buz_id: , // vivo certificate ID
  oppo_app_key: , // OPPO `APPKey`
  oppo_app_secret: , // OPPO `APP Secret`
  oppo_buz_id: , // OPPO certificate ID
  oppo_app_id: , // OPPO `APPID`
  google_buz_id: , // Google FCM certificate ID
  apple_buz_id: , // Apple certificate ID
);
 ```

>?For more information, see the [`lib/utils/push/push_constant.dart`](https://github.com/TencentCloud/TIMSDK/tree/master/Flutter/Demo/im-flutter-uikit/lib/utils/push/push_constant.dart) file in the demo.

### Step 2. Add vendor project configuration to the code[](id:step_2)

#### Google FCM

##### Support for Android emulator debugging

To use Firebase Emulator Suite, open the `android/app/src/main/AndroidManifest.xml` file and add the `usesCleartextTraffic` field to `application`.

```xml
<application 
    android:usesCleartextTraffic="true" // Add this line
>
  <!-- possibly other elements -->
</application>
```

##### Integrating Google Firebase for Flutter capabilities
1. Open the `pubspec.yaml` file, add the `firebase_core` dependency, and use v1.12.0.

>?As the latest version of the Google Firebase for Flutter plugin is supported only by Dart v2.16.0 or later, you need to use v1.12.0 released in March 2022.
>
```yaml
dependencies:
  firebase_core: 1.12.0
```
2. Run `flutter pub get` to complete installation.
3. Run the following command in the console to configure the Google Firebase for Flutter project as prompted.
For more information, see [FlutterFire Overview](https://firebase.flutter.dev/docs/overview).
```shell
// Install the Firebase CLI 
npm install -g firebase-tools
curl -sL https://firebase.tools | bash

dart pub global activate flutterfire_cli

// Generate a configuration file
flutterfire configure
```
4. The project will be associated with that created in Google Firebase:

Initialize the FirebaseAPP in the `main()` method.
```Dart
WidgetsFlutterBinding.ensureInitialized();

await Firebase.initializeApp(
  options: DefaultFirebaseOptions.currentPlatform,
);
```

##### (Optional) Installing Google FCM
1. As Google services are not available for most of the models in the Chinese mainland, you can ignore this configuration.
2. When importing the plugin later, you need to set the `isUseGoogleFCM` field to `false`.

#### Huawei

1. Open the `android/build.gradle` file.
2. Add the Huawei repository address and HMS Gradle plugin dependencies under **repositories and dependencies** in **buildscript**, respectively:
```
buildscript {
    repositories {
        google()
        jcenter()
        maven {url 'https://developer.huawei.com/repo/'}     // Add Huawei Maven repository address
    }
    dependencies {
        // Other `classpath` configurations
        classpath 'com.huawei.agconnect:agcp:1.3.1.300'     // Add the Gradle plugin dependencies of Huawei Push
    }
    
    // Set release signing and passwords in the same build configuration file
    signingConfigs {       
       release {            
           storeFile file('<keystore_file>')            
           storePassword '<keystore_password>'            
           keyAlias '<key_alias>'            
           keyPassword '<key_password>'        
       }    
   }  
   buildTypes {        
       // The debug mode also requires compilation with a certificate; otherwise, Huawei fingerprint verification may fail.
       debug {            
           signingConfig signingConfigs.release        
       }       
       release {            
           signingConfig signingConfigs.release        
       }    
    }
}
```
3. Open the `android/build.gradle` file, and add the Huawei dependency repository address under **repositories** in **allprojects**:
```
allprojects {
    repositories {
        google()
        jcenter()
        maven {url 'https://developer.huawei.com/repo/'}     // Add Huawei Maven repository address
    }
}
```

4. Log in to the Huawei Developer platform, go to **My Projects** > select a project > **Project Settings**, and download the latest configuration file `agconnect-services.json` of your Huawei application to the `android/app` directory.


##### Importing the HMS SDK Gradle plugin at the application layer

Open the `android/app/build.gradle` file and add the following configuration:

```
// Other Gradle plugins of application
apply plugin: 'com.huawei.agconnect'      // HMS Push SDK Gradle plugin
android {
    // Application configuration content
}
```

##### Huawei/HONOR push badge permission

Open the `android/app/src/main/AndroidManifest.xml` file and add the following `uses-permission` information:

```xml
<uses-permission android:name = "com.huawei.android.launcher.permission.CHANGE_BADGE "/>
<uses-permission android:name = "com.hihonor.android.launcher.permission.CHANGE_BADGE" />
```

#### vivo

##### Configuring APPID and APPKey
Open the `android/app/build.gradle` file and configure `APPID` and `App_Key` of vivo as follows:

```
      android: {
        defaultConfig {
          manifestPlaceholders = [
            ....
            vivo_APPID: "vivo `APPID`"
            vivo_APPKEY:"vivo `APP_Key`",
            .....
          ]
        }
      }
```

Open the `android/app/src/main/AndroidManifest.xml` file and add `meta-data` to `<application>` as follows:

```xml
    <meta-data
        android:name="com.vivo.push.api_key"
        android:value="Enter the vivo API_KEY that you obtained" />
    <meta-data
        android:name="com.vivo.push.app_id"
        android:value="Enter the vivo API_ID that you obtained" />
</application>
```

##### vivo badge permission

Open the `android/app/src/main/AndroidManifest.xml` file and add the following `uses-permission` information:

```xml
<uses-permission android:name="com.vivo.notification.permission.BADGE_ICON" />
```

#### Mi/OPPO/Meizu

1. Open the `android/app/build.gradle` file and add the package name to `defaultConfig`.
```
defaultConfig {
    applicationId "${Enter your package name}"
    ...
}
```
2. Open the `android/app/src/main/AndroidManifest.xml` file and configure permissions for each vendor.
```xml
    <!--Mi Start-->
    <permission
        android:name="${Enter your package name}.permission.MIPUSH_RECEIVE"
        android:protectionLevel="signature" />
    <uses-permission android:name="${Enter your package name}.permission.MIPUSH_RECEIVE" />
    <!--Mi End-->

    <!--OPPO Start-->
    <uses-permission android:name="com.coloros.mcs.permission.RECIEVE_MCS_MESSAGE" />
    <uses-permission android:name="com.heytap.mcs.permission.RECIEVE_MCS_MESSAGE" />
    <!--OPPO End-->
    
    <!--Meizu Start-->
    <!-- It is optional and used for compatibility with Flyme OS 5 and push services on earlier versions.-->
    <uses-permission android:name="android.permission.READ_PHONE_STATE" />
    <!-- Permission configuration for compatibility with Flyme OS 5-->
    <uses-permission android:name="com.meizu.flyme.push.permission.RECEIVE" />
    <permission android:name="${Enter your package name}.push.permission.MESSAGE"
        android:protectionLevel="signature"/>
    <uses-permission android:name="${Enter your package name}.push.permission.MESSAGE" />
    <!-- Permission configuration for compatibility with Flyme OS 3-->
    <uses-permission android:name="com.meizu.c2dm.permission.RECEIVE" />
    <permission android:name="${Enter your package name}.permission.C2D_MESSAGE" android:protectionLevel="signature"
        />
    <uses-permission android:name="${Enter your package name}.permission.C2D_MESSAGE"/>
    <!--Meizu End-->
```

### Step 3. Perform initialization upon application start[](id:step_3)
1. Call the `init` method of the plugin to initialize the vendor channels.
2. We recommend you call the method upon application start.
>?As Google services are not available for most of the Android devices in the Chinese mainland, the `isUseGoogleFCM` switch is provided for you to determine whether to enable Google FCM based on the user group.

```Dart
import 'package:tim_ui_kit_push_plugin/tim_ui_kit_push_plugin.dart';

final TimUiKitPushPlugin cPush = TimUiKitPushPlugin(
  isUseGoogleFCM: bool, // Whether to enable Google FCM. The default value is `true`.
);
cPush.init(
    pushClickAction: pushClickAction, // Callback for the event upon notification click, which is as detailed in step 6.
    appInfo: PushConfig.appInfo, // Pass in the `appInfo` in step 1
);
```
3. After the initialization, you need to call the `createNotificationChannel` method to create message channels for some vendors, such as OPPO and Mi.
>?If the channel IDs obtained from the vendor are the same, it is okay to call the channel ID only once.
```Dart
cPush.createNotificationChannel(
  channelId: "new_message", 
  channelName: "message push", 
  channelDescription: "push new messages");
```
4. The push permission is not provided by some vendors (such as OPPO) by default and needs to be applied for by calling the `requireNotificationPermission` method.
>?You can apply for the permission when appropriate, such as, after the user logs in.

```Dart
cPush.requireNotificationPermission();
```

### Step 4. Report the token and certificate ID[](id:step_4)

The vendor certificate ID and device token need to be reported to the IM console before vendor channels can be used by the server to issue notifications.

The plugin automatically locates the certificate ID of the current vendor in `appInfo` and reports the token.

>?
>- Call the method to report the information after user login, as required by privacy protection laws.
>- Use the same token for the same device, which needs to be reported only once upon login, rather than each time the application is started.

``` Dart
import 'package:tim_ui_kit_push_plugin/tim_ui_kit_push_plugin.dart';

final TimUiKitPushPlugin cPush = TimUiKitPushPlugin(
    isUseGoogleFCM: false,
  );

final bool isUploadSuccess = await cPush.uploadToken(PushConfig.appInfo);
```

### Step 5. Listen for the foreground/background switch[](id:step_5)
1. The current status of the application needs to be reported to the IM backend through the IM SDK upon each foreground/background switch.
2. If the application is in the foreground, the notification push will not be triggered when a new message is received; otherwise, it will be triggered.
3. For more information, see [How do I listen to Android activity lifecycle events?](https://docs.flutter.dev/get-started/flutter-for/android-devs#how-do-i-listen-to-android-activity-lifecycle-events).

We recommend you use the `setBadgeNum( int badgeNum )` method in the plugin before the application switches to the inactive/paused status, so as to update the latest unread count to the desktop badge. The iOS badge is automatically managed by the IM SDK. Here, the plugin supports configuring badges of Mi (MIUI 6 to MIUI 11), Huawei, Honor, vivo, and OPPO.

>? The OPPO badge is an advanced feature offered by OPPO and not available by default. To use it, contact the OPPO contact for application push.

  ```Dart
  /// coreInstance
  @override
  Future<V2TimCallback> setOfflinePushStatus({required AppStatus status, int? totalCount}) {
    if(Platfrom.isIOS){
      return;
    }
    if(status == AppStatus.foreground){
      // Report `doForeground()` when the application is in the foreground
      return TencentImSDKPlugin.v2TIMManager
          .getOfflinePushManager()
          .doForeground();
    }else{
      // Report `doBackground()` along with the unread count when the application is in the background
      return TencentImSDKPlugin.v2TIMManager
          .getOfflinePushManager()
          .doBackground(unreadCount: totalCount ?? 0);
    }
  }

  /// App
  final TimUiKitPushPlugin cPush = TimUiKitPushPlugin(
      isUseGoogleFCM: false,
    );
    
  @override
  void didChangeAppLifecycleState(AppLifecycleState state) async {
    print("--" + state.toString());
    int? unreadCount = await _getTotalUnreadCount();
    switch (state) {
      case AppLifecycleState.inactive: 
        _coreInstance.setOfflinePushStatus(status: AppStatus.background, totalCount: unreadCount);
        if(unreadCount != null){
          cPush.setBadgeNum(unreadCount);
        }
        break;
      case AppLifecycleState.resumed:
        _coreInstance.setOfflinePushStatus(status: AppStatus.foreground);
        break;
      case AppLifecycleState.paused: 
        _coreInstance.setOfflinePushStatus(status: AppStatus.background, totalCount: unreadCount);
        if(unreadCount != null){
          cPush.setBadgeNum(unreadCount);
        }
        break;
    }
  }
  ```

### Step 6. Configure offline push upon message sending and redirect upon notification click[](id:step_6)

#### Sending messages


##### Sending a message through the SDK
If you connect to the IM SDK on your own, configure the `OfflinePushInfo offlinePushInfo` field when sending a message.
```Dart
OfflinePushInfo({
    this.title = '', // Push notification title. When this string is left empty, the IM backend will automatically replace it with the sender nickname or, if the sender nickname is unavailable, the sender ID. Therefore, we recommend you leave it empty unless you have special needs.
    this.desc = '', // Push the second line
    this.disablePush = false,
    this.ext = '', // Extra information in the push, which can be obtained after the redirect upon notification click. We recommend you pass in the JSON string containing conversation information, so that the receiver can be redirected to the corresponding chat. For more information, see the following TUIKit instance code.
    this.androidOPPOChannelID = '', // OPPO channel ID
  });
```

##### Connecting to TUIKit

If you use TUIKit for Flutter, you can define the custom push by using `notificationTitle`/`notificationOPPOChannelID`/`notificationBody`/`notificationExt`/`notificationIOSSound` in `TIMUIKitChatConfig` of the `TIMUIKitChat` component as follows:
```Dart
TIMUIKitChat(
    config: TIMUIKitChatConfig(
            notificationTitle: "",// Push notification title. When this string is left empty, the IM backend will automatically replace it with the sender nickname or, if the sender nickname is unavailable, the sender ID. Therefore, we recommend you leave it empty unless you have special needs, which delivers the same experience as WeChat.
            notificationOPPOChannelID: "", // OPPO channel ID configured for message push
            notificationBody: (V2TimMessage message, String convID, ConvType convType) {
              return "the second line of the push you customize based on the given parameters";
            },
            notificationExt: (V2TimMessage message, String convID, ConvType convType) {
              // The `ext` field you customize based on the given parameters. We recommend you pass in the conversation ID in JSON format as follows:
              String createJSON(String convID){
                return "{\"conversationID\": \"$convID\"}";
              }
              String ext =  (convType == ConvType.c2c
                  ? createJSON("c2c_${message.sender}")
                  : createJSON("group_$convID"));
              return ext;
            }
        )
)

```

#### Processing the click callback 
1. Enter the callback method configured for `pushClickAction` in [step 3](#step_3).
2. During initialization, register the callback method to get the `Map` containing the push body and `ext` information.
3. If the JSON string containing `conversationID` is passed in for `ext` when `OfflinePushInfo` is created in the previous step, the receiver will be directly redirected to the corresponding chat.

>?If the receiver is redirected when the application is in the background, the Flutter homepage may have been unmounted and cannot provide a context for the redirect. Therefore, we recommend you cache a context upon start to ensure the success of the redirect.
>
>We recommend you call the `clearAllNotification()` method to clear other notifications on the notification bar after the redirect to avoid too many IM messages.

```Dart
BuildContext? _cachedContext;
final TimUiKitPushPlugin cPush = TimUiKitPushPlugin(
      isUseGoogleFCM: false,
    );
// TUIKit only
final TIMUIKitChatController _timuiKitChatController =
  TIMUIKitChatController();

@override
void initState() {
  super.initState();
  _cachedContext = context;
}

void handleClickNotification(Map<String, dynamic> msg) async {
    String ext = msg['ext'] ?? "";
    Map<String, dynamic> extMsp = jsonDecode(ext);
    String convId = extMsp["conversationID"] ?? "";

    // [TUIKit] Do not redirect if the current conversation is the target conversation
    final currentConvID = _timuiKitChatController.getCurrentConversation();
    if(currentConvID == convId.split("_")[1]){
      return;
    }

    final targetConversationRes = await TencentImSDKPlugin.v2TIMManager
        .getConversationManager()
        .getConversation(conversationID: convId);

    V2TimConversation? targetConversation = targetConversationRes.data;

    if(targetConversation != null){
      cPush.clearAllNotification();
      Navigator.push(
          _cachedContext ?? context,
          MaterialPageRoute(
            builder: (context) => Chat(
              selectedConversation: targetConversation,
            ),
          ));
    }
  }
```

### Step 7. Use TRTC to make one-to-one audio/video calls and send offline push[](id:step_7)

In general, you can start a TRTC call and use a signaling message to notify the receiver. In the signaling message, you can add the `offlinePushInfo` field as instructed in [step 6](#step_6).

#### Connecting to the Flutter call plugin
1. If you use the [tim_ui_kit_calling_plugin](https://pub.dev/packages/tim_ui_kit_calling_plugin) plugin, you need to upgrade it to v0.2.0 or later to use the offline push capability.
2. Pass in the `offlinePush` object in the third parameter of the `call` method as follows:
```Dart
final user = await sdkInstance.getLoginUser();
final myId = user.data;
OfflinePushInfo offlinePush = OfflinePushInfo(
  title: "",
  desc: "make an audio call to you",
  ext: "{\"conversationID\": \"c2c_$myId\"}",
  disablePush: false,
  ignoreIOSBadge: false,
  androidOPPOChannelID: PushConfig.OPPOChannelID
);

_calling?.call(widget.selectedConversation.userID!, CallingScenes.Audio, offlinePush);
```

>? Offline push is not supported for group call invitations.

## Using the Plugin to Run the Offline Push (iOS)
This section describes the steps required by iOS different from those required by Android to use the plugin to run the offline push.

Steps not mentioned here are the same as those for Android.

### Step 2. Add the iOS project configuration to the code
1. Use Xcode to open your project and configure the **Signing Profile** that supports **Push** in **Runner**>**Target**.
2. Add the `Push Notification` capability in the top-left corner.

3. Run `flutter pub get` to install the plugin, enter the iOS directory, and run `pod install` to install the dependency library.
4. Add the following code to the `didFinishLaunchingWithOptions` method of the `ios/Runner/AppDelegate.swift` file in the iOS project.
Objective-C:
```objc
if (@available(iOS 10.0, *)) {
  [UNUserNotificationCenter currentNotificationCenter].delegate = (id<UNUserNotificationCenterDelegate>) self;
}
```
Swift:
```swift
if #available(iOS 10.0, *) {
  UNUserNotificationCenter.current().delegate = self as? UNUserNotificationCenterDelegate
}
```
5. If you don't use the Firebase Emulator Suite, you need to add the following field to `info.plist`.
```xml
<key>flutter_apns.disable_firebase_core</key>
<false/>
```

### Step 3. Perform initialization upon application start
Call the `init` method of the plugin to initialize vendor channels and request the vendor notification permission. We recommend you call the method upon application start.
```Dart
import 'package:tim_ui_kit_push_plugin/tim_ui_kit_push_plugin.dart';

final TimUiKitPushPlugin cPush = TimUiKitPushPlugin();
cPush.init(
    pushClickAction: pushClickAction, // Callback for the event upon notification click, which is as detailed in step 6.
    appInfo: PushConfig.appInfo, // Pass in the `appInfo` in step 1
);
```

### Step 6. Configure offline push upon message sending and redirect upon notification click
#### Sending messages


##### Sending a message through the SDK
  If you connect to the IM SDK on your own, configure the `OfflinePushInfo offlinePushInfo` field when sending a message.
```Dart
OfflinePushInfo({
    // Other configurations
    this.iOSSound = "", // iOS offline push sound settings. `iOSSound = kIOSOfflinePushNoSound` indicates not to play back the system sound when a message is received; `iOSSound = kIOSOfflinePushDefaultSound` indicates to play back the system sound when a message is received. To customize `iOSSound`, you need to link the audio file to the Xcode project and pass in the filename (with the extension) to `iOSSound`.
    this.ignoreIOSBadge = false,
  });
```

##### Connecting to TUIKit
If you use TUIKit for Flutter, you can define the custom push by using `notificationTitle`/`notificationOPPOChannelID`/`notificationBody`/`notificationExt`/`notificationIOSSound` in `TIMUIKitChatConfig` of the `TIMUIKitChat` component as follows:
```Dart
TIMUIKitChat(
    config: TIMUIKitChatConfig(
            // Other configurations
            notificationIOSSound: "", // iOS offline push sound settings. `iOSSound = kIOSOfflinePushNoSound` indicates not to play back the system sound when a message is received; `iOSSound = kIOSOfflinePushDefaultSound` indicates to play back the system sound when a message is received. To customize `iOSSound`, you need to link the audio file to the Xcode project and pass in the filename (with the extension) to `iOSSound`.
        )
)
```


## Debugging

### Offline push check

You can use the [Push Message Tool](https://console.cloud.tencent.com/im/tool-push-check) to detect the terminal status/certificate reporting and send test messages.

### Debugging on vivo[](id:vivotest)
vivo requires that an application not have the permission to use its push capabilities before launch on vivo APP STORE. For more information, see [here](https://dev.vivo.com.cn/documentCenter/doc/151).
During development, you need to perform debugging in the following steps:
1. Get the `regId` (or device token) of the test device (vivo phone).
2. Add the device as the test device in the vivo console.

3. Push test messages to the device as instructed [here](https://dev.vivo.com.cn/documentCenter/doc/363#w2-98542835).
4. As you cannot change the push mode to the test mode for the test push in the IM console or the message push through the IM SDK, you need to use our JavaScript script that can trigger test messages, which can be downloaded [here](https://tuikit-1251787278.cos.ap-guangzhou.myqcloud.com/testvivo.js).
5. After the download, enter the vivo parameters based on the five comment rows at the top. By default, `ext` is `conversationID`. If you need other fields when processing the callback for notification click (see [step 6](#step_6)), you can modify the JavaScript code.

6. Run `npm install axios`, `npm install js-md5`, and then `node testvivo`, and the push result will be displayed in the last row of the log.

7. At this point, the test terminal can receive the test message push. After the message is clicked, the callback at the Dart layer will be triggered.

## Vendor's Push Restrictions

1. All vendors in China have adopted message classification mechanisms, and different push policies are assigned for different types of messages. To make the push timely and reliable, you need to set the push message type of your app as the system message or important message with a high priority based on the vendor's rules. Otherwise, offline push messages are affected by the vendor's push message classification and may vary from your expectations.

2. In addition, some vendors set limits on the daily volumes of app push messages. You can check such limits in the vendor's console.
If offline push messages are not pushed timely or cannot be received, consider the following:
- Huawei: Push messages are classified into service & communication messages and news & marketing messages with different push effects and policies. In addition, message classification is associated with the self-help message classification permission.
  - If there is no self-help message classification permission, the vendor will perform secondary intelligent message classification on push messages.
  - If you have applied for the self-help message classification permission, push messages will be classified based on the custom classification and then pushed.
  For more information, see [Message Classification Criteria](https://developer.huawei.com/consumer/cn/doc/development/HMSCore-Guides/message-classification-0000001149358835).

- vivo: Push messages are classified into system messages and operational messages with different push effects and policies. The system messages are further subject to the vendor's intelligent classification for correction. A message that cannot be intelligently identified as a system message will be automatically corrected as an operational message. If the judgment is incorrect, you can give a feedback by email. In addition, the total number of push messages is subject to a daily limit determined based on the app subscription statistics by the vendor. 
See [vendor description 1](https://dev.vivo.com.cn/documentCenter/doc/359) or [vendor description 2](https://dev.vivo.com.cn/documentCenter/doc/156) for details.

- OPPO: Push messages are classified into private messages and public messages with different push effects and policies. Private messages are those that a user pays certain attention to and wants to receive in time. The private message channel permission needs to be applied for via email. The public message channel is subject to a number limit.
See [vendor description 1](https://open.oppomobile.com/wiki/doc#id=11227) or [vendor description 2](https://open.oppomobile.com/wiki/doc#id=11210) for details.

- Mi: Push messages are classified into important messages and general messages with different push effects and policies. In particular, only instant messages, reminders of attracted events, agenda reminders, order status change, financial reminders, personal status change, resource changes, and device reminders fall into the important message category. The important message channel can be applied for in the vendor's console. General push messages are subject to a number limit.
See [vendor description 1](https://dev.mi.com/console/doc/detail?pId=2422) or [vendor description 2](https://dev.mi.com/console/doc/detail?pId=2086) for details.

- Meizu: Push messages are subject to a number limit. For details, see [here](http://open.res.flyme.cn/fileserver/upload/file/202201/85079f02ac0841da859c1da0ef351970.pdf).

- FCM: Upstream message push is subject to a frequency limit.
See [vendor description](https://firebase.google.com/docs/cloud-messaging/concept-options?hl=en#upstream_throttling) for details.

## How do I troubleshoot if I cannot receive offline push messages?
### 1. OPPO devices
This generally occurs for the following reasons:
- According to requirements on the official website of OPPO Push, ChannelID must be configured on OPPO mobile phones that run Android 8.0 or later versions. Otherwise, push messages cannot be displayed. For the configuration method, see [OPPO Push configuration](https://intl.cloud.tencent.com/document/product/1047/39156).
- The [custom content in the message for pass-through offline push](https://intl.cloud.tencent.com/document/product/1047/39156) is not in the JSON format. As a result, OPPO mobile phones do not receive the push message.
- The notification bar display feature is disabled by default for applications installed on the OPPO device. If this is the case, check the switch status.

### 2. Sending custom messages
Custom messages are pushed offline differently from ordinary messages. Custom message content cannot be parsed, so the push content cannot be determined. Therefore, custom messages are not pushed by default. If you want to push them, you need to set the `desc` field of `offlinePushInfo` when calling `sendMessage`, after which `desc` will be displayed by default during the push.

### 3. Notification bar settings of the device
The offline push message can be intuitively displayed in the notification bar, so, just as other notifications, it is subject to the notification settings of the device. Take a Huawei device as an example.

- "Settings - Notifications - Notifications (Lock Screen) - Hide or Do not Disturb" will affect the display of offline push notifications when the screen is locked.
- "Settings - Notifications - Advanced Settings - Show Notification Icons (Status Bar)" will affect the showing of the offline push notification icon in the status bar.
- "Settings - Notifications - Application Notifications - Allow Notifications" will directly affect the display of offline push notifications.
- "Settings - Notifications - Application Notifications - Notification Sound" and "Settings - Notifications - Application Notifications - Notification Mute" will affect the offline push notification sound.

### 4. The failure still exists after integration as instructed
- First, test whether messages can be properly pushed offline by using the [offline test tool](https://console.cloud.tencent.com/im/tool-push-check) in the IM console.
If offline push does not work properly, and the device status is exceptional, check the parameters in the IM console and then check the code initialization and registration logic, including the vendor push service registration and IM offline push configuration.
If offline push does not work properly but the device status is normal, check whether the ChannelID is correct or whether the backend service is working properly.
- The offline push relies on vendor capabilities, and some simple characters may be filtered out and cannot be pushed. For example, OPPO requires that the `ext` field be in JSON format.
- If offline push messages are not pushed timely or cannot be received, you need to check the vendor's push restrictions.


## Online Push - Creating a Local Message Notification[](id:online_push)

The section above describes how to use the plugin and the IM backend push capabilities to implement offline push through vendor channels.

However, vendor offline push doesn't apply in some cases, for example, when a Huaqiangbei-customized Android device, rather than a compatible model, is used.

In this case, you can only listen for the message receiving callback online and manually trigger the notification creation on the client. This method applies only when your application is not killed but is in the foreground or background and can communicate with the IM server.

In view of this, the plugin v0.3 offers two new methods to create a local message, that is, `displayNotification` for notification customization and `displayDefaultNotificationForMessage` for default notification generation based on the message. You can select one as needed.

### Preparing for integration

Install the IM for Flutter push plugin in your project:

```shell
flutter pub add tim_ui_kit_push_plugin
```



#### Android

1. Make sure that `@mipmap/ic_launcher` exists as your application icon. The complete path is `android/app/src/main/res/mipmap/ic_launcher.png`.
![](https://qcloudimg.tencent-cloud.cn/raw/8c4fb573992469301a9980c7372423ee.png)

If it doesn't exist, you can manually copy your application icon or automatically create a version of a different resolution through Android Studio (right-click the `mipmap` directory and select **New** > **Image Asset**).
![](https://qcloudimg.tencent-cloud.cn/raw/a688f809d1caa87525b694808bcec2ba.png)

2. Open the `android/app/src/main/AndroidManifest.xml` file and add the following code to the main `activity` of your application:
```xml
<activity
    android:showWhenLocked="true"
    android:turnScreenOn="true">
```

#### iOS

If you have configured iOS offline push, you can skip this section; if not, you need to add the following code to the `didFinishLaunchingWithOptions` function of the `ios/Runner/AppDelegate.swift` or `ios/Runner/AppDelegate.m` file. For detailed directions, see the demo.

Objective-C:
```objc
if (@available(iOS 10.0, *)) {
  [UNUserNotificationCenter currentNotificationCenter].delegate = (id<UNUserNotificationCenterDelegate>) self;
}
```

Swift:
```swift
if #available(iOS 10.0, *) {
  UNUserNotificationCenter.current().delegate = self as? UNUserNotificationCenterDelegate
}
```

### Initializing the plugin

After initializing the IM SDK, initialize the push plugin and instantiate a `cPush` plugin for subsequent calls.

```dart
final TimUiKitPushPlugin cPush = TimUiKitPushPlugin();

cPush.init(
  // Bind the function for the redirect upon notification click, which is as detailed below
  pushClickAction: onClickNotification,
);
```

### Listening for the notification triggered by the new message callback

#### Listening for `V2TimAdvancedMsgListener`

If you have mounted `V2TimAdvancedMsgListener`, skip this section; otherwise, mount the listener after IM login.

Below is the code:
```dart
final advancedMsgListener = V2TimAdvancedMsgListener(
  onRecvNewMessage: (V2TimMessage newMsg) {
    // Listen for the event triggered by the callback
    // Call the creation method in the next step here
  }, 
});

TencentImSDKPlugin.v2TIMManager
        .getMessageManager()
        .addAdvancedMsgListener(listener: advancedMsgListener);
```



#### Triggering local message notification

Select the `displayNotification` API for notification customization or `displayDefaultNotificationForMessage` API for default notification generation based on the message as needed.

For Android, you need to pass in `channelID` and `channelName` for both of the APIs. If no [Android push channels](https://developer.android.com/training/notify-user/channels) are created, you need to create one by using the `createNotificationChannel` API of the plugin.

```dart
cPush.createNotificationChannel(
        channelId: "new_message",
        channelName: "message push",
        channelDescription: "push new messages");
```

##### `displayNotification`

This API requires `title`, `body`, and `ext` for the redirect. You can parse the `V2TimMessage` as needed to generated them.



To facilitate the redirect, view the `displayDefaultNotificationForMessage` code for the `ext` generation rule.

```dart
cPush.displayNotification(
  channelID: "new_message",
  channelName: "message push",
  title: "",
  body: "",
  ext: ""
);
```

##### `displayDefaultNotificationForMessage`

We recommend you use this API to automatically generate a notification based on `V2TimMessage`.

You only need to pass in a `V2TimMessage` object.

```dart
cPush.displayDefaultNotificationForMessage(
        message: message, channelID: "new_message", channelName: "message push");
```

### Notification tap-to-redirect

Like the callback for click in [step 6](#step_6), this callback is in `ext`. It reads and redirects the receiver to the corresponding conversation.

If you use `displayDefaultNotificationForMessage` in the previous step or use the `ext` generation function identical to the default in `displayNotification`, the `ext` structure will be `"conversationID": "corresponding conversation"`.

Enter the callback method configured for `pushClickAction`.

During initialization, register the callback method to get the `Map` containing the push body and `ext` information.

>? If the receiver is redirected when the application is in the background, the Flutter homepage may have been unmounted and cannot provide a context for the redirect. Therefore, we recommend you cache a context upon start to ensure the success of the redirect.
>
>We recommend you call the `clearAllNotification()` method to clear other notifications on the notification bar after the redirect to avoid too many IM messages.

```Dart
BuildContext? _cachedContext;
final TimUiKitPushPlugin cPush = TimUiKitPushPlugin(
      isUseGoogleFCM: false,
    );
// TUIKit only
final TIMUIKitChatController _timuiKitChatController =
  TIMUIKitChatController();

@override
void initState() {
  super.initState();
  _cachedContext = context;
}

void onClickNotification(Map<String, dynamic> msg) async {
    String ext = msg['ext'] ?? "";
    Map<String, dynamic> extMsp = jsonDecode(ext);
    String convId = extMsp["conversationID"] ?? "";

    // [TUIKit] Do not redirect if the current conversation is the target conversation
    final currentConvID = _timuiKitChatController.getCurrentConversation();
    if(currentConvID == convId.split("_")[1]){
      return;
    }

    final targetConversationRes = await TencentImSDKPlugin.v2TIMManager
        .getConversationManager()
        .getConversation(conversationID: convId);

    V2TimConversation? targetConversation = targetConversationRes.data;

    if(targetConversation != null){
      cPush.clearAllNotification();
      Navigator.push(
          _cachedContext ?? context,
          MaterialPageRoute(
            builder: (context) => Chat(
              selectedConversation: targetConversation,
            ),
          ));
    }
  }
```

If you customize the `ext` structure, you need to implement the redirect function on your own.

At this point, you have connected to online push. After the test, you can define the time and scenario for triggering a push notification in `onRecvNewMessage`.
