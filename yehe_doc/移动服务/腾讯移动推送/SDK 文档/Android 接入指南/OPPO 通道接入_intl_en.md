

## Operation Scenarios
The OPPO PUSH channel is a system-level push channel officially provided by OPPO. On an OPPO phone, push messages can be delivered through OPPO's system channel without opening the application. For more information, please visit [OPPO PUSH's official website](https://push.oppo.com/).


>?
>- OPPO channel currently does not support in-app messages, which will be sent through the TPNS channel.
>- OPPO channel imposes a certain limit on the number of daily push messages, as detailed in [Vendor Channel Limit](https://intl.cloud.tencent.com/zh/document/product/1024/35829#oppo-.E5.B9.B3.E5.8F.B0.E9.99.90.E5.88.B6). When this limit is exceeded, excessive messages will be pushed through the TPNS channel.
>- OPPO PUSH is supported by OPPO ColorOS v3.1 or above.



## Directions
### Applying for permission
Use an OPPO enterprise developer account to log in to the [OPPO Developer Platform](https://open.oppomobile.com/) and select **Management Center** > **Application Service Platform** > **Mobile Application List** > **Select Application** > **Development Service** > **Push Service** to apply for the OPPO PUSH permission.

### Getting key
>?You can only view the key under a developer account (root account).

After your application for activating OPPO PUSH is approved, you can select **[OPPO PUSH Platform](https://push.oppo.com/)** > **Configuration Management** > **Application Configuration** to view the `AppKey`, `AppSecret`, and `MasterSecret`.


### Configuring push channel
To be compatible with channel configurations for Android 8.0 or above on OPPO phones, you need to create the default TPNS channel in the OPPO Console. For more information, please see [OPPO's official documentation](https://open.oppomobile.com/wiki/doc/#id=10198).
The configuration items are as described below:
- "Channel ID": "default_message"
- "Channel Name": "default notification"



### Configuration
#### Integrating through Android Studio

Import the dependencies related to OPPO PUSH. The sample code is as follows:
```js
implementation 'com.tencent.tpns:oppo:[VERSION]-release'// OPPO PUSH [VERSION] is the version number of the current SDK, which can be viewed on the SDK download page
```

>? OPPO Push [VERSION] refers to the SDK version number, which can be viewed on the [SDK download page](https://console.cloud.tencent.com/tpns/sdkdownload).


#### Integrating through Eclipse
After getting the TPNS SDK package for OPPO PUSH, configure the major TPNS version and the following content in the manual integration method detailed on TPNS's official website.

1. Import the jar packages related to OPPO PUSH. Import `oppo4tpns1.1.2.1.jar` to the project folder.
2. Add the following configuration to the `Androidmanifest.xml` file (two methods):
 - Use the following configuration for the TPNS SDK for Android below v1.2.0.2:
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
 - Use the following configuration for the TPNS SDK for Android v1.2.0.2 and above:
```
<!--Permissions required by OPPO PUSH-->
<uses-permission android:name="com.coloros.mcs.permission.RECIEVE_MCS_MESSAGE"/>
<uses-permission android:name="com.heytap.mcs.permission.RECIEVE_MCS_MESSAGE"/>
<application>
		<!-- The following is the OPPO component on v1.2.0.2 -->
		<service
			android:name="com.heytap.msp.push.service.CompatibleDataMessageCallbackService"
			android:permission="com.coloros.mcs.permission.SEND_MCS_MESSAGE">
			<intent-filter>
				<action android:name="com.coloros.mcs.action.RECEIVE_MCS_MESSAGE"/>
			</intent-filter>
		</service>
		<service
			android:name="com.heytap.msp.push.service.DataMessageCallbackService"
			android:permission="com.heytap.mcs.permission.SEND_PUSH_MESSAGE">
			<intent-filter>
				<action android:name="com.heytap.mcs.action.RECEIVE_MCS_MESSAGE"/>
				<action android:name="com.heytap.msp.push.RECEIVE_MCS_MESSAGE"/>
			</intent-filter>
		</service>
</application>
```

### Enabling OPPO Push
Call the following code before calling TPNS' `XGPushManager.registerPush`:
```java
// Note that OPPO's `AppKey` is entered here rather than the `AppId`
XGPushConfig.setOppoPushAppId(getApplicationContext(), "OPPO AppKey");
// Note that OPPO's `AppSecret` is entered here rather than the `AppKey`
XGPushConfig.setOppoPushAppKey(getApplicationContext(), "OPPO AppSecret");
// Enable the third-party push
XGPushConfig.enableOtherPush(getApplicationContext(), true);

// The log of successful registration is as follows:
I/XINGE: [XGOtherPush] other push token is : CN_93394e648ee5a73f5c5a0835b2a7e3d5  other push type: oppo
I/XINGE: [h] >> bind OtherPushToken success ack with [accId = 1500xxxxxx  , rsp = 0]  token = 0114d716bfe01d75f861d05a920cca8c8226 otherPushType = oppo otherPushToken = CN_93394e648ee5a73f5c5a0835b2a7e3d5
```


### Code obfuscation
```xml
-keep public class * extends android.app.Service
-keep class com.heytap.mcssdk.** {*;}
-keep class com.heytap.msp.push.** { *;}
```

>?Obfuscation rules must be stored in the `proguard-rules.pro` file at the application project level.
