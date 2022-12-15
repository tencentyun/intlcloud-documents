## General Upgrade Steps

### Automated integration via Android Studio
If your project is integrated by pulling dependencies remotely and doesn't involve the specific versions as described below, you can directly replace the Tencent Push Notification Service SDK dependencies added to the project with those on the latest version, which can be viewed and obtained in [SDK for Android](https://intl.cloud.tencent.com/document/product/1024/36191).

>! 
> - If your currently used version is largely different from the latest version, be sure to modify the configurations by referring to the version changes below.
> - Generally, we recommend you also upgrade and modify the vendor push dependencies from the Tencent Push Notification Service SDK.

For example, if the current version is 1.3.3.3 and the latest version is 1.3.6.2, you need to change your SDK dependency version from 1.3.3.3 to 1.3.6.2:
```
dependencies {
    // Tencent Push Notification Service main package
    implementation "com.tencent.tpns:tpns:1.3.6.2-release"

    // Mi push dependency package
    implementation "com.tencent.tpns:xiaomi:1.3.6.2-release"

    // Meizu push dependency package
    implementation "com.tencent.tpns:meizu:1.3.6.2-release"
    
    // Huawei push dependency package
    implementation "com.tencent.tpns:huawei:1.3.6.2-release"
    // Dependency package for the HMS Core Push module of Huawei push
    implementation 'com.huawei.hms:push:6.7.0.300'       

    // OPPO push dependency package
    implementation "com.tencent.tpns:oppo:1.3.6.2-release"
    // For SDK v1.3.2.0 or later, you need to add the following dependency statements. Otherwise, the registration of OPPO PUSH will fail.
    implementation 'com.google.code.gson:gson:2.6.2'
    implementation 'commons-codec:commons-codec:1.15'

    // vivo push dependency package
    implementation "com.tencent.tpns:vivo:1.3.6.2-release"

    // HONOR push dependency package
    implementation "com.tencent.tpns:honor:1.3.6.2-release"
}
```


