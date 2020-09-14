
## Operation Scenarios
The Vivo push channel is a system-level push channel officially provided by Vivo. On a Vivo phone, push messages can be delivered through Vivo's system channel without opening the application. For more information, please visit [Vivo Push's official website](https://dev.vivo.com.cn/home).

>?
>- If an application cannot be opened after you click the notification on the debugging version, please find the pop-up window permission and enable it for the current application.
>- Vivo channel currently does not support in-app messages, which will be sent through the TPNS channel.
>- Vivo channel imposes a certain limit on the number of daily push messages, as detailed in [Vendor Channel Limit](https://intl.cloud.tencent.com/zh/document/product/1024/35829). When this limit is exceeded, excessive messages will be pushed through the TPNS channel.
>- Vivo channel pushes messages during 7:00-23:00, and only pushes system messages in other time periods. See [How to Apply for Vivo System Message](https://intl.cloud.tencent.com/zh/document/product/1024/36250#vivozhinan) to apply for system message.
>- Vivo channel allows a user to receive up to 5 operational messages per application, and unlimited number of system messages. 
>- Vivo channel is only available in later models and systems. For more information, see [Vivo Push FAQs](https://dev.vivo.com.cn/documentCenter/doc/156#w1-08608733).

## Directions
### Getting key
You need to apply to Vivo for enabling the push permission so as to get three keys, namely, `AppID`, `AppKey`, and `AppSecret`. For more information, please see [Quick Integration Guide](https://dev.vivo.com.cn/documentCenter/doc/180).

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
implementation 'com.tencent.tpns:vivo:[VERSION]-release' // Vivo Push [VERSION] is the version number of the current SDK, which can be viewed on the SDK download page
```

>? Vivo Push [VERSION] refers to the SDK version number, which can be viewed on the [SDK download page](https://console.cloud.tencent.com/tpns/sdkdownload).


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
Enable the third-party push API before calling TPNS' ```XGPushManager.registerPush```:

```java
// Enable the third-party push
XGPushConfig.enableOtherPush(getApplicationContext(), true);


// The log of successful registration is as follows:
 I/XINGE: [XGOtherPush] other push token is : 15646472431991408944055  other push type: vivo
I/XINGE: [PushServiceBroadcastHandler]  bind OtherPushToken success ack with [accId = 1500xxxxxx  , rsp = 0]  token = 0139f9840030882cfe7cc791aebc800ed270 otherPushType = vivo otherPushToken = 15646472431991408944055

```


### Code obfuscation

```xml
-dontwarn com.vivo.push.**
-keep class com.vivo.push.**{*; }
-keep class com.vivo.vms.**{*; }
-keep class com.tencent.android.vivopush.VivoPushMessageReceiver{*;}

```

>?Obfuscation rules must be stored in the `proguard-rules.pro` file at the application project level.
