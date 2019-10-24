# Android SDK integration guide

### Operation Scenarios
Android SDK provided by TPNS contains APIs for clients to implement push messages. This document provides two integration methods.


## 1. AndroidStudio Gradle automatic integration method

### Steps
**Before configuring the SDK, ensure the application for Android platform has already been created**
1. Go to the [Application List](https://console.cloud.tencent.com/tpns/applist) page to get the application package name, accessID, and accessKey.

Configure the following content in the build.gradle file:

```
android {
    ......
    defaultConfig {

        // The package name registered in the console. Note that the application ID, the current app package name, and the app package name registered in the console must be the same.
        applicationId "your package name"
        ......

        ndk {
            // Choose and add .so files corresponding to the cpu type as needed.
            abiFilters 'armeabi', 'armeabi-v7a', 'arm64-v8a'
            // You can also add 'x86', 'x86_64', 'mips', and 'mips64'.
        }

        manifestPlaceholders = [

            XG_ACCESS_ID:"accessid of the registered app",
            XG_ACCESS_KEY : "accesskey of the registered app",
        ]
        ......
    }
    ......
}

dependencies {
    ......
    //Add the following dependencies:
    implementation 'com.tencent.jg:jg:1.1'
    implementation 'com.tencent.tpns:tpns:1.1.0.2-release' //  TPNS Push


}
```

### Note:

- If the following notification pops up in Android Studio after you add the above-mentioned abiFilter configuration:
NDK integration is deprecated in the current plugin. Consider trying the new experimental plugin.

    Then add the following to the gradle.properties file in the project's root directory:

    android.useDeprecatedNdk=true

- If you need to listen to messages, see the XGPushBaseReceiver API or the MessageReceiver class in the demo. You can inherit XGPushBaseReceiver and configure the following content in the configuration file:
    ```xml
    <receiver android:name="Complete class name, such as: com.qq.xgdemo.receiver.MessageReceiver">
        <intent-filter>
        <!-- Receive message passthrough -->
        <action android:name="com.tencent.android.tpush.action.PUSH_MESSAGE" />
        <!-- Listen to results of registration, unregistration, tag setting/deletion, and notification click ->
        <action android:name="com.tencent.android.tpush.action.FEEDBACK" />
        </intent-filter>
    </receiver>
    ```




## 2. Android Studio manual Integration configuration method

> If the first integration method is not suitable, you can use the manual integration method.

### Project Configuration


Steps to import SDK into the project are as follows:

(1) Create or open an Android project (for more information on how to create an Android project, see the developer environment section).

(2) Copy all the .jar files in the libs directory under the TPNS SDK directory to the libs (or lib) directory of the project.

(3) .so files are necessary components of TPNS and support armeabi, armeabi-v7a, arm64-v8a, mips, mips64, x86, and x86_64 platforms. Please add the appropriate platform currently supported by your .so files.

(5) Open Androidmanifest.xml, add the following configuration (we recommend you refer to the demo for modification), where YOUR_ACCESS_ID and YOUR_ACCESS_KEY should be replaced with the acce:ssId and accessKey of the app. Please configure as required, otherwise the service may fail.

#### Permissions Configuration
Permissions needed for TPNS SDK to function properly:
```xml
    <!-- **Required** Permissions required by the TPNS SDK VIP version -->
    <permission
        android:name="app package name.permission.XGPUSH_RECEIVE"
        android:protectionLevel="signature" />
    <uses-permission android:name="app package name.permission.XGPUSH_RECEIVE" />

    <!-- **(Required)** Permissions required by the TPNS SDK -->
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />

    <!-- **(Commonly used)** Permissions required by the TPNS SDK-->
    <uses-permission android:name="android.permission.WAKE_LOCK" />
    <uses-permission android:name="android.permission.VIBRATE" />
    <uses-permission android:name="android.permission.RECEIVE_USER_PRESENT" />
    <uses-permission android:name="android.permission.READ_PHONE_STATE" />
```

#### Component and application message configuration

```xml
<application>
    <!-- Other application configurations -->

    <!-- **Required** TPNS
default notification -->
    <activity
        android:name="com.tencent.android.tpush.XGPushActivity">
        <intent-filter>
            <action android:name="android.intent.action" />
        </intent-filter>
    </activity>

    <!-- **Required** TPNS
receiver broadcast receiver-->
    <receiver
        android:name="com.tencent.android.tpush.XGPushReceiver"
        android:process=":xg_vip_service">
        <intent-filter android:priority="0x7fffffff">
            <!-- **Required** TPNS
SDK internal broadcast -->
            <action android:name="com.tencent.android.xg.vip.action.SDK" />
            <action android:name="com.tencent.android.xg.vip.action.INTERNAL_PUSH_MESSAGE" />
              <action android:name="com.tencent.android.xg.vip.action.ACTION_SDK_KEEPALIVE" />


            <!-- **Optional** System broadcast: network switching -->
            <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
            <!-- **(Optional)** System broadcast: splash screen -->
            <action android:name="android.intent.action.USER_PRESENT" />
            <!-- [Optional] Common system broadcast for increasing the possibility of TPNS service reactivation. You can also add broadcast customized by the app to activate the service -->
            <action android:name="android.bluetooth.adapter.action.STATE_CHANGED" />
            <action android:name="android.intent.action.ACTION_POWER_CONNECTED" />
            <action android:name="android.intent.action.ACTION_POWER_DISCONNECTED" />
        </intent-filter>
    </receiver>

    <!-- **Required** TPNS
service -->
    <service
        android:name="com.tencent.android.tpush.service.XGVipPushService"
        android:persistent="true"
        android:process=":xg_vip_service"></service>

    <!-- Cloud Control -->
    <receiver android:name="com.tencent.android.tpush.cloudctr.network.CloudControlDownloadReceiver">
        <intent-filter>
            <action android:name="com.tencent.android.xg.vip.action.cloudcontrol.action.DOWNLOAD_FILE_FINISH" />
        </intent-filter>
    </receiver>
    <service android:name="com.tencent.android.tpush.cloudctr.network.CloudControlDownloadService" />

    <!-- **Required** Notification service, android:name should be changed into the current package name -->
    <service android:name="com.tencent.android.tpush.rpc.XGRemoteService">
        <intent-filter>
            <!-- **Required** Modify to the current app package name.XGVIP_PUSH_ACTION -->
            <action android:name="app package name.PUSH_ACTION" />
        </intent-filter>
    </service>

    <!-- **Required** **Note** Modify authorities to package name.XGVIP_PUSH_AUTH -->
    <provider
        android:name="com.tencent.android.tpush.XGPushProvider"
        android:authorities="app package name.XGVIP_PUSH_AUTH" />

    <!-- **Required** **Note** Modify authorities to package name.TPUSH_PROVIDER -->
    <provider
        android:name="com.tencent.android.tpush.SettingsContentProvider"
        android:authorities="app package name.TPUSH_PROVIDER" />

    <!-- **Optional** Used to strengthen the keep-alive capability -->
    <provider
        android:name="com.tencent.android.tpush.XGVipPushKAProvider"
        android:authorities="app package name.AUTH_XGPUSH_KEEPALIVE"
        android:exported="true" />

    <!-- **(Optional)** Receiver implemented by the app, which is used to receive the message passthrough and call back the operation result. Please add as needed -->
    <!-- YOUR_PACKAGE_PATH.CustomPushReceiver should be changed to your own receiver: -->
    <receiver android:name="app package name.MessageReceiver">
        <intent-filter>
            <!-- Receive message passthrough -->
            <action android:name="com.tencent.android.xg.vip.action.PUSH_MESSAGE" />
            <!-- Listen to results of registration, unregistration, tag setting/deletion, and notification click ->
            <action android:name="com.tencent.android.xg.vip.action.FEEDBACK" />
        </intent-filter>
    </receiver>

    <!-- MQTT START-->
    <service android:exported="false"
             android:process=":xg_vip_service"
             android:name="com.tencent.bigdata.mqttchannel.services.MqttService" />

    <!--**Note** Modify authorities to package name .XG_SETTINGS_PROVIDER, for example, the package name of demo is com.tencent.android.xg.cloud.demo -->
    <provider
        android:exported="false"
        android:name="com.tencent.bigdata.baseapi.base.SettingsContentProvider"
        android:authorities="app package name.XG_SETTINGS_PROVIDER" />

    <!-- MQTT END-->

    <!-- **Required** Change to the AccessId of your app, which is a 10-digit number beginning with "21" and cannot contain spaces -->
    <meta-data
        android:name="XG_V2_ACCESS_ID"
        android:value="The AccessID of the app" />
    <!-- **Required** Change to the AccessKey of your app, which is a 12-character string beginning with "A" and cannot contain spaces -->
    <meta-data
        android:name="XG_V2_ACCESS_KEY"
        android:value="The AccessKey of the app" />

</application>

<!-- **Required** Permissions required by TPNS SDK version 5.0 -->
<permission
    android:name="app package name.permission.XGPUSH_RECEIVE"
    android:protectionLevel="signature" />
<uses-permission android:name="app package name.permission.XGPUSH_RECEIVE" />

<!-- **Required** Permissions required by TPNS SDK -->
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.WAKE_LOCK" />

<!-- **Common** Permissions required by TPNS-->
<uses-permission android:name="android.permission.VIBRATE" />
<uses-permission android:name="android.permission.RECEIVE_USER_PRESENT" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```
<hr>

## 3. Debugging and device registration

**Enable debug log data**
Note: Set this to false when going online
```java
XGPushConfig.enableDebug(this,true);
```


**token registration**

```java
XGPushManager.registerPush(this, new XGIOperateCallback() {
    @Override
    public void onSuccess(Object data, int flag) {
        // token may change when the device is uninstalled and then reinstalled
        Log.d("TPush", "The registration is successful, the device token is: " + data);
    }

    @Override
    public void onFail(Object data, int errCode, String msg) {
        Log.d("TPush", "The registration failed, error code: " + errCode + ", error message: " + msg);
    }
});
```
Log of a successful registration filtered by "TPush" is as follows:

```xml
XG register push success with token : 6ed8af8d7b18049d9fed116a9db9c71ab44d5565
```
<hr>

## 4. Code Obfuscation

If your project uses tools such as ProGuard to obfuscate the code, please keep the following options, otherwise theTPNS service will not be available.

```xml
-keep public class * extends android.app.Service
-keep public class * extends android.content.BroadcastReceiver
-keep class com.tencent.android.tpush.** {* ;}
-keep class com.tencent.bigdata.baseapi.** {* ;}
-keep class com.tencent.bigdata.mqttchannel.** {* ;}
-keep class com.tencent.tpns.dataacquisition.** {* ;}

```

<hr>

## 5. API changes with 4.x

**1. Account registration API is deleted. Accounts can only be set via bindAccount or appendAccount**

```java
// The following APIs were deleted
XGPushManager.registerPush(Context context, String account)
XGPushManager.registerPush(Context context, String account, final XGIOperateCallback callback)
XGPushManager.registerPush(Context context, String account,String url, String payload, String otherToken, final XGIOperateCallback callback)
```

registerPush no longer supports account configuration. If you need to register for an account, you must call bindAccount or appendAccount. We recommend you call this in callback with successful registerPush

**2. When inheriting XGPushBaseReceiver, you must implement the following functions**
```java
/**
 * Account setting result processing function
 */
public abstract void onSetAccountResult(Context context, int errorCode,
        String operateName);

/**
 * Account deletion result processing function
 */
public abstract void onDeleteAccountResult(Context context, int errorCode,
        String operateName);
```


