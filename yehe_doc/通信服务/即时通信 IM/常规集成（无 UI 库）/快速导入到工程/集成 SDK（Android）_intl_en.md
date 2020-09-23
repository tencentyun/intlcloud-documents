This document describes how to quickly integrate the Tencent Cloud IM SDK in your projects. To configure and integrate the SDK, complete the following steps.
## Development Environment Requirements
- JDK 1.6
- Android 4.1 (SDK API 16) or later

## Integrating the SDK (aar)
You can automatically integrate the IM SDK by using Gradle or manually download aar and import it to your current project.

### Method 1: automatic loading (aar)
The IM SDK has been released to the JCenter repository, and you can configure Gradle to automatically download updates.
Use Android Studio to open the project that you want to integrate the SDK into and modify the app/build.gradle file as follows to complete SDK integration:

- **Step 1: Add SDK dependencies**

 Find build.gradle and add IM SDK dependencies to the "dependencies" section.
 If you are using the standard edition of IM SDK, add the following dependencies:
```
dependencies {
		api 'com.tencent.imsdk:imsdk: <Version number>'
}
```
If you are using the lite edition of IM SDK, add the following dependencies:
```
dependencies {
		api 'com.tencent.imsdk:imsdk-smart: <Version number>'
}
```
>? Replace "Version number" with the actual version number of the SDK. We recommend that you use the [latest version](https://github.com/tencentyun/TIMSDK/tree/master/Android/tuikit/libs).
> The following code uses the version number `4.9.1` as an example.
>```
> dependencies {
> api 'com.tencent.imsdk:imsdk:4.9.1'
>}
>```

 
- **Step 2: Specify the architecture used by the app**
In defaultConfig, specify the CPU architecture used by the app (armeabi-v7a, arm64-v8a, x86, and x86_64 are supported from IM SDK V4.3.118.)
```
   defaultConfig {
        ndk {
            abiFilters "arm64-v8a"
        }
    }
```

- **Step 3: Synchronize the SDK**
Click "Sync Now". If the connection to JCenter is normal, the SDK will be automatically downloaded and integrated into your project.
![](https://main.qcloudimg.com/raw/2e281799c00da2dba59551ff26c6561e.png)


### Method 2: manual download (aar)
If you encounter problems when accessing JCenter, you can manually download the SDK and integrate it into your project.
- **Step 1: Download the IM SDK**
Download the latest version of [IM SDK](https://github.com/tencentyun/TIMSDK/tree/master/Android/SDK) from GitHub.

- **Step 2: Copy the downloaded IM SDK to the project directory**
Copy the downloaded aar file to the **/libs** directory of the project.
![](https://main.qcloudimg.com/raw/4175f483d55c2f99b99c993ada8dd5a0.png)

- **Step 3: Specify the architecture used by the app and then compile and run the architecture**
In defaultConfig of app/build.gradle, specify the CPU architecture used by the app (armeabi-v7a, arm64-v8a, x86, and x86_64 are supported from IM SDK V4.3.118.)
```
defaultConfig {
	ndk {
		abiFilters "arm64-v8a"
	}
}
```


## Integrating the SDK
If you do not want to integrate the aar library, you can integrate the IM SDK by importing the jar and so libraries.

- **Step 1: Download and decompress the IM SDK**
[Download](https://github.com/tencentyun/TIMSDK/tree/master/Android/SDK) the latest version of the aar file from GitHub and decompress it. The extracted folder contains a jar file and a so subfolder. Rename **classes.jar** to **imsdk.jar**.
![](https://main.qcloudimg.com/raw/9a2cebad9475735c456fea0795088679.png)

- **Step 2: Copy the SDK files to the project directory**
Copy the renamed jar file and so files of different architectures to the default loading directories of Android Studio.
![](https://main.qcloudimg.com/raw/237b44da2ec04ba87a6cef66aa0b5321.png)

- **Step 3: Specify the architecture used by the app and then compile and run the architecture**
In defaultConfig of app/build.gradle, specify the CPU architecture used by the app (armeabi-v7a, arm64-v8a, x86, and x86_64 are supported from IM SDK V4.3.118.)
```
   defaultConfig {
        ndk {
            abiFilters "arm64-v8a"
        }
    }
```

## Configuring App Permissions
To configure app permissions in AndroidManifest.xml, the IM SDK must have the following permissions:

```
	<uses-permission android:name="android.permission.INTERNET" />
	<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
	<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
```

## Configuring Obfuscation Rules
In the `proguard-rules.pro` file, add the IM SDK classes that you do not want ProGuard to obfuscate.

```
-keep class com.tencent.imsdk.** { *; }
```

```
