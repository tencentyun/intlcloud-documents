## Overview

Tencent Cloud RT-Cube Superplayer for Android is an open-source Tencent Cloud player component. It can provide powerful playback functionality similar to Tencent Video with just a few lines of code. It has basic features such as landscape/portrait orientation switching, definition selection, gestures, and small window playback, as well as special features such as video buffering, software/hardware decoding switching, and adjustable-speed playback. It supports more formats and has better compatibility and functionality than system-default players. In addition, it features instant broadcasting of the first frame and low latency and offers advanced capabilities like video thumbnail.

## Version Support

The support for the features described in this document by Tencent Cloud RT-Cube is as follows:

| Version Name                            | Smart                                               | Live                                                | UGSV                                                  | TRTC                                             | Player                                                | All Features                                                       |
| ----------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ----------------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Support                            | -                                                            | -                                                            | -                                                            | -                                                           | &#10003;                                                     | &#10003;                                                     |
| SDK download <div style="width: 90px"/> | [Download](https://vcube.cloud.tencent.com/home.html?sdk=basicLive) | [Download](https://vcube.cloud.tencent.com/home.html?sdk=interactivelive) | [Download](https://vcube.cloud.tencent.com/home.html?sdk=shortVideo) | [Download](https://vcube.cloud.tencent.com/home.html?sdk=video) | [Download](https://vcube.cloud.tencent.com/home.html?sdk=player) | [Download](https://vcube.cloud.tencent.com/home.html?sdk=allPart) |


## Project Address[](id:sdkDownload)

The Tencent Cloud RT-Cube Superplayer for Android can be downloaded [here](https://github.com/tencentyun/SuperPlayer_Android).

## Target Audience

This document describes Tencent Cloud's proprietary capabilities. Please make sure that you have activated the relevant [Tencent Cloud](https://intl.cloud.tencent.com) services before reading it. If you haven't registered an account, please [sign up for free trial](https://intl.cloud.tencent.com/login) first.

## Integration Guide[](id:guide)
You can choose to use Gradle for automatic loading or manually download the aar and import it into your current project.

### Method 1. Automatic loading (AAR)

1. Download the SDK + Demo development kit for Android [here](https://github.com/tencentyun/SuperPlayer_Android).
2. Copy the `Demo/superplayerkit` module to your project and then configure as follows:
   - Import `superplayerkit` into `setting.gradle` in your project directory.
   ```xml
   include ':superplayerkit'
   ```
   - Open the `build.gradle` file of the `superplayerkit` project and modify the constant values of `compileSdkVersion`, `buildToolsVersion`, `minSdkVersion`, `targetSdkVersion`, and `rootProject.ext.liteavSdk`.
![](https://main.qcloudimg.com/raw/fd6bc41bfd8b80fe5e82e3345b6ce73f.png)
   ```xmls
   compileSdkVersion 26
   buildToolsVersion "26.0.2"
   
   defaultConfig {
       targetSdkVersion 23
       minSdkVersion 19
   }
   
   dependencies {
       implementation 'com.tencent.liteav:LiteAVSDK_Player:latest.release'
   }
   ```
3. Configure the `mavenCentral` library in Gradle, and LiteAVSDK will be automatically downloaded and updated. Open `app/build.gradle` and configure as follows:
![](https://main.qcloudimg.com/raw/65439d399ec584871a7a9bc88ccaef46.png)
   - Add the `LiteAVSDK_Player` dependencies to `dependencies`.
   ```xml
   dependencies {
       implementation 'com.tencent.liteav:LiteAVSDK_Player:latest.release'
       implementation project(':superplayerkit')
       // Third-party library for integration of the on-screen commenting feature of superplayer
       implementation 'com.github.ctiao:DanmakuFlameMaster:0.5.3'
   }
   ```
   - In the `defaultConfig` of `app/build.gradle`, specify the CPU architecture to be used by the application (currently, LiteAVSDK supports armeabi, armeabi-v7a, and arm64-v8a, which you can configure as needed).
   ```xmsl
   ndk {
       abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
   }
   ```
   - Add the `mavenCentral` library to the `build.gradle` in your project directory.
   ```
   repositories {
       mavenCentral()
   }
   ```

4. Click ![](https://main.qcloudimg.com/raw/d6b018054b535424bb23e42d33744d03.png) **Sync Now** to sync the SDK. If mavenCentral can be connected to, the SDK will be automatically downloaded and integrated into the project very soon.

### Method 2. Manual download (AAR)
1. Download the SDK + Demo development kit for Android [here](https://github.com/tencentyun/SuperPlayer_Android).
2. Import `SDK/LiteAVSDK_Player_XXX.aar` (`XXX` is the version number) into the `libs` folder under `app` and copy the `Demo/superplayerkit` module to the project.
3. Import `superplayerkit` into `setting.gradle` in your project directory.
   ```
   include ':superplayerkit'
   ```
4. Open the `build.gradle` file of the `superplayerkit` project and modify the constant values of `compileSdkVersion`, `buildToolsVersion`, `minSdkVersion`, `targetSdkVersion`, and `rootProject.ext.liteavSdk`.
![](https://main.qcloudimg.com/raw/479cb6ed7a29621998d1ee670e091437.png)
   ```xml
   compileSdkVersion 26
   buildToolsVersion "26.0.2"
   
   defaultConfig {
       targetSdkVersion 23
       minSdkVersion 19
   }
   
   dependencies {
       implementation(name:'LiteAVSDK_Player_8.9.10349', ext:'aar')
   }
   ```
   - Configure `repositories`
   ```xml
   repositories {
       flatDir {
           dirs '../app/libs'
       }
   }
   ```
5. Add dependencies to `app/build.gradle`:
   ```xml
   compile(name:'LiteAVSDK_Player_8.9.10349', ext:'aar')
   implementation project(':superplayerkit')
   // Third-party library for integration of the on-screen commenting feature of superplayer
   implementation 'com.github.ctiao:DanmakuFlameMaster:0.5.3'
   ```
6. Add the following to the project's `build.gradle`:
   ```xml
   allprojects {
       repositories {
           flatDir {
               dirs 'libs'
           }
       }
   }
   ```
7. In the `defaultConfig` of `app/build.gradle`, specify the CPU architecture to be used by the application (currently, LiteAVSDK supports armeabi, armeabi-v7a, and arm64-v8a).
   ```xmsl
   ndk {
       abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
   }
   ```
8. Click **Sync Now** to sync the SDK.

### Method 3. SDK integration (JAR + SO)
If you do not want to integrate the AAR library, you can choose to integrate LiteAVSDK by importing the JAR and SO libraries:
[](id:smallStep_1)
1. Download the SDK + demo development kit for Android [here](https://github.com/tencentyun/SuperPlayer_Android) and decompress it. Find `SDK/LiteAVSDK_Player_XXX.zip` (`XXX` is the version number) in the SDK directory. After decompression, you can get the `libs` directory which contains the JAR files and SO folders as listed below:
   ![](https://qcloudimg.tencent-cloud.cn/raw/9ac0f5b1b9b5d15a005fa2226dd960b6.png)
2. Copy the `Demo/superplayerkit` module to your project and import `superplayerkit` into `setting.gradle` in your project directory.
   ```xml
   include ':superplayerkit'
   ```
3. Copy the `libs` folder obtained by decompression in [step 1](#smallStep_1) to the `superplayerkit` project root directory.
4. Modify the `superplayerkit/build.gradle` file:
![](https://main.qcloudimg.com/raw/ed66e7d887bc5c28c2eff45807037c23.png)
   ```xml
   compileSdkVersion 26
   buildToolsVersion "26.0.2"
   
   defaultConfig {
       targetSdkVersion 23
       minSdkVersion 19
   }
   ```
   - Configure `sourceSets` and add the SO library import code.
   ```xml
   sourceSets{
         main{
             jniLibs.srcDirs = ['libs']
         }
     }
   ```
   - Configure `repositories`, add `flatDir`, and specify the path of the local repository.
   ```xml
   repositories {
       flatDir {
           dirs 'libs'
       }
   }
   ```
5. In the `defaultConfig` of `app/build.gradle`, specify the CPU architecture to be used by the application (currently, LiteAVSDK supports armeabi, armeabi-v7a, and arm64-v8a).
   ```xmsl
   ndk {
       abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
   }
   ```
6. Click **Sync Now** to sync the SDK.

### Configuring app permissions

Configure application permissions in `AndroidManifest.xml`. LiteAVSDK requires the following permissions:

```java
<!--Network permission-->
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<!--VOD player floating window permission -->
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
<!--Storage-->
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```

## Using Playback Features

### Using player[](id:usePlayer)

The main class of the player is `SuperPlayerView`, and videos can be played back after it is created.
```java
// Hotlink protection disabled
SuperPlayerModel model = new SuperPlayerModel();
model.appId = 1400329073;// Configure `AppId`
model.videoId = new SuperPlayerVideoId();
model.videoId.fileId = "5285890799710670616"; // Configure `FileId`
mSuperPlayerView.playWithModel(model);

// To enable hotlink protection, you need to enter the `psign`, which is a signature for superplayer. For more information on the signature and how to generate it, please see https://intl.cloud.tencent.com/document/product/266/38099
SuperPlayerModel model = new SuperPlayerModel();
model.appId = 1400329071;// Configure `AppId`
model.videoId = new SuperPlayerVideoId();
model.videoId.fileId = "5285890799710173650"; // Configure `FileId`
mSuperPlayerView.playWithModel(model);
model.videoId.pSign = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTQwMDMyOTA3MSwiZmlsZUlkIjoiNTI4NTg5MDc5OTcxMDE3MzY1MCIsImN1cnJlbnRUaW1lU3RhbXAiOjEsImV4cGlyZVRpbWVTdGFtcCI6MjE0NzQ4MzY0NywidXJsQWNjZXNzSW5mbyI6eyJ0IjoiN2ZmZmZmZmYifSwiZHJtTGljZW5zZUluZm8iOnsiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3fX0.yJxpnQ2Evp5KZQFfuBBK05BoPpQAzYAWo6liXws-LzU"; 
mSuperPlayerView.playWithModel(model);
```



Run the code and you can see that the video is played back on the phone and most of the features in the UI are available.


### Selecting FileId[](id:FileId)

A video `FileId` is usually returned by the server after the video is uploaded:

1. After the video is published on the client, the server will return a `FileId` to the client.
2. When the video is uploaded to the server, the corresponding `FileId` will be included in the notification of upload confirmation.

If the file already exists in Tencent Cloud, you can go to [Media Assets](https://console.cloud.tencent.com/vod/media), find it.



### Timestamping

When lengthy videos are played back, timestamps on the progress bar can help viewers find the points of interest easily. You can add timestamps by using the `AddKeyFrameDescs.N` parameter in the [ModifyMediaInfo](https://intl.cloud.tencent.com/document/product/266/37570) API.

After the call is made, new elements will be displayed in the player UI.



### Small window playback[](id:smallWindow)
Small window playback can float on top of all activities. It is very simple to implement. You just need to call the following code before playback starts:

```java
// Configure player
SuperPlayerGlobalConfig prefs = SuperPlayerGlobalConfig.getInstance();
// Enable floating window playback
prefs.enableFloatWindow = true;
// Set the initial position, width, and height of the floating window
SuperPlayerGlobalConfig.TXRect rect = new SuperPlayerGlobalConfig.TXRect();
rect.x = 0;
rect.y = 0;
rect.width = 810;
rect.height = 540;
// Other configurations
```

<img src="https://main.qcloudimg.com/raw/2cab897e43e4a01ee5f8e48372ce79a3.jpg" width="350">

### Exiting playback[](id:exitPlayer)

When the player is no longer needed, call `resetPlayer` to clear the internal state of the player and free up the memory.

```java
mSuperPlayerView.resetPlayer();
```

## More Features[](id:moreFeature)

To try out the complete features, scan the QR code below to download the Tencent Video Cloud toolkit or run the project demo directly.
<img src="https://main.qcloudimg.com/raw/6790ddaf4ffe4afd0ceb96b309a16496.png" width="150">
