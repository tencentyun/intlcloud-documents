

## Operation Scenarios

The Huawei push channel is a system-level push channel **officially provided by Huawei**. On a Huawei phone, push messages can be delivered through Huawei's system channel without opening the application.


>!
>- This document is only applicable to Huawei channel V2 integration. For the V4 integration, see [Huawei Channel V4 Integration](https://intl.cloud.tencent.com/document/product/1024/37176).
>- Huawei Push can only receive push messages in a signed package environment.
>- The Mobile Push Service on the Huawei phone must be upgraded to 2.5.3 or above; otherwise, the Huawei channel registration will fail and the TPNS channel will be used.
>- The Huawei channel supports click callback (custom parameters required) and passthrough (custom parameters ignored but arrival unguaranteed) but not arrival callback.

## Directions

### Getting key

1. Enter the [Huawei's development platform](http://developer.huawei.com).
2. Sign up for a developer account and log in to the platform. For more information, please see [Account Registration and Verification](https://developer.huawei.com/consumer/cn/devservice/doc/20300). (If you are registering a new account, you need to verify your identity.)
3. Create an application on the Huawei Push platform. For more information, please see [Creating App](https://developer.huawei.com/consumer/cn/doc/development/HMS-2-Guides/hmssdk_huaweipush_devprepare_agent#h1-1575111622057). (The application package name must be the same as that entered in the TPNS Console.)
4. Get and copy the application's `AppID` and `AppSecret` and paste them in Application Configuration > Huawei Channel in the TPNS Console.


### Configuring SHA256 certificate fingerprint
For more information on how to get the SHA256 certificate fingerprint, please see the [Huawei Push integration documentation](https://developer.huawei.com/consumer/cn/doc/development/HMS-2-Guides/hmssdk_huaweipush_devprepare_agent#h1-1575111604142).



### Integration steps
#### Integrating through Android Studio

Complete the configuration required by TPNS in the `build.gradle` file in the Application module and then add the following Huawei nodes:
1. Configure the Huawei `AppID`. The sample code is as follows:
```xml
 manifestPlaceholders = [
	 HW_APPID: "Huawei APPID"
        ]
```

2. Import the dependencies related to Huawei Push. The sample code is as follows:
```js
 implementation 'com.tencent.tpns:huawei:[VERSION]-release'// Huawei Push [VERSION] is the version number of the current SDK, which can be viewed on the SDK download page
```

>? Huawei Push [VERSION] refers to the SDK version number, which can be viewed on the [SDK download page](https://console.cloud.tencent.com/tpns/sdkdownload).


#### Integrating through Eclipse
1. Download the [SDK installation package](https://console.cloud.tencent.com/tpns/sdkdownload).
2. Open the `Other-Push-jar` folder and import the jar packages related to Huawei Push. Import `hw4tpns1.1.2.1.jar` to the project folder:
3. Add the following configuration to the `Androidmanifest.xml` file:
	```xml
	<meta-data
			android:name="com.huawei.hms.client.appid"
			android:value="your `APPID` (from Huawei's official website)" >
	</meta-data>
	<activity
			android:name="com.huawei.hms.activity.BridgeActivity"
			android:configChanges="orientation|locale|screenSize|layoutDirection|fontScale"
			android:excludeFromRecents="true"
			android:exported="false"
			android:hardwareAccelerated="true"
			android:theme="@android:style/Theme.Translucent" >
			<meta-data
					android:name="hwc-theme"
					android:value="androidhwext:style/Theme.Emui.Translucent" />
	</activity>
	<provider
			android:name="com.huawei.hms.update.provider.UpdateProvider"
			android:authorities="application package name.hms.update.provider"
			android:exported="false"
			android:grantUriPermissions="true" >
	</provider>
	<receiver android:name="com.huawei.hms.support.api.push.PushEventReceiver" >
			<intent-filter>
					<!-- Receive notification bar messages from the channel, which is compatible with the legacy version of PUSH -->
					<action android:name="com.huawei.intent.action.PUSH" />
			</intent-filter>
	</receiver>
	<!-- Note: this is the end required by Huawei Push -->
	```
4. Add the receiver to `AndroidManifest.xml` and configure it as follows:
```xml
<receiver android:name="com.tencent.android.hwpush.HWPushMessageReceiver" >
<intent-filter>
		<!-- Required; used to receive `TOKEN` -->
		<action android:name="com.huawei.android.push.intent.REGISTRATION" />
		<!-- Required; used to receive messages -->
		<action android:name="com.huawei.android.push.intent.RECEIVE" />
		<!-- Optional; used to trigger the `onEvent` callback after the notification bar or a button in it is clicked -->
		<action android:name="com.huawei.android.push.intent.CLICK" />
		<!-- Optional; used to check whether the PUSH channel is connected to; not needed if there is no need to view -->
		<action android:name="com.huawei.intent.action.PUSH_STATE" />
</intent-filter>
</receiver>
```

### Enabling Huawei Push
Enable the third-party push API before calling TPNS' `XGPushManager.registerPush`:

```java
// Enable the third-party push
XGPushConfig.enableOtherPush(getApplicationContext(), true);
```

The log of successful registration is as follows:
```xml
I/XINGE: [XGOtherPush] other push token is : 0865551032618726300001294600CN01 other push type: huawei
 I/XINGE: [a] binder other push token with accid = 2100274337  token = 17c32948df0346d5837d4748192e9d2f14c81e08 otherPushType = huawei otherPushToken = 0865551032618726300001294600CN01
```

### Code obfuscation
```xml
-ignorewarning
-keepattributes *Annotation*
-keepattributes Exceptions
-keepattributes InnerClasses
-keepattributes Signature
-keepattributes SourceFile,LineNumberTable
-keep class com.hianalytics.android.**{*;}
-keep class com.huawei.updatesdk.**{*;}
-keep class com.huawei.hms.**{*;}
-keep class com.huawei.android.hms.agent.**{*;}

```
>?Obfuscation rules must be stored in the `proguard-rules.pro` file at the application project level.

## Arrival Receipt Configuration for Huawei Channel
The arrival receipt for the Huawei channel should be configured by yourself. After configuring this feature as instructed in [Configuration Guide](https://intl.cloud.tencent.com/document/product/1024/35246#.E9.85.8D.E7.BD.AE.E6.8C.87.E5.BC.95), you can view the arrival data for the Huawei push channel in the push records.
![](https://main.qcloudimg.com/raw/19ddec21e90801763910c2ac787b6de9.png)

## Badge Adaptation for Huawei Devices
Huawei devices support setting application badge in the following steps:
1. Apply for the permission to set application badge by adding the following permission configuration under the `manifest` tag in the application's `AndroidManifest.xml` file:
```
<uses-permission android:name="com.huawei.android.launcher.permission.CHANGE_BADGE "/>
```
2. Set the application startup class
You need to enable the Huawei channel in the console and enter the `Activity` class of the application entry corresponding to the homescreen icon in parameter configurations, such as `com.test.badge.MainActivity` as shown below:
![](https://main.qcloudimg.com/raw/ef39ff78a14ac7ac394734fd4078b4b4.png)
For the usage of the badge, please see [Badge Adaptation Guide](https://intl.cloud.tencent.com/document/product/1024/35828#.E5.8D.8E.E4.B8.BA.E6.89.8B.E6.9C.BA.E8.A7.92.E6.A0.87.E9.80.82.E9.85.8D.E6.8C.87.E5.8D.97).
