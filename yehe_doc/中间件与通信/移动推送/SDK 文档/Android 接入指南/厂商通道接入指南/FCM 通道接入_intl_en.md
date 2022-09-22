## Overview 
The FCM channel is a system-level push channel provided by Google. On mobile phones with the Google service framework, as the background processes are managed loosely, push notifications can be received if application processes are not force stopped.

## Directions
### Obtaining a key
FCM PUSH supports the following two methods of key configuration. You just need to choose one of them, but the new proposal method using the server private key is recommended.
1. Server private key (recommended)
Register the application at the [FireBase official website](https://firebase.google.com/?hl=zh-cn). Select **Firebase Projects** > **Select a Project App** > **Settings** > **Service Account** > **Firebase Admin SDK**, and click **Generate a new private key** to get the json file containing the Firebase server private key. Then, go to the [**TPNS console**](https://console.cloud.tencent.com/tpns) > **Configuration Management** > **Basic Configuration** > **FCM Push Channel**, select Server Private Key (Recommended), and click **Click to Upload** to upload the above-mentioned json file.
![]()
2. Legacy server key
Register the application at the [FireBase official website](https://firebase.google.com/?hl=zh-cn). Select **Firebase Projects** > **Select a Project App** > **Settings** > **Cloud Messaging** to get the **Server Key** of the FCM app push, and enter the key in the [**TPNS console**](https://console.cloud.tencent.com/tpns) > **Configuration Management** > **Basic Configuration** > **FCM Push Channel**.
![]()
### Configuration
1. Configure the `google-services.json` file.
![](https://main.qcloudimg.com/raw/568561b72a775058bf06750bfab38ed0.png)
2. Configure gradle to integrate the Google service.

   1. Add the following code to the dependencies node in the project-level `build.gradle` file:
```xml
classpath 'com.google.gms:google-services:4.2.0'
```

>! If `FCM Register error! java.lang.IllegalStateException: Default FirebaseApp is not initialized in this process com.qq.xg4all. Make sure to call FirebaseApp.initializeApp(Context) first.` appears for a version below 4.2.0, add `YOUR_GOOGLE_APP_ID` in the `string.xml` file in the `res/values` folder.
>

  2.Add dependencies in the app-level `build.gradle` file:

```xml
	  implementation 'com.tencent.tpns:fcm:[VERSION]-release' // For FCM PUSH, [VERSION] is the version number of the current SDK and can be obtained from "SDK for Android".
      implementation  'com.google.firebase:firebase-messaging:17.6.0'
     // In the app-level gradle file, add the following to the last line of the code and put google-services.json under the root directory of your app model
	apply plugin: 'com.google.gms.google-services'
```
>!
>- For FCM PUSH, [VERSION] is the version number of the current SDK and can be obtained from the [SDK for Android](https://intl.cloud.tencent.com/document/product/1024/36191).
>- Configure `google-play-services` for Google (v17.0.0+ or later recommended; an earlier version may cause FCM registration failure).


### Enabling FCM PUSH
Add the following code before calling the TPNS registration code `XGPushManager.registerPush`:

```java
XGPushConfig.enableOtherPush(this, true);
```
The log of successful FCM registration is as follows:

```xml
V/TPush: [XGPushConfig] isUsedOtherPush:true
I/TPush: [OtherPush] checkDevice pushClassNamecom.tencent.android.tpush.otherpush.fcm.impl.OtherPushImpl
I/TPush: [XGPushManager] other push token is : dSJA5n4fSZ27YeDf2rFg1A:APA91bGiqSPCMZTuyup**********f1fBIahZKYkth2OoDpixDPQmEZkQ11fX06mw_1kEaW5-jFmT4YwlER4qfX66h_BIoUxOyj_tKqZSUg7oHigIKaOrDWmMQfMAqGoT8qSfg  other push type: fcm
```
