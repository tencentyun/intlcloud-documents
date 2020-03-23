

## Operation Scenarios

The Huawei push channel is a system-level push channel **officially provided by Huawei**. On a Huawei phone, push messages can be delivered through Huawei's system channel without opening the app.


>
>- Huawei Push can only receive push messages in a signed package environment.
>- The Mobile Push Service on the Huawei phone must be upgraded to 2.5.3 or above; otherwise, The Huawei channel registration will fail and the TPNS channel will be used.
>- The Huawei channel supports click callback (custom parameters required) and passthrough (custom parameters ignored but arrival unguaranteed) but not arrival callback.

## Directions

### Getting key

1. Enter the [Huawei's development platform](http://developer.huawei.com).
2. Sign up for a developer account and log in to the platform. For more information, please see [Account Registration and Verification](https://developer.huawei.com/consumer/cn/devservice/doc/20300). (If you are registering a new account, you need to verify your identity.)
3. Create an app on the Huawei Push platform. For more information, please see [Creating App](https://developer.huawei.com/consumer/cn/service/hms/catalog/HwJointOperationApp.html?page=hmssdk_jointOper_prepare_createapp). (The app package name must be the same as that entered in the TPNS Console.)
4. Get and copy the app's `AppID` and `AppSecret` and paste them in App Configuration > Huawei Channel in the TPNS Console.
		

### Configuring SHA256 certificate fingerprint
For more information on how to get the SHA256 certificate fingerprint, please see the [Huawei Push integration documentation](http://developer.huawei.com/consumer/cn/service/hms/catalog/huaweipush_agent.html?page=hmssdk_huaweipush_introduction_agent).



### Integration steps
#### Integrating through Android Studio

Complete the configuration required by TPNS in the `build.gradle` file in the App module and then add the following Huawei nodes:
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
			android:authorities="app package name.hms.update.provider"
			android:exported="false"
			android:grantUriPermissions="true" >
	</provider>      
	<receiver android:name="com.huawei.hms.support.api.push.PushEventReceiver" >
			<intent-filter>
					<!-- Receive notification panel messages from the channel, which is compatible with the legacy version of PUSH -->
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
		<!-- Optional; used to trigger the `onEvent` callback after the notification panel or a button in the notification panel is tapped -->
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

### Obfuscating code
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
>Obfuscation rules must be stored in the `proguard-rules.pro` file at the app project level.


When your app is released on Huawei AppGallery, it may fail the audit with the error message "Error:28: you need to package the certificate file into the APK when integrating with HMS. Please directly copy the assets directory to the app project's root directory" displayed.

Solution: download the official Huawei HMS SDK and copy all files and subdirectories under the `assets` directory to that in your app project. If the `assets` directory does not exist in the app project, create one.

