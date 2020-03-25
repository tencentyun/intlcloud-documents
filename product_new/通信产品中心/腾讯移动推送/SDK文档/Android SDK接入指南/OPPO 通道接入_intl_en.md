

## Operation Scenarios
The OPPO PUSH channel is a system-level push channel officially provided by OPPO. On an OPPO phone, push messages can be delivered through OPPO's system channel without opening the app. For more information, please visit [OPPO PUSH's official website](https://push.oppo.com/).


>
- OPPO PUSH currently does not support in-app messages, which will be displayed as notifications.
- OPPO PUSH imposes a certain limit (which is not disclosed) on the number of daily push messages (including notifications and passthrough messages). When this limit is exceeded, excessive messages will be pushed through TPNS channel.
- OPPO PUSH is supported by OPPO ColorOS v3.1 or above.
- When apps are installed on an OPPO phone, the notification bar permission will not be granted by default. You can call the [notification bar permission requesting](#qqtz) API or guide the user to manually grant the permission to the app.


## Directions
### Applying for permission
Use an OPPO enterprise developer account to log in to the [OPPO Developer Platform](https://open.oppomobile.com/) and select "Management Center > App Service Platform > Mobile App List > Select App > Development Service > Push Service" to apply for the OPPO PUSH permission.

### Getting key
>You can only view the key under a developer account (root account).

After your application for activating OPPO PUSH is approved, you can select [OPPO PUSH Platform](https://push.oppo.com/) > Configuration Management > App Configuration to view the `AppKey`, `AppSecret`, and `MasterSecret`. For more information, please see [Quick Integration Guide](https://open.oppomobile.com/wiki/doc#id=10195)



### Configuring push channel
To be compatible with channel configurations for Android 8.0 or above on OPPO phones, you need to create a default TPNS push channel in the OPPO Console. For more information, please see [OPPO's official documentation](https://open.oppomobile.com/wiki/doc/#id=10198).
The configuration items are as described below:
- "Channel ID": "default_message"
- "Channel Name": "default notification"
        


### Configuration
#### Integrating through Android Studio

Import the dependencies related to OPPO PUSH. The sample code is as follows:
```js
implementation 'com.tencent.tpns:oppo:[VERSION]-release'// OPPO PUSH [VERSION] is the version number of the current SDK, which can be viewed on the SDK download page
```




#### Integrating through Eclipse
After getting the TPNS SDK package for OPPO PUSH, configure the major TPNS version and the following content in the manual integration method detailed on TPNS's official website.

1. Import the jar packages related to OPPO PUSH. Import `oppo4tpns1.1.2.1.jar` to the project folder.
2. Add the following configuration to the ```Androidmanifest.xml``` file:

```
<!--Permissions required by OPPO PUSH-->
<uses-permission android:name="com.coloros.mcs.permission.RECIEVE_MCS_MESSAGE"/>
<uses-permission android:name="com.heytap.mcs.permission.RECIEVE_MCS_MESSAGE"/>

<application>
    <!--Components required by OPPO PUSH-->
    <service
        android:name="com.heytap.mcssdk.PushService"
        android:permission="com.coloros.mcs.permission.SEND_MCS_MESSAGE">
        <intent-filter>
            <action android:name="com.coloros.mcs.action.RECEIVE_MCS_MESSAGE"/>
        </intent-filter>
    </service>
    
    <service
        android:name="com.heytap.mcssdk.AppPushService"
        android:permission="com.heytap.mcs.permission.SEND_MCS_MESSAGE">
        <intent-filter>
            <action android:name="com.heytap.mcs.action.RECEIVE_MCS_MESSAGE"/>
        </intent-filter>
    </service>

</application>
```

<span id="qqtz"></span>
### Requesting notification bar permission
1. Call the following code before calling TPNS `XGPushManager.registerPush`:
```java
XGPushConfig.enableOppoNotification(getApplicationContext(), true);
```
When the app is opened for the first time, the window for requesting notification bar permission will pop up, and it pops up only once before the app is reinstalled. The TPNS-OPPO dependency package must be v1.1.5.1 or above, and the phone OS must be ColorOS 5.0 or above.




### Enabling OPPO PUSH
Call the following code before calling TPNS' ```XGPushManager.registerPush```:
```java
// Note that OPPO's `AppKey` is entered here rather than the `AppId`
XGPushConfig.setOppoPushAppId(getApplicationContext(), "OPPO AppKey"); 
// Note that OPPO's `AppSecret` is entered here rather than the `AppKey`
XGPushConfig.setOppoPushAppKey(getApplicationContext(), "OPPO AppSecret");
// Enable the third-party push
XGPushConfig.enableOtherPush(getApplicationContext(), true);

//The log of successful registration is as follows:
I/XINGE: [XGOtherPush] other push token is : CN_93394e648ee5a73f5c5a0835b2a7e3d5  other push type: oppo
I/XINGE: [h] >> bind OtherPushToken success ack with [accId = 1500xxxxxx  , rsp = 0]  token = 0114d716bfe01d75f861d05a920cca8c8226 otherPushType = oppo otherPushToken = CN_93394e648ee5a73f5c5a0835b2a7e3d5
```


### Obfuscating code
```xml
-keep public class * extends android.app.Service
-keep class com.heytap.mcssdk.** {*;}
```

>Obfuscation rules must be stored in the `proguard-rules.pro` file at the app project level.
