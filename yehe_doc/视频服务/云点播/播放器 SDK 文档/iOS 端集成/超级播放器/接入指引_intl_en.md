## Overview

Tencent Cloud RT-Cube Superplayer for iOS is an open-source Tencent Cloud player component. It can provide powerful playback functionality similar to Tencent Video with just a few lines of code. It has basic features such as landscape/portrait mode switching, definition selection, gestures, and small window playback, as well as special features such as video buffering, software/hardware decoding switching, and adjustable-speed playback. It supports more formats and has better compatibility and functionality than system-default players. In addition, it features instant broadcasting of the first frame and low latency and offers advanced capabilities like video thumbnail.


## Preparations
1. Activate [VOD](https://intl.cloud.tencent.com/product/vod). If you haven't registered an account, [sign up](https://intl.cloud.tencent.com/login) first.
2. Download Xcode from App Store. If you have already done so, skip this step.
3. Download and install CocoaPods as instructed at the [CocoaPods website](https://cocoapods.org/). If you have already done so, skip this step.

## Content Summary
- [How to integrate the Tencent Cloud RT-Cube Superplayer for iOS](#step1)
- [How to create and use a player](#step3)

## Preparations for Integration
[](id:step1)
### Step 1. Download the project
The Tencent Cloud RT-Cube Superplayer for iOS can be downloaded [here](https://github.com/LiteAVSDK/Player_iOS).

You can download the Tencent Cloud RT-Cube Superplayer for iOS by **[downloading the player component ZIP package](#zip)** or **[running the Git command](#git)**.
<dx-tabs>
::: Download the player component ZIP package[](id:zip)
You can directly download the player component ZIP package by clicking **Code** > **Download ZIP**.
![](https://qcloudimg.tencent-cloud.cn/raw/a38a9995bfe13d645bcd1d2e5242a297.png)
:::
::: Run the Git command[](id:git)
1. First, make sure that your computer has Git installed; if not, you can install it as instructed in [Git Installation Tutorial](https://git-scm.com/downloads).
2. Run the following command to clone the code of the superplayer component project to your local system.
```shell
git clone git@github.com:tencentyun/SuperPlayer_iOS.git
```
   If the following information is displayed, the project code has been cloned to your local system successfully.
```shell
Cloning to 'SuperPlayer_iOS'...
remote: Enumerating objects: 2637, done.
remote: Counting objects: 100% (644/644), done.
remote: Compressing objects: 100% (333/333), done.
remote: Total 2637 (delta 227), reused 524 (delta 170), pack-reused 1993
Receiving the object: 100% (2637/2637), 571.20 MiB | 3.94 MiB/s, done.
Processing delta: 100% (1019/1019), done.
```
After the project is downloaded, the directory generated after decompression of the project source code is as follows:
<table>
<thead><tr><th>Filename</th><th>Description</th></tr></thead>
<tbody>
<tr><td>SDK</td>
<td>Stores the player's framework static library</td>
</tr><tr>
<td>Demo</td><td>Stores the superplayer demo</td>
</tr><tr>
<td>App</td><td>Program entry UI</td>
</tr><tr>
<td>SuperPlayerDemo</td><td>Superplayer demo</td>
</tr><tr><td>SuperPlayerKit</td><td>Superplayer component</td>
</tr></tbody></table>
:::
</dx-tabs>

[](id:step2)
### Step 2. Integrate the project
This step describes how to integrate the player. We recommend you **[integrate it through CocoaPods](#cocoapods)** or **[manually download the SDK](#manual)** and then import it into your current project.
<dx-tabs>
::: Integration through CocoaPods[](id:cocoapods)
1. This project supports installation through CocoaPods. You only need to add the following code to the `Podfile`:
```xml
pod 'SuperPlayer'
```
2. Run `pod install` or `pod update`.
:::
::: Manual SDK download[](id:manual)
1. Download the SDK + demo package. The Tencent Cloud RT-Cube Superplayer for iOS can be downloaded [here](https://github.com/LiteAVSDK/Player_iOS).
2. Import `TXLiteAVSDK_Player.framework` into the project and select `Do Not Embed`.
:::
</dx-tabs>

[](id:step3)
### Step 3. Use the player features
This step describes how to create a player and use it for video playback.

1. **Player creation:**[](id:usePlayer)
The main class of the player is `SuperPlayerView`, and videos can be played back after it is created.
```xml
// Import the header file
#import <SuperPlayer/SuperPlayer.h>

// Create a player  
_playerView = [[SuperPlayerView alloc] init];
// Set the delegate to accept events
_playerView.delegate = self;
// Set the parent view. `_playerView` will be automatically added under `holderView`
_playerView.fatherView = self.holderView;
```
2. **Video playback:**
This step describes how to play back a video. The Tencent Cloud RT-Cube Superplayer for iOS supports playback through [`FileId` in VOD](#fileid) or [URL](#url). We recommend you **integrate the `FileId`** to use complete capabilities.
<dx-tabs>
::: Playback through `FileId` in VOD[](id:fileid)
A video `FileId` is usually returned by the server after the video is uploaded:

1. After the video is published on the client, the server will return a `FileId` to the client.
2. When the video is uploaded to the server, its `FileId` will be included in the notification of upload confirmation.
If the file already exists in Tencent Cloud, you can go to [Media Assets](https://console.cloud.tencent.com/vod/media), find it, and view its `FileId` as shown below, where ID is the `FileId`:
![](https://qcloudimg.tencent-cloud.cn/raw/f089346e01ab8e44e42f28c965809b9c.png)
>!
>- For playback through `FileId`, you need to first use the Adaptive-HLS(10) transcoding template to transcode the video or use the superplayer signature `psign` to specify the video to be played back; otherwise, the video may fail to be played back. For more information on how to transcode a video, see [Playing back Video Through Superplayer](https://intl.cloud.tencent.com/document/product/266/38098). For more information on how to generate a `psign`, see [Superplayer Signature](https://intl.cloud.tencent.com/document/product/266/38099).
>- If a "no v4 play info" exception occurs during playback through `FileId`, the above problem may exist. In this case, we recommend you make adjustments as instructed above. You can also directly get the playback link of the source video for playback through [URL](#url).
>- **As an untranscoded source video may experience a compatibility issue during playback, we recommend you transcode videos for playback.**

<dx-codeblock>
:::  java
// During playback with hotlink protection disabled, if a "no v4 play info" exception occurs, we recommend you use the Adaptive-HLS(10) transcoding template to transcode the video or directly get the playback link of the source video for playback through URL.

SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
model.appId = 1400329071;// Configure `AppId`
model.videoId = [[SuperPlayerVideoId alloc] init];
model.videoId.fileId = @"5285890799710173650"; // Configure `FileId`
// For private encrypted playback, you need to enter the `psign`, which is a signature for superplayer. For more information on the signature and how to generate it, visit https://intl.cloud.tencent.com/document/product/266/38099
//model.videoId.pSign = @"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTQwMDMyOTA3MSwiZmlsZUlkIjoiNTI4NTg5MDc5OTcxMDE3MzY1MCIsImN1cnJlbnRUaW1lU3RhbXAiOjEsImV4cGlyZVRpbWVTdGFtcCI6MjE0NzQ4MzY0NywidXJsQWNjZXNzSW5mbyI6eyJ0IjoiN2ZmZmZmZmYifSwiZHJtTGljZW5zZUluZm8iOnsiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3fX0.yJxpnQ2Evp5KZQFfuBBK05BoPpQAzYAWo6liXws-LzU"; 
[_playerView playWithModel:model];
:::
</dx-codeblock>
:::
::: Playback through URL[](id:url)
```java
SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
model.videoURL = @"http://your_video_url.mp4";   // Configure a URL for your video for playback
[_playerView playWithModel:model];
```
:::
</dx-tabs>
- **Playback exit:**[](id:exitPlayer)
When the player is no longer needed, call `resetPlayer` to clear the internal state of the player and free up the memory.
```java
[_playerView resetPlayer];
```

At this point, you have integrated the player creation, video playback, and playback exiting capabilities of the Tencent Cloud RT-Cube Superplayer for iOS.

[](id:moreFeature)
## Feature Usage[](id:moreFeature)

### 1. Full screen playback

The superplayer supports full screen playback, where it allows setting screen lock, volume and brightness control through gesture, on-screen commenting, screencapturing, and definition switch. This feature can be tried out in [**Tencent Cloud RT-Cube App**](#qrcode) > **Player** > **Superplayer**, and you can enter the full screen playback mode by tapping the full screen icon.



In window playback mode, the following API can be called to enter the full screen playback mode:

```objective-c
- (void)superPlayerFullScreenChanged:(SuperPlayerView *)player {
  // You can customize the logic after switching to the full screen mode here
}
```


<dx-tabs>
::: Return to the window mode[](id:window)
Tap **Back** to return to the window playback mode. The delegate method that will be triggered after the SDK processes the logic for switching to the full screen mode is as follows:

```objective-c
// Return the event
- (void)superPlayerBackAction:(SuperPlayerView *)player;
Triggered by tapping **Back** in the top-left corner
// Full screen change notification
- (void)superPlayerFullScreenChanged:(SuperPlayerView *)player;
```
:::
::: Screen lock[](id:screenlock)
The screen lock operation enables the immersive playback status. It will be processed by the SDK without a callback after the button is tapped.

```objective-c
// The following API can be called to control whether to lock the screen
@property(nonatomic, assign) BOOL isLockScreen;
```
:::
::: On-screen commenting[](id:barrage)
After the on-screen commenting feature is enabled, text comments sent by users will be displayed on the screen.

Get the `SPDefaultControlView` object here and set an event for the on-screen comment button of `SPDefaultControlView` during player view initialization. The on-screen comment content and view need to be customized. For more information, see `CFDanmakuView`, `CFDanmakuInfo`, and `CFDanmaku` under `SuperPlayerDemo`.

```objective-c
SPDefaultControlView *dv = (SPDefaultControlView *)**self**.playerView.controlView;
[dv.danmakuBtn addTarget:**self** action:**@selector**(danmakuShow:) forControlEvents:UIControlEventTouchUpInside];
```

CFDanmakuView: Configure the attributes of on-screen commenting during initialization.

```objective-c
// The following attributes are required--------
// On-screen emoji duration
@property(nonatomic, assign) CGFloat duration;
// Display duration of the on-screen comment on the screen
@property(nonatomic, assign) CGFloat centerDuration;
// On-screen comment line height
@property(nonatomic, assign) CGFloat lineHeight;
// Spacing between on-screen comment lines
@property(nonatomic, assign) CGFloat lineMargin;

// Maximum number of on-screen comment lines
@property(nonatomic, assign) NSInteger maxShowLineCount;

// Maximum number of on-screen comment lines on the screen
@property(nonatomic, assign) NSInteger maxCenterLineCount;
```
:::
::: Screencapturing[](id:screenshot)
The superplayer provides the feature of capturing the current video frame during playback, and you can save the screenshot for sharing. The tapping of the **Screencapture** button will be processed internally by the SDK without a callback for screencapturing success or failure, and the directory of the captured screenshots will be the phone album.
:::
::: Definition switch[](id:resolution)
Different video playback definitions can be selected as needed, such as HD, SD, and FHD. The definition display view triggered after button tapping and the definition options will be processed internally by the SDK without a callback.
:::
</dx-tabs>


### 2. Floating window playback

The superplayer supports playback in a small floating window, which allows users to switch to another app without interrupting the video playback. This feature can be tried out in [**Tencent Cloud RT-Cube App**](#qrcode) > **Player** > **Superplayer** by tapping **Back** in the top-left corner.

<img src="https://qcloudimg.tencent-cloud.cn/raw/e8a774cb9833f2de45fc1cf3cc928ee4.png" style="zoom:45%;" />



```objective-c
// Tapping the **Back** button during playback in portrait mode will trigger the API
[SuperPlayerWindowShared setSuperPlayer:self.playerView];
[SuperPlayerWindowShared show];
// The API triggered by tapping the floating window to return to the main window
SuperPlayerWindowShared.backController = self;
```

### 3. Video thumbnail

The superplayer supports customizing a video thumbnail for display before the callback for playing back the first video frame is received. This feature can be tried out in [**Tencent Cloud RT-Cube App**](#qrcode) > **Player** > **Superplayer** > **Thumbnail Customization Demo**.



* When the superplayer is set to the automatic playback mode `PLAY_ACTION_AUTO_PLAY`, the video will be played back automatically, and the thumbnail will be displayed before the first video frame is loaded.
* When the superplayer is set to the manual playback mode `PLAY_ACTION_MANUAL_PLAY`, the playback of the video will start only after the user taps **Play**. The thumbnail will be displayed until the first video frame is loaded.

A video thumbnail supports the use of a URL or local file address as instructed below. If you play back a video through its `FileId`, you can directly configure a video thumbnail in VOD.

```objective-c
SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
SuperPlayerVideoId *videoId = [SuperPlayerVideoId new];
videoId.fileId = @"8602268011437356984"; 
model.appId = 1400329071;
model.videoId = videoId;
// Playback mode, which can be set to the automatic `PLAY_ACTION_AUTO_PLAY` or manual `PLAY_ACTION_MANUAL_PLAY`
model.action  = PLAY_ACTION_MANUAL_PLAY; 
// Set a URL for the thumbnail. If `coverPictureUrl` is not set, the thumbnail configured in the VOD console will be used automatically
model.customCoverImageUrl = @"http://1500005830.vod2.myqcloud.com/6c9a5118vodcq1500005830/cc1e28208602268011087336518/MXUW1a5I9TsA.png"; 
[self.playerView playWithModel:model] 
```

### 4. Video list loop

The superplayer supports video list loop; that is, after a video list is given:

* Videos in the list can be played back in loop. The next video can be played back automatically or switched to manually during playback.
* After the last video in the list ends, the first video in the list will start automatically.

This feature can be tried out in [**Tencent Cloud RT-Cube App**](#qrcode) > **Player** > **Superplayer** > **Video List Loop Demo**.

```objective-c
// Step 1. Create a `NSMutableArray` for the loop data
NSMutableArray *modelArray = [NSMutableArray array];
SuperPlayerModel *model = [SuperPlayerModel new];
SuperPlayerVideoId *videoId = [SuperPlayerVideoId new];
videoId.fileId = @"8602268011437356984"; 
model.appId = 1252463788;
model.videoId = videoId;
[modelArray addObject:model];

model = [SuperPlayerModel new];
videoId = [SuperPlayerVideoId new];
videoId.fileId = @"4564972819219071679";
model.appId = 1252463788;
model.videoId = videoId;
[modelArray addObject:model];

// Step 2. Call the loop API of `SuperPlayerView`
[self.playerView playWithModelList:modelArray isLoopPlayList:YES startIndex:0];
```

```objective-c
(void)playWithModelList:(NSArray *)playModelList isLoopPlayList:(BOOL)isLoop startIndex:(NSInteger)index;
```

API parameter description

| Parameter | Type | Description |
| ------------- | --------- | --------- |
| playModelList | NSArray * | Loop data list    |
| isLoop        | Boolean   | Whether to loop      |
| index         | NSInteger | Index of the video from which to start the playback |

### 5. Video preview

The superplayer supports the video preview feature, which is suitable for non-VIP member preview. You can pass in different parameters to control the video preview duration, prompt message, and preview end screen. This feature can be tried out in [**Tencent Cloud RT-Cube App**](#qrcode) > **Player** > **Superplayer** > **Preview Feature Demo**.

```objective-c
 // Step 1. Create a preview model
 TXVipWatchModel *model = [[TXVipWatchModel alloc] init];
 model.tipTtitle = @"You can preview 15 seconds and activate the VIP membership to watch the full video";
 model.canWatchTime = 15;
 // Step 2. Set the preview model
 self.playerView.vipWatchModel = model;
 // Step 3. Call the method to display the preview feature
 [self.playerView showVipTipView];
```

  `TXVipWatchModel` class parameter description:

| Parameter | Type | Description |
| ------------ | -------- | --------- |
| tipTtitle    | NSString | Preview prompt message    |
| canWatchTime | float    | Preview duration in seconds |

### 6. Dynamic watermark

The superplayer allows you to add an irregular moving text watermark on the playback screen to prevent unauthorized recording. Watermarks can be displayed both in full screen playback mode and window playback mode. You can modify the watermark text, size, and color. This feature can be tried out in [**Tencent Cloud RT-Cube App**](#qrcode) > **Player** > **Superplayer** > **Dynamic Watermark Demo**.



```objective-c
// Step 1. Create a video source information model
SuperPlayerModel *  playermodel   = [SuperPlayerModel new];
// Add other information of the video source
// Step 2. Create a dynamic watermark model
DynamicWaterModel *model = [[DynamicWaterModel alloc] init];
// Step 3. Set the data of the dynamic watermark
model.dynamicWatermarkTip = @"shipinyun";
model.textFont = 30;
model.textColor = [UIColor colorWithRed:255.0/255.0 green:255.0/255.0 blue:255.0/255.0 alpha:0.8];
playermodel.dynamicWaterModel = model;
// Step 4. Call the method to display the dynamic watermark
[self.playerView playWithModel:playermodel];
```

`DynamicWaterModel` class parameter description:

| Parameter | Type | Description |
| ------------------- | -------- | ------ |
| dynamicWatermarkTip | NSString | Watermark text information |
| textFont            | CGFloat  | Text size   |
| textColor           | UIColor  | Text color   |

## Demo

To try out more features, you can directly run the project demo or scan the QR code to download the Tencent Cloud RT-Cube app demo.

### Running project demo

1. In the `Demo` directory, run the `pod update` command to generate the `TXLiteAVDemo.xcworkspace` file again.
2. Double-click to open the project, modify the certificate, and run the project on a real device.
3. After running the demo successfully, go to **Player** > **Superplayer** to try out the player features.

[](id:qrcode)
### Tencent Cloud RT-Cube app

You can try out more features of the superplayer in **Tencent Cloud RT-Cube App** > **Player**.

<img src="https://main.qcloudimg.com/raw/12c7da97cc910eda673cb19b66fc7cb3.png" width="150">
