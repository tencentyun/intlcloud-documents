## Product Overview

Tencent Cloud RT-Cube Player for iOS is an open-source Tencent Cloud player component. It can provide powerful playback functionality similar to Tencent Video with just a few lines of code. It has basic features such as landscape/portrait mode switching, definition selection, gestures, and small window playback, as well as special features such as video buffering, software/hardware decoding switching, and adjustable-speed playback. It supports more formats and has better compatibility and functionality than system-default players. In addition, it features instant broadcasting of the first frame and low latency and offers advanced capabilities like video thumbnail.

If the Player component cannot meet your custom requirements and you have development experience, you can integrate the RT-Cube Player as instructed in [VOD Scenario](https://cloud.tencent.com/document/product/881/20216) to customize the player UI and playback features.

## Prerequisites
1. Activate [VOD](https://cloud.tencent.com/product/vod). If you don't have an account yet, [sign up](https://cloud.tencent.com/login) first.
2. Download and install Xcode from App Store.
3. Download and install CocoaPods as instructed at the [CocoaPods website](https://cocoapods.org/).

## Content Summary
- [How to integrate the Tencent Cloud RT-Cube Player component for iOS](#step1)
- [How to create and use a player](#step3)

## Directions
[](id:step1)
### Step 1. Download the player code package
The Tencent Cloud RT-Cube Player for iOS can be downloaded [here](https://github.com/LiteAVSDK/Player_iOS).

You can download the Tencent Cloud RT-Cube Player for iOS by **[downloading the player component ZIP package](#zip)** or **[running the Git command](#git)**.
<dx-tabs>
::: Download the ZIP file[](id:zip)
Go to the Player GitHub page and click **Code** > **Download ZIP**.
![](https://qcloudimg.tencent-cloud.cn/raw/a38a9995bfe13d645bcd1d2e5242a297.png)
:::
::: Download using a Git command[](id:git)
1. First, make sure that your computer has Git installed; if not, you can install it as instructed in [Git Installation Tutorial](https://git-scm.com/downloads).
2. Run the following command to clone the code of the Player component to your local system.
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
(1) Directly integrate `SuperPlayer` as a Pod:
```objective-c
pod 'SuperPlayer
```
  To depend on the Player Edition, you can add the following dependency to the `podfile` file:
```objective-c
pod 'SuperPlayer/Player'
```
  To depend on the Professional Edition, you can add the following dependency to the `podfile` file:
```objective-c
pod 'SuperPlayer/Professional'
```

2. Run `pod install` or `pod update`.

:::
::: Manually download the SDK[](id:manual)
1. Download the SDK + demo package. The Tencent Cloud RT-Cube Player for iOS can be downloaded [here](https://github.com/LiteAVSDK/Player_iOS).
2. Import `TXLiteAVSDK_Player.framework` into your project and select **Do Not Embed**.
3. Copy `Demo/TXLiteAVDemo/SuperPlayerKit/SuperPlayer` to your project directory.
4. Third-party dependency libraries of `SuperPlayer` include `AFNetworking`, `SDWebImage`, `Masonry`, and `TXLiteAVSDK_Player`.
 1. To integrate `TXLiteAVSDK_Player` manually, you need to add the required system frameworks and libraries:
<b>System frameworks</b>: MetalKit, ReplayKit, SystemConfiguration, CoreTelephony, VideoToolbox, CoreGraphics, AVFoundation, Accelerate, MobileCoreServices, and VideoToolbox
<b>System libraries:</b> libz, libresolv, libiconv, libc++, and libsqlite3
For detailed directions, see [Integration Guide (Without UI)](https://cloud.tencent.com/document/product/266/73872).
In addition, you need to add `TXFFmpeg.xcframework` and `TXSoundTouch.scframework` under the `TXLiteAVSDK_Player` file as dynamic libraries.
![](https://qcloudimg.tencent-cloud.cn/raw/5834caae21d3413522c7d51d4b3b57b0.png)
 2. If you integrate `TXLiteAVSDK_Player` as a Pod, no libraries need to be added.


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
This step describes how to play back a video. The Tencent Cloud RT-Cube Player for iOS supports playback through [`FileId` in VOD](#fileid) or [URL](#url). We recommend you **integrate the `FileId`** to use complete capabilities.
<dx-tabs>
::: Play by VOD file ID[](id:fileid)
A video file ID is returned by the server after the video is uploaded.

1. After a video is published from a client, the server will return a file ID to the client.
2. When the video is uploaded to the server, its `FileId` will be included in the notification of the [upload confirmation](https://cloud.tencent.com/document/product/266/9757).
If the video you want to play is already saved with VOD, you can go to [Media Assets](https://console.cloud.tencent.com/vod/media) to view its file ID.
![](https://qcloudimg.tencent-cloud.cn/raw/f089346e01ab8e44e42f28c965809b9c.png)
<dx-alert infotype="notice">
<li>For playback through `FileId`, you need to first use the Adaptive-HLS(10) transcoding template to transcode the video or use the Player component signature `psign` to specify the video to be played back; otherwise, the video may fail to be played back. For more information on how to transcode a video, see [Stage 1. Play back a video with Player](https://intl.cloud.tencent.com/document/product/266/38098). For more information on how to generate a `psign`, see [Player Signature](https://intl.cloud.tencent.com/document/product/266/38099).</li>
<li>If a "no v4 play info" exception occurs during playback through `FileId`, the above problem may exist. In this case, we recommend you make adjustments as instructed above. You can also directly get the playback link of the source video for playback through [URL](#url).</li>
<li>**We recommend you transcode videos for playback because untranscoded videos may experience compatibility issues during playback.**</li></dx-alert>

<dx-codeblock>
:::  java
// If you haven’t enabled hotlink protection and a "no v4 play info" error occurs, please transcode your video using the Adaptive-HLS template (ID: 10) or get the playback URL of the video and play it by URL.

SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
model.appId = 1400329071;// Configure AppId
model.videoId = [[SuperPlayerVideoId alloc] init];
model.videoId.fileId = @"5285890799710173650"; // Configure `FileId`
// If you enable hotlink protection, you need to enter a `psign` (Player component signature) for playback. For more information on the signature and how to generate it, visit https://intl.cloud.tencent.com/document/product/266/38099.
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

At this point, you have integrated the player creation, video playback, and playback exiting capabilities of the Tencent Cloud RT-Cube Player for iOS.

[](id:moreFeature)
## More Features[](id:moreFeature)

### 1. Full screen playback

The Player component supports full screen playback, where it allows setting screen lock, volume and brightness control through gesture, on-screen commenting, screencapturing, and definition switch. This feature can be tried out in [**TCToolkit App**](#qrcode) > **Player** > **Player Component**, and you can enter the full screen playback mode by clicking the full screen icon.



You can call the API below to go full screen from the windowed playback mode:

```objective-c
- (void)superPlayerFullScreenChanged:(SuperPlayerView *)player {
  // You can customize the logic after switching to the full screen mode here
}
```

#### 


<dx-tabs>
::: Back to windowed mode[](id:window)
Click the back button to return to the windowed mode. The delegate method that will be triggered after the SDK implements the logic for exiting full screen is as follows:

```objective-c
// The back button clicking event
- (void)superPlayerBackAction:(SuperPlayerView *)player;
Triggered by clicking of the back button at the top left
// The exit full screen notification
- (void)superPlayerFullScreenChanged:(SuperPlayerView *)player;
```
:::
::: Disable touch screen[](id:screenlock)
Disabling touch screen allows users to enter an immersive playback mode. The SDK will handle the clicking event and no callbacks will be sent.

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
The Player component provides the feature of capturing the current video frame during playback, and you can save the screenshot for sharing. The clicking of the **Screencapture** button will be processed internally by the SDK without a callback for screencapturing success or failure, and the directory of the captured screenshots will be the phone album.
:::
::: Change resolution[](id:resolution)
Users can change the resolution (such as SD, HD, and UHD) during playback. After the resolution switching button is clicked, the SDK will implement the logic for displaying the resolution selection view and handle the resolution selection event. No callbacks will be sent.
:::
</dx-tabs>


### 2. Floating window playback

The Player component supports playback in a small floating window, which allows users to switch to another page of the application without interrupting the video playback. You can try out this feature in [**TCToolkit App**](#qrcode) > **Player** > **Player Component** by clicking **Back** in the top-left corner.



```objective-c
// Clicking the back button during playback in portrait mode will trigger the API
[SuperPlayerWindowShared setSuperPlayer:self.playerView];
[SuperPlayerWindowShared show];
// The API triggered by clicking the floating window to return to the main window
SuperPlayerWindowShared.backController = self;
```

### 3. Thumbnail

The Player component supports customizing a video thumbnail for display before the callback for playing back the first video frame is received. This feature can be tried out in [**TCToolkit App**](#qrcode) > **Player** > **Player Component** > **Thumbnail Customization Demo**.

* When the Player component is set to the automatic playback mode `PLAY_ACTION_AUTO_PLAY`, the video will be played back automatically, and the thumbnail will be displayed before the first video frame is loaded.
* When the Player component is set to the manual playback mode `PLAY_ACTION_MANUAL_PLAY`, the video will be played back only after the user clicks **Play**. The thumbnail will be displayed until the first video frame is loaded.

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

The Player component supports looping video lists.

* After a video ends, the next video in the list can be played automatically or users can manually start the next video.
* After the last video in the list ends, the first video in the list will start automatically.

This feature can be tried out in [**TCToolkit App**](#qrcode) > **Player** > **Player Component** > **Video List Loop Demo**.



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


### 5. Picture-in-Picture (PiP) feature

The Picture-in-Picture (PiP) feature has been launched on iOS 9 but could be used only on iPads. To use PiP on an iPhone, you need to update the iOS version to iOS 14.
Currently, Tencent Cloud RT-Cube Player supports PiP capabilities both in and outside the application, which meets users' requirements. To use the PiP feature, you need to enable the background mode as follows: In Xcode, select the target, click **Signing & Capabilities** > **Background Modes**, and select **Audio, AirPlay, and Picture in Picture**.
![](https://qcloudimg.tencent-cloud.cn/raw/116e1e741f80d810502221fd143d8434.png)



Code sample for using PiP capabilities:																								

```objective-c
// Enter the PiP mode
 if (![TXVodPlayer isSupportPictureInPicture]) {
    return;
 }
 [_vodPlayer enterPictureInPicture];

// Exit the PiP mode
[_vodPlayer exitPictureInPicture];
```

### 6. Preview

The Player component supports the video preview feature, which is suitable for non-VIP member preview. You can pass in different parameters to control the video preview duration, prompt message, and preview end screen. This feature can be tried out in [**TCToolkit App**](#qrcode) > **Player** > **Player Component** > **Preview Feature Demo**.



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

### 7. Dynamic watermark

The Player component allows you to add an irregular moving text watermark on the playback screen to prevent unauthorized recording. Watermarks can be displayed both in full screen playback mode and window playback mode. You can modify the watermark text, size, and color. This feature can be tried out in [**TCToolkit App**](#qrcode) > **Player** > **Player Component** > **Dynamic Watermark Demo**.



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
3. After running the demo successfully, go to **Player** > **Player Component** to try out the player features.

[](id:qrcode)
### TCToolkit app

You can try out more features of the Player component in **TCToolkit App** > **Player**.

<img src="https://qcloudimg.tencent-cloud.cn/raw/5c383bc7826d4f4835c9a7232cf9b50e.png" width="150">
