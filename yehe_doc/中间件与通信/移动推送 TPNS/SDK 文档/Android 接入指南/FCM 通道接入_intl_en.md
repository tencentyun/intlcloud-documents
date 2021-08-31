

## Overview
The FCM channel is a system-level push channel provided by Google. On mobile phones with the Google service framework, as the background processes are managed loosely, push notifications can be received if application processes are not force stopped.

## Directions
### Getting key
Register the application at [FireBase official website](https://firebase.google.com/?hl=zh-cn). Go to **Firebase Project**, **select a specific project application**, click **Settings** > **Cloud Messaging** to get the FCM application push **server key**, and enter it in **[TPNS Console](https://console.cloud.tencent.com/tpns)** > **Configuration Management** > **Basic Configuration** > **FCM Push Channel**.

### Configuration
1. Configure the `google-services.json` file as shown below:
![](https://main.qcloudimg.com/raw/568561b72a775058bf06750bfab38ed0.png)
2. Configure gradle to integrate the Google service.
  1. Add the following code to the `dependencies` node in the project-level `build.gradle` file:
```xml
classpath 'com.google.gms:google-services:4.2.0'
```
>!Note: if you use a version below 4.2.0, the following message will be displayed: `FCM Register error! java.lang.IllegalStateException: Default FirebaseApp is not initialized in this process com.qq.xg4all. Make sure to call FirebaseApp.initializeApp(Context) first.` We recommend you add `YOUR_GOOGLE_APP_ID` to `string.xml` in the `res/values` folder.

  2. Add dependencies to the application-level `build.gradle` file:
	```xml
	  implementation 'com.tencent.tpns:fcm:[VERSION]-release' // FCM push [VERSION] is the version number of the current SDK, which can be viewed on the SDK for Android updates page
      implementation  'com.google.firebase:firebase-messaging:17.6.0'

	 // In the application-level gradle file, add the following to the last line of the code and put `google-services.json` into the root path of your application model
	apply plugin: 'com.google.gms.google-services'
	```
>!
>- FCM push [VERSION] is the version number of the current SDK, which can be viewed in [SDK for Android Updates](https://intl.cloud.tencent.com/document/product/1024/36191).
>- Google configures `google-play-services` (we recommend you use a version higher than 17.0.0; otherwise, you may not be able to register for FCM).

### Enabling FCM push
Add the following code setting before the TPNS calling registration code (XGPushManager.registerPush):

```java
XGPushConfig.enableOtherPush(this, true);
```
The log of a successful FCM registration is as follows:

```xml
V/TPush: [XGPushConfig] isUsedOtherPush:true
I/TPush: [OtherPush] checkDevice pushClassNamecom.tencent.android.tpush.otherpush.fcm.impl.OtherPushImpl
I/TPush: [XGPushManager] other push token is : dSJA5n4fSZ27YeDf2rFg1A:APA91bGiqSPCMZTuyup**********f1fBIahZKYkth2OoDpixDPQmEZkQ11fX06mw_1kEaW5-jFmT4YwlER4qfX66h_BIoUxOyj_tKqZSUg7oHigIKaOrDWmMQfMAqGoT8qSfg  other push type: fcm
```

