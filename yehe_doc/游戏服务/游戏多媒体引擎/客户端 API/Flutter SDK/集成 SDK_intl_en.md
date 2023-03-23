This document describes how to configure a Flutter project for the GME APIs for Flutter.

## Supported Platforms

The GME SDK for Flutter supports iOS and Android platforms.

## Importing the SDK

### Step 1. Download the GME SDK for Flutter

Download the SDK file in [SDK Download Guide](https://intl.cloud.tencent.com/document/product/607/18521), which contains the GME plugin. Decompress the SDK file to a local directory.

### Step 2. Add dependencies of the GME plugin to the Flutter project

Add GME dependencies to the `pubspec.yaml` file in your Flutter project. Note that the `path` parameter is the path where the SDK file is decompressed to.
``` bash
dependencies:
  flutter:
    sdk: flutter
  gme:
    path: ../
```

After saving the `pubspec.yaml` file, run the `flutter pub get` command on the CLI to make the GME plugin in the project take effect (if the Flutter plugin is configured in your IDE, this command will be executed automatically once the file is saved).
``` bash
flutter pub get
```

## Modifying the iOS Project
1. In Terminal, go to the iOS project directory of your Flutter project and run `pod install`.

2. In the Xcode project, configure the following GME dependent library files (you can skip this step if such dependencies already exist in your project):
![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100022348635/3b7e2b2ba91e11ed9e14525400088f3a.png?q-sign-algorithm=sha1&q-ak=AKIDXRkeWGao-4Lv3f_Eu1m3VnMKKY6x8epsBbtjkms4ddDo74Ms78vFddiSrwbcU8jQ&q-sign-time=1677574660;1677578260&q-key-time=1677574660;1677578260&q-header-list=&q-url-param-list=&q-signature=bf2bce23372294095f44ea81d6ab081e19d3cdd0&x-cos-security-token=4BxBX1TdmsXQgKiC0yuQkiNKPjqcXA3ab3ea5ec8dc478a562f373af322df1e3bt1CAEDm-_AoFFamI9r7Z0Qo4kHjZ0fSHNxd4tvhUTTLE7ZVd9s-RurQ5v-9OEjAl4WGsJvhiUrpbooKU0qFC1HtwKSU8O6NVGJ6NZocBI0EAqA6XcsnjJfn8JsFxo1Hb7WAcR2k6sMrYl9csiYZW_poBONMAAwo_5tBmXa-et6MAuFNuBH4NlLm7eFJlTn0MR3L_csg8Q_8dFfnyxl14-y7FWsHh7olUQbIS3dyyuMMVUksk6zotFcewS08U5DdgVlsK5mzH68JMn2Ee4Ne2_OqLnxFB92a0TSIahKuWuB-vditl2wbPulD9DMkdb4ZEL38Zyvff1qsrO_RmrjtWinDWnEBnCw8vJZlT70QYeP3NYnGbhVBIfysFNbB6TyHp)

3. The GME SDK for iOS requires the following permissions:

- Required background modes: Allows running in the background (optional).

- Microphone Usage Description: Allows access to microphone.


## Modifying the Android Project
1. As GME requires permissions such as call permission and uses the permission management plugin `flutter permission-handler`, you need to modify the project as follows to use the SDK for Android 31 or later (skip this step if the SDK is already in the project):


   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100025598411/2be82716adce11ed9e14525400088f3a.png?q-sign-algorithm=sha1&q-ak=AKIDQvqZYxEAxGk7IGQ5VxYx9ES21_DoTUx_ubBjhure4A7pxIe0GL3MHmSAchNQKAA3&q-sign-time=1677574660;1677578260&q-key-time=1677574660;1677578260&q-header-list=&q-url-param-list=&q-signature=f1191c9c7b59a54d0509ecabefe7ea96456208e6&x-cos-security-token=bK7rgYee6Vlrw9RJjpxrtdfDlY04DBKa792613b4a003612ede236793ba1a4008OaKmfZJKditLmR-Y5Yin3UxRFASPLWyamAKRx-xY-qaRj0vYqXEMUqLjdbhfW9aTel3RxGt7GuYCuOILDA8msvrLtHDmWiPW1_kpPDq947w7kHezY0h4oaFirCp7LAgBNVsUBFydps-b0HOsFPkI8ceS7EMbLtxNhdsm3vx6dMf6JfHNK2cft32BuwaeSOFm3r1nsrsm9SoJv7yD5u1k76tUzdsMbI_xC_XUUztnKz0pxI2afuCsQeYmKLjLSevui57MB2cxuPRmZCKtD2HGEDyWnJFMVibQHnFTMw90i5DoT-GGre95x3cjeEIOglo0DZwjjdZuBIcFbRQ1sijX-35MpuYAga7_-s0oZ2eiHdvgpMhUC3x2deRanGBnvyhu)

2. Add the project permissions to the Flutter project file `android/app/src/AndroidManifest.xml` (skip this step if such permissions have been added):

   ``` bash
   <uses-permission android:name="android.permission.RECORD_AUDIO" />
   <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
   <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
   <uses-permission android:name="android.permission.INTERNET" />
   <uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
   ```