### Integration via Eclipse
If your project is integrated by importing JAR files manually and doesn't involve the specific versions as described below, refer to the following steps to make changes:
1. Obtain the latest SDK package from [SDK Download](https://console.cloud.tencent.com/tpns/sdkdownload).
2. Replace the original `tpns-*.jar` files in the project with the `tpns-*.jar` files in the `libs` directory of the SDK package.

>! 
> - If your currently used version is largely different from the latest version, be sure to modify the configurations by referring to the version changes below.
> - Generally, we recommend you also upgrade and replace the vendor push dependencies from the Tencent Push Notification Service SDK.


### Integration via other toolkits
If your project is integrated via other third-party toolkits such as MSDK and GCloud, refer to their respective upgrade guides first.

## Android SDK 1.3.6.2
SDK v1.3.6.2 has upgraded the versions of Huawei and Mi push dependencies. The original versions of vendor push SDKs currently in use are as follows:
- Huawei: 6.7.0.300
- Mi: 5.1.0
- Meizu: 4.1.0
- OPPO: 3.1.0
- vivo: 3.0.0.4


## Android SDK 1.3.6.1
SDK v1.3.6.1 has upgraded the versions of Mi and OPPO push dependencies. The original versions of vendor push SDKs currently in use are as follows:
- Huawei: 6.5.0.300
- Mi: 5.0.8
- Meizu: 4.1.0
- OPPO: 3.1.0
- vivo: 3.0.0.4

## Android SDK 1.3.2.0
SDK v1.3.2.0 has upgraded the versions of vendor push dependencies as detailed below:
- Huawei: 6.3.0.302
- Mi: 4.9.1
- Meizu: 4.1.0
- OPPO: 3.0.0
- vivo: 3.0.0.4

Upgraded vendor push dependencies involve changed configurations. See below to make changes.

### Automated integration via Android Studio
If your project is integrated by pulling dependencies remotely, note the following changes.
#### OPPO push
Add the following dependency statements; otherwise, OPPO Push registration may fail:
```groovy
implementation 'com.google.code.gson:gson:2.6.2'
implementation 'commons-codec:commons-codec:1.15'
```

### Integration via Eclipse
If your project is integrated by importing JAR files manually, note the following changes.
#### Mi push
Add the following nodes under the `application` tag in the `AndroidManifest` file; otherwise, notification clicks may not work on Mi devices on Android 12 or later.
```xml
<activity
    android:name="com.xiaomi.mipush.sdk.NotificationClickedActivity"
    android:theme="@android:style/Theme.Translucent.NoTitleBar"
    android:launchMode="singleInstance"
    android:exported="true"
    android:enabled="true">
</activity>
```

#### Meizu push
1. Add the following class resource files to the main project; otherwise, notification receipt may fail on Meizu devices on Android 6.0 or earlier. The code is as follows:
```java
package com.meizu.cloud.pushinternal;
public class R {
    public static final class drawable {
		    // Copy the resource file `stat_sys_third_app_notify.png` from the `flyme-notification-res` folder of the Meizu dependency directory in the Tencent Push Notification Service SDK package and paste it in your application's resource directory
        public static final int stat_sys_third_app_notify = com.tencent.android.tpns.demo.R.drawable.stat_sys_third_app_notify;
    }
}
```

2. Add the following permissions in the `AndroidManifest` file:
```xml
<uses-permission android:name="com.meizu.flyme.permission.PUSH" />
```
Remove the receiver node `com.meizu.cloud.pushsdk.SystemReceiver` and add the following receiver node under the `application` tag:
```xml
<receiver
    android:name="com.meizu.cloud.pushsdk.MzPushSystemReceiver"
    android:exported="false"
    android:permission="com.meizu.flyme.permission.PUSH">
    <intent-filter>
        <action android:name="com.meizu.flyme.push.intent.PUSH_SYSTEM" />
    </intent-filter>
</receiver>
```

#### OPPO push
1. Change the name of the class resource file `com.heytap.mcssdk.R` added for OPPO Push to `com.pushsdk.R` in your project (if it has never been added, add it directly); otherwise, OPPO Push registration may fail. Below is an example:
```java
package com.pushsdk;
class R {
    public static final class string {
        public final static int system_default_channel = com.tencent.android.tpns.demo.R.string.app_name; // This can be changed to a custom string resource ID
    }
}
```

2. Copy the `commons-codec-1.15.jar` and `gson-2.6.2-sources.jar` files from the OPPO dependency directory in the Tencent Notification Push Service SDK package to the `libs` directory of your project's `app` module and import the project. Otherwise, OPPO Push registration may fail.
```groovy
implementation files('libs/gson-2.6.2-sources.jar')
implementation files('libs/commons-codec-1.15.jar')
```

#### vivo push
1. Modify the service node `com.vivo.push.sdk.service.CommandClientService` under the `application` tag in the `AndroidManifest` file as follows:
```xml
<service
    android:name="com.vivo.push.sdk.service.CommandClientService"
    android:permission="com.push.permission.UPSTAGESERVICE"
    android:exported="true" />
```
2. Add the following nodes:
```xml
<meta-data
    android:name="sdk_version_vivo"
    android:value="483" />

<meta-data
    android:name="local_iv"
    android:value="MzMsMzQsMzUsMzYsMzcsMzgsMzksNDAsNDEsMzIsMzgsMzcsMzYsMzUsMzQsMzMsI0AzNCwzMiwzMywzNywzMywzNCwzMiwzMywzMywzMywzNCw0MSwzNSwzNSwzMiwzMiwjQDMzLDM0LDM1LDM2LDM3LDM4LDM5LDQwLDQxLDMyLDM4LDM3LDMzLDM1LDM0LDMzLCNAMzQsMzIsMzMsMzcsMzMsMzQsMzIsMzMsMzMsMzMsMzQsNDEsMzUsMzIsMzIsMzI" />
```



## Android SDK 1.3.1.1
### Integration via Eclipse
If your project is integrated by importing JAR files manually, note the following changes.

1. Add the following nodes under the `application` tag in the `AndroidManifest` file of the application; otherwise, pushes received by the application when it is online may not respond to the notification click event.
```xml
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
```

2. Modify the following nodes under the `application` tag in the `AndroidManifest` file of the application; otherwise, there may be a compliance risk with auto start.
```xml
    <!-- During manual integration, retain only the following three actions for the receiver's `intent-filter` -->
    <receiver
         android:name="com.tencent.android.tpush.XGPushReceiver"
         android:exported="false"
         android:process=":xg_vip_service">
         <intent-filter android:priority="0x7fffffff" tools:node="replace" >
            <!-- **(Required)** The internal broadcast of the Tencent Push Notification Service SDK -->
            <action android:name="com.tencent.android.xg.vip.action.SDK" />
            <action android:name="com.tencent.android.xg.vip.action.INTERNAL_PUSH_MESSAGE" />
            <action android:name="com.tencent.android.xg.vip.action.ACTION_SDK_KEEPALIVE" />
         </intent-filter>
    </receiver>
    
    <!-- When manually integrating the Mi channel, delete the `intent-filter` corresponding to the receiver -->
    <receiver
       android:name="com.xiaomi.push.service.receivers.NetworkStatusReceiver"
       android:exported="true" >
       <intent-filter tools:node="remove">
           <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
           <category android:name="android.intent.category.DEFAULT" />
       </intent-filter>
    </receiver>
```

## Android SDK 1.2.7.0

### Adding support for supplementary push via in-app messages
The API for setting whether to allow in-app message display is added. Please pay attention to the compatibility between WebView and higher Android version. For more information, see [API Documentation](https://intl.cloud.tencent.com/document/product/1024/30715).

## Android SDK 1.2.5.0

### 1. Configuring the dependent environment for your project (optional)

If you cannot pull the dependencies when using SDK dependencies, you can add the Google-recommended image source `MavenCentral` and Tencent Cloud image source in the `allprojects.repositories` file of your project's root directory `build.gradle`. Below is a code sample:
```
allprojects {
    repositories {
        google()
        // Google-recommended image source `MavenCentral`
        mavenCentral()
        jcenter()
        // Tencent Cloud image source
        maven { url 'https://mirrors.tencent.com/nexus/repository/maven-public/' }
    }
}
```

### 2. Adding configuration (required)
When using the newly added tag query API, you need to add the implementation method `onQueryTagsResult` in the implementation class that inherits `XGPushBaseReceiver`. Below is a code sample:
``` 
public class MessageReceiver extends XGPushBaseReceiver {

    // Other callback APIs
		// ...
		// Tag query callback API
    public void onQueryTagsResult(Context context, int errorCode, String data, String operateName) {
        Log.i(LogTag, "action - onQueryTagsResult, errorCode:" + errorCode + ", operateName:" + operateName + ", data: " + data);
    }
}
```


## Android SDK 1.2.1.3
### Changes to Huawei Push SDK connection
Starting from this version, Huawei push SDK v5 is officially supported. Please update the Huawei push integration configuration by referring to [Huawei Channel v5 Integration](https://intl.cloud.tencent.com/document/product/1024/37176).

## Android SDK 1.2.0.2
### Integration via Eclipse
If your project is integrated by importing JAR files manually, note the following changes.
#### Tencent Push Notification Service main package
1. Replace the `tpns-.jar` files in the `libs` directory of the SDK package.
2. Replace the `so` files for each platform in the `Other-Platform-SO` directory of the SDK package.
3. Remove the following data from the `application` tag in the `AndroidManifest` file:
```xml
    <activity
        android:name="com.tencent.android.tpush.XGPushActivity">
        <intent-filter>
            <action android:name="android.intent.action" />
        </intent-filter>
    </activity>

    <service android:exported="false"
            android:process=":xg_vip_service"
            android:name="com.tencent.bigdata.mqttchannel.services.MqttService" />

    <provider
            android:exported="false"
            android:name="com.tencent.bigdata.baseapi.base.SettingsContentProvider"
            android:authorities="application package name.XG_SETTINGS_PROVIDER" />
```
Add the following data:
```xml
    <activity android:name="com.tencent.android.tpush.TpnsActivity"
        android:theme="@android:style/Theme.Translucent.NoTitleBar">
        <intent-filter>
            <action android:name="${applicationId}.OPEN_TPNS_ACTIVITY" />
            <category android:name="android.intent.category.DEFAULT" />
        </intent-filter>
        <intent-filter>
            <data
                android:scheme="tpns"
                android:host="application package name"/>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.BROWSABLE" />
            <category android:name="android.intent.category.DEFAULT" />
        </intent-filter>
    </activity>

    <service android:exported="false"
            android:process=":xg_vip_service"
            android:name="com.tencent.tpns.mqttchannel.services.MqttService" />

    <provider
            android:exported="false"
            android:name="com.tencent.tpns.baseapi.base.SettingsContentProvider"
            android:authorities="application package name.XG_SETTINGS_PROVIDER" />
```
4. Add the following to the ProGuard obfuscation configuration:
```
-keep public class * extends android.app.Service
-keep public class * extends android.content.BroadcastReceiver
-keep class com.tencent.android.tpush.** {*;}
-keep class com.tencent.tpns.baseapi.** {*;} 
-keep class com.tencent.tpns.mqttchannel.** {*;}
-keep class com.tencent.tpns.dataacquisition.** {*;}
```

#### OPPO push
1. Add the class resource file `com.heytap.mcssdk.R` to the project with the following code:
```java
package com.heytap.mcssdk;
class R {
    public static final class string {
        public static final int system_default_channel = 
    com.tencent.android.tpns.demo.R.string.oppo_system_default_channel; //This can be changed to a custom string resource ID
    }
}
```
2. Remove the following data from the `application` tag in the `AndroidManifest` file:
```xml
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
```
Add the following data:
```xml
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
```
4. Add the following to the ProGuard obfuscation configuration:
```
-keep public class * extends android.app.Service
-keep class com.heytap.mcssdk.** {*;}
-keep class com.heytap.msp.push.** { *;}
```
