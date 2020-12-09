
## Overview
The Vivo channel is a system-level push channel officially provided by Vivo. On a Vivo phone, push messages can be delivered through Vivo's system channel without opening the application. For more information, please visit [Vivo Push's official website](https://dev.vivo.com.cn/home).

>?
>- If an application cannot be opened after you click the notification on the debugging version, please find the pop-up window permission and enable it for the current application.
>- The Vivo channel currently does not support in-app messages, which will be delivered through the TPNS channel.
>- The Vivo channel imposes a certain quota limit on the number of daily push messages. For more information, please see [Vendor Channel Limit Description](https://intl.cloud.tencent.com/document/product/1024/35829). When this limit is exceeded, excessive messages will be pushed through the TPNS channel.
>- Operation messages can be pushed through the Vivo channel between 7:00 and 23:00, while only system messages can be pushed in other periods. For more information on how to apply for system messages, please see [Vendor Message Categorization Feature Use Instructions](https://intl.cloud.tencent.com/document/product/1024/36250).
>- For the Vivo channel, the maximum number of operation messages one user can receive from one application per day is 5, while the number of system messages is unlimited.
>- The Vivo channel is supported only on certain newer models and corresponding OS versions. For more information, please see [here](https://dev.vivo.com.cn/documentCenter/doc/156#w1-08608733).

## Directions
### Getting key
1. You need to apply to Vivo for enabling the push permission so as to get three keys, namely, `AppID`, `AppKey`, and `AppSecret`. For more information, please see [Quick Integration Guide](https://dev.vivo.com.cn/documentCenter/doc/180).
2. Copy and paster the `AppId`, `AppKey`, and `AppSecret` parameters of the application into **[TPNS Console](https://console.cloud.tencent.com/tpns)** > **Configuration Management** > **Basic Configuration** > **Vivo Official Push Channel**.



### Configuration
#### Integrating through Android Studio

Complete the configuration required by TPNS in the `build.gradle` file in the Application module and then add the following nodes:
1. Configure Vivo's `AppID` and `AppKey`. The sample code is as follows:
```xml
 manifestPlaceholders = [
	 VIVO_APPID:"xxxx",
     VIVO_APPKEY:"xxxxx",
        ]
```
2. Import the dependencies related to Vivo. The sample code is as follows:
```js
implementation 'com.tencent.tpns:vivo:[VERSION]-release' // Vivo Push [VERSION] is the version number of the current SDK, which can be viewed in SDK for Android Updates
```

>? Vivo Push [VERSION] is the version number of the current SDK, which can be viewed in [SDK for Android Updates](https://intl.cloud.tencent.com/document/product/1024/36191).


#### Integrating through Eclipse
After getting the TPNS SDK package for Vivo Push, configure the major TPNS version and the following content in the manual integration method detailed on TPNS's official website.

1. Import the jar packages related to Vivo Push. Import `vivo4tpns1.1.2.1.jar` to the project folder:
2. Add the following configuration to the ```Androidmanifest.xml``` file:

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

        <!-- Receiver declaration for pushing application's custom messages -->
        <receiver android:name="com.tencent.android.vivopush.VivoPushMessageReceiver" >
            <intent-filter>

                <!-- Receive push message -->
                <action android:name="com.vivo.pushclient.action.RECEIVE" />
            </intent-filter>
        </receiver>

        <meta-data
            android:name="com.vivo.push.api_key"
            android:value="Vivo appkey" />
        <meta-data
            android:name="com.vivo.push.app_id"
            android:value="Vivo appid" />

</application>
```


### Enabling Vivo push
Enable the third-party push API before calling TPNS' `XGPushManager.registerPush`:

```java
// Enable the third-party push
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

>?Obfuscation rules must be stored in the `proguard-rules.pro` file at the application project level.
