## Operation Scenarios
The Mi push channel is a system-level push channel officially provided by Mi. On a Mi phone, push messages can be delivered through Mi's system channel without opening the app.

!
- The Mi channel supports arrival callback and passthrough (arrival unguaranteed) but not click callback.
- When you test message push through the Mi channel, avoid using words such as `test`; otherwise, the messages will be blocked by Mi and marked as "unimportant messages".

## Directions
### Getting key
Enter the [Mi open platform](httpsdev.mi.comconsoleappservicepush.html), sign up for a Mi developer account, and get the key of Mi Push. For more information, please see [Quick Connection Guide](httpsdev.mi.comconsoledocdetailpId=708).



### Configuration
#### Using JCenter for dependency import
JCenter is recommended for dependency import for AS development. Import the Jar package of Mi Push:
```js
 implementation 'com.tencent.tpnsxiaomi[VERSION]-release'   Mi Push [VERSION] is the version number of the current SDK, which can be viewed on the SDK download page
```




#### Integrating through Eclipse
1. Download the [SDK installation package](httpsconsole.cloud.tencent.comtpnssdkdownload).
2. Open the `Other-Push-jar` folder and import the jar packages related to Mi Push. Import `xm4tpns1.1.2.1.jar` to the project folder.
3. After successful TPNS configuration, add the configuration of Mi Push:
```xml
application
service
androidname=com.xiaomi.push.service.XMPushService
androidenabled=true
androidprocess=pushservice 
service
androidname=com.xiaomi.push.service.XMJobService
androidenabled=true
androidexported=false
androidpermission=android.permission.BIND_JOB_SERVICE
androidprocess=pushservice 
!-- Note: this service must be added for v3.0.1 and above --
service
androidname=com.xiaomi.mipush.sdk.PushMessageHandler
androidenabled=true
androidexported=true 
service
androidname=com.xiaomi.mipush.sdk.MessageHandleService
androidenabled=true 
!-- Note: this service must be added for v2.2.5 and above --
receiver
androidname=com.xiaomi.push.service.receivers.NetworkStatusReceiver
androidexported=true 
intent-filter
action androidname=android.net.conn.CONNECTIVITY_CHANGE 
category androidname=android.intent.category.DEFAULT 
intent-filter
receiver
receiver
androidname=com.xiaomi.push.service.receivers.PingReceiver
androidexported=false
androidprocess=pushservice 
intent-filter
action androidname=com.xiaomi.push.PING_TIMER 
intent-filter
receiver
application
!-- Note: this is the beginning of permission required by Mi Push --
permission
androidname=app package name.permission.MIPUSH_RECEIVE
androidprotectionLevel=signature 
!-- Here, change `com.example.mipushtest` to the app package name --
uses-permission androidname=app package name.permission.MIPUSH_RECEIVE 
!-- Here, change `com.example.mipushtest` to the app package name --
-- Note: this is the end of the permissions required by Mi Push --
```
3. Add ```Receiver``` in ```AndroidManifest.xml``` with the following configuration:
```xml
receiver
androidexported=true
androidname=com.tencent.android.mipush.XMPushMessageReceiver
intent-filter
action androidname=com.xiaomi.mipush.RECEIVE_MESSAGE 
intent-filter
intent-filter
action androidname=com.xiaomi.mipush.MESSAGE_ARRIVED 
intent-filter
intent-filter
action androidname=com.xiaomi.mipush.ERROR 
intent-filter
receiver
```

### Enabling Mi Push
Set Mi `AppID` and `AppKey`.

```java
XGPushConfig.setMiPushAppId(getApplicationContext(), APPID);
XGPushConfig.setMiPushAppKey(getApplicationContext(), APPKEY);
Enable third-party push
XGPushConfig.enableOtherPush(getApplicationContext(), true);


The log of successful registration is as follows:
12-02 161732.299 12584-12584com.qq.xgdemo IXINGE [XGPushManager] Action - Register to xinge server
12-02 161732.996 12584-12584com.qq.xgdemo IXINGE [XGPushManager] Register call back to com.qq.xgdemo
12-02 161732.997 12584-12626com.qq.xgdemo IXINGE [XGPushManager] XG register push success with token  1d31bb3ea6185baebdf05dfc2e586dfe5dc41fb5
12-02 161733.001 12584-12626com.qq.xgdemo IXINGE [XGOtherPush] other push token is  YZQfRxmxdfNlbSKpNWCa3tM4Esnq6op4qeOsQO2qT88= other push type xiaomi
```

If you need to get parameters through the click callback or redirect to a custom page, you can use the intent to do so. For more information, please see [FAQs for Android](httpscloud.tencent.comdocumentproduct54836674#.E5.A6.82.E4.BD.95.E8.AE.BE.E7.BD.AE.E6.B6.88.E6.81.AF.E7.82.B9.E5.87.BB.E4.BA.8B.E4.BB.B6.EF.BC.9F).



### Obfuscating code

```xml
-keep class com.xiaomi.{;}
-keep public class  extends com.xiaomi.mipush.sdk.PushMessageReceiver
```

Obfuscation rules must be stored in the `proguard-rules.pro` file at the app project level.


