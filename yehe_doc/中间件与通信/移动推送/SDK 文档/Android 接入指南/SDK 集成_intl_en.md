## Overview

This document describes how to integrate the online channel push capabilities of the Tencent Push Notification Service SDK using two methods: automatic integration with Android Studio Gradle and manual integration with Android Studio. If you want your push to be received even when the application process is killed, complete the integration operations provided in this document and integrate with vendor channels as instructed in the [Vendor Channel Integration Guide](https://www.tencentcloud.com/document/product/1024/37176).

## SDK Integration (Two Methods)

### Automatic integration with Android Studio Gradle

#### Directions

>! Before configuring the SDK, make sure you have created an application for the Android platform.
>

1. Log in to the [Tencent Push Notification Service console](https://console.cloud.tencent.com/tpns) and get the application's `AccessID` and `AccessKey` in **Product Management** > **Configuration Management**.
2. Get the version number of the latest SDK on the [SDK Download](https://console.cloud.tencent.com/tpns/sdkdownload) page.
3. Configure the following in the `build.gradle` file of the application:
```
android {
    ......
    defaultConfig {

        // The package name registered in the console. Note that the application ID, the current application package name, and the application package name registered in the console must be the same.
        applicationId "your package name"
        ......

        ndk {
            // Add .so libraries corresponding to the CPU type as needed.
            abiFilters 'armeabi', 'armeabi-v7a', 'arm64-v8a'
            // You can also add 'x86', 'x86_64', 'mips', and 'mips64'
        }

        manifestPlaceholders = [

            XG_ACCESS_ID : "accessid of the registered app",
            XG_ACCESS_KEY : "accesskey of the registered app",
        ]
        ......
    }
    ......
}

dependencies {
    ......
    // Add the following dependencies:             
    implementation 'com.tencent.tpns:tpns:[VERSION]-release' 
		  // For Tencent Push Notification Service push, [VERSION] is the latest SDK version number obtained in step 2 above
}
```

>!
> - If the service access point of your application is Guangzhou, the SDK implements this configuration by default.
> - If the service access point of your application is Shanghai, Singapore, or Hong Kong (China), follow the step to complete the configuration; otherwise, the push service registration will fail, with an error code -502 or 1008003 returned.
> Add the following metadata in the `application` tag in the `AndroidManifest` file:
> ```
<application>
	// Other Android components
	<meta-data
			android:name="XG_SERVER_SUFFIX"
			android:value="Domain names of other service access points" />
</application>
```
>The domain names of other service access points are as follows:
>   - Shanghai: `tpns.sh.tencent.com`
>   - Singapore: `tpns.sgp.tencent.com`
>   - Hong Kong (China): `tpns.hk.tencent.com`
>  

#### Points for attention

 - If the following notification appears in Android Studio after you add the above-mentioned `abiFilter` configuration:
   "NDK integration is deprecated in the current plugin. Consider trying the new experimental plugin", you need to add `android.useDeprecatedNdk=true` in the `gradle.properties` file under the project root directory.
 - If you need to listen for messages, see the `XGPushBaseReceiver` API or the `MessageReceiver` class in the demo (in the SDK compression package, which can be obtained from [SDK Download](https://console.cloud.tencent.com/tpns/sdkdownload)). You can inherit `XGPushBaseReceiver` and configure the following content in the configuration file (do not process time-consuming operations in the receiver):
```xml
<receiver android:name="com.tencent.android.xg.cloud.demo.MessageReceiver">
    <intent-filter>
        <!-- Receive in-app messages -->
        <action android:name="com.tencent.android.xg.vip.action.PUSH_MESSAGE" />
        <!-- Listen for results of registration, unregistration, tag setting/deletion, and notification clicks -->
        <action android:name="com.tencent.android.xg.vip.action.FEEDBACK" />
    </intent-filter>
</receiver>
```

 - For compatibility with Android P, you must add and use the Apache HTTP client library. To do this, add the following configuration to the AndroidManifest application node.
```
<uses-library android:name="org.apache.http.legacy" android:required="false"/>
```


### Manual integration with Android Studio

Go to [SDK Download](https://console.cloud.tencent.com/tpns/sdkdownload) to get the latest SDK version and import it into your Android project as instructed.


#### Configuring the project

Import the SDK into the project as follows:

1. Create or open an Android project.
2. Copy all the .jar files in the `libs` directory under the Tencent Push Notification Service SDK directory to the project's `libs` (or `lib`) directory.
3. .so files are necessary components of Tencent Push Notification Service and support armeabi, armeabi-v7a, arm64-v8a, mips, mips64, x86, and x86_64 platforms. Add the appropriate platform currently supported by your .so files.
4. Open `Androidmanifest.xml` and add the following configurations (we recommend you modify these configurations according to the Merged Manifest file in the demo provided in the download package). Make sure the configurations are completed as required. Otherwise, the service may not work properly.


#### Configuring permissions

The permissions required by the Tencent Push Notification Service SDK to operate normally. Sample code is as follows:

```xml
<!-- **(Required)** Permissions required by Tencent Push Notification Service SDK VIP version -->
<permission
		android:name="application package name.permission.XGPUSH_RECEIVE"
		android:protectionLevel="signature" />
<uses-permission android:name="application package name.permission.XGPUSH_RECEIVE" />

<!-- **(Required)** Permissions required by Tencent Push Notification Service SDK -->
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.SCHEDULE_EXACT_ALARM" />
<uses-permission android:name="android.permission.POST_NOTIFICATIONS"/>

<!-- **(Common)** Permissions required by Tencent Push Notification Service SDK -->
<uses-permission android:name="android.permission.WAKE_LOCK" />
<uses-permission android:name="android.permission.VIBRATE" />
<uses-permission android:name="android.permission.RECEIVE_USER_PRESENT" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.GET_TASKS" /> 
```

| Permission                                      | Required | Description                                                  |
| ----------------------------------------- | -------- | ----------------------------------------------------- |
| android.permission.INTERNET              | Yes   | Allows the application to access the internet, which may incur GPRS traffic        |
| android.permission.ACCESS_WIFI_STATE     | Yes   | Allows the application to get the current Wi-Fi access status and WLAN hotspot information |
| android.permission.ACCESS_NETWORK_STATE  | Yes   | Allows the application to get the network information status                 |
| android.permission.WAKE_LOCK             | Yes  | Allows the application to run in the background after the screen is off       |
| android.permission.SCHEDULE_EXACT_ALARM             | Yes     | Allows scheduled broadcasting            |
| android.permission.VIBRATE                | No     | Allows the application to access the vibrator |
| android.permission.RECEIVE_USER_PRESENT  | No   | Allows the application to receive screen-on or unlock broadcast          |
| android.permission.WRITE_EXTERNAL_STORAGE | No   | Allows the application to write to external storage                   |
| android.permission.RESTART_PACKAGES      | No   | Allows the application to end a task                     |
| android.permission.GET_TASKS             | No    | Allows the application to get task information                   |



#### Component and application information configuration

```xml
<application>
    <activity android:name="com.tencent.android.tpush.TpnsActivity"
            android:theme="@android:style/Theme.Translucent.NoTitleBar"
            android:launchMode="singleInstance"
            android:exported="true">
            <intent-filter>
                <action android:name="${applicationId}.OPEN_TPNS_ACTIVITY" />
                <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
            <intent-filter>
                <data
                    android:scheme="tpns"
                    android:host="${applicationId}"/>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.BROWSABLE" />
                <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
            <intent-filter>
                <action android:name="android.intent.action" />
            </intent-filter>
        </activity>

        <activity
            android:name="com.tencent.android.tpush.InnerTpnsActivity"
            android:exported="false"
            android:launchMode="singleInstance"
            android:theme="@android:style/Theme.Translucent.NoTitleBar">
            <intent-filter>
                <action android:name="${applicationId}.OPEN_TPNS_ACTIVITY_V2" />

                <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
            <intent-filter>
                <data
                    android:host="${applicationId}"
                    android:scheme="stpns" />

                <action android:name="android.intent.action.VIEW" />

                <category android:name="android.intent.category.BROWSABLE" />
                <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
            <intent-filter>
                <action android:name="android.intent.action" />
            </intent-filter>
        </activity>

        <!-- **(Required)** Tencent Push Notification Service broadcast receiver -->
        <receiver
            android:name="com.tencent.android.tpush.XGPushReceiver"
            android:exported="false"
            android:process=":xg_vip_service">

            <intent-filter android:priority="0x7fffffff">


                <!-- **(Required)** The internal broadcast of the Tencent Push Notification Service SDK -->
                <action android:name="com.tencent.android.xg.vip.action.SDK" />
                <action android:name="com.tencent.android.xg.vip.action.INTERNAL_PUSH_MESSAGE" />
                <action android:name="com.tencent.android.xg.vip.action.ACTION_SDK_KEEPALIVE" />
            </intent-filter>

        </receiver>

    <!-- **(Required)** Tencent Push Notification Service -->
    <service
        android:name="com.tencent.android.tpush.service.XGVipPushService"
        android:exported="false"
        android:process=":xg_vip_service">
    </service>
	
    <!-- **(Required)** Notification service. Change the android:name to the package name.XGVIP_PUSH_ACTION -->
        <service android:name="com.tencent.android.tpush.rpc.XGRemoteService"
            android:exported="false">
            <intent-filter>
                <!-- **(Required)** Changed to the current application package name.XGVIP_PUSH_ACTION -->
                <action android:name="application package name.XGVIP_PUSH_ACTION" />
            </intent-filter>
        </service>

    <!-- **(Required)** **Note:** Change authorities to package name.XGVIP_PUSH_AUTH -->
    <provider
        android:name="com.tencent.android.tpush.XGPushProvider"
        android:authorities="application package name.XGVIP_PUSH_AUTH" />

    <!-- **(Required)** **Note:** Change authorities to package name.TPUSH_PROVIDER -->
    <provider
        android:name="com.tencent.android.tpush.SettingsContentProvider"
        android:authorities="application package name.TPUSH_PROVIDER" />

    <!-- **(Optional)** Used to strengthen the keep-alive capability -->
    <provider
        android:name="com.tencent.android.tpush.XGVipPushKAProvider"
        android:authorities="application package name.AUTH_XGPUSH_KEEPALIVE"
        android:exported="true" />

    <!-- **(Optional)** Receiver implemented by the application, which is used to receive in-app messages and call back operation results. Add it as needed -->
    <!-- Change YOUR_PACKAGE_PATH.CustomPushReceiver to your own receiver： -->
    <receiver android:name="application package name.MessageReceiver"
        android:exported="false">
        <intent-filter>
            <!-- Receive in-app messages -->
            <action android:name="com.tencent.android.xg.vip.action.PUSH_MESSAGE" />
            <!-- Listen for results of registration, unregistration, tag setting/deletion, and notification clicks -->
            <action android:name="com.tencent.android.xg.vip.action.FEEDBACK" />
        </intent-filter>
    </receiver>

    <!-- MQTT START -->
    <service android:exported="false"
            android:process=":xg_vip_service"
            android:name="com.tencent.tpns.mqttchannel.services.MqttService" />

	<provider
            android:exported="false"
            android:name="com.tencent.tpns.baseapi.base.SettingsContentProvider"
            android:authorities="application package name.XG_SETTINGS_PROVIDER" />

    <!-- MQTT END-->
		
    <!-- **(Required)** Changed to the `AccessId` of your application, which is a 10-digit number beginning with "15" and cannot contain spaces -->
    <meta-data
        android:name="XG_V2_ACCESS_ID"
        android:value="Application AccessId" />
    <!-- **(Required)** Changed to the `AccessKey` of your application, which is a 12-character string beginning with "A" and cannot contain spaces -->
    <meta-data
        android:name="XG_V2_ACCESS_KEY"
        android:value="Application AccessKey" />

</application>

<!-- **(Required)** Permissions required by Tencent Push Notification Service SDK v5.0 -->
<permission
    android:name="application package name.permission.XGPUSH_RECEIVE"
    android:protectionLevel="signature" />
<uses-permission android:name="application package name.permission.XGPUSH_RECEIVE" />

<!-- **(Required)** Permissions required by Tencent Push Notification Service SDK -->
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.WAKE_LOCK" />
<uses-permission android:name="android.permission.POST_NOTIFICATIONS"/>

<!-- **(Common)** Permissions required by Tencent Push Notification Service SDK -->
<uses-permission android:name="android.permission.VIBRATE" />
<uses-permission android:name="android.permission.RECEIVE_USER_PRESENT" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```

>!
> - If the service access point of your application is Guangzhou, the SDK implements this configuration by default.
> - If the service access point of your application is Shanghai, Singapore, or Hong Kong (China), follow the step to complete the configuration; otherwise, the push service registration will fail, with an error code -502 or 1008003 returned.
> Add the following metadata in the `application` tag in the `AndroidManifest` file:
> ```
<application>
	// Other Android components
	<meta-data
			android:name="XG_SERVER_SUFFIX"
			android:value="Domain names of other service access points" />
</application>
```
>The domain names of other service access points are as follows:
>   - Shanghai: `tpns.sh.tencent.com`
>   - Singapore: `tpns.sgp.tencent.com`
>   - Hong Kong (China): `tpns.hk.tencent.com`


## Debugging and Registering Devices

### Enabling debug log data

>! When launching your application, set the field to `false` to disable debug log data.
>

```java
XGPushConfig.enableDebug(this,true);
```


### Registering with token
Call the push registration API where you need to start the push service:

>! You are advised to call the registration API only in the main process of your app.
>

```java
XGPushManager.registerPush(this, new XGIOperateCallback() {
    @Override
    public void onSuccess(Object data, int flag) {
        // The token may change after you uninstall and then reinstall the SDK in a device.
        Log.d("TPush", "Registration succeeded. Device token: " + data);
    }

    @Override
    public void onFail(Object data, int errCode, String msg) {
        Log.d("TPush", "Registration failed. Error code: " + errCode + "; error message: " + msg);
    }
});
```

The log of successful registration filtered by "TPush" is as follows:

```xml
TPNS register push success with token : 6ed8af8d7b18049d9fed116a9db9c71ab44d5565
```
### Disabling log printing
If you call `XGPushConfig.enableDebug(context, false)` to disable SDK debugging logs, the SDK still prints certain daily run logs (including the Tencent Push Notification Service token) by default.

You can call the following method in `Application.onCreate` to stop printing such daily run logs in the console：
```java
new XGPushConfig.Build(context).setLogLevel(Log.ERROR);
```

## Code Obfuscation

If you perform code obfuscation by using tools such as ProGuard in your project, keep the following options; otherwise, the Tencent Push Notification Service will become unavailable:

```xml
-keep public class * extends android.app.Service
-keep public class * extends android.content.BroadcastReceiver
-keep class com.tencent.android.tpush.** {*;}
-keep class com.tencent.tpns.baseapi.** {*;} 
-keep class com.tencent.tpns.mqttchannel.** {*;}
-keep class com.tencent.tpns.dataacquisition.** {*;}

-keep class com.tencent.bigdata.baseapi.** {*;}   // This configuration item is not required on v1.2.0.1 or later
-keep class com.tencent.bigdata.mqttchannel.** {*;}  // This configuration item is not required on v1.2.0.1 or later
```

>! If the Tencent Push Notification Service SDK is included in the application's common SDK, you still need to configure obfuscation rules for the main project application even though the common SDK includes obfuscation rules.

## Advanced Configuration (Optional)


### Disabling session keep-alive

To disable the feature, call the following API in `onCreate` of `Application` or `LauncherActivity` during application initialization and pass in `false`:
>! 
>- The session keep-alive feature can be disabled only in SDK v1.1.6.0 or later. In SDKs earlier than v1.1.6.0, the feature is enabled by default and cannot be disabled.
>- Starting from Tencent Push Notification Service SDK v1.2.6.0, the session keep-alive feature is disabled by default, and you do not need to call this API.
>

```java
XGPushConfig.enablePullUpOtherApp(Context context, boolean pullUp);
```

If you use Gradle automatic integration, configure the following node under the `<application>` tag of the `AndroidManifest.xml` file of your application, where `xxx` is a custom name. For manual integration, modify node attributes as follows:
```xml
<!-- Add the following node to the `AndroidManifest.xml` file of your application, where xxx is a custom name: -->     
<!-- To disable the feature of keep-alive with Tencent Push Notification Service, configure as follows: -->
<provider
		 android:name="com.tencent.android.tpush.XGPushProvider"
		 tools:replace="android:authorities"
		 android:authorities="application package name.xxx.XGVIP_PUSH_AUTH"
		 android:exported="false" />    
```

If the following log is printed in the console, the session keep-alive feature has been disabled: `I/TPush: [ServiceUtil] disable pull up other app`

### Suggestions on getting the Tencent Push Notification Service token

After you integrate the SDK, we recommend that you use gestures or other methods to display the Tencent Push Notification Service token in the application's less commonly used UIs such as **About** or **Feedback**. The console and RESTful APIs need to use the token to push messages. Subsequent troubleshooting will also need the token for problem locating.
Sample code:

```java
// Get the token
XGPushConfig.getToken(getApplicationContext());
```

### Suggestions on getting Tencent Push Notification Service running logs

The SDK provides a log reporting API. If you encounter push-related problems after the application is launched, trigger this API to upload SDK running logs and get the download address of the log file returned by the callback to facilitate troubleshooting. For more information, see [here](https://www.tencentcloud.com/document/product/1024/30715#reporting-logs).

Sample code:
```java
XGPushManager.uploadLogFile(context, new HttpRequestCallback() {
    @Override
    public void onSuccess(String result) {
        Log.d("TPush", "Upload succeeded. File address:" + result);
    }
        @Override
    public void onFailure(int errCode, String errMsg) {
        Log.d("TPush", "Upload failed. Error code:" + errCode + ", error message:" + errMsg);
    }
});
```


### Suggestions on privacy policy statement

When applying for application permissions, you can use the following content to declare the purpose of authorization:


<pre>
We use <a href="https://cloud.tencent.com/product/tpns">Tencent Push Notification Service</a> to push product information. After you authorize us the `android.permission.INTERNET` and `android.permission.ACCESS_NETWORK_STATE` permissions, you agree to the <a href="https://cloud.tencent.com/document/product/548/50955">Tencent SDK Privacy Agreement</a>. You can refuse to accept this SDK push service by disabling the notification option on the terminal device.
</pre>

The links to the two authorization items mentioned above are as follows:
- Tencent Push Notification Service: `https://cloud.tencent.com/product/tpns`
