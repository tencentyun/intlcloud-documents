This document describes how to quickly integrate RT-Cube's player SDK into your project. Different versions of the SDK can be integrated in the same way.

## Environment Requirements
- Android Studio 2.0 or above
- Android 4.1 (SDK API level 16) or above

## Integrating the SDK (AAR)
You can use Gradle to automatically load the AAR file or manually download the AAR file and import it into your project.

### Method 1: automatic loading (AAR) 
The player SDK has been released to the [mavenCentral repository](https://repo1.maven.org/maven2/com/tencent/liteav/LiteAVSDK_Player_Premium/), and you can configure it in Gradle to download `LiteAVSDK_Player_Premium` updates automatically.
Open your project with Android Studio and modify the `build.gradle` file as described below to complete the integration.
![](https://qcloudimg.tencent-cloud.cn/raw/7de67c57e87f2803217b77ed308d537d.png)

1. Add the `mavenCentral` repository to the `build.gradle` in your project's root directory.
```xml
repositories {
    mavenCentral()
}
```

2. Open the `build.gradle` in the `app` directory and add the `LiteAVSDK_Player` dependencies to `dependencies`.
```
dependencies {
  // This configuration integrates the latest version of `LiteAVSDK_Player_Premium` by default.
	implementation 'com.tencent.liteav:LiteAVSDK_Player_Premium:latest.release'
  // To integrate an earlier version such as 10.8.0.29000, configure as follows:
  // implementation 'com.tencent.liteav:LiteAVSDK_Player_Premium:10.8.0.29000'
}
```
3. In `defaultConfig`, specify the CPU architecture to be used by the application. Currently, LiteAVSDK_Player supports armeabi, armeabi-v7a, and arm64-v8a.
```
defaultConfig {
	ndk {
		abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
	}
}
```
4. Click the **Sync Now** button ![](https://main.qcloudimg.com/raw/d6b018054b535424bb23e42d33744d03.png) to sync the SDK. If you have no problem accessing Maven Central, the SDK will be downloaded and integrated into your project automatically.

### Method 2: manual download (AAR)
If you have problem accessing Maven Central, you can manually download the SDK and integrate it into your project.
1. Download [LiteAVSDK_Player_Premium](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Player_Premium_Android_latest.zip) and decompress the file.
2. Copy the AAR file in the SDK directory to the **app/libs** directory of your project.
    ![](https://qcloudimg.tencent-cloud.cn/raw/ab00ad0f12a271750d6f84f7333f8cd3.png)
3. Add **flatDir** to `build.gradle` under your project’s root directory to specify the local path for the repository.
    ![](https://main.qcloudimg.com/raw/726771558714a2b4fae8dc1a59c33ffc.png) 
4. Add the LiteAVSDK_Player_Premium dependency and then add code that references the AAR file in `app/build.gradle`.
    ![](https://qcloudimg.tencent-cloud.cn/raw/ac9ab42dda8992d435832c605f1e6798.png)
```
implementation(name:'LiteAVSDK_Player_10.8.0.29000', ext:'aar')
```
5. In `defaultConfig` of `app/build.gradle`, specify the CPU architecture to be used by the application. Currently, LiteAVSDK_Player supports armeabi, armeabi-v7a, and arm64-v8a.
```
defaultConfig {
	ndk {
		abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
	}
}
```
6. Click **Sync Now** to complete the integration of LiteAVSDK.

## Integrating the SDK (JAR)
If you do not want to import the AAR library, you can also integrate LiteAVSDK by importing JAR and SO libraries.

1. Download [LiteAVSDK_Player_Premium](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Player_Premium_Android_latest.zip) and decompress it. Find `LiteAVSDK_Player_Premium_xxx.zip` (`xxx` is the version number) in the SDK directory. After decompression, you can get the `libs` directory, which contains the JAR file and folders of SO files as listed below:
    ![](https://qcloudimg.tencent-cloud.cn/raw/ab82529bd214ba8488f29b45b38f61f6.png)

  If you also need the .so file for the armeabi architecture, copy the `armeabi-v7a` directory and rename it `armeabi`.

2. Copy the JAR file and `armeabi`, `armeabi-v7a`, and `arm64-v8a` folders to the `app/libs` directory.
    ![](https://main.qcloudimg.com/raw/d9b6339cb52fb85afda42de6001be337.png)
3. Add code that references the JAR library in `app/build.gradle`.
    ![](https://main.qcloudimg.com/raw/695520309d9a01b19ce2f50439a42890.png)      
```
dependencies {
	implementation fileTree(dir:'libs',include:['*.jar'])
}
```
4. Add **flatDir** to `build.gradle` under the project’s root directory to specify the local path for the repository.
![](https://main.qcloudimg.com/raw/6c68b846f6f7258ae4d96bc1d95d7816.png)
5. In `app/build.gradle`, add code that references the SO libraries.
![](https://main.qcloudimg.com/raw/e0f2f39c5f53a9fd5ca084febdd4e637.png)
6. In the `defaultConfig` of `app/build.gradle`, specify the CPU architecture to be used by the application (currently, LiteAVSDK supports armeabi, armeabi-v7a, and arm64-v8a). 
```
defaultConfig {
    ndk {
        abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
    }
}
```
7. Click **Sync Now** to complete the integration.

## Setting Packaging Parameters
![](https://main.qcloudimg.com/raw/dabfd69ee06e4d38bb3b51fc436c0ad1.png)
```
packagingOptions{
	pickFirst '**/libc++_shared.so'
	doNotStrip "*/armeabi/libYTCommon.so"
	doNotStrip "*/armeabi-v7a/libYTCommon.so"
	doNotStrip "*/x86/libYTCommon.so"
	doNotStrip "*/arm64-v8a/libYTCommon.so"
} 
```

## Configuring Permissions

Configure permissions for your application in `AndroidManifest.xml`. LiteAVSDK needs the following permissions:

```
<!--network permission-->
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<!--storage-->
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```

## Configuring Obfuscation Rules
In the `proguard-rules.pro` file, add LiteAVSDK classes to the "do not obfuscate" list.

```
-keep class com.tencent.** { *;}
```

## Configuring License

Click [Apply for License](https://www.tencentcloud.com/document/product/266/51098) to apply for a trial license as instructed in [Adding and Renewing a License](https://www.tencentcloud.com/document/product/266/51098#.E7.94.B3.E8.AF.B7.E6.B5.8B.E8.AF.95.E7.89.88-license). If no license is configured, video playback will fail. You will get two strings: a license URL and a decryption key.

Before you use the SDK features in your application, complete the following configurations (preferably in the application class).

```java
public class MApplication extends Application {

    @Override
    public void onCreate() {
        super.onCreate();
        String licenceURL = ""; // The license URL obtained
        String licenceKey = ""; // The license key obtained
        TXLiveBase.getInstance().setLicence(this, licenceURL, licenceKey);
        TXLiveBase.setListener(new TXLiveBaseListener() {
            @Override
            public void onLicenceLoaded(int result, String reason) {
                Log.i(TAG, "onLicenceLoaded: result:" + result + ", reason:" + reason);
            }
        });
    }
}
```

## Viewing License Information

After the license is successfully configured, you can call the API below to view the license information. Please note that it may take a while for the configuration to take effect. The exact time needed depends on your network conditions.

```java
TXLiveBase.getInstance().getLicenceInfo();
```

## FAQs

1. What should I do if a duplicate symbol error occurs because my project integrates multiple editions of LiteAVSDK such as CSS, TRTC, and Player?

If you integrate two or more editions of LiteAVSDK (MLVB, Player, TRTC, UGSV), a library conflict error will occur when you build your project. This is because some symbol files are shared among the underlying libraries of the SDKs. To solve the problem, we recommend you integrate the All-in-One SDK, which includes the features of MLVB, Player, TRTC, and UGSV. For details, see [SDK Download](https://www.tencentcloud.com/document/product/266/50561).
