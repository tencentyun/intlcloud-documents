This document describes how to quickly integrate Tencent Cloud LiteAVSDK for Android into your project through the following procedure.

## Development Environment Requirements
- Android Studio 3.0 or later.
- Android 4.4 (SDK API 19) or later.

## Integrating the SDK (aar)
You can manually download the aar and import it into your current project.

### Download (aar)
 you can manually download the SDK and integrate it into your project:

- **Step 1: download the LiteAVSDK**
   Download the [LiveAVSDK](https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_International_Android_lastest.zip), and then decompress it.

- **Step 2: copy the LiteAVSDK to the project directory**  
  After decompressing the downloaded file, copy the aar file in the SDK directory to the **app/libs** directory of the project:
  ![](https://main.qcloudimg.com/raw/61ad7ee6accbfdf95c5283183388e35b.png)
  
- **Step 3: add the LiteAVSDK dependencies**   
  Add the code that imports the aar library to `app/build.gradle`.
  ![](https://main.qcloudimg.com/raw/1fa4e5a657611431516cad02ed159fe2.png)
```
 implementation fileTree(dir: "libs", include: ["*.jar", "*.aar"])
```

- **Step 5: specify the application architecture**
  In the `defaultConfig` of `app/build.gradle`, specify the CPU architecture to be used by the application. Currently, the LiteAVSDK supports armeabi, armeabi-v7a, and arm64-v8a.
```
defaultConfig {
        ndk {
            abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
        }
    }
```

- **Step 6: sync the SDK**
  Click **Sync Now** to complete the integration of LiteAVSDK.

## Integrating the SDK (jar)
If you do not want to integrate the aar library, you can choose to integrate the LiteAVSDK by importing the jar and so libraries:

- **Step 1: download and decompress the LiteAVSDK**
  Download the [LiveAVSDK](https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_International_Android_lastest.zip), and then decompress it. In the SDK directory, find `LiteAVSDK_International_xxx.zip` (in which `xxx` indicates the LiteAVSDK version number):

  ![](https://main.qcloudimg.com/raw/e1d44e1e8e75f3deae9a2564a149a64d.png)

  After decompression, you can get the `libs` directory which contains the jar files and so folders as listed below:
  ![](https://main.qcloudimg.com/raw/a683bcfe31c65d5348552b0d66dea416.png)

- **Step 2: copy the SDK files to the project directory**
  Copy the extracted jar files as well as armeabi, armeabi-v7a, and arm64-v8a folders to the `app/libs` directory.
  ![](https://main.qcloudimg.com/raw/1237c595de270f44dfd32509543d988c.png)

- **Step 3: import the jar library**
  Add the code that imports the jar library to `app/build.gradle`.
![](https://main.qcloudimg.com/raw/c68b21e92151db5fe098cafb1b0ccebc.png)      
```
dependencies {
    implementation fileTree(dir: "libs", include: ["*.jar", "*.aar"])
}
```


- **Step 4: import the so library**
  Add the code that imports the so library to `app/build.gradle`.
  ![](https://main.qcloudimg.com/raw/84fd7df878904535e3b079e812116d71.png)


- **Step 5: specify the application architecture**
  In the `defaultConfig` of `app/build.gradle`, specify the CPU architecture to be used by the application. Currently, the LiteAVSDK supports armeabi, armeabi-v7a, and arm64-v8a.
```
   defaultConfig {
        ndk {
            abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
        }
    }
```

- **Step 6: sync the SDK**
  Click **Sync Now** to complete the integration of LiteAVSDK.

## Configuring Application Permissions
Configure application permissions in `AndroidManifest.xml`. The LiteAVSDK requires the following permissions:

```
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.CAMERA" />
    <uses-permission android:name="android.permission.RECORD_AUDIO" />
    <uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
    <uses-permission android:name="android.permission.BLUETOOTH" />
```

## Configuring License Authorization

Click [License application](https://console.cloud.tencent.com/live/license) to obtain a Trial License. You will get two character strings: one is licenseURL, and the other is the decryption key.

Before your app calls relevant features of the SDK Enterprise Edition, we recommend that you configure the following settings (in the Application class):

```java
public class MApplication extends Application {

    @Override
    public void onCreate() {
        super.onCreate();
        String licenceURL = ""; // The license URL obtained
        String licenceKey = ""; // The license key obtained
        TXLiveBase.getInstance().setLicence(this, licenceURL, licenceKey);
    }
}
```



## Setting Obfuscation Rules
In the `proguard-rules.pro` file, add the classes related to the LiteAVSDK to the "do not obfuscate" list:

```
-keep class com.tencent.** { *; }
```
