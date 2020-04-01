This document describes how to configure an Android project for GME APIs for Android.

## SDK Preparations
1. Download the applicable demo and SDK. For more information, please see [Download Guide](https://intl.cloud.tencent.com/document/product/607/18521).
2. Decompress the obtained SDK resources.
3. The SDK development resources are in the `libs` folder.



>The SDK is supported on Android 4.2 or above; however, hardware encoding can be enabled only on Android 4.3 (API 18) or above.

## Configuration Guide

#### SDK file import
Copy `mobilepb.jar`, `tmgsdk.jar`, and `wup-1.0.0-SNAPSHOT.jar` from the `libs` directory of the SDK to your Android project's `libs` directory as shown below (if there is no `libs` directory in your project, create one; if there is no `armeabi` and `armeabi-v7a` in it, copy them to it):

#### Project configuration
Add the code that imports the library into `build.gradle` in the `App` directory of the project.  

```
sourceSets {
        main {
            jniLibs.srcDirs = ['libs']
        }
}
```

#### Application permission configuration

Add the following permissions in the `AndroidManifest.xml` file of the project:

```
  <uses-permission android:name="android.permission.RECORD_AUDIO" />
  <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
  <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
  <uses-permission android:name="android.permission.INTERNET" />
  <uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
  <uses-permission android:name="android.permission.BLUETOOTH"/>
  <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
```

If the voice messaging and speech-to-text feature is to be used, add the following under the `application` node in the manifest file:
```
  <application android:usesCleartextTraffic="true" >
```

#### Code obfuscation
If you want to obfuscate the code, configure the following:
```
-dontwarn com.tencent.**
-keep class com.tencent.** { *;}
-keepclassmembers class com.tencent.**{*;}
```


## Advanced Android Configuration
According to [Behavior changes: all apps](https://developer.android.com/about/versions/pie/android-9.0-changes-all) for Android 9 on the Android Developers platform, Android 9 limits background apps' access to user inputs and sensor data, that is, apps running in the background cannot access the mic or camera.
If Android 9 users need to continue capturing audio or video after locking the screen, a service can be initiated before the screen is locked or the app is brought to the background and terminated before the screen is unlocked or the app is brought to the foreground.


