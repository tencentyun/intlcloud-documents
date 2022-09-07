This document mainly describes the notes on exporting the Android project so that the Android developers can easily debug and integrate the APIs for Game Multimedia Engine (GME).

## Project Export

The GME SDK provides lib files for v7a, v8a, x86, and x86_64 by default. Please delete unnecessary files as needed.


<dx-alert infotype="alarm" title="Note">
If the so file of the corresponding architecture is missing during the running of the Android system device, the system will crash.
</dx-alert>



## Configuring Permissions

**Add the following permissions in the AndroidManifest.xml file of the project**:

```
  <uses-permission android:name="android.permission.RECORD_AUDIO" />
  <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
  <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
  <uses-permission android:name="android.permission.INTERNET" />
  <uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
  <uses-permission android:name="android.permission.BLUETOOTH"/>
  <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
```
In the above permissions, read and write permissions are not mandatory.
```
  <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
```

- If you use the default log path (/SDCARD/Android/Data/files), it means that you do not call SetLogPath, and do not need Write_External_Storage permission.
- If you call the setLogPath API to set the log path to an external storage device, and the storage path of the voice message recording is an external storage device, you need to apply for the Write_External_Storage permission to the user and get the user's approval.

## App obfuscation

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
 [1. After the APP is exported to an Android mobile phone, when I open the app, an error message pops up indicating that the app is not supported by the device.](https://intl.cloud.tencent.com/document/product/607/39522#android-.E5.AF.BC.E5.87.BA.E9.97.AE.E9.A2.98)
 [2. What should I do if the screen goes black when I try to open an application after integrating the GME SDK and exporting an Apk file?](https://intl.cloud.tencent.com/document/product/607/39522#.E9.9B.86.E6.88.90-gme-sdk-.E5.B9.B6.E5.AF.BC.E5.87.BA-apk-.E5.90.8E.EF.BC.8C.E5.90.AF.E5.8A.A8.E7.A8.8B.E5.BA.8F.E5.8F.91.E7.94.9F.E9.BB.91.E5.B1.8F.E7.8E.B0.E8.B1.A1.EF.BC.8C.E5.A6.82.E4.BD.95.E8.A7.A3.E5.86.B3.EF.BC.9F)
</dx-fold-block>


