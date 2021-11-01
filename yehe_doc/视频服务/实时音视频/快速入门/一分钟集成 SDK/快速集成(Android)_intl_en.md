This document describes how to quickly integrate the Tencent Cloud TRTC SDK for Android into your project in the following steps.

## Environment Requirements
- Android Studio 3.5 or above.
- Android 4.1 (SDK API 16) or above.

## Integrating the SDK (AAR)

You can use Gradle to automatically load the AAR file or manually download the AAR file and import it into your project.

### Method 1. Automatic loading (aar)
The TRTC SDK has been released to the JCenter repository, and you can configure Gradle to download updates automatically.
Simply use Android Studio to open the project that needs to be integrated with the SDK ([TRTCScenesDemo](https://github.com/tencentyun/LiteAVClassic/tree/master/Android/TRTCScenesDemo) is used as an example in this document), and then modify the `app/build.gradle` file in three simple steps to complete SDK integration:
![](https://main.qcloudimg.com/raw/47b8e9f7ee41895a479334f16dd50a12.png)

1. Add the TRTC SDK dependency to `dependencies`.
 - Run the following command to use com.android.tools.build:gradle v3.x:
```
dependencies {
         implementation 'com.tencent.liteav:LiteAVSDK_TRTC:latest.release'
}
```
 - Run the following command if you use the 2.x version of com.android.tools.build:gradle.
```
dependencies {
         compile 'com.tencent.liteav:LiteAVSDK_TRTC:latest.release'
}
```
2. In `defaultConfig`, specify the CPU architecture to be used by your application.
```
defaultConfig {
       ndk {
           abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
       }
}
```
>?Currently, the TRTC SDK supports armeabi, armeabi-v7a, and arm64-v8a.
3. Click **Sync Now** to automatically download the SDKs and integrate them into your project.


### Method 2: manual download (AAR)
If you have difficulty accessing JCenter, you can manually download the SDK and integrate it into your project.

1. [Download the SDK](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Android_latest.zip).
2. Copy the downloaded AAR file to the **app/libs** directory of your project.
3. Add **flatDir** to `build.gradle` under the project's root directory and specify a local path for the repository.
![](https://main.qcloudimg.com/raw/3b07d38f105167ae52ffdda9a1712cec.png)
4. Add code in `app/build.gradle` to import the AAR file.
![](https://main.qcloudimg.com/raw/143621f900eb6f7b867d89b71c0dd13d.png)
5. In `defaultConfig` of `app/build.gradle`, specify the CPU architecture to be used by your application.
```
defaultConfig {
       ndk {
           abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
       }
}
```
>?Currently, the TRTC SDK supports armeabi, armeabi-v7a, and arm64-v8a.
6. Click **Sync Now** to complete the integration of TRTC SDK.


## Integrating SDK (JAR)
If you do not want to import the AAR library, you can also integrate TRTC SDK by importing JAR and SO libraries.

1. [Download the JAR library](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Android_latest.zip). The file path is `SDK/LiteAVSDK_TRTC_xxx.zip` (xxx indicates the version number of TRTC SDK).
2. Decompress the file, and you will find a `libs` directory that contains a JAR file and several SO folders.
3. Copy the JAR file and `armeabi`, `armeabi-v7a`, and `arm64-v8a` folders to the `app/libs` directory.
![](https://main.qcloudimg.com/raw/c7b498b40bff8c248cd72fcd01f07933.png)
4. Add the code that imports the JAR library to `app/build.gradle`.
![](https://main.qcloudimg.com/raw/5369b8c9bbb855622b22c7843a591e2e.png)	
5. Add the code that imports the SO library to `app/build.gradle`.
```
sourceSets {
       main {
           jniLibs.srcDirs = ['libs']
       }
}
```
![](https://main.qcloudimg.com/raw/7aa7eea5d26086b0b9c54ef7a910c6dd.png)
6. In `defaultConfig` of `app/build.gradle`, specify the CPU architecture to be used by your application. 
```
defaultConfig {
       ndk {
           abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
       }
}
```
>?Currently, the TRTC SDK supports armeabi, armeabi-v7a, and arm64-v8a.
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

>! Do not set `android:hardwareAccelerated="false"`; otherwise, the video stream of the remote user cannot be rendered after hardware acceleration is disabled.

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
![](https://main.qcloudimg.com/raw/b847d95fc05d2b97f85ffdb0b89438cc.png)


[](id:using_cpp)
## Using SDK Through C++ APIs (Optional)
If you prefer to use C++ APIs instead of Java for development, you can perform this step. If you only use Java to call the TRTC SDK, please skip this step.
1. First, you need to integrate the TRTC SDK by importing JAR and SO libraries as instructed above.
2. Copy the C++ header file in the SDK to the project (path: `SDK/LiteAVSDK_TRTC_xxx/libs/include`) and configure the `include` folder path and dynamic link to the SO library in `CMakeLists.txt`.
```
cmake_minimum_required(VERSION 3.6)

# Configure the C++ API header file path
include_directories(
        ${CMAKE_CURRENT_SOURCE_DIR}/include  # Copied from `SDK/LiteAVSDK_TRTC_xxx/libs/include`
)

add_library(
        native-lib
        SHARED
        native-lib.cpp)

# Configure the path of the `libliteavsdk.so` dynamic library
add_library(libliteavsdk SHARED IMPORTED)
set_target_properties(libliteavsdk  PROPERTIES IMPORTED_LOCATION ${CMAKE_CURRENT_SOURCE_DIR}/../../../libs/${ANDROID_ABI}/libliteavsdk.so)

find_library(
        log-lib
        log)

# Configure the dynamic link as `libliteavsdk.so`
target_link_libraries(
        native-lib
        libliteavsdk
        ${log-lib})
```
3. Use the namespace: the methods and types of cross-platform C++ APIs are defined in the `trtc` namespace. To simplify your code, you are advised to use the `trtc` namespace.
```
using namespace trtc;
```

>?
>- For more information on how to configure the Android Studio C/C++ development environments, please see [Add C and C++ code to your project](https://developer.android.com/studio/projects/add-native-code). 
>- Currently, only the TRTC edition of the SDK supports C++ APIs. For more information on how to use C++ APIs, please see [Overview](https://intl.cloud.tencent.com/document/product/647/35131).
