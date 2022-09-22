## Overview
The vivo channel is a system-level push channel officially provided by vivo. On a vivo phone, push messages can be delivered through vivo's system channel without opening the application. For more information, please visit [vivo push official website](https://dev.vivo.com.cn/home).

>?
> - If an application cannot be opened after you click the notification on the debugging version, please find the pop-up window permission and enable it for the current application.
> - The vivo channel currently does not support in-app messages, which will be delivered through the TPNS channel.
> - The vivo channel imposes a certain quota limit on the number of daily push messages. For more information, please see [Vendor Channel Limit Description](https://intl.cloud.tencent.com/document/product/1024/35829). When this limit is exceeded, excessive messages will be pushed through the TPNS channel.
> - Operation messages can be pushed through the vivo channel between 7:00 and 23:00, while only system messages can be pushed in other periods. For more information on how to apply for system messages, please see [Applying for vivo system messages](https://intl.cloud.tencent.com/document/product/1024/36250#applying-for-vivo-system-messages).
> - For the vivo channel, the maximum number of operation messages one user can receive from one application per day is 5, while the number of system messages is unlimited.
> - The vivo channel is supported only on certain newer models and corresponding OS versions. For more information, please see [here](https://dev.vivo.com.cn/documentCenter/doc/156#w1-08608733).
> 

## Directions

### Obtaining a key
1. You need to apply to vivo for enabling the push permission so as to get three key parameters, namely, `AppID`, `AppKey`, and `AppSecret`. For more information, please see [Quick Integration Guide](https://dev.vivo.com.cn/documentCenter/doc/180).
>? Only applications that have been approved by and launched to the vivo open platform can be approved by the TPNS service.
>
2. Copy and paste the `AppId`, `AppKey`, and `AppSecret` parameters of the application into **[TPNS console](https://console.cloud.tencent.com/tpns)** -> **Configuration Management** -> **Basic Config** -> **vivo Official Push Channel**.

### Configuration
#### Integrating through Android Studio

Complete the configuration required by TPNS in the `build.gradle` file in the **Application** module and then add the following nodes:
1. Configure vivo's `AppID` and `AppKey`. The sample code is as follows:
```xml
 manifestPlaceholders = [
	 VIVO_APPID:"xxxx",
     VIVO_APPKEY:"xxxxx",
        ]
```
2. Import the dependencies related to vivo. The sample code is as follows:
```js
implementation 'com.tencent.tpns:vivo:[VERSION]-release' //  For vivo pushes, [VERSION] is the SDK's version number, which can be obtained from the release notes of SDK for Android.
```

>? For vivo pushes, [VERSION] is the SDK’s version number, which can be obtained from the release notes of [SDK for Android](https://intl.cloud.tencent.com/document/product/1024/36191).
>


### Integrating through Eclipse
After getting the TPNS SDK package for vivo Push, configure the major TPNS version and the following content in the manual integration method detailed on TPNS's official website.

1. Download the [SDK installation package](https://console.cloud.tencent.com/tpns/sdkdownload).
2. Open the `Other-Push-jar` folder and import the vivo Push-related jar package.
2. Add the following configuration to the `Androidmanifest.xml` file:
```xml
  <application>
	<service
            android:name="com.vivo.push.sdk.service.CommandClientService"
            android:exported="true" />

        <activity
            android:name="com.vivo.push.sdk.LinkProxyClientActivity"
            android:exported="false"
            android:screenOrientation="portrait"
            android:theme="@android:style/Theme.Translucent.NoTitleBar" />

        <!-- Receiver declaration for pushing app's custom messages -->
        <receiver android:name="com.tencent.android.vivopush.VivoPushMessageReceiver" >
            <intent-filter>

                <!-- Receive push message -->
                <action android:name="com.vivo.pushclient.action.RECEIVE" />
            </intent-filter>
        </receiver>

        <meta-data
            android:name="com.vivo.push.api_key"
            android:value="vivo appkey" />
        <meta-data
            android:name="com.vivo.push.app_id"
            android:value="vivo appid" />

</application>
```


### Enabling vivo Push
Enable the third-party push API before calling TPNS' `XGPushManager.registerPush`:
```java
// Enable third-party push
XGPushConfig.enableOtherPush(getApplicationContext(), true);


// The log of successful registration is as follows:
I/TPush: [OtherPushClient] handleUpdateToken other push token is : 160612459******08955218 other push type: vivo
I/TPush: [PushServiceBroadcastHandler] >> bind OtherPushToken success ack with [accId = 150000****  , rsp = 0]  token = 01a22fb503a33******66b89fad6be3ed343 otherPushType = vivo otherPushToken = 160612459******08955218

```

### Code obfuscation

```xml
-dontwarn com.vivo.push.**
-keep class com.vivo.push.**{*; }
-keep class com.vivo.vms.**{*; }
-keep class com.tencent.android.vivopush.VivoPushMessageReceiver{*;}
```

>? Obfuscation rules must be stored in the `proguard-rules.pro` file at the application project level.
>


## Troubleshooting

### Querying vivo Push registration error codes

If you observe logs similar to the following, it indicates that registration with the vivo channel fails. In that case, you can use the method described as below to get the vivo Push registration error code.
```
[OtherPushClient] handleUpdateToken other push token is :  other push type: vivo
```

In debugging mode of the push service, filter logs by the keyword `OtherPush` to view the return code logs, for example, `[OtherPushVivoImpl] vivoPush Register or UnRegister fail, code = 10003`. Then locate the error cause and rectify the error by referring to [Troubleshooting Vendor Channel Registration Failures](https://intl.cloud.tencent.com/document/product/1024/37006).

### Why do I receive the error code 10045 when I push messages with vivo Push?

Official messages cannot be sent during application approval. Please go to the vivo push platform to check the push permission approval progress.
