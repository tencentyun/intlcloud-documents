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
    implementation  'com.tencent.xinge:xinge:4.3.2-release'
    // jg package
    implementation'com.tencent.jg:jg:1.1'
    // wup package
    implementation 'com.tencent.wup:wup:1.0.0.E-Release'
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
- Versions above 4.X are already compatible with Android P. HTTPS is used by default. If you want to use HTTP, you need to configure it by yourself ([Click here to view the configuration method](https://intl.cloud.tencent.com/document/product/1024/30723).


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
![](https://main.qcloudimg.com/raw/bfeccdabcf0a555e00b8b87983146841.png)



(5) Open Androidmanifest.xml, add the following configuration (it is recommended to see the demo in the downloaded package for modification), where YOUR_ACCESS_ID and YOUR_ACCESS_KEY should be replaced with the accessId and accessKey of the app. Please ensure that the configuration is completed as required; otherwise, the service may fail.

```
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


## Registration and Partial Log Output

<hr>

1. According to <a href="https://intl.cloud.tencent.com/document/product/1024/30713" target="_blank" >manual access</a> or <a href="https://intl.cloud.tencent.com/document/product/1024/30713" target="_blank" >automatic access</a>, get the TPNS registration log after configuring TPNS (it is recommended to call the registration API with callback during the access process to enable debugging log output of TPNS. For Android Studio, it is recommended to use automatic access via jcenter, without having to configure each node of TPNS in the configuration file as all of them are imported by the dependencies.)

**Enable debugging log data**

```java
XGPushConfig.enableDebug(this,true);
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

```




