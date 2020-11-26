## Operation Scenarios
Huawei launches HMS Push SDK v4.0 as an upgrade of **Huawei Push** SDK v2.6.3.
Compared with SDK v2.6, v4.0 features major changes in API call and push service enablement steps.
As TPNS always keeps up with the update progress of each vendor channel's push service, it provides plugin dependency packages integrated with HMS Push SDK v4.0 for your choice.
>!  
>- HMS Push SDK v4 is incompatible with v2. If both are integrated, their dependency packages will conflict with each other. Please choose one of them for integration.
>- HMS Push SDK v4 no longer supports direct delivery of custom parameters in `key-value` format from the server and the `onEvent` callback for notification click events provided in v2. You are recommended to use the general intent scheme on Android to deliver such events. For more information, please see [How do I set the message click event?](https://cloud.tencent.com/document/product/548/36674#.E5.A6.82.E4.BD.95.E8.AE.BE.E7.BD.AE.E6.B6.88.E6.81.AF.E7.82.B9.E5.87.BB.E4.BA.8B.E4.BB.B6.EF.BC.9F).
>- You can still integrate Huawei Push SDK v2 to use the Huawei Push service. For more information, please see [Huawei Channel v2 Connection](https://cloud.tencent.com/document/product/548/36653).
>- For Huawei Push, you can successfully register with the Huawei channel and push messages through it only in a signed package environment.
>- The Huawei channel supports click callback but not arrival callback.


## Application Configuration on Huawei Push Platform
### Getting key
1. Go to the [Huawei Developer platform](http://developer.huawei.com).
2. Sign up for a developer account and log in to the platform. For more information, please see [Account Registration and Verification](https://developer.huawei.com/consumer/cn/devservice/doc/20300). (If you are registering a new account, you need to complete identity verification.)
3. Create an application on the Huawei Push platform. For more information, please see [Creating Application](https://developer.huawei.com/consumer/cn/doc/distribution/app/agc-create_app). (The application package name must be the same as that entered in the TPNS Console.)
4. Get and copy the application's `AppID` and `AppSecret` and paste them in **Application Configuration** > **Huawei Channel** in the TPNS Console.
   
### Configuring SHA-256 certificate fingerprint
Get the SHA-256 certificate fingerprint and configure it on the Huawei Push platform as instructed in [Generating Signature Certificate Fingerprint](https://developer.huawei.com/consumer/cn/doc/development/HMS-Guides/Preparations#generate_finger).

### Getting Huawei Push configuration file
Download the latest configuration file `agconnect-services.json` from Huawei developer platform in **My Project** -> **Select Project** -> **Project Setting**.

### Enabling push service
Enable the push service on the Huawei Push platform. For more information, please see [Enabling Push Service](https://developer.huawei.com/consumer/cn/doc/distribution/app/agc-enable_service#enable-service).

## SDK Integration (Two Methods)
### Using Android Studio Gradle for automatic integration
1. In the `build.gradle` file in the Android project-level directory, add the Huawei repository address and HMS Gradle plugin dependencies under `repositories` and `dependencies` in `buildscript`, respectively:
```
buildscript {
    repositories {
        google()
        jcenter()
        maven {url 'http://developer.huawei.com/repo/'}     // Huawei Maven repository address
    }
    dependencies {
        // Other `classpath` configurations
        classpath 'com.huawei.agconnect:agcp:1.2.1.301'     // Gradle plugin dependencies of Huawei Push
    }
}
```

2. In the `build.gradle` file in the Android project-level directory, add the Huawei dependency repository address under `repositories` in `allprojects`:
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
![](https://main.qcloudimg.com/raw/90cefd6b26ad2bd2c80925ccbb4e67c7.png)

4. Add the following configuration to the `build.gradle` file at its beginning in the `app` module:
```
// Other Gradle plugins of application
apply plugin: 'com.huawei.agconnect'      // HMS Push SDK v4 Gradle plugin
android {
    // Application configuration content
}
```

5. Import the dependencies related to Huawei Push into the `build.gradle` file under the `app` module:
```
dependencies {
    // Other dependencies of the program
    implementation 'com.tencent.tpns:huawei:v3-1.0.0.0-release'      // HMS Push v4 TPNS plugin
    implementation 'com.huawei.hms:push:4.0.3.301'       // HMS SDK v4 push module dependency package
    }
```

### Using Android Studio for manual integration
If you cannot access Huawei Maven repository in your internal development environment, you can try the following manual integration method:
1. Manually download all dependency packages required by HMS Push SDK v4.0 from the Huawei repository and store them in the `libs` directory under the `app` module:   
   1. One JAR dependency for Gradle script: [agcp-1.2.1.301.jar](https://developer.huawei.com/repo/com/huawei/agconnect/agcp/1.2.1.301/agcp-1.2.1.301.jar)
   2. Nine AAR program dependencies:
      1. [agconnect-core-1.0.0.300.aar](https://developer.huawei.com/repo/com/huawei/agconnect/agconnect-core/1.0.0.300/agconnect-core-1.0.0.300.aar)
      2. [base-4.0.2.300.aar](https://developer.huawei.com/repo/com/huawei/hms/base/4.0.2.300/base-4.0.2.300.aar)
      3. [network-common-4.0.2.300.aar](https://developer.huawei.com/repo/com/huawei/hms/network-common/4.0.2.300/network-common-4.0.2.300.aar)
      4. [network-grs-4.0.2.300.aar](https://developer.huawei.com/repo/com/huawei/hms/network-grs/4.0.2.300/network-grs-4.0.2.300.aar)
      5. [opendevice-4.0.1.301.aar](https://developer.huawei.com/repo/com/huawei/hms/opendevice/4.0.1.301/opendevice-4.0.1.301.aar)
      6. [push-4.0.3.301.aar](https://developer.huawei.com/repo/com/huawei/hms/push/4.0.3.301/push-4.0.3.301.aar)
      7. [tasks-1.3.3.300.aar](https://developer.huawei.com/repo/com/huawei/hmf/tasks/1.3.3.300/tasks-1.3.3.300.aar)
      8. [update-2.0.6.300.aar](https://developer.huawei.com/repo/com/huawei/hms/update/2.0.6.300/update-2.0.6.300.aar)
      9. [huawei-v3-1.0.0.0-release.aar](https://bintray.com/lc123/maven/download_file?file_path=com%2Ftencent%2Ftpns%2Fhuawei%2Fv3-1.0.0.0-release%2Fhuawei-v3-1.0.0.0-release.aar)

2. In the `build.gradle` file in the Android project-level directory, add HMS Gradle plugin dependencies under `dependencies` in `buildscript`:
```
buildscript {
    repositories {
        google()
        jcenter()
    }
    dependencies {
        // Other `classpath` configurations
        classpath files('app/libs/agcp-1.2.1.301.jar')     // Gradle plugin dependencies of Huawei Push
    }
}
```

3. Copy the application configuration file `agconnect-services.json` obtained from the Huawei Push platform to the `app` module directory.  

  ![](https://main.qcloudimg.com/raw/90cefd6b26ad2bd2c80925ccbb4e67c7.png)

4. Add the following configuration to the `build.gradle` file at its beginning in the `app` module:
```
// Other Gradle plugins of application
apply plugin: 'com.huawei.agconnect'      // HMS Push SDK v4 Gradle plugin
android {
    // Application configuration content
}
```

5. Import the dependencies related to Huawei Push into the `build.gradle` file under the `app` module:
```
dependencies {
    // Other dependencies of the program
    implementation fileTree(include: ['*.aar'], dir: 'libs')
    }
```

6. Add the following components between the `<application>` and `</application>` tags in the `manifest` file:
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
I/TPush: [XGOtherPush] other push token is : 0865551032618726300001294600CN01 other push type: huawei
I/TPush: [a] binder other push token with accid = 2100274337  token = 17c32948df0346d5837d4748192e9d2f14c81e08 otherPushType = huawei otherPushToken = 0865551032618726300001294600CN01
```

## Code Obfuscation
```
-ignorewarnings
-keepattributes *Annotation* 
-keepattributes Exceptions 
-keepattributes InnerClasses 
-keepattributes Signature 
-keepattributes SourceFile,LineNumberTable 
-keep class com.hianalytics.android.**{*;} 
-keep class com.huawei.updatesdk.**{*;} 
-keep class com.huawei.hms.**{*;}
```
>?Obfuscation rules must be stored in the `proguard-rules.pro` file at the application project level.

## Advanced Configuration (Optional)
### Arrival receipt configuration for Huawei channel
The arrival receipt for the Huawei channel should be configured by yourself. After configuring this feature as instructed in [Receipt Configuration Guide for Huawei Channel](https://intl.cloud.tencent.com/document/product/1024/35246#.E5.8D.8E.E4.B8.BA.E5.8E.82.E5.95.86.E9.80.9A.E9.81.93.E5.9B.9E.E6.89.A7.E9.85.8D.E7.BD.AE.E6.8C.87.E5.BC.95), you can view the arrival data for the Huawei push channel in the push records.
![](https://main.qcloudimg.com/raw/11c44dfc000045458a627e12b67ef611.png)

### Badge adaptation for Huawei devices
You can set the application badge on Huawei devices after applying for the application badge setting permission and setting the application start class. For more information, please see [Badge Adaption Guide](https://cloud.tencent.com/document/product/548/43693#.E5.8D.8E.E4.B8.BA.E6.89.8B.E6.9C.BA.E8.A7.92.E6.A0.87.E9.80.82.E9.85.8D.E6.8C.87.E5.8D.97).

## Troubleshooting
### Querying Huawei Push registration error code
The Huawei Push service has strict requirements on the connection configuration. If you fail to register with the Huawei channel, you can use either of the following ways to get the Huawei Push registration error code:
1. In debugging mode of the push service, filter logs by the keyword `OtherPush` or `HMSSDK` to view the return code logs.
2. Call the `XGPushConfig.getOtherPushErrCode(context)` API in the callback method of the TPNS registration API `XGPushManager.registerPush` to get the vendor channel registration return code:

You can find the cause of the error and get the solution in [Common error codes](https://developer.huawei.com/consumer/cn/doc/development/HMS-2-References/hmssdk_huaweipush_api_reference_errorcode).

### Others
When your application is released on Huawei AppGallery, it may fail the audit with the error message "Error:28: you need to package the certificate file into the APK when integrating with HMS. Please directly copy the assets directory to the application project's root directory" displayed. Please fix the problem as follows:   
```
Download the official Huawei HMS SDK and copy all files and subdirectories in the `assets` directory to that in your application project. If the `assets` directory does not exist in the application project, create one.
```

