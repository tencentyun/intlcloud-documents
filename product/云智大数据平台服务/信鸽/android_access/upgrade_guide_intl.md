## Automated Integration via Android Studio

### Importing Dependencies
In Android Studio, you can automatically access TPNS using jcenter remote repository, without having to import jar packages or so files to the project.
There is no need to configure TPNS-related content in AndroidManifest.xml as jcenter will automatically import.
After the dependencies are imported, modify the app configuration and write the registration code to achieve fast access to TPNS. 
The corresponding dependencies are all the latest version at the official website.
For the user-defined receiver, you need to configure related nodes in Androidmanifest.xml.

Configure the following in the ```app's build.gradle``` file.

```java
    
    android {
        ......
        defaultConfig {

            // The package name registered at TPNS' official website. Note that the application ID, the current app package name, and the package name of the app registered at TPNS' official website must be the same.
            applicationId "your package name" 
            ......

            ndk {
                // Choose and add the .so libraries corresponding to the cpu type as needed. 
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
    
    // jar of the TPNS general version with no vendor-specific channels.
    implementation  'com.tencent.xinge:xinge:4.0.5-release'
    //implementation'com.tencent.xinge:xinge:4.3.2-beta'
    // jg package
    implementation'com.tencent.jg:jg:1.1'
    // wup package
    implementation 'com.tencent.wup:wup:1.0.0.E-release'
    // mid package, minSdkVersion 14
    implementation 'com.tencent.mid:mid:4.0.7-Release'
        
    }
```

**Note:**

- If Android Studio prompts the following after you add the abiFilter configuration above:

NDK integration is deprecated in the current plugin. Consider trying the new experimental plugin.

Please add the following to the gradle.properties file in the project's root directory:

android.useDeprecatedNdk=true


- If you need to listen to messages, please see the XGBaseReceiver API or the MessageReceiver class of the demo. Inherit XGBaseReceiver and configure the following in the configuration file:

```xml
<receiver android:name="Complete class name such as: com.qq.xgdemo.receiver.MessageReceiver"
android:exported="true" >
<intent-filter>
<!-- Receive message passthrough -->
<action android:name="com.tencent.android.tpush.action.PUSH_MESSAGE" />
<!-- Listen to handling results such as registration, unregistration, tag setting/deletion, and notification tap ->
<action android:name="com.tencent.android.tpush.action.FEEDBACK" />
</intent-filter>
</receiver>
```
- Versions above 4.X are already compatible with Android P. HTTPS is used by default. If you want to use HTTP, you need to configure it by yourself ([Click here to view the configuration method](https://intl.cloud.tencent.com/document/product/1024/30723)).


## Manual Configuration for Integration
### Registering and Downloading the SDK

<hr>

Visit the TPNS console at xg.qq.com, log in with your QQ account number, go to the app registration page, enter the "App name" and "App package name" (which must be the same with the app), select "Operating system" and "Category", and click "Create app".

After the app is created successfully, click "App configuration" to view the app-specific information such as  AccessId and AccessKey.

After registration is completed, download the latest version of the Android SDK to your local system and unzip it.

### Project Configuration

<hr>

The steps to import the SDK into the project are as follows:

(1) Create or open an Android project (for more information about how to create an Android project, see the developing environment section).

(2) Copy all the files in the libs directory under the TPNS SDK directory to the libs (or lib) directory of the project.

(3) Select the TPNS jar packages in the libs (or lib) directory, right-click them and select Build Path, and select Add to Build Path to add the SDK to the reference directory of the project.
(4).so files are necessary components of TPNS and support armeabi, armeabi-v7a, misp and x86 platforms. Please add the appropriate .so files according to the platform currently supported.

a) If your project does not use other .so files, it is recommended to copy the four platform directories to your project;

b) If there are already .so files, you only need to copy the files in the corresponding directory of TPNS;

c) If the app is a game with MSDK access, usually only the .so files in the armeabi directory are needed;

d) If the current project already has armeabi, then you only need to add the .so files in the armeabi directory of TPNS but not other directories. In other similar situations,
only add the ones that exist on the current platform;

