
This document describes how to quickly integrate Tencent Cloud LiteAVSDK for Android into your project.

## Environment Requirements
- Android Studio 2.0 or above
- Android 4.1 (SDK API level 16) or above

## Integrating the SDK (AAR)
You can use Gradle to automatically load the AAR file or manually download the AAR file and import it into your project.

### Method 1: automatic loading (AAR)
Since JCenter has been deprecated, you can configure a Maven Central repository in Gradle to automatically download and update LiteAVSDK.
Open your project with Android Studio and modify the `build.gradle` file as described below to complete the integration.
![](https://qcloudimg.tencent-cloud.cn/raw/288cbffd943bd8c03c3863980cf00455.png)

1. Open `build.gradle` under your application.
2. Add the LiteAVSDK dependency to `dependencies`.
<dx-codeblock>
:::  jar
dependencies {
	implementation 'com.tencent.liteav:LiteAVSDK_International:latest.release'
}
::: 
</dx-codeblock>
Or
<dx-codeblock>
:::  jar
dependencies {
	implementation 'com.tencent.liteav:LiteAVSDK_International:latest.release@aar'
}
::: 
</dx-codeblock>
3. In `defaultConfig`, specify the CPU architecture to be used by the application. Currently, LiteAVSDK supports armeabi, armeabi-v7a, and arm64-v8a.
<dx-codeblock>
:::  jar
defaultConfig {
	ndk {
		abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
	}
}
::: 
</dx-codeblock>
4. Click the **Sync Now** button ![](https://main.qcloudimg.com/raw/d6b018054b535424bb23e42d33744d03.png) to sync the SDK. If you have no problem accessing Maven Central, the SDK will be downloaded and integrated into your project automatically.

### Method 2: manual download (AAR)
If you have problem accessing Maven Central, you can manually download the SDK and integrate it into your project.

1. Download [LiteAVSDK](https://intl.cloud.tencent.com/document/product/1071/38150) and decompress the file.
2. Copy the AAR file in the SDK directory to the **app/libs** directory of your project.
    ![](https://qcloudimg.tencent-cloud.cn/raw/32b42946b8240fa3c2b4066091a6bc1c.png)
3. Add **flatDir** to `build.gradle` under your project’s root directory to specify the local path for the repository.
    ![](https://main.qcloudimg.com/raw/726771558714a2b4fae8dc1a59c33ffc.png) 
4. Add the LiteAVSDK dependency and, in `app/build.gradle`, add code that references the AAR file.
    ![](https://qcloudimg.tencent-cloud.cn/raw/ad7f3e2ce465c7d47f7d71f020cb02a2.png)
```
implementation(name:'LiteAVSDK_International_8.7.10102', ext:'aar')
```
5. In `defaultConfig` of `app/build.gradle`, specify the CPU architecture to be used by the application. Currently, LiteAVSDK supports armeabi, armeabi-v7a, and arm64-v8a.
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

1. Download [LiteAVSDK](https://intl.cloud.tencent.com/document/product/1071/38150) and decompress the file. In the SDK directory, find `LiteAVSDK_International_xxx.zip` (`xxx` indicates the version number of LiteAVSDK).
    ![](https://main.qcloudimg.com/raw/aae5879bccd31e8c082eebc24aa4ff7c.png)
    Decompress the file, and you will find a `libs` directory that contains a JAR file and several SO folders, as shown below:
    ![](https://main.qcloudimg.com/raw/e916aaddf844785991dc25f78776d773.png)
2. Copy the JAR file and `armeabi`, `armeabi-v7a`, and `arm64-v8a` folders to the `app/libs` directory.
    ![](https://main.qcloudimg.com/raw/d9b6339cb52fb85afda42de6001be337.png)
3. Add code that references the JAR library in `app/build.gradle`.
![](https://main.qcloudimg.com/raw/695520309d9a01b19ce2f50439a42890.png)      
<dx-codeblock>
:::  jar
dependencies {
	implementation fileTree(dir:'libs',include:['*.jar'])
}
:::
</dx-codeblock>
4. Add **flatDir** to `build.gradle` under the project’s root directory to specify the local path for the repository.
    ![](https://main.qcloudimg.com/raw/6c68b846f6f7258ae4d96bc1d95d7816.png)
5. In `app/build.gradle`, add code that references the SO libraries.
    ![](https://main.qcloudimg.com/raw/e0f2f39c5f53a9fd5ca084febdd4e637.png)
6. In `defaultConfig` of `app/build.gradle`, specify the CPU architecture to be used by the application. Currently, LiteAVSDK supports armeabi, armeabi-v7a, and arm64-v8a.
<dx-codeblock>
:::  jar
defaultConfig {
    ndk {
        abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
    }
}
:::
</dx-codeblock>
7. Click **Sync Now** to complete the integration.

## Setting Packaging Parameters
![](https://main.qcloudimg.com/raw/dabfd69ee06e4d38bb3b51fc436c0ad1.png)

<dx-codeblock>
::: Packaging parameters
    packagingOptions {
        pickFirst '**/libc++_shared.so'
        doNotStrip "*/armeabi/libYTCommon.so"
        doNotStrip "*/armeabi-v7a/libYTCommon.so"
        doNotStrip "*/x86/libYTCommon.so"
        doNotStrip "*/arm64-v8a/libYTCommon.so"
    } 
:::
</dx-codeblock>

## Configuring Permissions
Configure permissions for your application in `AndroidManifest.xml`. LiteAVSDK needs the following permissions:

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

## Configuring License

Log in to the CSS console, go to **MLVB SDK** > **[License Management](https://console.intl.cloud.tencent.com/live/license)**, and click **Get License** to obtain a trial license. For detailed directions, see [Applying for trial license](https://intl.cloud.tencent.com/document/product/1071/38546). You will get two strings: a license URL and a decryption key.

Before you use LiteAVSDK features in your application, complete the following configurations (preferably in the application class).

<dx-codeblock>
::: java java
public class MApplication extends Application {

    @Override
    public void onCreate() {
        super.onCreate();
        String licenceURL = ""; // The license URL obtained
        String licenceKey = ""; // The license key obtained
        TXLiveBase.getInstance().setLicence(this, licenceURL, licenceKey);
    }
}
:::
</dx-codeblock>

## Configuring Obfuscation Rules
In the `proguard-rules.pro` file, add LiteAVSDK classes to the "do not obfuscate" list.

```
-keep class com.tencent.** { *;}
```