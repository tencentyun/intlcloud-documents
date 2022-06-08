## Overview

The RT-Cube iOS Superplayer is an open-source component that allows you to integrate powerful playback capabilities similar to those in Tencent Video into your project with just a few lines of code changes. In addition to basic features such as landscape/portrait orientation, resolution selection, gestures, and small-window playback, it also supports buffering, software/hardware decoding, and changing playback speed. Compared with built-in players, the RT-Cube Superplayer supports more formats and has better compatibility and more diverse features. It also features instant streaming and low latency, and comes with advanced features such as thumbnail generation.

## Prerequisites
1. Activate [VOD](https://intl.cloud.tencent.com/product/vod). If you don’t have an account yet, [sign up](https://intl.cloud.tencent.com/login) first.
2. Download and install Xcode from App Store.
3. Download and install CocoaPods as instructed at the [CocoaPods website](https://cocoapods.org/).

## Content Summary
- [How to integrate the Tencent Cloud RT-Cube Superplayer for iOS](#step1)
- [How to create and use a player](#step3)

## Directions
[](id:step1)
### Step 1. Download the Superplayer code package
GitHub page: [SuperPlayer_iOS](https://github.com/LiteAVSDK/Player_iOS)

You can download a [ZIP file](#zip) of Superplayer from the GitHub page or use the [Git clone command](#git) to download the component.
<dx-tabs>
::: Download the ZIP file[](id:zip)
Go to the Superplayer GitHub page and click **Code > Download ZIP**.
![](https://qcloudimg.tencent-cloud.cn/raw/a38a9995bfe13d645bcd1d2e5242a297.png)
:::
::: Download using a Git command[](id:git)

1. First, make sure that your computer has Git installed; if not, you can install it as instructed in [Git Installation Tutorial](https://git-scm.com/downloads).
2. Run the following command to clone the code of the Superplayer component to your local system.
```shell
git clone git@github.com:tencentyun/SuperPlayer_iOS.git
```
   If you see the following information, the project code has been cloned to your local system successfully.
```shell
Cloning to 'SuperPlayer_iOS'...
remote: Enumerating objects: 2637, done.
remote: Counting objects: 100% (644/644), done.
remote: Compressing objects: 100% (333/333), done.
remote: Total 2637 (delta 227), reused 524 (delta 170), pack-reused 1993
Receiving the object: 100% (2637/2637), 571.20 MiB | 3.94 MiB/s, done.
Processing delta: 100% (1019/1019), done.
```
Below is the directory structure of the component’s source code after decompression:
<table>
<thead><tr><th>Filename</th><th>Description</th></tr></thead>
<tbody>
<tr><td>SDK</td>
<td>Stores the Superplayer framework and static library.</td>
</tr><tr>
<td>Demo</td><td>Stores the Superplayer demo.</td>
</tr><tr>
<td>App</td><td>The entry point UI.</td>
</tr><tr>
<td>SuperPlayerDemo</td><td>The Superplayer demo.</td>
</tr><tr><td>SuperPlayerKit</td><td>The Superplayer component.</td>
</tr></tbody></table>
:::
</dx-tabs>

[](id:step2)
### Step 2. Integrate the component
This step describes how to integrate the player. We recommend you [integrate it through CocoaPods](#cocoapods) or [manually download the SDK](#manual) and then import it into your current project.
<dx-tabs>
::: Integrate via CocoaPods[](id:cocoapods)

1. To install the component using CocoaPods, add the code below to Podfile:
```xml
pod 'SuperPlayer'
```
2. Run `pod install` or `pod update`.
:::
::: Manually download the SDK[](id:manual)
1. Download the Superplayer SDK and demo at [GitHub](https://github.com/LiteAVSDK/Player_iOS).
2. Import `TXLiteAVSDK_Player.framework` into your project and select **Do Not Embed**.
:::
</dx-tabs>

[](id:step3)
### Step 3. Use the player features
This step describes how to create a player and use it for video playback.

1. **Create a player**[](id:usePlayer)
Create a `SuperPlayerView` object to play videos (`SuperPlayerView` is the main class of the Superplayer).
```xml
// Import the header file
#import <SuperPlayer/SuperPlayer.h>

// Create a player  
_playerView = [[SuperPlayerView alloc] init];
// Set a delegate for events
_playerView.delegate = self;
// Set the parent view. _playerView will be automatically added under holderView.
_playerView.fatherView = self.holderView;
```
2. **Play**
This step describes how to play a video. You can play a video by [VOD file ID](#fileid) or [URL](#url) using Superplayer. We recommend **the former** because it allows you to use more VOD capabilities.
<dx-tabs>
::: Play by VOD file ID[](id:fileid)
A video file ID is returned by the server after the video is uploaded.

1. After a video is published from a client, the server will return a file ID to the client.
2. After a video is uploaded to the server, the notification for successful upload will contain a file ID for the video.
If the video you want to play is already saved with VOD, you can go to [Media Assets](https://console.cloud.tencent.com/vod/media) to view its file ID.
![](https://qcloudimg.tencent-cloud.cn/raw/f089346e01ab8e44e42f28c965809b9c.png)

<dx-alert infotype="notice">
- To play by VOD file ID, you need to use the Adaptive-HLS template (ID: 10) to transcode the video or use the Superplayer signature `psign` to specify the video to play; otherwise, the playback may fail. For more information on how to transcode a video and generate `psign`, see [Play back a video with Superplayer](https://intl.cloud.tencent.com/document/product/266/38098) and [Superplayer Signature](https://intl.cloud.tencent.com/document/product/266/38099).</li>
- If a "no v4 play info" error occurs, it indicates that you haven’t transcoded the video or used the Superplayer signature correctly. Troubleshoot the issue according to the above documents or get the playback URL of the video and play it by [URL](#url).</li>
- **We recommend you transcode videos for playback because untranscoded videos may experience compatibility issues during playback.**</li></dx-alert>

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
::: Play by URL[](id:url)

```java
SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
model.videoURL = @"http://your_video_url.mp4";   // Enter the URL of the video to play
[_playerView playWithModel:model];
```
:::
</dx-tabs>
- **Stop playback**[](id:exitPlayer)
If the player is no longer needed, call `resetPlayer` to reset the player and free up memory.
```java
[_playerView resetPlayer];
```

At this point, you have learned how to create a player, use it to play videos, and stop playback.

[](id:moreFeature)
## More Features[](id:moreFeature)

### 1. Full screen playback

Superplayer supports full screen playback. In the full screen mode, users can disable touch screen, use gestures to control volume and brightness, send on-screen comments, take a screenshot of the video, and change the resolution. You can try these features in the [TCToolkit app](#qrcode): Go to **Player** > **Superplayer** and tap the full screen button at the bottom right of the video.

You can call the API below to go full screen from the windowed playback mode:

```objective-c
- (void)superPlayerFullScreenChanged:(SuperPlayerView *)player {
  // You can customize the logic after switching to the full screen mode here
}
```


<dx-tabs>
::: Back to windowed mode[](id:window)
Tap the back button to return to the windowed mode. The delegate method that will be triggered after the SDK implements the logic for exiting full screen is as follows:

```objective-c
// The back button tapping event
- (void)superPlayerBackAction:(SuperPlayerView *)player;
Triggered by tapping of the back button at the top left
// The exit full screen notification
- (void)superPlayerFullScreenChanged:(SuperPlayerView *)player;
```
:::
::: Disable touch screen[](id:screenlock)
Disabling touch screen allows users to enter an immersive playback mode. The SDK will handle the tapping event and no callbacks will be sent.

```objective-c
// Use the API below to disable/enable touch screen
@property(nonatomic, assign) BOOL isLockScreen;
```
:::
::: On-screen comment[](id:barrage)
After the on-screen commenting feature is enabled, text comments sent by users will be displayed on the screen.

Get the `SPDefaultControlView` object and, during initialization of the player view, set an event for the on-screen comment button of `SPDefaultControlView`. The on-screen comment content and view are customized by yourself. For details, see `CFDanmakuView`, `CFDanmakuInfo`, and `CFDanmaku` in `SuperPlayerDemo`.

```objective-c
SPDefaultControlView *dv = (SPDefaultControlView *)**self**.playerView.controlView;
[dv.danmakuBtn addTarget:**self** action:**@selector**(danmakuShow:) forControlEvents:UIControlEventTouchUpInside];
```

CFDanmakuView: Configure the attributes of on-screen commenting during initialization.

```objective-c
// The following attributes are required--------
// On-screen time
@property(nonatomic, assign) CGFloat duration;
// On-screen time in the center, at top, and at bottom
@property(nonatomic, assign) CGFloat centerDuration;
// On-screen comment line height
@property(nonatomic, assign) CGFloat lineHeight;
// Spacing between on-screen comment lines
@property(nonatomic, assign) CGFloat lineMargin;

// Maximum number of on-screen comment lines
@property(nonatomic, assign) NSInteger maxShowLineCount;

// Maximum number of on-screen comment lines in the center, at top, and at bottom
@property(nonatomic, assign) NSInteger maxCenterLineCount;
```
:::
::: Screenshot[](id:screenshot)
Superplayer allows users to take and save a screenshot of a video during playback. The SDK will handle the screenshot button tapping event and no callbacks will be sent for successful or failed screenshots. Screenshots are saved to the phone album.
:::
::: Change resolution[](id:resolution)
Users can change the resolution (such as SD, HD, and UHD) during playback. After the resolution switching button is tapped, the SDK will implement the logic for displaying the resolution selection view and handle the resolution selection event. No callbacks will be sent.
:::
</dx-tabs>


### 2. Floating window playback

Superplayer supports playback in a small floating window, which allows users to go to other pages of the app without interrupting the playback. You can try this feature in the [TCToolkit app](#qrcode): Go to **Player** > **Superplayer** and tap the back button at the top left of the video.

<img src="https://qcloudimg.tencent-cloud.cn/raw/e8a774cb9833f2de45fc1cf3cc928ee4.png" style="zoom:45%;" />



```objective-c
// Tapping the back button during playback in portrait mode will trigger the API
[SuperPlayerWindowShared setSuperPlayer:self.playerView];
[SuperPlayerWindowShared show];
// The API triggered by tapping the floating window to return to the main window
SuperPlayerWindowShared.backController = self;
```

### 3. Thumbnail

Superplayer supports customizing a video thumbnail for display before the callback for the first video frame is received. You can find a demo for this feature in the [TCToolkit app](#qrcode): **Player** > **Superplayer** > **Thumbnail Customization Demo**.



* When Superplayer is set to the automatic playback mode `PLAY_ACTION_AUTO_PLAY`, the thumbnail will be displayed before the first video frame is loaded.
* When Superplayer is set to the manual playback mode `PLAY_ACTION_MANUAL_PLAY`, videos are played only after users tap the play button, and the thumbnail will be displayed until the first video frame is loaded.

You can set the thumbnail by specifying the URL of a local or online file. For detailed directions, see the code below. If you play by VOD file ID, you can also set the thumbnail in the VOD console.

```objective-c
SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
SuperPlayerVideoId *videoId = [SuperPlayerVideoId new];
videoId.fileId = @"8602268011437356984"; 
model.appId = 1400329071;
model.videoId = videoId;
// Playback mode, which can be set to automatic (`PLAY_ACTION_AUTO_PLAY`) or manual (`PLAY_ACTION_MANUAL_PLAY`)
model.action  = PLAY_ACTION_MANUAL_PLAY; 
// Specify the URL of an online file to use as the thumbnail. If `coverPictureUrl` is not set, the thumbnail configured in the VOD console will be used.
model.customCoverImageUrl = @"http://1500005830.vod2.myqcloud.com/6c9a5118vodcq1500005830/cc1e28208602268011087336518/MXUW1a5I9TsA.png"; 
[self.playerView playWithModel:model] 
```

### 4. Video playlist loop

Superplayer supports looping video playlists.

* After a video ends, the next video in the list can be played automatically or users can manually start the next video.
* After the last video in the list ends, the first video in the list will start automatically.

You can find a demo for this feature in the [TCToolkit app](#qrcode): **Player** > **Superplayer** > **Video List Loop Demo**.

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

API parameters:

| Parameter           | Type        | Description        |
| ------------- | --------- | --------- |
| playModelList | NSArray * | Loop data list    |
| isLoop        | Boolean   | Whether to loop the playlist      |
| index         | NSInteger | Index of the video from which to start the playback |

### 5. Preview

The Superplayer supports video preview, which is useful if you want to allow non-subscribers to watch the beginning of a video. We offer parameters for you to set the video preview duration, pop-up message, and preview end screen. You can find a demo for this feature in the [TCToolkit app](#qrcode): **Player** > **Superplayer** > **Preview Feature Demo**.



```objective-c
 // Step 1. Create a preview model
 TXVipWatchModel *model = [[TXVipWatchModel alloc] init];
 model.tipTtitle = @"You can preview 15 seconds of the video. Become a subscriber to watch the full video.";
 model.canWatchTime = 15;
 // Step 2. Set the preview model
 self.playerView.vipWatchModel = model;
 // Step 3. Call the method below to display the preview
 [self.playerView showVipTipView];
```

  `TXVipWatchModel` class parameter description:

| Parameter          | Type       | Description        |
| ------------ | -------- | --------- |
| tipTtitle    | NSString | Pop-up message    |
| canWatchTime | float    | Preview duration in seconds |

### 6. Dynamic watermark

The Superplayer allows you to add a randomly moving text watermark to protect your content against piracy. Watermarks are visible in both the full screen mode and windowed mode. The text, font size, and color of a watermark are customizable. You can find a demo for this feature in the [TCToolkit app](#qrcode): **Player** > **Superplayer** > **Dynamic Watermark Demo**.

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
// Step 4. Call the method below to display the dynamic watermark
[self.playerView playWithModel:playermodel];
```

Parameters for `DynamicWaterModel`:

| Parameter          | Type       | Description        |
| ------------------- | -------- | ------ |
| dynamicWatermarkTip | NSString | Watermark text |
| textFont            | CGFloat  | Font size   |
| textColor           | UIColor  | Text color   |

## Demo

You can run a demo project or scan the QR code below to download the TCToolkit app to try out more features.

### Run a demo project

1. In the `Demo` directory, run the `pod update` command to generate the `TXLiteAVDemo.xcworkspace` file again.
2. Double-click the file to open it, modify the certificate, and run the project on a real device.
3. After the demo is run successfully, go to **Player** > **Superplayer** to try out the Superplayer features.

[](id:qrcode)
### TCToolkit app

You can also try Superplayer on the **Player** page of the TCToolkit app.

<img src="https://main.qcloudimg.com/raw/12c7da97cc910eda673cb19b66fc7cb3.png" width="150">