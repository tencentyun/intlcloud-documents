This document describes how to quickly integrate the Tencent Cloud IM SDK into your projects. To configure and integrate the SDK, follow these steps.
## Development Environment Requirements
- JDK 1.6.
- Android 4.0 (SDK API 14) or later.

## Integrating the SDK (aar)
You can either automatically integrate the IM SDK by using Gradle, or manually download aar and import it to your current project.

### Method 1: Automatic loading (aar)
The IM SDK has been published to the jcenter library, and you can configure Gradle to automatically download updates.
Use Android Studio to open the project that you want to integrate the SDK into ([TIM SDK Demo](https://github.com/tencentyun/TIMSDK/tree/master/Android) is used as an example here) and modify the app/build.gradle file as follows to complete SDK integration:

- **Step 1: Add SDK dependencies**

 Find build.gradle in the tuikit lib project and add IM SDK dependencies to "dependencies".
```
dependencies {
		api 'com.tencent.imsdk:imsdk: Version number'
}
```
>Replace "Version number" with the actual version number of the SDK. We recommend that you use the [latest version](https://github.com/tencentyun/TIMSDK/tree/master/Android/tuikit/libs).
>Here, the version number `4.0.10` is used as an example:
>```
dependencies {
		api 'com.tencent.imsdk:imsdk:4.0.10'
}
```
>
 ![](https://main.qcloudimg.com/raw/211945758a897f53299951d415209ea6.png)
- **Step 2: Specify the architecture used by the app**
In defaultConfig, specify the CPU architecture used by the app (armeabi-v7a, arm64-v8a, x86, and x86_64 are supported since IM SDK 4.3.118):
```
   defaultConfig {
        ndk {
            abiFilters "armeabi-v7a"
        }
    }
```

- **Step 3: Synchronize the SDK**
Click **Sync Now**. If you can access jcenter, the SDK is automatically downloaded and integrated into your project.
![](https://main.qcloudimg.com/raw/e3ce64d671fd4a159f8919332ce1ae15.png)


### Method 2: Manual download (aar)
If you encounter problems accessing jcenter, you can manually download the SDK and integrate it into your project:
- **Step 1: Download the IM SDK**
The latest version of the [IM SDK](https://github.com/tencentyun/TIMSDK/tree/master/Android/tuikit/libs) can be downloaded from Github.

- **Step 2: Copy the IM SDK to the project directory**
Copy the downloaded aar file to the **/libs** directory under the tuikit lib project:
![](https://main.qcloudimg.com/raw/bf71b27bbb52e879b75528e707194a2a.png)

- **Step 3: Specify the local repository path**
Add **flatDir** to build.gradle under the project’s root directory and specify the local repository path:
![](https://main.qcloudimg.com/raw/61b30f5e1c9cca868c1a0220231ffcde.png)

- **Step 4: Add IM SDK dependencies**
As tuikit is imported as a lib project, you need to add code for referencing the aar package to app/build.gradle and tuikit/build.gradle.
 ![](https://main.qcloudimg.com/raw/53d530fd5ce0b66c88e678250b3d9386.png)
 ![](https://main.qcloudimg.com/raw/5175545f0e583fba7b7099ee94c721fa.png)
- **Step 5: Specify the architecture used by the app**
In defaultConfig of app/build.gradle, specify the CPU architecture used by the app (armeabi-v7a, arm64-v8a, x86, and x86_64 are supported since IM SDK 4.3.118):
```
defaultConfig {
            ndk {
                abiFilters "armeabi-v7a"
            }
    }
```

- **Step 6: Synchronize the SDK**
Click **Sync Now** to finish the IM SDK integration.


## Integrating the SDK (jar and so)
If you do not want to integrate the aar library, you can integrate the IM SDK by importing the jar and so libraries:

- **Step 1: Download and decompress the IM SDK**
[Download](https://github.com/tencentyun/TIMSDK/tree/master/Android/tuikit/libs) the latest version of the aar file from Github and decompress it:
![](https://main.qcloudimg.com/raw/0529e40e225998b0a4419f33c55283b6.png)
The extracted folder contains a jar file and a so subfolder. Rename **classes.jar** to **imsdk.jar**. The file list is as follows:
![](https://main.qcloudimg.com/raw/cbe70a310281e4085cbe77f129202762.png)

- **Step 2: Copy SDK files to the project directory**
Copy the renamed jar file and armeabi-v7a folder to the tuikit/libs directory:
![](https://main.qcloudimg.com/raw/2c7b9300124815eeed1e942b799037af.png)

- **Step 3: Reference the jar library**
As tuikit is imported as a lib project, you need to add code for referencing the jar library to app/build.gradle and tuikit/build.gradle.
 - In app/build.gradle, add code for referencing the jar library:
![](https://main.qcloudimg.com/raw/83e5ce182acc734dd6d5674a18cb12be.png)
 - In tuikit/build.gradle, add code for referencing the jar library:
![](https://main.qcloudimg.com/raw/637afa9cebeb0b3b7506c414fef1becb.png)


- **Step 4: Reference the so library**
- In atuikit/build.gradle, add code for referencing the so library:
![](https://main.qcloudimg.com/raw/e48d628afa3f97e663f8e6c810badb01.png)

- **Step 5: Specify the architecture used by the app**
In defaultConfig of app/build.gradle, specify the CPU architecture used by the app (armeabi-v7a, arm64-v8a, x86, and x86_64 are supported since IM SDK 4.3.118):
```
   defaultConfig {
        ndk {
            abiFilters "armeabi-v7a"
        }
    }
```

- **Step 6: Synchronize the SDK**
Click **Sync Now** to finish the IM SDK integration.

## Configuring App Permissions
To configure app permissions in AndroidManifest.xml, the IM SDK requires the following permissions:

```
	<uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
	<uses-permission android:name="android.permission.INTERNET" />
	<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
	<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
```

## Setting Obfuscation Rules
In the proguard-rules.pro file, add IM SDK classes that you want ProGuard not to obfuscate:

```
-keep class com.tencent.** { *; }
```
