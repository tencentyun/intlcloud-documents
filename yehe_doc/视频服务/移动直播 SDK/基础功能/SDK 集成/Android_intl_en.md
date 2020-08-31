This document describes how to quickly integrate Tencent Cloud LiteAVSDK for Android into your project through the following procedure.

## Development Environment Requirements
- Android Studio 3.0 or later.
- Android 4.4 (SDK API 19) or later.

## Integrating the SDK (aar)
You can choose to use Gradle to automatically load aar or manually download the aar and import it into your current project.

### Method 1: automatic loading (aar)
LiteAVSDK has been released to the JCenter repository, and you can configure Gradle to download updates automatically.
Simply use Android Studio to open the project that needs to be integrated with the SDK and then modify the `app/build.gradle` file in three simple steps to complete SDK integration:
![](https://main.qcloudimg.com/raw/eb6bcb3cb1dff43f459245ed9045e685.png)

- **Step 1: add SDK dependencies**   
  Add the LiteAVSDK dependencies to `dependencies`.
```
dependencies {
     implementation 'com.tencent.liteavsdk:LiteAVSDK_Smart:latest.release'
}
```
Or
```
dependencies {
     implementation 'com.tencent.liteavsdk:LiteAVSDK_Smart:latest.release@aar'
}
```
- **Step 2: specify the application architecture**
  In `defaultConfig`, specify the CPU architecture to be used by the application. Currently, LiteAVSDK supports armeabi, armeabi-v7a, and arm64-v8a.
```
defaultConfig {
     ndk {
         abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
     }
}
```
- **Step 3: sync the SDK**
  Click ![](https://main.qcloudimg.com/raw/d6b018054b535424bb23e42d33744d03.png)**Sync Now**. If JCenter can be accessed, the SDK will be automatically downloaded and integrated into the project soon.

### Method 2: manual download (aar)
If JCenter cannot be accessed, you can manually download the SDK and integrate it into your project:

- **Step 1: download the LiteAVSDK**
   Download the [LiveAVSDK](https://intl.cloud.tencent.com/document/product/1071/38150), and then decompress it.

- **Step 2: copy the LiteAVSDK to the project directory**  
  After decompressing the downloaded file, copy the aar file in the SDK directory to the **app/libs** directory of the project:
  ![](https://main.qcloudimg.com/raw/0550edd82139cbbfaba3cc656b4fdd9e.png)
  
- **Step 3: specify the path to the local repository**
  Add **flatDir** to `build.gradle` under the project’s root directory and specify the local repository path.
  ![](https://main.qcloudimg.com/raw/726771558714a2b4fae8dc1a59c33ffc.png)
  
- **Step 4: add the LiteAVSDK dependencies**   
  Add the code that imports the aar library to `app/build.gradle`.
  ![](https://main.qcloudimg.com/raw/2333ec86f332907e7bf45b6cf83ee7b3.png)
```
implementation(name:'LiteAVSDK_Smart_6.4.7265', ext:'aar')
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
  Download the [LiveAVSDK](https://intl.cloud.tencent.com/document/product/1071/38150), and then decompress it. In the SDK directory, find `LiteAVSDK_Smart_xxx.zip` (in which `xxx` indicates the LiteAVSDK version number):

  ![](https://main.qcloudimg.com/raw/e17f5e1e2a712d86f541013c176d9ece.png)

  After decompression, you can get the `libs` directory which contains the jar files and so folders as listed below:
  ![](https://main.qcloudimg.com/raw/58196dc2b1e4e1cd63f47e6cac8d3be6.png)

- **Step 2: copy the SDK files to the project directory**
  Copy the extracted jar files as well as armeabi, armeabi-v7a, and arm64-v8a folders to the `app/libs` directory.
  ![](https://main.qcloudimg.com/raw/d9b6339cb52fb85afda42de6001be337.png)

- **Step 3: import the jar library**
  Add the code that imports the jar library to `app/build.gradle`.
	![](https://main.qcloudimg.com/raw/695520309d9a01b19ce2f50439a42890.png)			
```
dependencies {
		implementation fileTree(dir:'libs',include:['*.jar'])
}
```


- **Step 4: import the so library**
  Add the code that imports the so library to `app/build.gradle`.
  ![](https://main.qcloudimg.com/raw/e0f2f39c5f53a9fd5ca084febdd4e637.png)


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

## Setting Application Packaging Parameters
![](https://main.qcloudimg.com/raw/dabfd69ee06e4d38bb3b51fc436c0ad1.png)

```
    packagingOptions {
        pickFirst '**/libc++_shared.so'
        doNotStrip "*/armeabi/libYTCommon.so"
        doNotStrip "*/armeabi-v7a/libYTCommon.so"
        doNotStrip "*/x86/libYTCommon.so"
        doNotStrip "*/arm64-v8a/libYTCommon.so"
    } 
```

## Configuring Application Permissions
Configure application permissions in `AndroidManifest.xml`. The LiteAVSDK requires the following permissions:

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