e) If an error (10004.SOERROR) occurs when you import the .so files to Android Studio, add the file named jniLibs in the main file directory.
Then, copy all the schema files into it, i.e., all the folders under Other-Platform-SO in the SDK directory. See the figure below:
![![](https://main.qcloudimg.com/raw/bfeccdabcf0a555e00b8b87983146841.png)



(5) Open Androidmanifest.xml, add the following configuration (it is recommended to see the demo in the downloaded package for modification), where YOUR_ACCESS_ID and YOUR_ACCESS_KEY should be replaced with the accessId and accessKey of the app. Please ensure that the configuration is completed as required; otherwise, the service may fail.

```xml
<application
<!-- TPNS broadcast receiver, which is **required** -->
<receiver android:name="com.tencent.android.tpush.XGPushReceiver"
android:process=":xg_service_v4" >
<intent-filter android:priority="0x7fffffff" >
<!-- **(Required)** The internal broadcast of the TPNS SDK -->
<action android:name="com.tencent.android.tpush.action.SDK" />
<action android:name="com.tencent.android.tpush.action.INTERNAL_PUSH_MESSAGE" />
<!-- **(Required)** System broadcast: splash screen and network switch -->
<action android:name="android.intent.action.USER_PRESENT" />
<action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
<!-- **(Optional)** Some commonly used system broadcasts, which enhance the chance of restart of the TPNS service. Please choose as needed. You can also add some custom broadcasts of the app to start the service -->
<action android:name="android.bluetooth.adapter.action.STATE_CHANGED" />
<action android:name="android.intent.action.ACTION_POWER_CONNECTED" />
<action android:name="android.intent.action.ACTION_POWER_DISCONNECTED" />
</intent-filter>
</receiver>

<!-- **(Optional)** The receiver implemented by the app, which is used to receive the message passthrough and call back the operation result. Please add as needed -->
<!-- YOUR_PACKAGE_PATH.CustomPushReceiver should be changed to your own receiver: -->
<receiver android:name="com.qq.xgdemo.receiver.MessageReceiver"
android:exported="true" >
<intent-filter>
<!-- Receive message passthrough -->
<action android:name="com.tencent.android.tpush.action.PUSH_MESSAGE" />
<!-- Listen to handling results such as registration, unregistration, tag setting/deletion, and notification tap ->
<action android:name="com.tencent.android.tpush.action.FEEDBACK" />
</intent-filter>
</receiver>

<!-- **Note:** If the start mode of the opened activity is SingleTop, SingleTask, or SingleInstance, please handle it according to the 8th point in the notification troubleshooting self-check list -->
<activity
android:name="com.tencent.android.tpush.XGPushActivity"
android:exported="false" >
<intent-filter>
<!-- If Android Studio is used, please set android:name="android.intent.action"-->
<action android:name="" />
</intent-filter>
</activity>

<!-- **(Required)** TPNS service -->
<service
android:name="com.tencent.android.tpush.service.XGPushServiceV4"
android:exported="true"
android:persistent="true"
android:process=":xg_service_v4" />


<!-- **(Required)** This improves the survival rate of the service -->
<service
android:name="com.tencent.android.tpush.rpc.XGRemoteService"
android:exported="true">
<intent-filter>
<!-- **(Required)** Please change to the current app package name.PUSH_ACTION, such as the demo package name: com.qq.xgdemo -->
<action android:name="current app package name.PUSH_ACTION" />
</intent-filter>
</service>


<!-- **(Required)** **Note:** The authorities should be changed to the package name.AUTH_XGPUSH, such as the demo package name: com.qq.xgdemo -->
<provider
android:name="com.tencent.android.tpush.XGPushProvider"
android:authorities="current app package name.AUTH_XGPUSH"
android:exported="true"/>

<!-- **(Required)** **Note:** The authorities should be changed to the package name.TPUSH_PROVIDER, such as the demo package name: com.qq.xgdemo -->
<provider
android:name="com.tencent.android.tpush.SettingsContentProvider"
android:authorities="current app package name.TPUSH_PROVIDER"
android:exported="false" />

<!-- **(Required)** **Note:** The authorities should be changed to the package name.TENCENT.MID.V3, such as the demo package name: com.qq.xgdemo -->
<provider
android:name="com.tencent.mid.api.MidProvider"
android:authorities="current app package name.TENCENT.MID.V3"
android:exported="true" >
</provider>



<!-- **(Required)** Please change YOUR_ACCESS_ID to the AccessId of your app, which is a 10-digit number beginning with "21" and cannot contain spaces -->
<meta-data
android:name="XG_V2_ACCESS_ID"
android:value="YOUR_ACCESS_ID" />
<!-- **(Required)** Please change YOUR_ACCESS_KEY to the AccessKey of your app, which is a 12-character string beginning with "A" and cannot contain spaces -->
<meta-data
android:name="XG_V2_ACCESS_KEY"
android:value="YOUR_ACCESS_KEY" />
</application>
<!-- **(Required)** Permissions required by the TPNS SDK -->
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.WAKE_LOCK" />
<uses-permission android:name="android.permission.VIBRATE" />
<!-- **(Commonly used)** Permissions required by the TPNS SDK-->
<uses-permission android:name="android.permission.RECEIVE_USER_PRESENT" />
<uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.WRITE_SETTINGS" />
<!-- **(Optional)** Permissions required by the TPNS SDK-->
<uses-permission android:name="android.permission.RESTART_PACKAGES" />
<uses-permission android:name="android.permission.BROADCAST_STICKY" />
<uses-permission android:name="android.permission.KILL_BACKGROUND_PROCESSES" />
<uses-permission android:name="android.permission.GET_TASKS" />
<uses-permission android:name="android.permission.READ_LOGS" />
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.BATTERY_STATS" />

```




### Manual Configuration for Integration by Upgrading from 3.x to 4.x

1.	 **(Required)** Extract the latest jar packages from the SDK directory and replace the current TPNS SDK version.                         
2.	 **(Required)** Based on the required platform, extract ```libtpnsSecurity.so``` and  replace the old version, and delete the original ```libxguardian.so```

3. **(Required)** Check whether the configuration is correct (upgrading from v3 to v4)
```
com.tencent.android.tpush.service.XGPushServiceV4
com.tencent.android.tpush.XGPushReceiver
```


```xml
<!-- **(Required)** TPNS service -->
       <service
           android:name="com.tencent.android.tpush.service.XGPushServiceV4"
           android:exported="true"
           android:persistent="true"
           android:process=":xg_service_v4" />

<!-- **(Required)** Notification service; this option helps to improve the arrival rate -->
       <receiver
            android:name="com.tencent.android.tpush.XGPushReceiver"
            android:process=":xg_service_v4" >
            <intent-filter android:priority="0x7fffffff" >

                <!-- **(Required)** The internal broadcast of the TPNS SDK -->
                <action android:name="com.tencent.android.tpush.action.SDK" />
                android:name="com.tencent.android.tpush.action.INTERNAL_PUSH_MESSAGE" />
                <!-- **(Required)** System broadcast: network switch -->
                <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />

                <!-- **(Optional)** System broadcast: splash screen -->
                <action android:name="android.intent.action.USER_PRESENT" />

                <!-- **(Optional)** Some commonly used system broadcasts, which enhance the chance of restart of the TPNS service. Please choose as needed. You can also add some custom broadcasts of the app to start the service -->
                <action android:name="android.bluetooth.adapter.action.STATE_CHANGED" />
                <action android:name="android.intent.action.ACTION_POWER_CONNECTED" />
                <action android:name="android.intent.action.ACTION_POWER_DISCONNECTED" />
            </intent-filter>
            <!-- **(Optional)** USB-related system broadcasts, which enhance the chance of restart of the TPNS service. Please add as needed -->
            <intent-filter android:priority="0x7fffffff" >
                <action android:name="android.intent.action.MEDIA_UNMOUNTED" />
                <action android:name="android.intent.action.MEDIA_REMOVED" />
                <action android:name="android.intent.action.MEDIA_CHECKING" />
                <action android:name="android.intent.action.MEDIA_EJECT" />

                <data android:scheme="file" />
            </intent-filter>
        </receiver>
        
```


 ###	 **(Optional)** If you need to use multiple channels, add the following configuration:

<!-- Mi configuration -->
```xml


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


        <receiver
            android:name="com.tencent.android.mipush.XMPushMessageReceiver"
            android:exported="true" >
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
		
		 <!-- Note: Meizu Push -->
        <service
            android:name="com.meizu.cloud.pushsdk.NotificationService"
            android:exported="true" />

        <receiver android:name="com.meizu.cloud.pushsdk.SystemReceiver" >
            <intent-filter>
                <action android:name="com.meizu.cloud.pushservice.action.PUSH_SERVICE_START" />

                <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
        </receiver>
        <receiver android:name="com.tencent.android.mzpush.MZPushMessageReceiver" >
            <intent-filter>

                <!-- Receive push message -->
                <action android:name="com.meizu.flyme.push.intent.MESSAGE" />
                <!-- Receive register message -->
                <action android:name="com.meizu.flyme.push.intent.REGISTER.FEEDBACK" />
                <!-- Receive unregister message -->
                <action android:name="com.meizu.flyme.push.intent.UNREGISTER.FEEDBACK" />
                <action android:name="com.meizu.c2dm.intent.REGISTRATION" />
                <action android:name="com.meizu.c2dm.intent.RECEIVE" />
                <!-- Your app package name -->
                <category android:name="your app package name" >
                </category>
            </intent-filter>
        </receiver>
		
		<!-- Note: This is the beginning required by Huawei Push -->
		<meta-data
        android:name="com.huawei.hms.client.appid"
        android:value="Your registered Huawei APPID" >
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
            android:authorities="your app package name.hms.update.provider"
            android:exported="false"
            android:grantUriPermissions="true" >
        </provider>



        <receiver android:name="com.huawei.hms.support.api.push.PushEventReceiver" >
            <intent-filter>

                <!-- Receive notification bar messages from the channel, which is compatible with the old version of PUSH -->
                <action android:name="com.huawei.intent.action.PUSH" />
            </intent-filter>
        </receiver>
        <receiver android:name="com.tencent.android.hwpush.HWPushMessageReceiver" >
            <intent-filter>

                <!-- Required; used to receive TOKEN -->
                <action android:name="com.huawei.android.push.intent.REGISTRATION" />
                <!-- Required; used to receive message -->
                <action android:name="com.huawei.android.push.intent.RECEIVE" />
                <!-- Optional; used to trigger the onEvent callback after the notification bar or a button in the notification bar is tapped -->
                <action android:name="com.huawei.android.push.intent.CLICK" />
                <!-- Optional; used to check whether the PUSH channel is connected; not needed if there is no need to view -->
                <action android:name="com.huawei.intent.action.PUSH_STATE" />
            </intent-filter>
        </receiver>
		
		 <!-- Cloud control-related -->
        <receiver
            android:name="com.tencent.android.tpush.cloudctr.network.CloudControlDownloadReceiver"
            android:exported="true">
            <intent-filter>
                <action android:name="com.tencent.android.tpush.cloudcontrol.action.DOWNLOAD_FILE_FINISH" />
            </intent-filter>
        </receiver>
        <service
            android:name="com.tencent.android.tpush.cloudctr.network.CloudControlDownloadService"
            android:exported="true"
            android:persistent="true" />
        <!-- Cloud control-related - End -->
        
     <!-- Add vendor permissions -->
	 <!-- Compatible with Flyme versions below 5.0. Meizu's internal integration pushSDK is required; otherwise, messages cannot be received -->
    <uses-permission android:name="com.meizu.flyme.push.permission.RECEIVE"></uses-permission>
    <permission android:name="your app package name.push.permission.MESSAGE" android:protectionLevel="signature"/>
    <uses-permission android:name="your app package name.push.permission.MESSAGE"></uses-permission>
    <!-- Compatible with Flyme 3.0 configuration permissions -->
    <uses-permission android:name="com.meizu.c2dm.permission.RECEIVE" />
    <permission android:name="your app package name.permission.C2D_MESSAGE"
        android:protectionLevel="signature"></permission>
    <uses-permission android:name="your app package name.permission.C2D_MESSAGE"/>
    <!-- Note: This is the end of permission required by Meizu Push -->
	<!-- Permission required by Mi -->
    <permission
        android:name="your app package name.permission.MIPUSH_RECEIVE"
        android:protectionLevel="signature" />
    <uses-permission android:name="your app package name.permission.MIPUSH_RECEIVE" />
```




## Registration and Partial Log Output

<hr>

1. According to <a href="https://intl.cloud.tencent.com/document/product/1024/30713" target="_blank" >manual access</a> or <a href="https://intl.cloud.tencent.com/document/product/1024/30713" target="_blank" >automatic access</a>, get the TPNS registration log after configuring TPNS (it is recommended to call the registration API with callback during the access process to enable debugging log output of TPNS. For Android Studio, it is recommended to use automatic access via jcenter, without having to configure each node of TPNS in the configuration file as all of them are imported by the dependencies.)

**Enable debugging log data**

```java
XGPushConfig.enableDebug(this,true);
```

**Enable vendor-specific channel initialization code**


If otherpush version is used, you need to add the following to your app's attachBaseContext function:
```java
 StubAppUtils.attachBaseContext(context);
```

Add the following to the initialization or main page's onCreat function
```java

 XGPushConfig.enableOtherPush(getApplicationContext(), true);
 XGPushConfig.setHuaweiDebug(true);
 XGPushConfig.setMiPushAppId(getApplicationContext(), "APPID");
 XGPushConfig.setMiPushAppKey(getApplicationContext(), "APPKEY");
 XGPushConfig.setMzPushAppId(this, "APPID");
 XGPushConfig.setMzPushAppKey(this, "APPKEY");
```


**token registration**

```java
XGPushManager.registerPush(this, new XGIOperateCallback() {
@Override
public void onSuccess(Object data, int flag) {
// token may change after the app is uninstalled and then reinstalled on the device
Log.d("TPush", "The registration succeeded, and the device token is: " + data);
}
@Override
public void onFail(Object data, int errCode, String msg) {
Log.d("TPush", "The registration failed; error code: " + errCode + ", error message: " + msg);
}
})
```
The log of successful registration filtered by "TPush" is as follows:

```xml
10-09 20:08:46.922 24290-24303/com.qq.xgdemo I/XINGE: [TPush] get RegisterEntity:RegisterEntity [accessId=2100250470, accessKey=null, token=5874b7465d9eead746bd9374559e010b0d1c0bc4, packageName=com.qq.xgdemo, state=0, timestamp=1507550766, xgSDKVersion=3.11, appVersion=1.0]
10-09 20:08:47.232 24290-24360/com.qq.xgdemo D/TPush: The registration succeeded, and the device token is: 5874b7465d9eead746bd9374559e010b0d1c0bc4
```
**Vendor-specific channel token registration**

1. Start vendor-specific channel initialization and wait for the cloud controller to download the vendor's dex package for the corresponding device.
Take Mi as an example. The log of successful download is as follows:
```xml
10-25 15:16:31.067 16551-16551/? D/XINGE: [DownloadService] onCreate()
10-25 15:16:31.073 16551-16757/? D/XINGE: [DownloadService] action:onHandleIntent
10-25 15:16:31.083 16551-16757/? V/XINGE: [CloudCtrDownload] Create downloadControl
10-25 15:16:31.089 16551-16757/? I/XINGE: [CloudCtrDownload] action:download - url:https://pingjs.qq.com/xg/Xg-Xm-plug-1.0.2.pack, saveFilePath:/data/user/0/com.qq.xgdemo1122/app_dex/XG/5/, fileName:Xg-Xm-plug-1.0.2.pack
10-25 15:16:31.097 16551-16757/? V/XINGE: [CloudCtrDownload] Download file: Xg-Xm-plug-1.0.2.pack
10-25 15:16:31.641 16551-16757/? D/XINGE: [DownloadService] download file Succeed
10-25 15:16:31.650 16551-16757/? D/XINGE: [CloudCtrDownload] Download succeed.
10-25 15:16:31.653 16551-16551/? D/XINGE: [CloudControlDownloadReceiver] onReceive
10-25 15:16:31.673 16551-16738/? I/test: Download file SuccessXg-Xm-plug-1.0.2.pack to /data/user/0/com.qq.xgdemo1122/app_dex/XG/5/
```
2. After observing the downloaded log, kill the app process and restart the app to complete the registration:
```xml
10-25 15:34:26.423 18700-18700/? D/TPush: +++ register push sucess. token:22dc455f79d36dec1065418e1d284639bac776b4
10-25 15:34:26.432 18700-18731/? I/XINGE: [XGOtherPush] other push token is : lYDvOWispXGoVADhRyiVdw3krLIolEd21JqdmjqBqDISK+gwl/PBm3tA9U43jxfH other push type: xiaomi
```
**Set an account**

```java
// Note that TPNS v3.2.2 has upgraded the account binding and unbinding APIs. For details, see the API documentation.
XGPushManager.bindAccount(getApplicationContext(), "XINGE");
```
The log of successful account registration filtered by "TPush" is as follows:

```xml
// If the push returns error code 48: account invalid, please confirm whether the account API is successfully called
10-11 15:55:57.810 29299-29299/com.qq.xgdemo D/TPushReceiver: TPushRegisterMessage [accessId=2100250470, deviceId=853861b6bba92fb1b63a8296a54f439e, account=XINGE, ticket=0, ticketType=0, token=3f13f775079df2d54e1f82475a28bccd3bfef8c1] successful registration
```

**Set a tag**

```java
XGPushManager.setTag(this,"XINGE");
```

Log of successful tagging:

```xml
10-09 20:11:42.558 27348-27348/com.qq.xgdemo I/XINGE: [XGPushManager] Action -> setTag with tag = XINGE
```

**Receive message log**

```xml
10-16 19:50:01.065 5969-6098/com.qq.xgdemo D/XINGE: [i] Action -> handleRemotePushMessage
10-16 19:50:01.065 5969-6098/com.qq.xgdemo I/XINGE: [i] >> msg from service, @msgId=1 @accId=2100250470 @timeUs=1508154601660412 @recTime=1508154601076 @msg.date= @msg.busiMsgId=0 @msg.timestamp=1508154601 @msg.type=1 @msg.multiPkg=0 @msg.serverTime=1508154601000 @msg.ttl=259200 @expire_time=1508154860200076 @currentTimeMillis=1508154601076
10-16 19:50:01.095 5969-6098/com.qq.xgdemo D/XINGE: [m] Action -> handlerPushMessage
10-16 19:50:01.105 5969-6098/com.qq.xgdemo I/XINGE: [m] Receiver msg from server :PushMessageManager [msgId=1, accessId=2100250470, busiMsgId=0, content={"n_id":0,"title":"XGDemo","style_id":1,"icon_type":0,"builder_id":1,"vibrate":0,"ring_raw":"","content":"token push","lights":1,"clearable":1,"action":{"aty_attr":{"pf":0,"if":0},"action_type":1,"activity":""},"small_icon":"","ring":1,"icon_res":"","custom_content":{}}, timestamps=1508154601, type=1, intent=Intent { act=com.tencent.android.tpush.action.INTERNAL_PUSH_MESSAGE cat=[android.intent.category.BROWSABLE] pkg=com.qq.xgdemo (has extras) }, messageHolder=BaseMessageHolder [msgJson={"n_id":0,"title":"XGDemo","style_id":1,"icon_type":0,"builder_id":1,"vibrate":0,"ring_raw":"","content":"token push","lights":1,"clearable":1,"action":{"aty_attr":{"pf":0,"if":0},"action_type":1,"activity":""},"small_icon":"","ring":1,"icon_res":"","custom_content":{}}, msgJsonStr={"n_id":0,"title":"XGDemo","style_id":1,"icon_type":0,"builder_id":1,"vibrate":0,"ring_raw":"","content":"token push","lights":1,"clearable":1,"action":{"aty_attr":{"pf":0,"if":0},"action_type":1,"activity":""},"small_icon":"","ring":1,"icon_res":"","custom_content":{}}, title=XGDemo, content=token push, customContent=null, acceptTime=null]]
10-16 19:50:01.105 5969-6098/com.qq.xgdemo V/XINGE: [XGPushManager] Action -> msgAck(com.qq.xgdemo,1)
10-16 19:50:01.115 5969-6098/com.qq.xgdemo I/XINGE: [TPush] title encry obj:{"cipher":"YZXM+CuPhqaBn4eK0SE9ApWieHznugNT2uKo0OaXtlDDHLJiY7NlvSL2ZnlSb8E7yd7E7i9JU3g0PlFyYNLjokNp1buJuPoMYEHaJ0s6vmUMY+cq0Sv782XHxNzekV4a9mRcJ5xsOccIjH1VoskUmikfZJo3XLhZveWNYGPaoto="}
10-16 19:50:01.125 5969-6098/com.qq.xgdemo E/XINGE: [MessageInfoManager] delOldShowedCacheMessage Error! toDelTime: 1507981801138
10-16 19:50:01.145 5969-6098/com.qq.xgdemo I/XINGE: [MessageHelper] Action -> showNotification {"n_id":0,"title":"XGDemo","style_id":1,"icon_type":0,"builder_id":1,"vibrate":0,"ring_raw":"","content":"token push","lights":1,"clearable":1,"action":{"aty_attr":{"pf":0,"if":0},"action_type":1,"activity":""},"small_icon":"","ring":1,"icon_res":"","custom_content":{}}

```

## Code Obfuscation


If your project uses tools such as ProGuard to obfuscate the code, please keep the following options; otherwise, the TPNS service will not be available.

```xml
-keep public class * extends android.app.Service
-keep public class * extends android.content.BroadcastReceiver
-keep class com.tencent.android.tpush.** {* ;}
-keep class com.tencent.mid.** {* ;}
-keep class com.qq.taf.jce.** {*;}
-keep class com.tencent.bigdata.** {* ;}

Huawei channel
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

Mi channel
-keep class com.xiaomi.**{*;}
-keep public class * extends com.xiaomi.mipush.sdk.PushMessageReceiver

Meizu channel
-dontwarn com.meizu.cloud.pushsdk.**
-keep class com.meizu.cloud.pushsdk.**{*;}

```




