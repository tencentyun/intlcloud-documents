## Overview 
The OPPO channel is a system-level push channel officially provided by OPPO. The OPPO's system channel can deliver push messages to an OPPO phone without requiring the user to open the application. For more information, visit [OPPO PUSH's official website](https://push.oppo.com/).

>?
> - The OPPO channel currently does not support in-app messages, which will be delivered through the TPNS channel.
> - The OPPO channel imposes a certain quota limit on the number of daily push messages. For more information, see [Vendor Channel Limit Description](https://intl.cloud.tencent.com/document/product/1024/35829). When this limit is exceeded, excessive messages will be pushed through the TPNS channel.
> - The OPPO channel is supported by OPPO ColorOS v3.1 or later.
> 

## Directions
### Applying for permission
Use an OPPO enterprise developer account to log in to the [OPPO Developer Platform](https://open.oppomobile.com/), and select **Management Center** > **App Service Platform** > **Mobile App List** > **Select App** > **Development Service** > **Push Service** to apply for the OPPO PUSH permission.
![]()
>? The notification bar push permissions can be granted only if the application is published on OPPO AppStore and its main business is not lending.
>

### Obtaining a key

>? You can only view the key under a developer account (root account).
>

1. After OPPO PUSH is activated, you can select [**OPPO PUSH Platform**](https://push.oppo.com/) > **Configuration Management** > **Application Configuration** to view the `AppKey`, `AppSecret`, and `MasterSecret`.
![]()
2. Copy and paste the `AppKey`, `AppSecret`, and `MasterSecret` parameters of the application into [**TPNS console**](https://console.cloud.tencent.com/tpns) > **Configuration Management** > **Basic Configuration** > **OPPO Official Push Channel**.

### Configuring the push channel
To be compatible with channel configurations for Android 8.0 or later on OPPO phones, you need to create a default TPNS channel in the OPPO console. For more information, see [OPPO's official documentation](https://open.oppomobile.com/wiki/doc/#id=10198).
The configuration items are as described below:
- Channel ID: `default_message`
- Channel Name: `default notification`


### Configuration
#### Integrating through Android Studio

Import the dependencies related to OPPO PUSH. The sample code is as follows:
```
// For OPPO PUSH SDK, [VERSION] is the version number of the current SDK and can be obtained from the "SDK for Android".
implementation 'com.tencent.tpns:oppo:[VERSION]-release'

// For SDK v1.3.2.0 or later, you need to add the following dependency statements. Otherwise, the registration of OPPO PUSH will fail.
implementation 'com.google.code.gson:gson:2.6.2'
implementation 'commons-codec:commons-codec:1.15'
```
>? For OPPO PUSH, [VERSION] is the version number of the current SDK and can be viewed in [SDK for Android](https://console.cloud.tencent.com/tpns/sdkdownload).
>

### Integrating through Eclipse

After getting the TPNS SDK package for OPPO PUSH, configure the major TPNS version and the following content in the manual integration method detailed on TPNS's official website.

1. Open the `Other-push-jar` folder and import the OPPO PUSH-related JAR into the project.
2. Add a class resource file to the project with the following code:
```java
package com.pushsdk;

class R {
    public static final class string {
	public final static int system_default_channel = com.tencent.android.tpns.demo.R.string.app_name; //This can be changed to a custom string resource ID
    }
}
```
3. Add the following configuration to the `Androidmanifest.xml` file :
 
```
<!--Permissions required by OPPO PUSH-->
<uses-permission android:name="com.coloros.mcs.permission.RECIEVE_MCS_MESSAGE"/>
<uses-permission android:name="com.heytap.mcs.permission.RECIEVE_MCS_MESSAGE"/>
<application>
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

### Enabling OPPO PUSH

Call the following code before calling TPNS' `XGPushManager.registerPush`:
```java
// Note that OPPO's `AppKey` rather than the `AppID` is required here
XGPushConfig.setOppoPushAppId(getApplicationContext(), "OPPO’s AppKey");
// Note that OPPO's `AppSecret` rather than the `AppKey` is required here 
XGPushConfig.setOppoPushAppKey(getApplicationContext(), "OPPO’s AppSecret");
// Enable third-party push
XGPushConfig.enableOtherPush(getApplicationContext(), true);

// The log of successful registration is as follows:
I/TPush: [RegisterReservedInfo] Reservert info: other push token is : CN_fc0f0b38220cba7a1bcbda20857e021b  other push type: oppo
I/TPush: [PushServiceBroadcastHandler] >> bind OtherPushToken success ack with [accId = 150000****  , rsp = 0]  token = 007a4105425********52ac1e1360c6780f3 otherPushType = oppo otherPushToken = CN_fc0f0b3822****7a1bcbda20857e021b

```


### Code obfuscation

```xml
-keep public class * extends android.app.Service
-keep class com.heytap.mcssdk.** {*;}
-keep class com.heytap.msp.push.** { *;}
```

>? Obfuscation rules must be stored in the `proguard-rules.pro` file at the application project level.
>

## Troubleshooting

### Querying OPPO PUSH registration error codes

If you observe logs similar to the following, it indicates that registration with the OPPO channel fails. In this case, you can use the method described below to get the OPPO PUSH registration error code.
```
[OtherPushClient] handleUpdateToken other push token is: other push type: OPPO
```

In debugging mode of the push service, filter logs by the keyword `OtherPush` to view the return code logs, for example, `[OtherPushOppoImpl] OppoPush Register failed, code=14, msg=INVALID_APP_KEY`. Then locate the error cause and rectify the error by referring to [Troubleshooting Vendor Channel Registration Failures](https://intl.cloud.tencent.com/document/product/1024/37006).

### Why do I receive the error code 30 when I push messages with OPPO PUSH?

Official messages cannot be sent during application approval. Please go to the OPPO PUSH platform to check the push permission approval progress.
