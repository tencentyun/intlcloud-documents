## Product Overview
The Tencent Cloud RT-Cube Superplayer for Android is an open-source player component of Tencent Cloud. It integrates quality monitoring, video encryption, TESHD, definition switch, and small window playback and is suitable for all VOD and live playback scenarios. It encapsulates complete features and provides upper-layer UIs to help you quickly create a playback program comparable to popular video apps.

If the Superplayer component cannot meet your custom requirements and you have development experience, you can integrate the Player SDK to customize the player UI and playback features.

## Prerequisites
1. To try out complete player features, we recommend you activate [VOD](https://intl.cloud.tencent.com/product/vod). If you haven't registered an account, [sign up](https://intl.cloud.tencent.com/login) first. If you don't use the VOD service, skip this step; however, you can use only basic player features after integration.
2. Download and install [Android Studio](https://developer.android.com/studio). If you have already done so, skip this step.

## Content Summary
1. How to integrate the Tencent Cloud RT-Cube Superplayer for Android
2. How to create and use a player


## Directions
### Step 1. Download the Superplayer code package
The Tencent Cloud RT-Cube Superplayer for Android can be downloaded [here](https://github.com/LiteAVSDK/Player_Android).

You can download the Tencent Cloud RT-Cube Superplayer for Android by **[downloading the player component ZIP package](#zip)** or **[running the Git command](#git)**.
<dx-tabs>
::: Download the ZIP file[](id:zip)
Go to the Superplayer GitHub page and click **Code > Download ZIP**.
![](https://qcloudimg.tencent-cloud.cn/raw/a38a9995bfe13d645bcd1d2e5242a297.png)
:::
::: Download using a Git command[](id:git)
1. First, make sure that your computer has Git installed; if not, you can install it as instructed in [Git Installation Tutorial](https://git-scm.com/downloads).
2. Run the following command to clone the code of the Superplayer component to your local system.
```shell
git clone git@github.com:tencentyun/SuperPlayer_Android.git
```
If you see the following information, the project code has been cloned to your local system successfully.
```shell
Cloning to 'SuperPlayer_Android'...
remote: Enumerating objects: 2637, done.
remote: Counting objects: 100% (644/644), done.
remote: Compressing objects: 100% (333/333), done.
remote: Total 2637 (delta 227), reused 524 (delta 170), pack-reused 1993
Receiving the object: 100% (2637/2637), 571.20 MiB | 3.94 MiB/s, done.
Processing delta: 100% (1019/1019), done.
```
After the project is downloaded, the directory generated after decompression of the source code is as follows:

| Filename                      | Description                                                         |
| --------------------------- | ------------------------------------------------------------ |
| LiteAVDemo(Player)          | Superplayer demo project, which can be run directly after being imported into Android Studio   |
| app                         | Homepage entry                                                   |
| superplayerkit              | Superplayer component (SuperPlayerView), which provides common features such as playback, pause, and gesture control |
| superplayerdemo             | Superplayer demo code                                         |
| common                      | Tool module                                                   |
| SDK                         | RT-Cube player SDK, including `LiteAVSDK_Player_x.x.x.aar` (SDK provided in AAR format) and `LiteAVSDK_Player_x.x.x.zip` (SDKs provided in lib and JAR formats) |
| Player Documentation (Android).pdf | Superplayer user guide                                           |
:::
</dx-tabs>

### Step 2. Integrate the component
This step describes how to integrate the player. You can integrate the project by using Gradle for automatic loading, manually downloading the AAR and importing it into your current project, or importing the JAR and SO libraries.
<dx-tabs>
::: Automatic loading in Gradle (AAR)
1. Download the SDK + demo package for Android [here](https://github.com/LiteAVSDK/Player_Android).
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
       // To integrate an older version, change `latest.release` to the corresponding version number, such as `8.5.290009`
       implementation 'com.tencent.liteav:LiteAVSDK_Player:latest.release'
   }
   ```
   Import the `common` module into your project as instructed above and configure it.
3. Configure the `mavenCentral` library in Gradle, and LiteAVSDK will be automatically downloaded and updated. Open `app/build.gradle` and configure as follows:
   ![](https://main.qcloudimg.com/raw/65439d399ec584871a7a9bc88ccaef46.png)
   
   1. Add the `LiteAVSDK_Player` dependencies to `dependencies`.
```xml
dependencies {
	 implementation 'com.tencent.liteav:LiteAVSDK_Player:latest.release'
	 implementation project(':superplayerkit')
	 // Third-party library for integration of the on-screen commenting feature of Super Player
	 implementation 'com.github.ctiao:DanmakuFlameMaster:0.5.3'
}
```
   If you need to integrate an older version of the LiteAVSDK_Player SDK, view it in [MavenCentral](https://repo1.maven.org/maven2/com/tencent/liteav/LiteAVSDK_Player/) and then integrate it as instructed below: 
```xml
dependencies {
	 // Integrate the LiteAVSDK_Player SDK v8.5.10033
	 implementation 'com.tencent.liteav:LiteAVSDK_Player:8.5.10033'
}
```
   2. In the `defaultConfig` of `app/build.gradle`, specify the CPU architecture to be used by the application (currently, LiteAVSDK supports armeabi, armeabi-v7a, and arm64-v8a, which you can configure as needed).
```xmsl
ndk {
	 abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
}
```
   If you haven't used the download cache feature (an API in `TXVodDownloadManager`) of the SDK v9.4 or earlier and don't need to play back the downloaded files in the SDK v9.5 or later, you don't need to use the SO file of the feature, which helps reduce the size of the installation package. For example, if you have downloaded a cached file by using the `setDownloadPath` and `startDownloadUrl` functions of the `TXVodDownloadManager` class in the SDK v9.4 or earlier, and the `getPlayPath` path called back by `TXVodDownloadManager` is stored in the app for subsequent playback, you will need `libijkhlscache-master.so` to play back the file at the `getPlayPath` path; otherwise, you won't need it. You can add the following to `app/build.gradle`:
```xml
packagingOptions{
	exclude "lib/armeabi/libijkhlscache-master.so"
	exclude "lib/armeabi-v7a/libijkhlscache-master.so"
	exclude "lib/arm64-v8a/libijkhlscache-master.so"
}
```
   3. Add the `mavenCentral` library to the `build.gradle` in your project directory.
 ```
 repositories {
		 mavenCentral()
 }
 ```
4. Click ![](https://main.qcloudimg.com/raw/d6b018054b535424bb23e42d33744d03.png) **Sync Now** to sync the SDK. If mavenCentral can be connected to, the SDK will be automatically downloaded and integrated into the project very soon.
:::
::: Manual download in Gradle (AAR)
1. Download the SDK + demo package for Android [here](https://github.com/LiteAVSDK/Player_Android).
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
Import the `common` module into your project as instructed above and configure it.
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
// Third-party library for integration of the on-screen commenting feature of Super Player
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
If you haven't used the download cache feature (an API in `TXVodDownloadManager`) of the SDK v9.4 or earlier and don't need to play back the downloaded files in the SDK v9.5 or later, you don't need to use the SO file of the feature, which helps reduce the size of the installation package. For example, if you have downloaded a cached file by using the `setDownloadPath` and `startDownloadUrl` functions of the `TXVodDownloadManager` class in the SDK v9.4 or earlier, and the `getPlayPath` path called back by `TXVodDownloadManager` is stored in the app for subsequent playback, you will need `libijkhlscache-master.so` to play back the file at the `getPlayPath` path; otherwise, you won't need it. You can add the following to `app/build.gradle`:
```xml
packagingOptions{
	exclude "lib/armeabi/libijkhlscache-master.so"
	exclude "lib/armeabi-v7a/libijkhlscache-master.so"
	exclude "lib/arm64-v8a/libijkhlscache-master.so"
}
```
8. Click **Sync Now** to sync the SDK.
:::
::: SDK integration (jar + so)
If you do not want to import the AAR library, you can also integrate LiteAVSDK by importing JAR and SO libraries.
[](id:smallStep_1)
1. Download the SDK + demo development kit for Android [here](https://github.com/LiteAVSDK/Player_Android) and decompress it. Find `SDK/LiteAVSDK_Player_XXX.zip` (`XXX` is the version number) in the SDK directory. After decompression, you can get the `libs` directory which contains the JAR files and SO folders as listed below:
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
Import the `common` module into your project as instructed above and configure it.
   - Configure `sourceSets` and add the SO library import code.
```xml
sourceSets{
		 main{
				 jniLibs.srcDirs = ['libs']
		 }
 }
```
   - Configure `repositories`, add `flatDir`, and specify the paths of the local repositories.
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
:::
</dx-tabs>
At this point, you have completed integrating the Tencent Cloud RT-Cube Superplayer for Android.


### Step 3. Configure application permissions
Configure permissions for your application in `AndroidManifest.xml`. LiteAVSDK needs the following permissions:

```java
<!--network permission-->
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<!--VOD player floating window permission -->
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
<!--storage-->
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```

### Step 4. Set obfuscation rules
In the `proguard-rules.pro` file, add the classes related to the TRTC SDK to the "do not obfuscate" list:
```xml
-keep class com.tencent.** { *;}
```
At this point, you have completed configuring permissions for the Tencent Cloud RT-Cube Superplayer application for Android.

### Step 5. Use the player features
This step describes how to create a player and use it for video playback.

1. **SDK connection environment configuration**

In order to help you conduct business with higher quality and security in compliance with applicable laws and regulations in different countries and regions, Tencent Cloud provides two SDK connection environments. If you serve global users, we recommend you use the following API to configure the global connection environment.

```java
// If you serve global users, configure the global SDK connection environment.
TXLiveBase.setGlobalEnv("GDPR");
```

2. **Player creation**[](id:usePlayer)
   The main class of the player is `SuperPlayerView`, and videos can be played back after it is created. `FileId` or URL can be integrated for playback. Create `SuperPlayerView` in the layout file:

```xml
<!--Superplayer-->
<com.tencent.liteav.demo.superplayer.SuperPlayerView
    android:id="@+id/superVodPlayerView"
    android:layout_width="match_parent"
    android:layout_height="200dp" />
```
3. **Video playback**[](id:playe)
   This step describes how to play back a video. The Tencent Cloud RT-Cube Superplayer for Android can be used for VOD and live playback as follows:

- VOD playback: The superplayer supports two VOD playback methods, namely, through [`FileId`](#fileid) or [URL](#url).
- Live playback: The superplayer can use the [playback through URL](#url) method for live playback. A live audio/video stream can be pulled for playback simply by passing in its URL. For more information on how to generate a Tencent Cloud live streaming URL, see [Splicing Live Streaming URL](https://intl.cloud.tencent.com/document/product/267/38393).
<dx-tabs>
::: VOD and live playback through URL[](id:url)
A URL can be the playback address of a VOD file or the pull address of a live stream. A video file can be played back simply by passing in its URL.

```java
SuperPlayerModel model = new SuperPlayerModel();
model.appId = 1400329073; // Configure `AppId`
model.url = "http://your_video_url.mp4";   // Configure a URL for your video for playback
mSuperPlayerView.playWithModel(model);
```
:::
::: VOD playback through `FileId`[](id:fileid)
A video file ID is returned by the server after the video is uploaded.
1. After a video is published from a client, the server will return a file ID to the client.
2. When the video is uploaded to the server, the corresponding `FileId` will be included in the notification of upload confirmation.

If the video you want to play is already saved with VOD, you can go to [Media Assets](https://console.cloud.tencent.com/vod/media) to view its file ID.
![](https://qcloudimg.tencent-cloud.cn/raw/f089346e01ab8e44e42f28c965809b9c.png)
<dx-alert infotype="notice">
<li>For playback through `FileId`, you need to first use the Adaptive-HLS(10) transcoding template to transcode the video or use the Superplayer signature `psign` to specify the video to be played back; otherwise, the video may fail to be played back. For more information on how to transcode a video, see [Playing back Video Through Superplayer](https://intl.cloud.tencent.com/document/product/266/38098). For more information on how to generate a `psign`, see [Superplayer Signature](https://intl.cloud.tencent.com/document/product/266/38099).</li>
<li>If a "no v4 play info" exception occurs during playback through `FileId`, the above problem may exist. In this case, we recommend you make adjustments as instructed above. You can also directly get the playback link of the source video for playback through [URL](#url).</li>
<li> **We recommend you transcode videos for playback because untranscoded videos may experience compatibility issues during playback.**</li></dx-alert>

<dx-codeblock>
:::  java
// If you haven’t enabled hotlink protection and a "no v4 play info" error occurs, please transcode your video using the Adaptive-HLS template (ID: 10) or get the playback URL of the video and play it by URL.

SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
model.appId = 1400329071;// Configure AppId
model.videoId = [[SuperPlayerVideoId alloc] init];
model.videoId.fileId = @"5285890799710173650"; // Configure `FileId`
// If you enable hotlink protection, you need to enter a `psign` (Superplayer signature) for playback. For more information on the signature and how to generate it, see https://intl.cloud.tencent.com/document/product/266/38099
//model.videoId.pSign = @"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTQwMDMyOTA3MSwiZmlsZUlkIjoiNTI4NTg5MDc5OTcxMDE3MzY1MCIsImN1cnJlbnRUaW1lU3RhbXAiOjEsImV4cGlyZVRpbWVTdGFtcCI6MjE0NzQ4MzY0NywidXJsQWNjZXNzSW5mbyI6eyJ0IjoiN2ZmZmZmZmYifSwiZHJtTGljZW5zZUluZm8iOnsiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3fX0.yJxpnQ2Evp5KZQFfuBBK05BoPpQAzYAWo6liXws-LzU"; 
[_playerView playWithModel:model];
:::
</dx-codeblock>
:::
</dx-tabs>
4. **Playback exit**[](id:exitPlayer)
   If the player is no longer needed, call `resetPlayer` to reset the player and free up memory.

```java
mSuperPlayerView.resetPlayer();
```

At this point, you have integrated the player creation, video playback, and playback exiting capabilities of the Tencent Cloud RT-Cube Superplayer for Android.


[](id:moreFeature)
## More Features[](id:moreFeature)

This section describes several common player features. For more features, see [Demo](#demo).

### 1. Full screen playback

The superplayer supports full screen playback, where it allows setting screen lock, volume and brightness control through gesture, on-screen commenting, screencapturing, and definition switch. This feature can be tried out in **[Tencent Cloud RT-Cube App](#qrcode) > Player > Superplayer**, and you can enter the full screen playback mode by tapping the full screen icon.

You can call the API below to go full screen from the windowed playback mode:

```java
mControllerCallback.onSwitchPlayMode(SuperPlayerDef.PlayerMode.FULLSCREEN);
```


<dx-tabs>
::: Return to the window
Tap **Back** to return to the window playback mode.

```java
// API triggered after tapping
mControllerCallback.onBackPressed(SuperPlayerDef.PlayerMode.FULLSCREEN);
onSwitchPlayMode(SuperPlayerDef.PlayerMode.WINDOW);
```
:::
::: Screen lock[](id:lockscreen)
The screen lock operation enables the immersive playback status.
```java
// API triggered after tapping
toggleLockState();
```
:::
::: On-screen comment[](id:barrage)
After the on-screen commenting feature is enabled, text comments sent by users will be displayed on the screen.
```java
// Step 1. Add an on-screen comment to the on-screen comment view
addDanmaku(String content, boolean withBorder);
// Step 2. Enable or disable on-screen commenting
toggleBarrage();
```
:::
::: Screenshot[](id:screenshot)
The superplayer provides the feature of capturing the current video frame during playback, and you can save the screenshot for sharing. Tap the button in image 4 to capture the screen, and you can save the captured screenshot in the `mSuperPlayer.snapshot` API.
```java
mSuperPlayer.snapshot(new TXLivePlayer.ITXSnapshotListener() {
  @Override
  public void onSnapshot(Bitmap bitmap) {
        // The captured screenshot can be saved here
  }
});
```
:::
::: Change resolution[](id:resolution)
Different video playback definitions can be selected as needed, such as HD, SD, and FHD.
```java
// The API for displaying the definition view triggered after tapping
showQualityView();
// The callback API for tapping the definition option is as follows
mListView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
  @Override
  public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
    // The event of tapping the definition list view
    VideoQuality quality = mList.get(position);
    mCallback.onQualitySelect(quality);
  }
});
// Callback for the eventually selected definition
@Override
public void onQualityChange(VideoQuality quality) {
   mFullScreenPlayer.updateVideoQuality(quality);
   mSuperPlayer.switchStream(quality);
}
```
:::
</dx-tabs>


### 2. Floating window playback
The superplayer supports playback in a small floating window, which allows users to switch to another app without interrupting the video playback. This feature can be tried out in [**Tencent Cloud RT-Cube App**](#qrcode) > **Player** > **Superplayer** by tapping **Back** in the top-left corner.
<img src="https://qcloudimg.tencent-cloud.cn/raw/e8a774cb9833f2de45fc1cf3cc928ee4.png" style="zoom:35%;" />
Floating window playback relies on the following permission in `AndroidManifest`:
```java
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
```
```java
// The API triggered by switching to the floating window
mSuperPlayerView.switchPlayMode(SuperPlayerDef.PlayerMode.FLOAT);
// The API triggered by tapping the floating window to return to the main window
mControllerCallback.onSwitchPlayMode(SuperPlayerDef.PlayerMode.WINDOW);
```

### 3. Thumbnail

The superplayer supports customizing a video thumbnail for display before the callback for playing back the first video frame is received. This feature can be tried out in [**Tencent Cloud RT-Cube App**](#qrcode) > **Player** > **Superplayer** > **Thumbnail Customization Demo**.



* When the superplayer is set to the automatic playback mode `PLAY_ACTION_AUTO_PLAY`, the video will be played back automatically, and the thumbnail will be displayed before the first video frame is loaded.
* When Superplayer is set to the manual playback mode `PLAY_ACTION_MANUAL_PLAY`, videos are played only after users tap the play button, and the thumbnail will be displayed until the first video frame is loaded.

You can set the thumbnail by specifying the URL of a local or online file. For detailed directions, see the code below. If you play by VOD file ID, you can also set the thumbnail in the VOD console.

```java
SuperPlayerModel model = new SuperPlayerModel();
model.appId = "Your `appid`";
model.videoId = new SuperPlayerVideoId();
model.videoId.fileId = "Your `fileId`"; 
// Playback mode, which can be set to automatic (`PLAY_ACTION_AUTO_PLAY`) or manual (`PLAY_ACTION_MANUAL_PLAY`)
model.playAction = PLAY_ACTION_MANUAL_PLAY;
// Specify the URL of an online file to use as the thumbnail. If `coverPictureUrl` is not set, the thumbnail configured in the VOD console will be used.
model.coverPictureUrl = "http://1500005830.vod2.myqcloud.com/6c9a5118vodcq1500005830/cc1e28208602268011087336518/MXUW1a5I9TsA.png" 
mSuperPlayerView.playWithModel(model);
```

### 4. Video playlist loop

Superplayer supports looping video playlists.

* After a video ends, the next video in the list can be played automatically or users can manually start the next video.
* After the last video in the list ends, the first video in the list will start automatically.

This feature can be tried out in [**Tencent Cloud RT-Cube App**](#qrcode) > **Player** > **Superplayer** > **Video List Loop Demo**.



```java
// Step 1. Create a loop list<SuperPlayerModel>
ArrayList<SuperPlayerModel> list = new ArrayList<>();
SuperPlayerModel model = new VideoModel();
model = new SuperPlayerModel();
model.videoId = new SuperPlayerVideoId();
model.appid = 1252463788;
model.videoId.fileId = "4564972819219071568";
list.add(model);

model = new SuperPlayerModel();
model.videoId = new SuperPlayerVideoId();
model.appid = 1252463788;
model.videoId.fileId = "4564972819219071679";
list.add(model);
// Step 2. Call the loop API
mSuperPlayerView.playWithModelList(list, true, 0);
```

```java
public void playWithModelList(List<SuperPlayerModel> models, boolean isLoopPlayList, int index);
```

API parameters:

| Parameter | Type | Description |
| -------------- | ---------------------- | ------------------------------ |
| models         | List<SuperPlayerModel> | Loop data list                   |
| isLoopPlayList | boolean                | Whether to loop                       |
| index          | int                    | Index of `SuperPlayerModel` from which to start the playback |

### 5. Preview

The superplayer supports the video preview feature, which is suitable for non-VIP member preview. You can pass in different parameters to control the video preview duration, prompt message, and preview end screen. This feature can be tried out in [**Tencent Cloud RT-Cube App**](#qrcode) > **Player** > **Superplayer** > **Preview Feature Demo**.



```java
 Method 1:
 // Step 1. Create a video model
 SuperPlayerModel mode = new SuperPlayerModel();
 //... Add the video source information
 // Step 2. Create a preview information model
 VipWatchModel vipWatchModel = new VipWatchModel("You can preview %ss and activate the VIP membership to watch the full video",15);
 mode.vipWatchMode = vipWatchModel;
 // Step 3. Call the method for playing back videos
 mSuperPlayerView.playWithModel(mode);

 Method 2:
 // Step 1. Create a preview information model
 VipWatchModel vipWatchModel = new VipWatchModel("You can preview %ss and activate the VIP membership to watch the full video",15);
  // Step 2. Call the method for setting the preview feature
 mSuperPlayerView.setVipWatchModel(vipWatchModel);
```

```java
public VipWatchModel(String tipStr, long canWatchTime)
```

`VipWatchModel` API parameter description:

| Parameter | Type | Description |
| ------------ | ------ | --------- |
| tipStr       | String | Preview prompt message    |
| canWatchTime | Long   | Preview duration in seconds |

### 6. Dynamic watermark

The superplayer allows you to add an irregular moving text watermark on the playback screen to prevent unauthorized recording. Watermarks can be displayed both in full screen playback mode and window playback mode. You can modify the watermark text, size, and color. This feature can be tried out in [**Tencent Cloud RT-Cube App**](#qrcode) > **Player** > **Superplayer** > **Dynamic Watermark Demo**.



```java
 Method 1:
 // Step 1. Create a video model
 SuperPlayerModel mode = new SuperPlayerModel();
 //... Add the video source information
 // Step 2. Create a watermark information model
 DynamicWaterConfig dynamicWaterConfig = new DynamicWaterConfig("shipinyun", 30, Color.parseColor("#80FFFFFF"));
 mode.dynamicWaterConfig = dynamicWaterConfig;
 // Step 3. Call the method for playing back videos
 mSuperPlayerView.playWithModel(mode);

 Method 2:
 // Step 1. Create a watermark information model
 DynamicWaterConfig dynamicWaterConfig = new DynamicWaterConfig("shipinyun", 30, Color.parseColor("#80FFFFFF"));
  // Step 2. Call the method for setting the dynamic watermark feature
 mSuperPlayerView.setDynamicWatermarkConfig(dynamicWaterConfig);
```

```java
public DynamicWaterConfig(String dynamicWatermarkTip, int tipTextSize, int tipTextColor)
```

API parameters:

| Parameter | Type | Description |
| ------------------- | ------ | ------ |
| dynamicWatermarkTip | String | Watermark text information |
| tipTextSize         | int    | Text size   |
| tipTextColor        | int    | Text color   |

[](id:demo)
## Demo

To try out more features, you can directly run the project demo or scan the QR code to download the Tencent Cloud RT-Cube app demo.

### Run a demo project

1. Select **File** > **Open** on the navigation bar of Android Studio. In the pop-up window, select the `$SuperPlayer_Android/Demo` directory of the **demo** project. After the demo project is imported successfully, click **Run app** to run the demo.
2. After running the demo successfully as shown below, go to **Player** > **Superplayer** to try out the player features.

[](id:qrcode)
### TCToolkit app
You can also try Superplayer on the **Player** page of the TCToolkit app.
<img src="https://main.qcloudimg.com/raw/6790ddaf4ffe4afd0ceb96b309a16496.png" width="150">
