## Operation Scenarios
The Mi push channel is a system-level push channel **officially provided by Mi**. On a Mi phone, push messages can be delivered through Mi's system channel without opening the application.

>!
>- The Mi channel supports arrival callback but not click callback.
>- When you test message push through the Mi channel, avoid using words such as `test`; otherwise, the messages will be blocked by Mi and marked as "unimportant messages".

## Directions
### Getting key
Enter the [Mi open platform](https://dev.mi.com/console/appservice/push.html), sign up for a Mi developer account, and get the key of Mi Push. For more information, please see [Quick Connection Guide](https://dev.mi.com/console/doc/detail?pId=708).



### Configuration
#### Using JCenter for dependency import
JCenter is recommended for dependency import for AS development. Import the Jar package of Mi Push:
```js
implementation 'com.tencent.tpns:xiaomi:[VERSION]-release'// Mi Push [VERSION] is the version number of the current SDK, which can be viewed on the SDK download page
```

>? Xiaomi Push [VERSION] refers to the SDK version number, which can be viewed on the [SDK download page](https://console.cloud.tencent.com/tpns/sdkdownload).


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
    <!-- Note: this service must be added for version 3.0.1 or above -->
    <service
        android:name="com.xiaomi.mipush.sdk.PushMessageHandler"
        android:enabled="true"
        android:exported="true" />
    <service
        android:name="com.xiaomi.mipush.sdk.MessageHandleService"
        android:enabled="true" />
    <!-- Note: this service must be added for version 2.2.5 or above -->
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
        android:process=":pushservice" >
        <intent-filter>
            <action android:name="com.xiaomi.push.PING_TIMER" />
        </intent-filter>
    </receiver>
</application>

<!-- Note: this is the beginning of permission required by Mi Push -->
<permission
    android:name="application package name.permission.MIPUSH_RECEIVE"
    android:protectionLevel="signature" />
<!-- Here, change application package name to the actual application package name -->

<uses-permission android:name="application package name.permission.MIPUSH_RECEIVE" />
<!-- Here, change application package name to the actual application package name -->
<!-- Note: this is the end of the permissions required by Mi Push -->
```

4. Add `Receiver` in `AndroidManifest.xml` and configure it as follows:

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

### Enabling Mi push
Set Mi `AppID` and `AppKey`.

```java
XGPushConfig.setMiPushAppId(getApplicationContext(), "APPID");
XGPushConfig.setMiPushAppKey(getApplicationContext(), "APPKEY");
// Enable the third-party push
XGPushConfig.enableOtherPush(getApplicationContext(), true);


// The log of successful registration is as follows:
12-02 16:17:32.299 12584-12584/com.qq.xgdemo I/XINGE: [XGPushManager] Action -> Register to xinge server
12-02 16:17:32.996 12584-12584/com.qq.xgdemo I/XINGE: [XGPushManager] Register call back to com.qq.xgdemo
12-02 16:17:32.997 12584-12626/com.qq.xgdemo I/XINGE: [XGPushManager] XG register push success with token : 1d31bb3ea6185baebdf05dfc2e586dfe5dc41fb5
12-02 16:17:33.001 12584-12626/com.qq.xgdemo I/XINGE: [XGOtherPush] other push token is : YZQfRxmxdfNlbSKpNWCa3tM4Esnq6op4qeOsQO2qT88= other push type: xiaomi
```

If you need to get parameters through the click callback or redirect to a custom page, you can use the intent to do so. For more information, please see [FAQs for Android](https://intl.cloud.tencent.com/document/product/1024/32624).



### Code obfuscation

```xml
-keep class com.xiaomi.**{*;}
-keep public class * extends com.xiaomi.mipush.sdk.PushMessageReceiver
```

>?Obfuscation rules must be stored in the `proguard-rules.pro` file at the application project level.


