# Mi Push Channel Integration Direction

Mi push channel is a system-level push channel **officially provided by Mi**. On a Mi phone, push messages can be delivered through Mi's system channel without opening the app.

## Getting Mi Push Key


(a) Sign up for a Mi developer account as instructed on [Mi open platform](https://dev.mi.com/console/appservice/push.html), then register the app and get the key of Mi Push. 

Verify your identity for your Mi developer account:

![](/assets/认证小米开发者.jpeg)

Get the Mi Push key:

![](/assets/或者小米ID.jpeg)

## Configuring Mi Push-related Content
### Jcenter Dependencies Access is Recommended for AS Development

1. Configure the package name.

```java
 manifestPlaceholders = [
	 PACKAGE_NAME:"app package name"
        ]
```
2. Reference the jar package of Mi Push
```js

/* Mi v3.2.7-release
 * Note: If the Mi channel uses this version, the TPNS SDK also needs to use v3.2.7-release at the same time.
 */
 compile 'com.tencent.xinge:mipush:3.2.7-Release'

/ * Mi v3.2.8-release
 * Note: If the Mi channel uses this version, the TPNS SDK also needs to use v4.0.5 at the same time.
 */
 compile 'com.tencent.xinge:mipush:3.2.8-release'
```




### Eclipse Development Access

1. Reference the jar package of Mi Push, which can be downloaded [here](https://dev.mi.com/mipush/downpage/).


2. On the basis of successful TPNS configuration, add the configuration of Mi Push:

```xml
</application>
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
android:process=":pushservice" >
<intent-filter>
<action android:name="com.xiaomi.push.PING_TIMER" />
</intent-filter>
</receiver>
</application>
<!-- Note: This is the beginning of permission required by Mi Push -->
<permission
android:name="app package name.permission.MIPUSH_RECEIVE"
android:protectionLevel="signature" />
<!-- Here, change com.example.mipushtest to the app package name -->

<uses-permission android:name="app package name.permission.MIPUSH_RECEIVE" />
<!-- Here, change com.example.mipushtest to the app package name -->
<!-- Note: This is the end of the permissions required by Mi Push -->
```

3. Add a custom ```Receiver``` in ```AndroidManifest.xml``` with the following configuration:

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
## Starting Mi Push

Set Mi APPID and APPKEY.

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
**Note: If you need to get parameters through tap callback or redirect to a custom page, you can use the Intent to do so. Click [here](http://docs.developer.qq.com/xg/android_access/android_faq.html#%E6%B6%88%E6%81%AF%E7%82%B9%E5%87%BB%E4%BA%8B%E4%BB%B6%E4%BB%A5%E5%8F%8A%E8%B7%B3%E8%BD%AC%E9%A1%B5%E9%9D%A2%E6%96%B9%E6%B3%95) to view the tutorials.**



## Code Obfuscation

```xml
-keep class com.xiaomi.**{*;}
-keep public class * extends com.xiaomi.mipush.sdk.PushMessageReceiver
```

## Vendor-specific Channel Testing Method (Generic)

1. Integrate the TPNS SDK v3.2.1 or higher in your app and integrate the required vendor-specific SDK according to the Integration Guide for Vendor-specific Channels.

2. Confirm that the relevant app information has been enter in "App configuration > Vendor-specific and global channels" in the TPNS console. Usually, <font color= darkblue>**the relevant configuration will take effect after 1 hour. Please wait patiently and proceed to the next step after it takes effect.**</font>

3. Install the integrated app (testing version) on a test device and run the app.

4. Keep the app running in the foreground and try to make unicast/full push to the device.

5. If the app receives the message, switch the app to the background and end all app processes.

6. Make unicast/full push again, and if the push is received, the vendor-specific channel integration is successful.
