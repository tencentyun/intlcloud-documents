This document describes how to quickly integrate the Tencent Cloud TRTC SDK for Android into your project in the following steps.

## Development Environment Requirements
- Android Studio 2.0+.
- Android 4.1 (SDK API 16) or above.

## Integrating the SDK (aar)

You can choose to use Gradle for automatic loading or manually download the aar and import it into your current project.

### Method 1. Automatic loading (aar)
The TRTC SDK has been released to the JCenter repository, and you can configure Gradle to download updates automatically.
Simply use Android Studio to open the project that needs to be integrated with the SDK ([TRTC SDK Demo](https://github.com/tencentyun/TRTCSDK/tree/master/Android) is used as an example in this document), and then modify the `app/build.gradle` file in three simple steps to complete SDK integration:
![](https://main.qcloudimg.com/raw/05caa51b138e99ac32b177201c02f649.jpg)

- **Step 1. Add SDK dependencies**   
Add the TRTC SDK dependencies to `dependencies`.
```
dependencies {
    compile 'com.tencent.liteav:LiteAVSDK_TRTC:latest.release'
}
```

- **Step 2. Specify the application architecture**
In `defaultConfig`, specify the CPU architecture to be used by the application (currently, the TRTC SDK supports armeabi, armeabi-v7a, and arm64-v8a).
```
   defaultConfig {
        ndk {
            abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
        }
    }
```

- **Step 3. Sync the SDK**
Click "Sync Now". If JCenter can be connected to, the SDK will be automatically downloaded and integrated into the project very soon.


### Method 2. Manual download (aar)
If JCenter cannot be connected to, you can manually download the SDK and integrate it into your project:

- **Step 1. Download the TRTC SDK**  
Download the latest version of the [TRTC SDK](https://github.com/tencentyun/TRTCSDK/tree/master/Android/SDK) from GitHub:
![](https://main.qcloudimg.com/raw/75434db66f21ed185b30528d45128cd4.png)

- **Step 2. Copy the TRTC SDK to the project directory**  
Copy the downloaded aar file to the **app/libs** directory of the project:
![](https://main.qcloudimg.com/raw/bdbc00b67ae7d087769d25a31dd6beed.png)

- **Step 3. Specify the path to the local repository**
In `build.gradle` in the project's root directory, add **flatDir** to specify the path to the local repository.
![](https://main.qcloudimg.com/raw/2bd3f6fc086314f300b0c2eddafb9215.jpg)

- **Step 4. Add the TRTC SDK dependencies**   
Add the code that imports the aar package to `app/build.gradle`.
![](https://main.qcloudimg.com/raw/98b4806ed2484e96d47eb1ad165e900d.jpg)

- **Step 5. Specify the application architecture**
In the `defaultConfig` of `app/build.gradle`, specify the CPU architecture to be used by the application (currently, the TRTC SDK supports armeabi, armeabi-v7a, and arm64-v8a).
```
   defaultConfig {
        ndk {
            abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
        }
    }
```

- **Step 6. Sync the SDK**
Click **Sync Now** to complete the integration of TRTC SDK.


## Integrating the SDK (jar)
If you do not want to integrate the aar library, you can choose to integrate the TRTC SDK by importing the jar and so libraries:

- **Step 1: Download and decompress the TRTC SDK**
You can [download](https://github.com/tencentyun/TRTCSDK/tree/master/Android) the latest version of the jar package from GitHub. The filename is generally `LiteAV_TRTC_xxx.zip` (where xxx is the version number of the TRTC SDK):
![](https://main.qcloudimg.com/raw/8a97ef2b6a0cb2860b57b220d0684328.png)
After decompression, you can get the `libs` directory which contains the jar files and so folders as listed below:
![](https://main.qcloudimg.com/raw/7b8efbef6d003896e91730b8f68abf76.png)

- **Step 2. Copy the SDK files to the project directory**
Copy the extracted jar files as well as armeabi, armeabi-v7a, and arm64-v8a folders to the `app/libs` directory.
![](https://main.qcloudimg.com/raw/9af01cf965bbaf3dd9bcb23216eb0e6b.png)

- **Step 3. Import the jar library**
Add the code that imports the jar library to `app/build.gradle`.
![](https://main.qcloudimg.com/raw/f9cbdca4a493c0bf1e12557a15974b9d.jpg)			

- **Step 4. Import the so library**
Add the code that imports the so library to `app/build.gradle`.
![](https://main.qcloudimg.com/raw/10003cdc49d4856ee4feb840f24680a7.jpg)

- **Step 5. Specify the application architecture**
In the `defaultConfig` of `app/build.gradle`, specify the CPU architecture to be used by the application (currently, the TRTC SDK supports armeabi, armeabi-v7a, and arm64-v8a). 
```
   defaultConfig {
        ndk {
            abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
        }
    }
```

- **Step 6. Sync the SDK**
Click "Sync Now" to complete the integration of TRTC SDK.


## Configuring Application Permissions
Configure application permissions in `AndroidManifest.xml`. The TRTC SDK requires the following permissions:

```
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-feature android:name="android.hardware.Camera"/>
<uses-feature android:name="android.hardware.camera.autofocus" />
```

## Setting Obfuscation Rules
In the `proguard-rules.pro` file, add the classes related to the TRTC SDK to the "do not obfuscate" list:

```
-keep class com.tencent.** { *; }
```
## Setting Application Packaging Parameters
![](https://main.qcloudimg.com/raw/dabfd69ee06e4d38bb3b51fc436c0ad1.png)


