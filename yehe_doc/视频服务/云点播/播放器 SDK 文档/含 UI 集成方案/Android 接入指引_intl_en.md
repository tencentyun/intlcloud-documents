## Overview
The Tencent Cloud RT-Cube Player for Android is an open-source player component of Tencent Cloud. It integrates quality monitoring, video encryption, Top Speed Codec, definition selection, and small window playback and is suitable for all VOD and live playback scenarios. It encapsulates complete features and provides upper-layer UIs to help you quickly create a playback program comparable to mainstream video applications.

If the Player component cannot meet your requirements, and you have some knowledge of engineering, you can integrate the Player SDK to customize the UI and playback features.



## Limits
1. To try out all features of the player, we recommend you activate [VOD](https://intl.cloud.tencent.com/product/vod). If you don't have an account yet, [sign up](https://intl.cloud.tencent.com/login) for one first. If you don't use the VOD service, you can skip this step; however, you will only be able to use basic player features after integration.
2. Download and install [Android Studio](https://developer.android.com/studio). If you have already done so, skip this step.

## This Document Describes
1. How to integrate the Player component for Android
2. How to create and use the player


## Prerequisites
### Step 1. Download the player code package
GitHub page: [LiteAVSDK/Player_Android](https://github.com/LiteAVSDK/Player_Android)

You can download the Player for Android by **[downloading the Player component ZIP package](#zip)** or **[running the Git clone command](#git)**.
<dx-tabs>
::: Download the ZIP file[](id:zip)
Go to the Player GitHub page and click **Code > Download ZIP**.
![](https://qcloudimg.tencent-cloud.cn/raw/a38a9995bfe13d645bcd1d2e5242a297.png)
:::
::: Download using Git command[](id:git)
1. First, make sure that your computer has Git installed; if not, you can install it as instructed in [Git Installation Tutorial](https://git-scm.com/downloads).
2. Run the following command to clone the code of the Player component to your local system.
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
| LiteAVDemo(Player)          | The Player demo project, which can be run directly after being imported into Android Studio.   |
| app                         | Homepage entry                                                   |
| superplayerkit              | The Player component (SuperPlayerView), which provides common features such as playback, pause, and gesture control. |
| superplayerdemo             | The Player component demo code                                         |
| common                      | Tool module                                                   |
| SDK                         | Player SDK, including `LiteAVSDK_Player_x.x.x.aar` (SDK provided in AAR format) and `LiteAVSDK_Player_x.x.x.zip` (SDKs provided in lib and JAR formats) |
| Player Documentation (Android).pdf | The Player component user guide                                           |
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
       // To integrate an older version, change `latest.release` to the corresponding version number, such as `10.8.0.29000`
       implementation 'com.tencent.liteav:LiteAVSDK_Player_Premium:latest.release'
   }
   ```
   Import the `common` module into your project as instructed above and configure it.
3. Configure the `mavenCentral` library in Gradle, and LiteAVSDK will be automatically downloaded and updated. Open `app/build.gradle` and configure as follows:
   ![](http://1500005830.vod2.myqcloud.com/6c9a5118vodcq1500005830/ed597d17243791576461148950/WWCM0KnCcEQA.png)
   
   1. Add the `LiteAVSDK_Player_Premium` dependencies to `dependencies`.
```xml
dependencies {
	 implementation 'com.tencent.liteav:LiteAVSDK_Player_Premium:latest.release'
	 implementation project(':superplayerkit')
	 // Third-party library for integration of the on-screen commenting feature of the Player component
	 implementation 'com.github.ctiao:DanmakuFlameMaster:0.5.3'
}
```
   If you need to integrate an older version of the LiteAVSDK_Player_Premium SDK, view it in [MavenCentral](https://repo1.maven.org/maven2/com/tencent/liteav/LiteAVSDK_Player_Premium/) and then integrate it as instructed below: 
```xml
dependencies {
	 // Integrate the LiteAVSDK_Player_Premium SDK v10.8.0.29000
	 implementation 'com.tencent.liteav:LiteAVSDK_Player_Premium:10.8.0.29000'
}
```
   2. In the `defaultConfig` of `app/build.gradle`, specify the CPU architecture to be used by the application (currently, LiteAVSDK supports armeabi, armeabi-v7a, and arm64-v8a, which you can configure as needed).
```xmsl
ndk {
	 abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
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
2. Import `SDK/LiteAVSDK_Player_Premium_XXX.aar` (`XXX` is the version number) into the `libs` folder under `app` and copy the `Demo/superplayerkit` module to the project.
3. Import `superplayerkit` into `setting.gradle` in your project directory.
```
include ':superplayerkit'
```
4. Open the `build.gradle` file of the `superplayerkit` project and modify the constant values of `compileSdkVersion`, `buildToolsVersion`, `minSdkVersion`, `targetSdkVersion`, and `rootProject.ext.liteavSdk`.
![](http://1500005830.vod2.myqcloud.com/6c9a5118vodcq1500005830/93519621243791576463697337/xuE8HZ2LdSIA.png)
```xml
compileSdkVersion 26
buildToolsVersion "26.0.2"

defaultConfig {
	 targetSdkVersion 23
	 minSdkVersion 19
}

dependencies {
	 implementation(name:'LiteAVSDK_Player_Premium_10.8.0.29000', ext:'aar')
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
compile(name:'LiteAVSDK_Player_Premium_10.8.0.29000', ext:'aar')
implementation project(':superplayerkit')
// Third-party library for integration of the on-screen commenting feature of the Player component
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
7. In `defaultConfig` of `app/build.gradle`, specify the CPU architecture to be used by the application (currently, LiteAVSDK supports armeabi, armeabi-v7a, and arm64-v8a).
```xmsl
ndk {
	 abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
}
```
8. Click **Sync Now** to sync the SDK.
:::
::: SDK integration (jar + so)
If you do not want to import the AAR library, you can also integrate LiteAVSDK by importing JAR and SO libraries.
[](id:smallStep_1)
1. Download the SDK + demo package for Android [here](https://github.com/LiteAVSDK/Player_Android) and decompress it. Find `SDK/LiteAVSDK_Player_Premium_XXX.zip` (`XXX` is the version number) in the SDK directory. After decompression, you can get the `libs` directory, which contains the JAR file and folders of SO files as listed below:
 ![](https://qcloudimg.tencent-cloud.cn/raw/ab928524839c7944f78d504c0e637586.png)
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
5. In `defaultConfig` of `app/build.gradle`, specify the CPU architecture to be used by the application (currently, LiteAVSDK supports armeabi, armeabi-v7a, and arm64-v8a).
```xmsl
ndk {
	 abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
}
```
6. Click **Sync Now** to sync the SDK.
:::
</dx-tabs>
At this point, you have completed integrating the RT-Cube Player for Android.

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
At this point, you have completed configuring permissions for the RT-Cube Player application for Android.

### Step 5. Use the player features
This step describes how to create a player and use it for video playback.
1. **Player creation**[](id:usePlayer)
The main class of the player is `SuperPlayerView`, and videos can be played back after it is created. `FileId` or URL can be integrated for playback. Create `SuperPlayerView` in the layout file:
```xml
<!-- Player component -->
<com.tencent.liteav.demo.superplayer.SuperPlayerView
    android:id="@+id/superVodPlayerView"
    android:layout_width="match_parent"
    android:layout_height="200dp" />
```
2. **License configuration**
If you have obtained a license, you can view the license URL and key in the [RT-Cube console](https://console.cloud.tencent.com/vcube).

If you don't have the required license yet, you can get it as instructed in <a href="https://cloud.tencent.com/document/product/881/74588">Video Playback License</a>.<br>
After obtaining the license information, before calling relevant APIs of the SDK, initialize the license through the following API. We recommend you set the following in the `Application` class:
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

3. **Video playback**[](id:playe)
This step describes how to play back a video. The RT-Cube Player for Android can be used for VOD and live playback as follows:
	- VOD playback: The Player component supports two VOD playback methods, namely, through [`FileId`](#fileid) or [URL](#url).
	- Live playback: The Player component can use the [playback through URL](#url) method for live playback. A live audio/video stream can be pulled for playback simply by passing in its URL. For more information on how to generate a Tencent Cloud live streaming URL, see [Splicing Live Streaming URLs](https://intl.cloud.tencent.com/document/product/267/38393).

<dx-tabs>
::: VOD and live playback through URL[](id:url)
A URL can be the playback address of a VOD file or the pull address of a live stream. A video file can be played back simply by passing in its URL.
```java
SuperPlayerModel model = new SuperPlayerModel();
model.appId = 1400329073; // Configure `AppId`
model.url = "http://your_video_url.mp4";   // Configure a URL for your video for playback
mSuperPlayerView.playWithModelNeedLicence(model);
```
:::
::: VOD playback through `FileId`[](id:fileid)
A video file ID is returned by the server after the video is uploaded.
1. After a video is published from a client, the server will return a file ID to the client.
2. After a video is uploaded to the server, the notification for successful upload will contain a file ID for the video.

If the video you want to play is already saved with VOD, you can go to [Media Assets](https://console.cloud.tencent.com/vod/media) to view its file ID.
![](https://qcloudimg.tencent-cloud.cn/raw/f089346e01ab8e44e42f28c965809b9c.png)
>!
>- To play by VOD file ID, you need to use the Adaptive-HLS template (ID: 10) to transcode the video or use the player signature `psign` to specify the video to play; otherwise, the playback may fail. For more information on how to transcode a video and generate `psign`, see [Play back a video with the Player component](https://intl.cloud.tencent.com/document/product/266/38098) and [Player Signature](https://intl.cloud.tencent.com/document/product/266/38099).
>- If a "no v4 play info" exception occurs during playback through `FileId`, the above problem may exist. In this case, we recommend you make adjustments as instructed above. You can also directly get the playback link of the source video for playback through [URL](#url).
>- **We recommend you transcode videos for playback because untranscoded videos may experience compatibility issues during playback.**

<dx-codeblock>
:::  java
// If you haven't enabled hotlink protection and a "no v4 play info" error occurs, transcode your video by using the Adaptive-HLS template (ID: 10) or get the playback URL of the video and play it by URL.

```java
SuperPlayerModel model = new SuperPlayerModel();
model.appId = 1400329071;// Configure AppId
model.videoId = new SuperPlayerVideoId();
model.videoId.fileId = "5285890799710173650"; // Configure `FileId`
// `psign` is a player signature. For more information on the signature and how to generate it, see [Player Signature](https://intl.cloud.tencent.com/document/product/266/38099).
model.videoId.pSign = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTQwMDMyOTA3MSwiZmlsZUlkIjoiNTI4NTg5MDc5OTcxMDE3MzY1MCIsImN1cnJlbnRUaW1lU3RhbXAiOjEsImV4cGlyZVRpbWVTdGFtcCI6MjE0NzQ4MzY0NywidXJsQWNjZXNzSW5mbyI6eyJ0IjoiN2ZmZmZmZmYifSwiZHJtTGljZW5zZUluZm8iOnsiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3fX0.yJxpnQ2Evp5KZQFfuBBK05BoPpQAzYAWo6liXws-LzU";
mSuperPlayerView.playWithModelNeedLicence(model);
```

:::
</dx-codeblock>
:::
</dx-tabs>

3. **Playback exit**[](id:exitPlayer)
If the player is no longer needed, call `resetPlayer` to reset the player and free up memory.
```java
mSuperPlayerView.resetPlayer();
```

At this point, you have learned how to create a player, use it to play videos, and stop playback.

## More Features[](id:moreFeature)

This section describes several common player features. For more features, see [Demo](#demo). For features supported by the Player component, see [Features](https://cloud.tencent.com/document/product/881/61375).

### 1. Full screen playback

The Player component supports full screen playback. In full screen mode, users can lock the screen, control volume and brightness with gestures, send on-screen comments, take screenshots, and switch the video definition. You can try out this feature in [**TCToolkit App**](#qrcode) > **Player** > **Player Component**, and you can enter the full screen playback mode by clicking the full screen icon in the bottom-right corner.

You can call the API below to enter full screen from the windowed playback mode:

```java
mControllerCallback.onSwitchPlayMode(SuperPlayerDef.PlayerMode.FULLSCREEN);
```

#### Features of full screen playback mode

<dx-tabs>
::: Return to the window
Click **Back** to return to the window playback mode.

```java
// API triggered after tapping
mControllerCallback.onBackPressed(SuperPlayerDef.PlayerMode.FULLSCREEN);
onSwitchPlayMode(SuperPlayerDef.PlayerMode.WINDOW);
```
:::
::: Screen lock[](id:lockscreen)
Screen locking disables touch screen and allows users to enter an immersive playback mode.
```java
// API triggered after tapping
toggleLockState();
```
:::
::: On-screen comments[](id:barrage)
After the on-screen commenting feature is enabled, text comments sent by users will be displayed on the screen.
```java
// Step 1. Add an on-screen comment to the on-screen comment view
addDanmaku(String content, boolean withBorder);
// Step 2. Enable or disable on-screen commenting
toggleBarrage();
```
:::
::: Screenshot[](id:screenshot)
The Player component allows users to take and save a screenshot of a video during playback. Click the button in image 4 to capture the screen, and you can save the captured screenshot with the `mSuperPlayer.snapshot` API.
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
Users can change the video definition (such as SD, HD, and FHD) during playback.
```java
// The API for displaying the definition selection view triggered after the button is tapped
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
// Callback for the selected definition
@Override
public void onQualityChange(VideoQuality quality) {
   mFullScreenPlayer.updateVideoQuality(quality);
   mSuperPlayer.switchStream(quality);
}
```
:::
</dx-tabs>


### 2. Floating window playback
The Player component supports playback in a small floating window, which allows users to switch to another application without interrupting the video playback. You can try out this feature in [**TCToolkit App**](#qrcode) > **Player** > **Player Component** by clicking **Back** in the top-left corner.
<img src="https://qcloudimg.tencent-cloud.cn/raw/e8a774cb9833f2de45fc1cf3cc928ee4.png" alt="img" style="zoom:25%;" />
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

The Player component supports customizing a video thumbnail, which is displayed before the callback is received for playing back the first video frame. You can try out this feature in [**TCToolkit App**](#qrcode) > **Player** > **Player Component** > **Thumbnail Customization Demo**.


* When the Player component is set to the automatic playback mode `PLAY_ACTION_AUTO_PLAY`, the thumbnail will be displayed before the first video frame is loaded.
* When the Player component is set to the manual playback mode `PLAY_ACTION_MANUAL_PLAY`, videos are played only after users tap the play button, and the thumbnail will be displayed until the first video frame is loaded.

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
mSuperPlayerView.playWithModelNeedLicence(model);
```

### 4. Video playlist loop

The Player component supports looping video playlists.

* After a video ends, the next video in the list can be played automatically or users can manually start the next video.
* After the last video in the list ends, the first video in the list will start automatically.

This feature can be tried out in [**TCToolkit App**](#qrcode) > **Player** > **Player Component** > **Video List Loop Demo**.



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
mSuperPlayerView.playWithModelListNeedLicence(list, true, 0);
```

```java
public void playWithModelListNeedLicence(List<SuperPlayerModel> models, boolean isLoopPlayList, int index);
```

API parameters:

| Parameter | Type | Description |
| -------------- | ---------------------- | ------------------------------ |
| models         | List<SuperPlayerModel> | Loop data list                   |
| isLoopPlayList | boolean                | Whether to loop video playback                      |
| index          | int                    | Index of `SuperPlayerModel` from which to start the playback |

### 5. Preview

The Player component supports the video preview feature, which allows non-member viewers to view a preview of the video. You can pass in different parameters to control the video preview duration, prompt message, and preview end screen. You can try out this feature in [**Tencent Cloud Toolkit App**](#qrcode) > **Player** > **Player Component** > **Preview Feature Demo**.



```java
 Method 1:
 // Step 1. Create a video model
 SuperPlayerModel mode = new SuperPlayerModel();
 //... Add the video source information
 // Step 2. Create a preview information model
 VipWatchModel vipWatchModel = new VipWatchModel("You can preview %ss and activate the VIP membership to watch the full video",15);
 mode.vipWatchMode = vipWatchModel;
 // Step 3. Call the method for playing back videos
 mSuperPlayerView.playWithModelNeedLicence(mode);

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

The Player component allows you to add a randomly moving text watermark to protect your content against piracy. Watermarks are visible in both the full screen mode and windowed mode. The text, font size, and color of a watermark are customizable. You can find a demo for this feature in the [TCToolkit app](#qrcode): **Player** > **Player Component** > **Dynamic Watermark Demo**.



```java
 Method 1:
 // Step 1. Create a video model
 SuperPlayerModel mode = new SuperPlayerModel();
 //... Add the video source information
 // Step 2. Create a watermark information model
 DynamicWaterConfig dynamicWaterConfig = new DynamicWaterConfig("shipinyun", 30, Color.parseColor("#80FFFFFF"));
 mode.dynamicWaterConfig = dynamicWaterConfig;
 // Step 3. Call the method for playing back videos
 mSuperPlayerView.playWithModelNeedLicence(mode);

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

### 7. Video download

Video download allows users to cache online videos and watch them offline. The cached video can be played back only in the client but cannot be actually downloaded to the device. This feature can effectively prevent downloaded videos from being distributed without authorization and protect the video security.
You can try out this feature in full screen mode in TCToolkit App > Player > Player Components > Offline Cache.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/rUaM578_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_1669772078943.png)

`DownloadMenuListView` (cache selection list view) is used to select and download videos at different definitions. After selecting the definition in the top-left corner, click the option of the video to be downloaded. When a check mark appears, the download has started. After clicking the **video download list** button below, you will be redirected to the Activity where `VideoDownloadListView` is located.

```java
// Step 1. Initialize the download data with the following parameters
DownloadMenuListView mDownloadMenuView = findViewById(R.id.superplayer_cml_cache_menu);
mDownloadMenuView.initDownloadData(superPlayerModelList, mVideoQualityList, mDefaultVideoQuality, "default");
 
// Step 2. Set the options of the video being played back
mDownloadMenuView.setCurrentPlayVideo(mSuperplayerModel);

// Step 3. Set the click event of the **video download list** button
mDownloadMenuView.setOnCacheListClick(new OnClickListener() {
     @Override
     public void onClick(View v) {
       // Redirect to the Activity where `VideoDownloadListView` is located
       startActivity(DownloadMeduListActivity.this,VideoDownloadListActivity.class);
     }
});

// Step 4. Display the view with animation
mDownloadMenuView.show();
```

```java
public void initDownloadData(List<SuperPlayerModel> superPlayerModelList,
                             List<VideoQuality> qualityList,
                             VideoQuality currentQuality,
                             String userName)
```

API parameters:

| Parameter | Type | Description |
| -------------------- | ---------------------- | ---------------- |
| superPlayerModelList | List<SuperPlayerModel> | The downloaded video data   |
| qualityList          | List<VideoQuality>     | The video definition data   |
| currentQuality       | VideoQuality           | The current video definition |
| userName             | String                 | The username           |

`VideoDownloadListView` (video download list) displays the list of views of all the videos that are being downloaded and have been downloaded. When this button is clicked, if the download is in progress, it will be paused; if it is paused, it will be resumed; if it has completed, the video will be played back.

<img src="http://1400155958.vod2.myqcloud.com/facd87c8vodcq1400155958/a69c6b2c387702307128674240/wt31IYPsdQoA.jpg" style="zoom: 33%;" />



```java
// Step 1. Bind the control
VideoDownloadListView mVideoDownloadListView = findViewById(R.id.video_download_list_view);

//Step 2. Add data  
mVideoDownloadListView.addCacheVideo(mDataList, true);

```

API parameters:

```
public void addCacheVideo(List<TXVodDownloadMediaInfo> mediaInfoList, boolean isNeedClean);
```

| Parameter | Type | Description |
| ------------- | ---------------------------- | ------------------ |
| mediaInfoList | List<TXVodDownloadMediaInfo> | The type of the added video data |
| isNeedClean   | boolean                      | Whether to clear the previous data |



### 8. Image sprite and timestamp information

#### Timestamp information

You can add text descriptions at key positions on the progress bar, which the user can click to view and quickly understand the video information at the current position. After clicking the video information, the user can seek to the desired position.

You can try out this feature in full screen mode in TCToolkit App > Player > Player Components > Tencent Cloud Video.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/Qc3t442_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16697206995071%20%281%29.png)

#### Image sprite

Users can view video thumbnails when dragging or seeking on the progress bar so as to quickly understand the video content at the specified position. The thumbnail preview is implemented based on the video's image sprite. You can generate the image sprite of a video file in the VOD console or directly generate an image sprite file.
You can try out this feature in full screen mode in TCToolkit App > Player > Player Components > Tencent Cloud Video.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/Ii2h727_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16697206895960%20%281%29.png)

```java
// Step 1. Get the image sprite and timestamp information in the `onPlayEvent` callback (this works only if the video is played back through `PlayWithField`, with the `url` variable of `superplayerModel` being empty and `videoId` not being empty).
mSuperplayerView.play(superplayerModel);

// Step 2. Get timestamp and image sprite information in the `VOD_PLAY_EVT_GET_PLAYINFO_SUCC` callback event during playback through `PlayWithFileId`.
public void onPlayEvent(TXVodPlayer player, int event, Bundle param) {
    switch (event) {
        case TXVodConstants.VOD_PLAY_EVT_GET_PLAYINFO_SUCC:
    
            // Get the list of image URLs of the image sprite
            playImageSpriteInfo.imageUrls = param.getStringArrayList(TXVodConstants.EVT_IMAGESPRIT_IMAGEURL_LIST);
            // Get the download URL of the image sprite WebVTT file
            playImageSpriteInfo.webVttUrl = param.getString(TXVodConstants.EVT_IMAGESPRIT_WEBVTTURL);
            // Get the timestamp information    
           ArrayList<String> keyFrameContentList =
                    param.getStringArrayList(TXVodConstants.EVT_KEY_FRAME_CONTENT_LIST);
            // Get the time information of the timestamp information
            float[] keyFrameTimeArray = param.getFloatArray(TXVodConstants.EVT_KEY_FRAME_TIME_LIST);
        
            // Construct the list of timestamp information
            if (keyFrameContentList != null && keyFrameTimeArray != null
                    && keyFrameContentList.size() == keyFrameTimeArray.length) {
                for (int i = 0; i < keyFrameContentList.size(); i++) {
                    PlayKeyFrameDescInfo frameDescInfo = new PlayKeyFrameDescInfo();
                    frameDescInfo.content = keyFrameContentList.get(i);
                    frameDescInfo.time = keyFrameTimeArray[i];
                    mKeyFrameDescInfoList.add(frameDescInfo);
                }
            }
            break;
        default:
            break;
　　}
}

// Step 3. Assign the obtained timestamp information and image sprite to the corresponding view through the `updateVideoImageSpriteAndKeyFrame` method. 
// The view of the image sprite corresponds to `mIvThumbnail` in the `VideoProgressLayout` component.
// The view of the timestamp information corresponds to `TCPointView` in the `PointSeekBar` component.
updateVideoImageSpriteAndKeyFrame(playImageSpriteInfo,keyFrameDescInfoList);
```

[](id:demo)

## Demo

To try out more features, you can directly run the demo project or scan the QR code to download the TCToolkit App demo.

### Running a demo project

1. Select **File** > **Open** on the navigation bar of Android Studio. In the pop-up window, select the `$SuperPlayer_Android/Demo` directory of the **demo** project. After the demo project is imported successfully, click **Run app** to run the demo.
2. After running the demo successfully, go to **Player** > **Player Component** to try out the player features.
