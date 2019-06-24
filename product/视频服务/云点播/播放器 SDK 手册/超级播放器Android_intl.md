## Overview

The Super Player SDK for Android is an open-source Tencent Cloud player component, and it provides powerful playback capabilities similar to Tencent Video - users can easily switch between portrait and landscape mode, select the video quality, enable gesture recognition, floating video player, as well as cache video, switch between software/hardware decoding and adjust playback speed. It is compatible with more video formats and more powerful than the system-default player. It also boasts many other advanced functions such as instant playback on the splash screen and video thumbnails.

## SDK Download

The VOD Super Player SDK for Android can be downloaded [here](https://github.com/tencentyun/SuperPlayer_Android).

## Target Audience

This document describes Tencent Cloud's proprietary capabilities. Please make sure that you have activated the relevant [Tencent Cloud](https://cloud.tencent.com) services before reading it. If you haven't registered an account, please [sign up for a free trial](https://cloud.tencent.com/login) first.

## Quick Integration

### aar Integration

1. Download the SDK + Demo development kit for Android [here](https://github.com/tencentyun/SuperPlayer_Android).
2. Import `SDK/LiteAVSDK_XXX.aar` and  `Demo/app/libs/lib_tcsuperplayer.aar` into the project.
3. Add dependencies to `app/build.gralde`:
```java
compile(name: 'LiteAVSDK_Professional', ext: 'aar')
compile(name: 'lib_tcsuperplayer', ext: 'aar')
// Third-party library for integration of the on-screen commenting feature of Super Player
compile 'com.github.ctiao:DanmakuFlameMaster:0.5.3'
```
4. Add the following to the project's `build.gralde`:
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

>! `lib_tcsuperplayer.aar` is made open source in the form of module. You can find all the source code in Demo/lib_tcsuperplayer.

### Using the Player

The main class of the player is `SuperPlayerView`, and videos can be played after it is created.
```java
mSuperPlayerView = findViewById(R.id.main_super_player_view);
// Configure video information through fileid
SuperPlayerModel model = new SuperPlayerModel();
model.appid = 1252463788;   // AppId
model.fileid = "5285890781763144364"; // Video FileId
// Start playback
mSuperPlayerView.playWithMode(model);
```

Run the code and you can see that the video is played on the phone and most of the features in the interface are available.

![](https://main.qcloudimg.com/raw/128c45edfc77b319475868c21caec2de.png)

### Selecting a FileID

A video FileID is usually returned by the server after the video is uploaded:
1. After the video is released to the client, the server will return a [FileID](https://cloud.tencent.com/document/product/584/9367#8..E5.8F.91.E5.B8.83.E7.BB.93.E6.9E.9C) to the client.
2. When the video is uploaded to the server, the corresponding FileID is included in the notification of the [upload confirmation](https://cloud.tencent.com/document/product/266/9757).

If the file already exists in Tencent Cloud, you can go to [Video Management](https://console.cloud.tencent.com/video/videolist), find the corresponding file, and view its FileID. The ID as shown in the figure below is the FileID:

![Video management](https://main.qcloudimg.com/raw/15c5d181b9037b58db5cf192fe831f1b.png)

## Thumbnails and Timestamps

When long videos are played, thumbnails (image sprite) and timestamps can help viewers find the points of interest easily. You can use TencentCloud API to quickly process videos.
- [Create a sprite via screen capture](https://cloud.tencent.com/document/product/266/8101)
- [Add a timestamp](https://cloud.tencent.com/document/product/266/14190)

After the task is successfully executed, new elements will be displayed in the player interface.

![](https://main.qcloudimg.com/raw/55ebce6d0c703dafa1ac131e1852e025.png)

## Playing a DRM-encrypted Video

Digital Rights Management (DRM) encrypts copyrighted works through technical means and controls their use, modification, and distribution to protect their security. It is applicable to copyrighted multimedia content such as music and movies.

The Android player can play the outputs of two encryption methods:

1. Encrypted Dash format based on Widevine
2. Encrypted HLS format based on SimpleAES

For more information about DRM, see [How to Protect the Copyright of Content](<https://cloud.tencent.com/document/product/266/34105#.E5.95.86.E4.B8.9A.E7.BA.A7-drm>).

### How to Use

First, the app needs to get the token from your **business backend**. For more information about how to generate a token, see [here](<https://cloud.tencent.com/document/product/266/34102#token-.E7.94.9F.E6.88.90>). Then, play the video through FileID + Token with the following playback code:

```java
SuperPlayerModel model = new SuperPlayerModel();
String fileId = "15517827183920333646";
model.appId = 1253039488;
model.videoId = new SuperPlayerVideoId();
model.videoId.fileId = fileId;
model.videoId.playDefinition = "20";  // Playback template
model.videoId.version = SuperPlayerVideoId.FILE_ID_V3; // The V3 protocol is required for DRM
try {
    // The token needs to be URL-encoded
    String encodedToken = URLEncoder.encode("Token issued by the business", "UTF-8");
    model.token = encodedToken;
} catch (UnsupportedEncodingException e) {
    e.printStackTrace();
}
mSuperPlayerView.playWithModel(model);
```

`playDefinition` in the code is the ID of the [playback template](https://cloud.tencent.com/document/product/266/34101#.E6.92.AD.E6.94.BE.E6.A8.A1.E6.9D.BF). The player will play the video as specified by the playback template. For example, if the template ID is 20, the player will first try to play the output of commercial encryption, and if it cannot play, downgrade and play the output of SimpleAES encryption.

## Floating Video Player

A floating video player video playback on top of other activities. Floating video player is easy to use. You just need to call the following code before playback starts:
```java
// Player configuration
SuperPlayerGlobalConfig prefs = SuperPlayerGlobalConfig.getInstance();
// Enable floating video player
prefs.enableFloatWindow = true;
// Set the initial position, width, and height of the floating window
SuperPlayerGlobalConfig.TXRect rect = new SuperPlayerGlobalConfig.TXRect();
rect.x = 0;
rect.y = 0;
rect.width = 810;
rect.height = 540;
// Other configurations
```
![](https://main.qcloudimg.com/raw/d6783a450e339526e0ca0b2ed3ef6142.png)

## Exiting Playback

When the player is no longer needed, please call `resetPlayer` to clear the internal state of the player and free up the memory.
```java
mSuperPlayerView.resetPlayer();
```

## More Features

To experience all features, scan the QR code to download the Tencent Video Cloud toolkit or run the project demo directly.
![Download QR code for Android](https://main.qcloudimg.com/raw/344d9d41fc5e305a17e22e104b9305da.png)
