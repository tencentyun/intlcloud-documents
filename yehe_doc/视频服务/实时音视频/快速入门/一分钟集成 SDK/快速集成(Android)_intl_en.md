This document describes how to quickly integrate the Tencent Cloud TRTC SDK for Android into your project in the following steps.

## Development Environment Requirements
- Android Studio 3.5 or above.
- Android 4.1 (SDK API 16) or above.

## Integrating the SDK (aar)

You can choose to use Gradle for automatic loading or manually download the aar and import it into your current project.

### Method 1. Automatic loading (aar)
The TRTC SDK has been released to the JCenter repository, and you can configure Gradle to download updates automatically.
Simply use Android Studio to open the project that needs to be integrated with the SDK ([TRTCSimpleDemo](https://github.com/tencentyun/TRTCSDK/tree/master/Android/TRTCScenesDemo) is used as an example in this document), and then modify the `app/build.gradle` file in three simple steps to complete SDK integration:
![](https://main.qcloudimg.com/raw/fd01c252724cbf31ec7356286a931661.png)

1. Add the TRTC SDK dependencies to `dependencies`.
 - Run the following command to use com.android.tools.build:gradle v3.x:
```
dependencies {
         implementation 'com.tencent.liteav:LiteAVSDK_TRTC:latest.release'
}
```
 - Run the following command to use com.android.tools.build:gradle v2.x:
```
dependencies {
         compile 'com.tencent.liteav:LiteAVSDK_TRTC:latest.release'
}
```
2. In `defaultConfig`, specify the CPU architecture to be used by the application.
```
defaultConfig {
       ndk {
           abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
       }
}
```
>?Currently, the TRTC SDK supports armeabi, armeabi-v7a, and arm64-v8a.
>
3. Click **Sync Now** to automatically download and integrate the SDK into the project.


### Method 2. Manual download (aar)
If JCenter cannot be connected to, you can manually download the SDK and integrate it into your project:

1. [Download the SDK](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Android_latest.zip).
2. Copy the downloaded aar file to the **app/libs** directory of the project.
3. Add **flatDir** to `build.gradle` under the project’s root directory and specify the local repository path.
![](https://main.qcloudimg.com/raw/bc3215028103fe980aedcbf011b97b02.png)
4. Add the code that imports the aar library to `app/build.gradle`.
![](https://main.qcloudimg.com/raw/449a4a2d8d7cb2503da9fb480beb9c32.png)
5. In `defaultConfig` of `app/build.gradle`, specify the CPU architecture to be used by the application.
```
defaultConfig {
       ndk {
           abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
       }
}
```
>Currently, the TRTC SDK supports armeabi, armeabi-v7a, and arm64-v8a.
>
6. Click **Sync Now** to complete the integration of TRTC SDK.


## Integrating the SDK (jar)
If you do not want to integrate the aar library, you can choose to integrate the TRTC SDK by importing the jar and so libraries:

1. [Download the jar library](https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Android_latest.zip). The file path is `SDK/LiteAVSDK_TRTC_xxx.zip` (xxx indicates the version number of TRTC SDK).
2. After decompression, you can get the `libs` directory which contains the jar files and so folders.
3. Copy the extracted jar files as well as armeabi, armeabi-v7a, and arm64-v8a folders to the `app/libs` directory.
![](https://main.qcloudimg.com/raw/5bf82ca89b3a14cca470fcedc048d7fa.png)
4. Add the code that imports the jar library to `app/build.gradle`.
![](https://main.qcloudimg.com/raw/6ffbb4b79c06555376b137c849b43bb7.png)	
5. Add the code that imports the so library to `app/build.gradle`.
```
sourceSets {
       main {
           jniLibs.srcDirs = ['libs']
       }
}
```
![](https://main.qcloudimg.com/raw/299eeb5b3e8961e816f3ce17b97b4339.png)
6. In `defaultConfig` of `app/build.gradle`, specify the CPU architecture to be used by the application. 
```
defaultConfig {
       ndk {
           abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
       }
}
```
>？Currently, the TRTC SDK supports armeabi, armeabi-v7a, and arm64-v8a.
>
7. Click **Sync Now** to complete the integration of TRTC SDK.


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
<uses-feature android:name="android.hardware.camera" />
<uses-feature android:name="android.hardware.camera.autofocus" />
```
>! Do not run the `android:hardwareAccelerated="false"` code to disable hardware acceleration; otherwise, the video streams of the peer cannot be rendered.
## Setting Obfuscation Rules
In the `proguard-rules.pro` file, add the classes related to the TRTC SDK to the "do not obfuscate" list:

```
-keep class com.tencent.** { *; }
```
## Setting Application Packaging Parameters
Add the following code to `app/build.gradle`:

```
packagingOptions {
	pickFirst '**/libc++_shared.so'
	doNotStrip "*/armeabi/libYTCommon.so"
	doNotStrip "*/armeabi-v7a/libYTCommon.so"
	doNotStrip "*/x86/libYTCommon.so"
	doNotStrip "*/arm64-v8a/libYTCommon.so"
}
```
![](https://main.qcloudimg.com/raw/e40d5c294a59d56a1f89f20960c7e4c1.png)


