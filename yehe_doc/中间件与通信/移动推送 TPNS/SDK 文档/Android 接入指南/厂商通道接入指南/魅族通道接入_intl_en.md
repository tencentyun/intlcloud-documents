## Overview
The Meizu push channel is a system-level push channel **officially provided by Meizu**. On a Meizu phone, push messages can be delivered through Meizu's system channel without opening the app.

>?
> - For the Meizu push channel, the notification title can support up to 32 characters, and the notification content can support up to 100 characters.
> - The Meizu push channel does not support in-app messages.
> 

## Directions

### Obtaining a key

1. Go to the [Meizu push website](https://open.flyme.cn) to sign up for a developer account and log in. Then, get the values of the `AppID`, `AppKey`, and `AppSecret`. For more information, see [Meizu Development Documentation](http://open.res.flyme.cn/fileserver/upload/file/201709/a271468fe23b47408fc2ec1e282f851f.pdf).
2. Copy the application's `AppID`, `AppKey`, and `AppSecret` and paste them into [**TPNS console**](https://console.cloud.tencent.com/tpns) > **Configuration Management** > **Basic Configuration** > **Meizu Official Push Channel**.

### Integration methods

#### Integrating through Android Studio

```js
implementation 'com.tencent.tpns:meizu:[VERSION]-release'// For Meizu pushes, [VERSION] is the version number of the current SDK and can be obtained from the "SDK for Android".
```
>? For Meizu pushes, [VERSION] is the version number of the current SDK and can be obtained from the [SDK for Android](https://intl.cloud.tencent.com/document/product/1024/36191).
>

#### Integrating through Eclipse
1. Download the [SDK installation package](https://console.cloud.tencent.com/tpns/sdkdownload).
2. Open the `Other-Push-jar` folder and import the Meizu push-related JAR package. Import `mz4tpns1.1.2.1.jar` to the project folder.
3. Add the following class resource file to the project:
```java
package com.meizu.cloud.pushinternal;
public class R {
    public static final class drawable {
            // Obtain the `stat_sys_third_app_notify.png` resource file from the `flyme-notification-res` folder in `Other-Push-jar` > `meizu` of the TPNS SDK package, and copy it to the resource directory of the application.
        public static final int stat_sys_third_app_notify = com.tencent.android.tpns.demo.R.drawable.stat_sys_third_app_notify;
    }
}
```
4. Add the following configuration to the `AndroidManifest` file:
```xml
<application>
  <!-- Note: This is the beginning of permissions required by Meizu push -->
    <service
        android:name="com.meizu.cloud.pushsdk.NotificationService"
        android:exported="true" />
  <!-- version 4.1.0-->
    <receiver
        android:name="com.meizu.cloud.pushsdk.MzPushSystemReceiver"
        android:exported="false"
        android:permission="com.meizu.flyme.permission.PUSH">
        <intent-filter>
            <action android:name="com.meizu.flyme.push.intent.PUSH_SYSTEM" />
        </intent-filter>
    </receiver>
</application>
<!-- version 4.1.0-->
<uses-permission android:name="com.meizu.flyme.permission.PUSH" />
<!-- version 3.9.0-->
<!-- Note: This is the beginning of permissions required by Meizu push -->
<!-- Compatible with Flyme v5.0 or earlier. Meizu's internal integration pushSDK is required; otherwise, messages cannot be received -->
<uses-permission android:name="com.meizu.flyme.push.permission.RECEIVE"></uses-permission>
<permission
    android:name="${applicationId}.push.permission.MESSAGE"
    android:protectionLevel="signature" />
<uses-permission android:name="${applicationId}.push.permission.MESSAGE"></uses-permission>
<!-- Compatible with Flyme 3.0 configuration permissions -->
<uses-permission android:name="com.meizu.c2dm.permission.RECEIVE" />
<permission
    android:name="${applicationId}.permission.C2D_MESSAGE"
    android:protectionLevel="signature"></permission>
<uses-permission android:name="${applicationId}.permission.C2D_MESSAGE" />
<!-- Note: this is the end of permissions required by Meizu push -->
```
5. Add the following `receiver` configuration in `AndroidManifest.xml`:
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
6. Manual integration is needed for Meizu phones running Flyme v6.0 or earlier. To do so, you need to place an image named exactly `stat_sys_third_app_notify` to the `drawable` folders for each resolution. For more information, download [TPNS Android SDK](https://console.cloud.tencent.com/tpns/sdkdownload) and refer to the `flyme-notification-res` folder in `Other-Push-jar` > `meizu`.

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
I/TPush: [OtherPushClient] handleUpdateToken other push token is: V5R5b7c02********47744c6b635e464b527e487802 other push type: meizu
I/TPush: [PushServiceBroadcastHandler] >> bind OtherPushToken success ack with [accId = 150000****  , rsp = 0]  token = 0398291156ce7d2f****66bd0952c87c372f otherPushType = meizu otherPushToken = V5R5b7c02********47744c6b635e464b527e487802
```

You can use Intent to obtain parameters or redirect to custom pages via click callback. For more information, see [Android FAQs](https://intl.cloud.tencent.com/document/product/1024/32624).

### Code obfuscation

1. Add the following obfuscation rules in the `proguard-rules.pro` file at the application project level.
```
-dontwarn com.meizu.cloud.pushsdk.**
-keep class com.meizu.cloud.pushsdk.**{*;}
```

>? If a debug version of an application can register a Meizu token normally, but the release version cannot, upgrade the SDK to v1.3.2.0 or later.

2. If the application uses the plug-in AndResGuard, add the following in the configuration allowlist of AndResGuard. Skip this step if AndResGuard is not used.
```
whiteList = [
"R.drawable.stat_sys_third_app_notify"
]
```

### Configuring Arrival Receipt for Meizu channel

The arrival receipt for the Meizu channel should be configured by yourself. After configuring this feature as instructed in [Acquisition of Vendor Channel Arrival Receipt](https://intl.cloud.tencent.com/document/product/1024/35246), you can view the arrival data for the Meizu push channel in the push records.
![]()

## Troubleshooting

### Querying Meizu push registration error codes

If you observe logs similar to the following, it indicates that registration with the Meizu channel fails. In that case, you can use the method described as below to get the Meizu push registration error code.
```
[OtherPushClient] handleUpdateToken other push token is :  other push type: mezu
```

In debugging mode of the push service, filter logs by the keyword `OtherPush` to view the return code logs, for example, `[OtherPush_XG_MZ] onRegisterStatus BasicPushStatus{code='110000', message='Invalid appId'}`. Then locate the error cause and rectify the error by referring to [Troubleshooting Vendor Channel Registration Failures](https://intl.cloud.tencent.com/document/product/1024/37006).

### Why do I receive the client/server error code 500 when I push messages through the Meizu channel?

The arrival receipt for the Meizu channel is incorrectly configured. You can configure it by referring to [Receipt Configuration Guide for the Meizu Channel](https://intl.cloud.tencent.com/document/product/1024/35246#receipt-configuration-guide-for-the-meizu-channel).

