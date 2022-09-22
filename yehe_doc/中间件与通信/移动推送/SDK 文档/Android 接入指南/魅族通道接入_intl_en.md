## Overview
The Meizu push channel is a system-level push channel **officially provided by Meizu**. On a Meizu phone, push messages can be delivered through Meizu's system channel without opening the app.

>?
> - For the Meizu push channel, the notification title can support up to 32 characters, and the notification content can support up to 100 characters.
> - The Meizu push channel does not support in-app messages.
> - Meizu channel supports arrival callback and click callback but not passthrough.
> 

## Directions

### Obtaining a key

1. Go to the [Meizu Push website](https://open.flyme.cn/open-web/views/push.html) to sign up for a developer account and log in. Then, get the values of the `AppID`, `AppKey`, and `AppSecret` key parameters. For more information, please see [Meizu Development Documentation](http://open.res.flyme.cn/fileserver/upload/file/201709/a271468fe23b47408fc2ec1e282f851f.pdf).
2. Copy the application's `AppId`, `AppKey`, and `AppSecret` and paste them to [TPNS console](https://console.cloud.tencent.com/tpns) > **Configuration Management** > **Basic Config** > **Meizu Official Push Channel**.

### Integration methods

#### Android Studio integration

```js
implementation 'com.tencent.tpns:meizu:[VERSION]-release'// For Meizu pushes, [VERSION] is the SDK’s version number, which can be obtained from the release notes of SDK for Android.
```
>? For Meizu pushes, [VERSION] is the SDK’s version number, which can be obtained from the release notes of [SDK for Android](https://intl.cloud.tencent.com/document/product/1024/36191).
>

#### Eclipse integration
1. Download the [SDK installation package](https://console.cloud.tencent.com/tpns/sdkdownload).
2. Open the `Other-Push-jar` folder and import the JAR packages related to Meizu Push. Import `mz4tpns1.1.2.1.jar` to the project folder:
3. Perform the following configuration under the Android manifest:
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
 <!-- Note: this is the beginning of permissions required by Meizu Push -->
 <!-- Compatible with Flyme versions below 5.0. Meizu's internal integration pushSDK is required; otherwise, messages cannot be received -->
<uses-permission android:name="com.meizu.flyme.push.permission.RECEIVE"></uses-permission>
<permission android:name="app package name.push.permission.MESSAGE" 
                android:protectionLevel="signature"/>
<uses-permission android:name="app package name.push.permission.MESSAGE"></uses-permission>
<!-- Compatible with Flyme 3.0 configuration permissions -->
<uses-permission android:name="com.meizu.c2dm.permission.RECEIVE" />
<permission android:name="app package name.permission.C2D_MESSAGE"
                android:protectionLevel="signature">
</permission>
<uses-permission android:name="app package name.permission.C2D_MESSAGE"/>
<!-- Note: this is the end of permissions required by Meizu Push -->
```
4. Add the following `receiver` configuration in `AndroidManifest.xml`:
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
         <category android:name="app package name"></category>
     </intent-filter>
</receiver>
```
5. Manual integration is needed for Meizu phones running Flyme 6.0 or earlier. To do so, you need to place an image named exactly `stat_sys_third_app_notify` to the `drawable` folders for each resolution. For more information, please download [TPNS Android SDK](https://console.cloud.tencent.com/tpns/sdkdownload) and refer to the `flyme-notification-res` folder in `Other-Push-jar` > `meizu`.

### Enabling Meizu push

Configure the following code before you start TPNS and call `XGPushManager.registerPush`:
```java
// Set the Meizu AppId and AppKey.
XGPushConfig.enableOtherPush(context, true);
XGPushConfig.setMzPushAppId(this, APP_ID);
XGPushConfig.setMzPushAppKey(this, APP_KEY);
```

The log of successful registration is as follows:
```java
// If the TPNS token and Meizu token are successfully obtained and bound, the registration is successful.
I/TPush: [OtherPushClient] handleUpdateToken other push token is : V5R5b7c02********47744c6b635e464b527e487802 other push type: meizu
I/TPush: [PushServiceBroadcastHandler] >> bind OtherPushToken success ack with [accId = 150000****  , rsp = 0]  token = 0398291156ce7d2f****66bd0952c87c372f otherPushType = meizu otherPushToken = V5R5b7c02********47744c6b635e464b527e487802
```

If you want to obtain parameters or redirect to custom pages via click callback, you can use Intent to implement it. For more information, please see [Android FAQs](https://intl.cloud.tencent.com/document/product/1024/32624).

### Code obfuscation

```xml
-dontwarn com.meizu.cloud.pushsdk.**
-keep class com.meizu.cloud.pushsdk.**{*;}
```
>? If a debug version of an app can register a Meizu token normally, but the release version cannot, please check whether the code obfuscation rules above have been added.
> - If you use Android Studio 3.4 or above, the problem is caused by Android Studio enabling R8 obfuscation by default.
> Solution: Add `android.enableR8 = false` in `gradle.properties`.
> - Obfuscation rules must be stored in the `proguard-rules.pro` file at the application project level.
> 

### Arrival receipt configuration for Meizu channel

The arrival receipt for the Meizu channel should be configured by yourself. After configuring this feature as instructed in [Acquisition of Vendor Channel Arrival Receipt](https://intl.cloud.tencent.com/document/product/1024/35246), you can view the arrival data for the Meizu push channel in the push records.


## Troubleshooting

### Querying Meizu Push registration error codes

If you observe logs similar to the following, it indicates that registration with the Meizu channel fails. In that case, you can use the method described as below to get the Meizu PUSH registration error code.
```
[OtherPushClient] handleUpdateToken other push token is :  other push type: mezu
```

In debugging mode of the push service, filter logs by the keyword `OtherPush` to view the return code logs, for example, `[OtherPush_XG_MZ] onRegisterStatus BasicPushStatus{code='110000', message='Invalid appId'}`. Then locate the error cause and rectify the error by referring to [Troubleshooting Vendor Channel Registration Failures](https://intl.cloud.tencent.com/document/product/1024/37006).

### Why do I receive the client/server error code 500 when I push messages through the Meizu channel?

The arrival receipt for the Meizu channel is incorrectly configured. You can configure it by referring to [Receipt Configuration Guide for the Meizu Channel](https://intl.cloud.tencent.com/document/product/1024/35246#receipt-configuration-guide-for-the-meizu-channel).

