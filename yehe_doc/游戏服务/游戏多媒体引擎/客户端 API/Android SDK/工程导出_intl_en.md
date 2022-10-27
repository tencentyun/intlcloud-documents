This document mainly describes the notes on exporting the Android project so that the Android developers can easily debug and integrate the APIs for Game Multimedia Engine (GME).

## Project Export

The GME SDK provides lib files for v7a, v8a, x86, and x86_64 by default. Please delete unnecessary files as needed.


<dx-alert infotype="alarm" title="Note">
If the so file of the corresponding architecture is missing during the running of the Android system device, the system will crash.
</dx-alert>



## Configuring Permissions

### Required permissions

You must add the following permissions in the `AndroidManifest.xml` file of the project:

```
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
```

### Adding permissions as needed

Add the following permissions in the `AndroidManifest.xml` file of the project as needed:

<dx-tabs>
::: Read/Write permission
The read/write permission is not required. Determine whether to add it according to the following rules:

- If you use the default log path (/SDCARD/Android/Data/files), it means that you do not call SetLogPath, and do not need Write_External_Storage permission.
- If you call the setLogPath API to set the log path to an external storage device, and the storage path of the voice message recording is an external storage device, you need to apply for the Write_External_Storage permission to the user and get the user's approval.

```
 <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
```
:::
::: Bluetooth permission
Add the Bluetooth permission according to the following rules:

- If `targetSDKVersion` in the project is v30 or earlier:
```
<uses-permission android:name="android.permission.BLUETOOTH"/>
```

- If `targetSDKVersion` in the project is v31 or later:
```
<uses-permission android:name="android.permission.BLUETOOTH" android:maxSdkVersion="30" />
<uses-permission android:name="android.permission.BLUETOOTH_CONNECT" />
```
:::
</dx-tabs>






## App Obfuscation

If you want to obfuscate the code, configure the following:

```
-dontwarn com.tencent.**
-keep class com.tencent.** { *;}
-keepclassmembers class com.tencent.**{*;}
```

Note that after **v2.9.0**, obfuscation is required with the following configurations.
```
-dontwarn com.gme.**
-keep class com.gme.** { *;}
-keepclassmembers class com.gme.**{*;}
```

## Advanced Android Configuration

- According to [Behavior changes: all apps](https://developer.android.com/about/versions/pie/android-9.0-changes-all) for Android 9 on the Android Developers platform, Android 9 limits background apps' access to user inputs and sensor data, that is, apps running in the background cannot access the mic or camera.
- If Android 9 users need to continue capturing audio or video after locking the screen, a service can be initiated before the screen is locked or the app is brought to the background and terminated before the screen is unlocked or the app is brought to the foreground.


## Android Project Export FAQs

<dx-fold-block title="Project problems occurred during or after the export of the executable files">
 [1. After the APP is exported to an Android mobile phone, when I open the app, an error message pops up indicating that the app is not supported by the device.](https://intl.cloud.tencent.com/document/product/607/39522)
 [2. What should I do if the screen goes black when I try to open an application after integrating the GME SDK and exporting an APK file?](https://intl.cloud.tencent.com/document/product/607/39522)
</dx-fold-block>


