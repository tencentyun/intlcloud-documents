## Overview


As TPNS always keeps up with the update progress of each vendor channel's push service, it provides plugin dependency packages integrated with HMS Core Push SDK for your choice.

> !  
> - For Huawei Push, you can successfully register with the Huawei channel and push messages through it only in a signed package environment.
> - The Huawei channel supports click callback but not arrival callback.

## Application Configuration on Huawei Push Platform

### Getting key

1. Go to the [Huawei Developer platform](http://developer.huawei.com).
2. Sign up for a developer account and log in to the platform. For more information, please see [Account Registration and Verification](https://developer.huawei.com/consumer/cn/devservice/doc/20300). (If you are registering a new account, you need to complete identity verification; otherwise, you cannot use the platform.)
3. Create an application on the Huawei Push platform. For more information, please see [Creating Application](https://developer.huawei.com/consumer/cn/doc/distribution/app/agc-create_app). (The application package name must be the same as that entered in the TPNS Console.)
4. Get and copy the application's `AppID` and `AppSecret` and paste them into **[TPNS Console](https://console.cloud.tencent.com/tpns)** > **Configuration Management** > **Basic Configuration** > **Huawei Official Push Channel**.



### Configuring SHA-256 certificate fingerprint

Get the SHA-256 certificate fingerprint and configure it on the Huawei Push platform as instructed in [Generating Signature Certificate Fingerprint](https://developer.huawei.com/consumer/cn/doc/development/HMS-Guides/Preparations#generate_finger).

### Getting Huawei Push configuration file

Log in to the Huawei Developer platform, go to **My Projects** > select a project > **Project Settings**, and download the latest configuration file `agconnect-services.json` of your Huawei application.



### Enabling push service

Enable the push service in **Development** > **Push Service** on the Huawei Push platform. For more information, please see [Enabling Push Service](https://developer.huawei.com/consumer/cn/doc/distribution/app/agc-enable_service#enable-service).



## SDK Integration (Two Methods)

### Using Android Studio Gradle for automatic integration

1. In the `build.gradle` file in the Android project-level directory, add the Huawei repository address and HMS Gradle plugin dependencies under **repositories and dependencies** in **buildscript**, respectively:
```
buildscript {
    repositories {
        google()
        jcenter()
        maven {url 'http://developer.huawei.com/repo/'}     // Huawei Maven repository address
    }
    dependencies {
        // Other `classpath` configurations
        classpath 'com.huawei.agconnect:agcp:1.3.1.300'     // Gradle plugin dependencies of Huawei Push
    }
}
```
2. In the `build.gradle` file in the Android project-level directory, add the Huawei dependency repository address under **repositories** in **allprojects**:
```
allprojects {
    repositories {
        google()
        jcenter()
        maven {url 'http://developer.huawei.com/repo/'}     // Huawei Maven repository address
    }
}
```
3. Copy the application configuration file `agconnect-services.json` obtained from the Huawei Push platform to the `app` module directory.  
 ![](https://main.qcloudimg.com/raw/338c87faaeb388f648835f17aeddc490.png)
4. Add the following configuration to the `build.gradle` file at its beginning in the `app` module:
```
// Other Gradle plugins of application
apply plugin: 'com.huawei.agconnect'      // HMS Push SDK Gradle plugin
android {
    // Application configuration content
}
```
5. Import the dependencies related to Huawei Push into the `build.gradle` file under the `app` module:
```
dependencies {
		// ...Other dependencies of the program
		implementation 'com.tencent.tpns:huawei:[VERSION]-release'      // Huawei Push [VERSION] is the version number of the current latest SDK, which can be viewed in SDK for Android Updates
		implementation 'com.huawei.hms:push:5.0.2.300'       // HMS Core Push module dependency package
		}
```

>?
>- Huawei Push \[VERSION\] is the version number of the current latest SDK, which can be viewed in [SDK for Android Updates](https://intl.cloud.tencent.com/document/product/1024/36191).
>- Starting v1.2.1.3, TPNS SDK for Android officially supports Huawei Push v5. Please use TPNS Huawei dependency v1.2.1.3 or above to avoid integration conflicts.


### Using Android Studio for manual integration

If you cannot access Huawei Maven repository in your internal development environment, you can try the following manual integration method:

1. Download the [SDK installation package](https://console.cloud.tencent.com/tpns/sdkdownload).
2. Open the `Other-Push-jar` folder and import the dependent packages related to huaweiv5 by copying all jar and aar packages into the project.
3. In the `build.gradle` file in the Android project-level directory, add HMS Gradle plugin dependencies under **dependencies** in **buildscript**:
```
buildscript {
    repositories {
        google()
        jcenter()
    }
    dependencies {
        // Other `classpath` configurations
        classpath files('app/libs/agcp-1.3.1.300.jar')     // Gradle plugin dependencies of Huawei Push
    }
}
```
4. Copy the application configuration file `agconnect-services.json` obtained from the Huawei Push platform to the `app` module directory.  
![](https://main.qcloudimg.com/raw/447e6453a5a996128b12c5ca9cdb10c7.png)
5. Add the following configuration to the `build.gradle` file at its beginning in the `app` module:
```
// Other Gradle plugins of application
apply plugin: 'com.huawei.agconnect'      // HMS Push SDK v4 Gradle plugin
android {
    // Application configuration content
}
```
6. Import the dependencies related to Huawei Push into the `build.gradle` file under the `app` module:
```
dependencies {
        // ...Other dependencies of the program
        implementation files('libs/tpns-huaweiv5-1.2.1.1.jar')      // TPNS plugin for HMS Core
        implementation fileTree(include: ['*.aar'], dir: 'libs')    // HMS Core Push module dependency package
    }
```
7. Add the following components between the `<application>` and `</application>` tags in the `manifest` file:
```
<application>
        <service
            android:name="com.huawei.android.hms.tpns.HWHmsMessageService"
            android:exported="false">
            <intent-filter>
                <action android:name="com.huawei.push.action.MESSAGING_EVENT" />
            </intent-filter>
        </service>
</application>
```

## Huawei Push Activation

Enable the third-party push API before calling the TPNS registration API `XGPushManager.registerPush`:

```
// Enable the third-party push
XGPushConfig.enableOtherPush(getApplicationContext(), true);
```

The log of successful registration is as follows:

```
V/TPush: [XGPushConfig] isUsedOtherPush:true
E/xg.vip: get otherpush errcode: errCode : 0 , errMsg : success
V/TPush: [XGPushConfig] isUsedOtherPush:true
I/TPush: [OtherPushClient] handleUpdateToken other push token is : IQAAAACy0PsqAADxfCrWG3kupbOraeAiYoo9n2B-bAfb2d--kctc8E_UnY_mrIdg9ionukZvC******dVD8GlJi_5-0rpskunnNMcat35HA other push type: huawei
```

## Code Obfuscation

```plaintext
-ignorewarnings
-keepattributes *Annotation* 
-keepattributes Exceptions 
-keepattributes InnerClasses 
-keepattributes Signature 
-keepattributes SourceFile,LineNumberTable 
-keep class com.hianalytics.android.**{*;} 
-keep class com.huawei.updatesdk.**{*;} 
-keep class com.huawei.hms.**{*;}
-keep class com.huawei.agconnect.**{*;}
```


> ?Obfuscation rules must be stored in the `proguard-rules.pro` file at the application project level.

## Advanced Configuration (Optional)

### Arrival receipt configuration for Huawei channel

The arrival receipt for the Huawei channel should be configured by yourself. After configuring this feature as instructed in [Acquisition of Vendor Channel Arrival Receipt](https://intl.cloud.tencent.com/document/product/1024/35246#.E5.8D.8E.E4.B8.BA.E5.8E.82.E5.95.86.E9.80.9A.E9.81.93.E5.9B.9E.E6.89.A7.E9.85.8D.E7.BD.AE.E6.8C.87.E5.BC.95), you can view the arrival data for the Huawei push channel in the push records.
![](https://main.qcloudimg.com/raw/11c44dfc000045458a627e12b67ef611.png)

### Badge adaptation for Huawei devices

You can set the application badge on Huawei devices after applying for the application badge setting permission and setting the application start class. For more information, please see [Badge Adaption Guide](https://intl.cloud.tencent.com/document/product/1024/35828).

## Troubleshooting

#### Querying Huawei Push registration error code

The Huawei Push service has strict requirements on the connection configuration. If you fail to register with the Huawei channel, you can use one of the following ways to get the Huawei Push registration error code:


1. In debugging mode of the push service, filter logs by the keyword `OtherPush` or `HMSSDK` to view the return code logs.
2. You can find the cause of the error and get the solution in [Common error codes](https://developer.huawei.com/consumer/cn/doc/development/HMS-2-References/hmssdk_huaweipush_api_reference_errorcode).



#### Why are there no alerts for notifications delivered through the Huawei channel?


Starting EMUI 10.0, Huawei Push intelligently categorizes notification messages into two levels: general and important. Versions below EMUI 10.0 don't categorize notifications but have only one level, so all notifications are displayed through the "default notification" channel, which is equivalent to the important level on EMUI 10.0. If a notification is categorized as "general", there will be no vibration, sound, or status bar icon alerts for it. Currently, the notification level can be set to "important" through the custom notification channel; however, according to the applicable Huawei Push rules, the final display effect will still be determined jointly by the set level and the level calculated by Huawei Push's intelligent categorization, and the lower level will prevail; for example, if the two levels are "important" and "general", "general" will prevail. For more information, please see [Vendor Message Categorization Feature Use Instructions](https://intl.cloud.tencent.com/document/product/1024/36250).


#### Others

When your application is released on Huawei AppGallery, it may fail the audit with the error message "Error:28: you need to package the certificate file into the APK when integrating with HMS. Please directly copy the assets directory to the application project's root directory" displayed. Please fix the problem as follows:

1. Download the official Huawei HMS SDK.
2. Copy all files and subdirectories in the `assets` directory to that in your application project. If the `assets` directory does not exist in the application project, create one.

