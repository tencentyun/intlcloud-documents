This document describes how to import the SDK into your project.
![](https://qcloudimg.tencent-cloud.cn/raw/f85f7ee54d462d85290fc6f50e5ed96a.png)

## Environment Requirements
- Android Studio 3.5 or later.
- Android 4.1 (SDK API level 16) or later

## Step 1. Import the SDK

### Method 1. Automatic loading (aar)
The TRTC SDK has been released to the mavenCentral repository, and you can configure Gradle to download updates automatically.
1. Add the TRTC SDK dependency to `dependencies`.
```
dependencies {
        implementation 'com.tencent.liteav:LiteAVSDK_TRTC:latest.release'
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
3. Click ![](https://main.qcloudimg.com/raw/d6b018054b535424bb23e42d33744d03.png) **Sync Now** to automatically download the SDK and integrate them into your project.


### Method 2. Download the SDK and import it manually
1. Download the [SDK](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Android_latest.zip) and decompress it locally.
2. Copy the decompressed AAR file to the **app/libs** directory of your project.
3. Add **flatDir** to `build.gradle` under your project's root directory to specify the local path for the repository.
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
6. Click ![](https://main.qcloudimg.com/raw/d6b018054b535424bb23e42d33744d03.png) **Sync Now** to integrate the TRTC SDK.

## Step 2. Configure app permissions
Configure application permissions in `AndroidManifest.xml`. The TRTC SDK requires the following permissions:
```java
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-feature android:name="android.hardware.camera.autofocus" />
```

>! Do not set `android:hardwareAccelerated="false"`. Disabling hardware acceleration will result in failure to render remote users' videos.

### Step 3. Set obfuscation rules
In the `proguard-rules.pro` file, add the classes related to the TRTC SDK to the "do not obfuscate" list:
```java
-keep class com.tencent.** { *;}
```

[](id:using_cpp)
## Using SDK Through C++ APIs (Optional)
If you prefer to use C++ APIs instead of Java for development, you can perform this step. If you only use Java to call the TRTC SDK, skip this step.
1. First, you need to integrate the TRTC SDK by importing JAR and SO libraries as instructed above.
2. Copy the C++ header file in the SDK to the project (path: `SDK/LiteAVSDK_TRTC_xxx/libs/include`) and configure the `include` folder path and dynamic link to the SO library in `CMakeLists.txt`.
```java
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
3. Use the namespace: The methods and types of cross-platform C++ APIs are all defined in the `trtc` namespace. To simplify your code, we recommend you use the `trtc` namespace.
```
using namespace trtc;
```

>?
>- For more information on how to configure the Android Studio C/C++ development environments, see [Add C and C++ code to your project](https://developer.android.com/studio/projects/add-native-code). 
>- Currently, only the TRTC edition of the SDK supports C++ APIs. For more information on how to use C++ APIs, see [Overview](https://intl.cloud.tencent.com/document/product/647/35131).


