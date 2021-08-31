## Overview
The Mi push channel is a system-level push channel **officially provided by Mi**. On a Mi phone, push messages can be delivered through Mi's system channel without opening the application.

>!
> - The Mi channel supports arrival callback but not click callback.
> - When you test message push through the Mi channel, avoid using words such as `test`; otherwise, the messages will be blocked by Mi and marked as "unimportant messages".
> 

## Directions

### Enabling Mi push service

Enable the push service for the application on **[Mi Open Platform](https://dev.mi.com/console/appservice/push.html)** -> **Push Platform**.


### Obtaining a key

1. Go to the [Mi Open Platform](https://dev.mi.com/console/appservice/push.html), sign up for a Mi developer account, and get three key parameters of `AppId`, `AppKey`, and `AppSecret`. For more information, please see [Quick Connection Guide](https://dev.mi.com/console/doc/detail?pId=708).
2. Copy and paster the `AppId`, `AppKey`, and `AppSecret` parameters of the application into **[TPNS console](https://console.cloud.tencent.com/tpns)** -> **Configuration Management** -> **Basic Configuration** -> **Xiaomi Official Push Channel**.


### Configuration

#### Using JCenter for dependency import

JCenter is recommended for dependency import for AS development. Import the Jar package of Mi Push:
```js
implementation 'com.tencent.tpns:xiaomi:[VERSION]-release' // For Mi pushes, [VERSION] is the SDK's current version number, which can be obtained from the release notes of SDK for Android.
```

>? For Mi pushes, [VERSION] is the SDK's current version number, which can be obtained from the release notes of [SDK for Android](https://intl.cloud.tencent.com/document/product/1024/36191).
>

#### Integrating through Eclipse
1. Download the [SDK installation package](https://console.cloud.tencent.com/tpns/sdkdownload).
2. Open the `Other-Push-jar` folder and import the jar packages related to Mi Push. Import `xm4tpns1.1.2.1.jar` to the project folder.
3. After successful TPNS configuration, add the configuration of Mi Push:
```xml
<application>
    <service
        android:name="com.xiaomi.push.service.XMPushService"
        android:enabled="true"
        android:process=":pushservice" />
    <service
        android:name="com.xiaomi.push.service.XMJobService"
        android:enabled="true"
        android:exported="false"
        android:permission="android.permission.BIND_JOB_SERVICE"
        android:process=":pushservice" />
    <!-- Note: This service must be added for version 3.0.1 and higher -->
    <service
        android:name="com.xiaomi.mipush.sdk.PushMessageHandler"
        android:enabled="true"
        android:exported="true" />
    <service
        android:name="com.xiaomi.mipush.sdk.MessageHandleService"
        android:enabled="true" />
    <!-- Note: This service must be added for version 2.2.5 and higher -->
    <receiver
        android:name="com.xiaomi.push.service.receivers.NetworkStatusReceiver"
        android:exported="true" >
        <intent-filter>
            <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
            <category android:name="android.intent.category.DEFAULT" />
        </intent-filter>
    </receiver>
    <receiver
        android:name="com.xiaomi.push.service.receivers.PingReceiver"
        android:exported="false"
        android:process=":pushservice">
        <intent-filter>
            <action android:name="com.xiaomi.push.PING_TIMER" />
        </intent-filter>
    </receiver>
</application>

<!-- Note: This is the beginning of permission required by Mi Push -->
<permission
    android:name="app package name.permission.MIPUSH_RECEIVE"
    android:protectionLevel="signature" />
<!-- Here, change application package name to the actual application package name -->

<uses-permission android:name="app package name.permission.MIPUSH_RECEIVE" />
<!-- Here, change application package name to the actual application package name -->
<!-- Note: This is the end of the permissions required by Mi Push -->
```
4. Add `receiver` in `AndroidManifest.xml` and configure it as follows:
```xml
<receiver
    android:exported="true"
    android:name="com.tencent.android.mipush.XMPushMessageReceiver">
    <intent-filter>
        <action android:name="com.xiaomi.mipush.RECEIVE_MESSAGE" />
    </intent-filter>
    <intent-filter>
        <action android:name="com.xiaomi.mipush.MESSAGE_ARRIVED" />
    </intent-filter>
    <intent-filter>
        <action android:name="com.xiaomi.mipush.ERROR" />
    </intent-filter>
</receiver>
```

### Enabling Mi Push
Set Mi `AppID` and `AppKey`.
```java
XGPushConfig.setMiPushAppId(getApplicationContext(), "APPID");
XGPushConfig.setMiPushAppKey(getApplicationContext(), "APPKEY");
// Enable third-party push
XGPushConfig.enableOtherPush(getApplicationContext(), true);


// The log of successful registration is as follows:

I/TPush: [OtherPushClient] handleUpdateToken other push token is : 3CvDLfyPRArAGnv****dvQ7rYko+OthWo90rW+Edeqn53RUudp6U1dhySpV35 other push type: xiaomi
I/TPush: [PushServiceBroadcastHandler] >> bind OtherPushToken success ack with [accId = 1500001048  , rsp = 0]  token = 03be2036762f******33bce72d40eb5e677a otherPushType = xiaomi otherPushToken = 3CvDLfyPRArAGnv****dvQ7rYko+OthWo90rW+Edeqn53RUudp6U1dhySpV35G
```

If you need to get parameters through the click callback or redirect to a custom page, you can use the intent to do so. For more information, please see [FAQs for Android](https://intl.cloud.tencent.com/document/product/1024/32624).



### Code obfuscation

```xml
-keep class com.xiaomi.**{*;}
-keep public class * extends com.xiaomi.mipush.sdk.PushMessageReceiver
```

>? Obfuscation rules must be stored in the `proguard-rules.pro` file at the application project level.
>

## Troubleshooting

#### Querying Mi Push registration error codes

If you observe logs similar to the following, it indicates that registration with the Mi channel fails. In that case, you can use the method described as below to get the Mi PUSH registration error code.
```
[OtherPushClient] handleUpdateToken other push token is :  other push type: xiaomi
```

In debugging mode of the push service, filter logs by the keyword `OtherPush` to view the return code logs, for example, `[OtherPush_XG_MI] register failed, errorCode: 22022, reason: Invalid package name: com.xxx.xxx`. Then locate the error cause and rectify the error by referring to [Troubleshooting Vendor Channel Registration Failures](https://intl.cloud.tencent.com/document/product/1024/37006).



