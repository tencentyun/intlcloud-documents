The Superplayer SDK for Android is an open-source Tencent Cloud player component. It can provide powerful playback functionality similar to Tencent Video with just a few lines of code. It has basic features such as landscape/portrait mode switching, definition selection, gestures, and small window playback, as well as special features such as video buffering, software/hardware decoding switching, and adjustable-speed playback. It supports more formats and has better compatibility and functionality than system-default players. In addition, it offers advanced capabilities like instant playback on splash screen, low latency, and video thumbnail.

## SDK Download

The VOD Superplayer SDK for Android can be downloaded [here](https://github.com/tencentyun/SuperPlayer_Android).

## Target Audience

This document describes Tencent Cloud's proprietary capabilities. Please make sure that you have activated the relevant [Tencent Cloud](https://intl.cloud.tencent.com) services before reading it. If you haven't registered an account, please [sign up for free trial](https://intl.cloud.tencent.com/login) first.

## Quick Integration

### Integrating aar

1. Download the SDK + Demo development kit for Android [here](https://github.com/tencentyun/SuperPlayer_Android).
2. Import `SDK/LiteAVSDK_XXX.aar` and the `Demo/superplayerkit` module into the project.
3. Add dependencies to `app/build.gralde`:
```java
compile(name: 'LiteAVSDK_Professional', ext: 'aar')
compile(name: 'libsuperplayer', ext: 'aar')
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

>! `lib_tcsuperplayer.aar` is made open source in the form of module. You can find all the source code in `Demo/lib_tcsuperplayer`.

### Using player

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


### Selecting FileId

A video `FileId` is usually returned by the server after the video is uploaded:

1. After the video is published on the client, the server will return a `FileId` to the client.
2. When the video is uploaded to the server, the corresponding `FileId` will be included in the notification of upload confirmation.

If the file already exists in Tencent Cloud, you can go to [Media Assets](https://console.cloud.tencent.com/vod/media), find it, and view its `FileId` as shown below, where ID is the `FileId`:



### Timestamping

When lengthy videos are played back, timestamps on the progress bar can help viewers find the points of interest easily. You can add timestamps by using the `AddKeyFrameDescs.N` parameter in the [ModifyMediaInfo](https://intl.cloud.tencent.com/document/product/266/37570) API.

After the call is made, new elements will be displayed in the player UI.


### Small window playback
Small window playback can float on top of all activities. It is very simple to implement. You just need to call the following code before playback starts:

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

### Exiting playback

When the player is no longer needed, call `resetPlayer` to clear the internal state of the player and free up the memory.

```java
mSuperPlayerView.resetPlayer();
```

## More Features

To try out the complete features, scan the QR code below to download the Tencent Video Cloud toolkit or run the project demo directly.
<img src="https://main.qcloudimg.com/raw/344d9d41fc5e305a17e22e104b9305da.png" width="150">

