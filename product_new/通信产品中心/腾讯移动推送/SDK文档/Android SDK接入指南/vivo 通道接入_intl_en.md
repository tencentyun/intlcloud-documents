
## Operation Scenarios
The Vivo push channel is a system-level push channel officially provided by Vivo. On a Vivo phone, push messages can be delivered through Vivo's system channel without opening the app. For more information, please visit [Vivo Push's official website](https://dev.vivo.com.cn/home).

>
- If an app cannot be opened after you tap the notification on the debugging version, please find the pop-up window permission and enable it for the current app.
- Vivo Push currently does not support in-app messages, which will be displayed as notifications.
- Vivo Push imposes a certain limit (which is not disclosed) on the number of daily push messages (including notifications and passthrough messages). When this limit is exceeded, excessive messages will be pushed through TPNS' channel.

## Directions
### Getting key
You need to apply to Vivo for enabling the push permission so as to get three keys, namely, `AppID`, `AppKey`, and `AppSecret`. For more information, please see [Quick Integration Guide](https://dev.vivo.com.cn/documentCenter/doc/180).

### Configuration
#### Integrating through Android Studio

Complete the configuration required by TPNS in the `build.gradle` file in the App module and then add the following nodes:
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

        <!-- Receiver declaration for pushing app's custom messages -->
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


### Enabling Vivo Push
Enable the third-party push API before calling TPNS' ```XGPushManager.registerPush```:

```java
// Enable the third-party push
XGPushConfig.enableOtherPush(getApplicationContext(), true);


//The log of successful registration is as follows:
 I/XINGE: [XGOtherPush] other push token is : 15646472431991408944055  other push type: vivo
I/XINGE: [PushServiceBroadcastHandler]  bind OtherPushToken success ack with [accId = 1500xxxxxx  , rsp = 0]  token = 0139f9840030882cfe7cc791aebc800ed270 otherPushType = vivo otherPushToken = 15646472431991408944055

```


### Obfuscating code

```xml
-dontwarn com.vivo.push.**
-keep class com.vivo.push.**{*; }
-keep class com.vivo.vms.**{*; }
-keep class com.tencent.android.vivopush.VivoPushMessageReceiver{*;}

```

>Obfuscation rules must be stored in the `proguard-rules.pro` file at the app project level.
