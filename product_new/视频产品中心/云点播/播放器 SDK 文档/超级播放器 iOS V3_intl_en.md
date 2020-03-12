## Overview

The Superplayer SDK for iOS is a player component used to play back videos in VOD. It can implement powerful playback functionality similar to Tencent Video with just a few lines of code.

* Basic features: landscape/portrait mode switch, definition selection, gestures, small window playback, etc.
* Advanced features: video buffering, software/hardware decoding switch, adjustable-speed playback, video thumbnails, DRM-encrypted playback, etc.

The Superplayer SDK supports more formats and has better compatibility and functionality than system-default players. In addition, it features instant playback on splash screen and low latency.

## SDK Download

The VOD Superplayer SDK for iOS can be downloaded [here](https://github.com/tencentyun/SuperPlayer_iOS).

## Quick Integration

### CocoaPods integration

Add the following code to your Podfile:
```
pod 'SuperPlayer'
```

Enter `pod install` or `pod update` on the command line to perform the installation.

### Preparing videos

Log in to the [VOD Console](https://console.cloud.tencent.com/vod/overview), click **Media Assets** on the left sidebar, and you will see the uploaded video and its corresponding ID (i.e., `FileId`) in the video list in the **Uploaded** column. If you don't have a video, please click **Upload Video** to upload one.
![](https://main.qcloudimg.com/raw/5aa5675fb0b702b447e422328f54cb72.png)

You can initiate an [adaptive bitrate streaming](https://intl.cloud.tencent.com/document/product/266/33942) task for the uploaded video through [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125):
You are recommended to enter 10 for `MediaProcessTask.AdaptiveDynamicStreamingTaskSet.Definition` in the API parameter, indicating transcoding to adaptive bitstream in HLS format.

### Starting playback

The main class of the player is `SuperPlayerView`, and videos can be played back after it is created.
```objective-c
// Import the header file
#import <SuperPlayer/SuperPlayer.h>
_playerView = [[SuperPlayerView alloc] init];
// Set the delegate to accept events
_playerView.delegate = self;
// Set the parent View; `_playerView` will be automatically added under `holderView`
_playerView.fatherView = self.holderView;
SuperPlayerModel *playerModel = [[SuperPlayerModel alloc] init];
SuperPlayerVideoId *video = [[SuperPlayerVideoId alloc] init];
// Set the playback information
video.appId = 1256993030;  //AppId
video.fileId = @"7447398157015849771";  // Video `FileId`
video.playDefinition = @"10";   // Playback template ID
video.version = FileIdV3;
playerModel.videoId = video;
// Start playback
[_playerView playWithModel:self.playerModel];
```

In the code, `appId` is your AppId, `fileId` is the ID of the video you want to play back, `playDefinition` is the ID of the playback template used for playback, and `version` is fixed to `SuperPlayerVideoId.FILE_ID_V3`.

Run the code and you can see that the video is played back on the phone and most of the features in the UI are available.
<img src="https://main.qcloudimg.com/raw/128c45edfc77b319475868c21caec2de.png" width="550">

## Thumbnails and Timestamps

When videos are played back, the "thumbnails" and "timestamps" on the progress bar can help viewers find the points of interest easily. Thumbnails are implemented through [image sprites](#APIhttps://intl.cloud.tencent.com/document/product/266/8101), while timestamps by [modifying timestamp information in media assets](#APIhttps://intl.cloud.tencent.com/document/product/266/31762#.E7.A4.BA.E4.BE.8B3-.E4.BF.AE.E6.94.B9.E5.AA.92.E4.BD.93.E6.96.87.E4.BB.B6.E8.A7.86.E9.A2.91.E6.89.93.E7.82.B9.E4.BF.A1.E6.81.AF).

After image sprites are generated and timestamps are added, new elements will be displayed in the player UI.
<img src="https://main.qcloudimg.com/raw/55ebce6d0c703dafa1ac131e1852e025.png" width="550">

## Small Window Playback

A small window is a player that floats over the main window within the application. Small window playback is very simple. You just need to call the following code in the appropriate position:

```objective-c
[SuperPlayerWindow sharedInstance].superPlayer = _playerView; // Set the player for small window playback
[SuperPlayerWindow sharedInstance].backController = self;  // Set the returned view controller
[[SuperPlayerWindow sharedInstance] show]; // Floating display
```
<img src="https://main.qcloudimg.com/raw/e2ee64230af1b9c3a79cad935afa8b6a.jpeg" width="300">

## Exiting Playback

If the player is no longer needed, please call `resetPlayer` to clear the internal state of the player and free up the memory.
```objective-c
[_playerView resetPlayer];
```

## More Features

To try out the complete features, scan the QR code below to download the Tencent Video Cloud toolkit or run the project demo directly.
<img src="https://main.qcloudimg.com/raw/b670e99ddb3f0d828798520e19f40fa7.png" width="150">
