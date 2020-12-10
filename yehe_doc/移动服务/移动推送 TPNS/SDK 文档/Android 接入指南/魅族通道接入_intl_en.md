## Overview
The Meizu push channel is a system-level push channel **officially provided by Meizu**. On a Meizu phone, push messages can be delivered through Meizu's system channel without opening the application.

>?
>- For the Meizu push channel, the notification title cannot contain more than 32 characters, and the notification content cannot contain more than 100 characters.
>- The Meizu push channel does not support in-app messages.
>- The Meizu channel supports arrival callback and click callback but not passthrough.

## Directions
### Getting key
1. Enter [Meizu Push official website](https://open.flyme.cn/open-web/views/push.html), sign up for a developer account and log in, and get three key parameters of `AppID`, `AppKey`, and `AppSecret`. For more information, please see the [Meizu development documentation](http://open.res.flyme.cn/fileserver/upload/file/201709/a271468fe23b47408fc2ec1e282f851f.pdf).
2. Copy and paster the `AppId`, `AppKey`, and `AppSecret` parameters of the application into **[TPNS Console](https://console.cloud.tencent.com/tpns)** > **Configuration Management** > **Basic Configuration** > **Meizu Official Push Channel**.


### Integration steps
#### Integrating through Android Studio
```js
implementation 'com.tencent.tpns:meizu:[VERSION]-release'// Meizu Push [VERSION] is the version number of the current SDK, which can be viewed in SDK for Android Updates
```
>? Meizu Push [VERSION] is the version number of the current SDK, which can be viewed in [SDK for Android Updates](https://intl.cloud.tencent.com/document/product/1024/36191).

#### Integrating through Eclipse
1. Download the [SDK installation package](https://console.cloud.tencent.com/tpns/sdkdownload).
2. Open the `Other-Push-jar` folder and import the jar packages related to Meizu Push. Import `mz4tpns1.1.2.1.jar` to the project folder:
3. Configure the following content under Android manifest:

```xml
<application>
<service
                 android:name="com.meizu.cloud.pushsdk.NotificationService"
                 android:exported="true"/>
<receiver android:name="com.meizu.cloud.pushsdk.SystemReceiver" >
 <intent-filter>
                <action android:name="com.meizu.cloud.pushservice.action.PUSH_SERVICE_START"/>
                <category android:name="android.intent.category.DEFAULT" />
 </intent-filter>
 </receiver>
</application>
 <!-- Note: this is the beginning of permission required by Meizu Push -->
 <!-- Compatible with Flyme versions below 5.0. Meizu's internal integration pushSDK is required; otherwise, messages cannot be received -->
<uses-permission android:name="com.meizu.flyme.push.permission.RECEIVE"></uses-permission>
<permission android:name="application package name.push.permission.MESSAGE" 
                android:protectionLevel="signature"/>
<uses-permission android:name="application package name.push.permission.MESSAGE"></uses-permission>
<!-- Compatible with Flyme 3.0 configuration permissions -->
<uses-permission android:name="com.meizu.c2dm.permission.RECEIVE" />
<permission android:name="application package name.permission.C2D_MESSAGE"
                android:protectionLevel="signature">
</permission>
<uses-permission android:name="application package name.permission.C2D_MESSAGE"/>
<!-- Note: this is the end of permission required by Meizu Push -->
```
4. Meizu message receiver: add `Receiver` in `AndroidManifest.xml` and configure it as follows:

```xml
<receiver android:name="com.tencent.android.mzpush.MZPushMessageReceiver">
    <intent-filter>
        <!-- Receive push message -->
        <action android:name="com.meizu.flyme.push.intent.MESSAGE" />
        <!-- Receive register message -->
         <action android:name="com.meizu.flyme.push.intent.REGISTER.FEEDBACK"/>
        <!-- Receive unregister message -->
         <action android:name="com.meizu.flyme.push.intent.UNREGISTER.FEEDBACK"/>
         <action android:name="com.meizu.c2dm.intent.REGISTRATION" />
         <action android:name="com.meizu.c2dm.intent.RECEIVE" />
         <category android:name="application package name"></category>
     </intent-filter>
</receiver>
```

5. For Meizu phones on Flyme 6.0 or below, you should use manual integration. You need to place an image exactly named `stat_sys_third_app_notify` in the drawable folders with different resolutions. For more information, please see the `flyme-notification-res` folder in the [TPNS SDK for Android](https://console.cloud.tencent.com/tpns/sdkdownload).

### Enabling Meizu push
Configure the following code before starting TPNS and calling `XGPushManager.registerPush`:

```java
// Set Meizu `APPID` and `APPKEY`
XGPushConfig.enableOtherPush(context, true);
XGPushConfig.setMzPushAppId(this, APP_ID);
XGPushConfig.setMzPushAppKey(this, APP_KEY);
```

The log of successful registration is as follows:

```java
// The tokens of TPNS and Meizu are successfully obtained, and the binding is successful, indicating that the registration is successful.
I/TPush: [OtherPushClient] handleUpdateToken other push token is : V5R5b7c02********47744c6b635e464b527e487802 other push type: meizu
I/TPush: [PushServiceBroadcastHandler] >> bind OtherPushToken success ack with [accId = 150000****  , rsp = 0]  token = 0398291156ce7d2f****66bd0952c87c372f otherPushType = meizu otherPushToken = V5R5b7c02********47744c6b635e464b527e487802
```

If you need to get parameters through the click callback or redirect to a custom page, you can use the intent to do so. For more information, please see [Android](https://intl.cloud.tencent.com/document/product/1024/32624).

### Code obfuscation
```xml
-dontwarn com.meizu.cloud.pushsdk.**
-keep class com.meizu.cloud.pushsdk.**{*;}
```
>? If the Meizu token can be normally registered with the Debug version of the application but cannot be obtained from the Release version, please check whether the above code obfuscation rules are added.
- If you use Android Studio 3.4 or higher and the above problem occurs, it is caused by the fact that R8 obfuscation is enabled in Android Studio by default.
Solution: add `android.enableR8 = false` in `gradle.properties`
- Obfuscation rules must be stored in the `proguard-rules.pro` file at the application project level.


### Arrival receipt configuration for Meizu channel
The arrival receipt for the Meizu channel should be configured by yourself. After configuring this feature as instructed in [Receipt Configuration Guide for Meizu Channel](https://cloud.tencent.com/document/product/548/41318#.E9.AD.85.E6.97.8F.E5.8E.82.E5.95.86.E9.80.9A.E9.81.93.E5.9B.9E.E6.89.A7.E9.85.8D.E7.BD.AE.E6.8C.87.E5.BC.95), you can view the arrival data for the Meizu push channel in the push records.

