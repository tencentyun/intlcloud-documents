## Overview

The Superplayer SDK for Android is a player component used to play back videos in VOD. It can implement powerful playback functionality similar to Tencent Video with just a few lines of code.

* Basic features: landscape/portrait mode switch, definition selection, gestures, small window playback, etc.
* Advanced features: video buffering, software/hardware decoding switch, adjustable-speed playback, video thumbnails, DRM-encrypted playback, etc.

The Superplayer SDK supports more formats and has better compatibility and functionality than system-default players. In addition, it features instant playback on splash screen and low latency.

## SDK Download

The VOD Superplayer SDK for Android can be downloaded [here](https://github.com/tencentyun/SuperPlayer_Android).

## Quick Integration

It takes just a few simple steps to integrate with the VOD Superplayer SDK for video playback.

### aar integration

1. Download the SDK and Demo development kit for Android here: [SuperPlayer_Android](https://github.com/tencentyun/SuperPlayer_Android).
2. Import `SDK/LiteAVSDK_XXX.aar` and `Demo/app/libs/lib_tcsuperplayer.aar` into the project.
3. Add dependencies to `app/build.gralde`:
```java
compile(name: 'LiteAVSDK_Professional', ext: 'aar')
compile(name: 'lib_tcsuperplayer', ext: 'aar')
// Third-party library for integration of the on-screen commenting feature of superplayer
compile 'com.github.ctiao:DanmakuFlameMaster:0.5.3'
```
4. Add the following to the project's `build.gradle`:
```
...
allprojects {
    repositories {
        flatDir {
            dirs 'libs'
        }
        ...
    }
}
...
```
5. Declare the permissions:
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

>! `lib_tcsuperplayer.aar` is made open source in the form of module. You can find all the source code in `Demo/lib_tcsuperplayer`.

### Preparing videos

Log in to the [VOD Console](https://console.cloud.tencent.com/vod/overview), click **Media Assets** on the left sidebar, and you will see the uploaded video and its corresponding ID (i.e., `FileId`) in the video list in the **Uploaded** column. If you don't have a video, please click **Upload Video** to upload one.
![](https://main.qcloudimg.com/raw/2193e70a3f4c19b18e31c63778f3795e.png)

You can initiate an [adaptive bitrate streaming](https://intl.cloud.tencent.com/document/product/266/33942) task for the uploaded video through [ProcessMedia](#APIhttps://intL.cloud.tencent.com/document/product/266/33427):
You are recommended to enter 10 for `MediaProcessTask.AdaptiveDynamicStreamingTaskSet.Definition` in the API parameter, indicating transcoding to adaptive bitstream in HLS format.

### Starting playback

The main class of the player is `SuperPlayerView`, and videos can be played back after it is created.
```java
mSuperPlayerView = findViewById(R.id.main_super_player_view);
// Configure video information through `fileid`
SuperPlayerModel model = new SuperPlayerModel();
model.appid = 1256993030;   // AppId
model.fileid = "7447398157015849771"; // Video `FileId`
model.videoId.playDefinition = "10";  // Playback template
model.videoId.version = SuperPlayerVideoId.FILE_ID_V3;
// Start playback
mSuperPlayerView.playWithMode(model);
```

In the code, `appid` is your AppId, `fileid` is the ID of the video you want to play back, `playDefinition` is the ID of the playback template used for playback, and `version` is fixed to `SuperPlayerVideoId.FILE_ID_V3`.

Run the code and you can see that the video is played back on the phone and most of the features in the UI are available.
<img src="https://main.qcloudimg.com/raw/128c45edfc77b319475868c21caec2de.png" width="550">

## Thumbnails and Timestamps

When videos are played back, the "thumbnails" and "timestamps" on the progress bar can help viewers find the points of interest easily. Thumbnails are implemented through [image sprites](#APIhttps://intl.cloud.tencent.com/document/product/266/8101), while timestamps by [modifying timestamp information in media assets](#APIhttps://intl.cloud.tencent.com/document/product/266/31762#.E7.A4.BA.E4.BE.8B3-.E4.BF.AE.E6.94.B9.E5.AA.92.E4.BD.93.E6.96.87.E4.BB.B6.E8.A7.86.E9.A2.91.E6.89.93.E7.82.B9.E4.BF.A1.E6.81.AF).

After image sprites are generated and timestamps are added, new elements will be displayed in the player UI.
<img src="https://main.qcloudimg.com/raw/55ebce6d0c703dafa1ac131e1852e025.png" width="550">

### How to use

First, the application needs to get the token from your **business backend**. Then, play back the video through `FileId` and `Token` with the following playback code:

```java
SuperPlayerModel model = new SuperPlayerModel();
String fileId = "7447398157015849771";
model.appId = 1256993030;
model.videoId = new SuperPlayerVideoId();
model.videoId.fileId = fileId;
model.videoId.playDefinition = "20";  // Playback template
model.videoId.version = SuperPlayerVideoId.FILE_ID_V3; // The V3 protocol needs to be used for DRM
try {
    // The token needs to be URL-encoded
    String encodedToken = URLEncoder.encode("Token issued by the business", "UTF-8");
    model.token = encodedToken;
} catch (UnsupportedEncodingException e) {
    e.printStackTrace();
}
mSuperPlayerView.playWithModel(model);
```
## Small Window Playback

Small window playback can float on top of all `Activities`. It is very simple. You just need to call the following code before playback starts:
```java
// Player configuration
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

## Exiting Playback

If the player is no longer needed, please call `resetPlayer` to clear the internal state of the player and free up the memory.
```java
mSuperPlayerView.resetPlayer();
```

## More Features

To try out the complete features, scan the QR code below to download the Tencent Video Cloud toolkit or run the project demo directly.
<img src="https://main.qcloudimg.com/raw/344d9d41fc5e305a17e22e104b9305da.png" width="150">
