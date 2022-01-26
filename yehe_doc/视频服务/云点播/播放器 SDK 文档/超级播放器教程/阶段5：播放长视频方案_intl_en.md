This document describes how to use the superplayer to play back long videos common on audio/video platforms. It covers the web, iOS, and Android versions of the superplayer and also details the features of automatic adaptive bitstream switch, video thumbnail preview, and video timestamping.

## Overview
After reading this document, you will know:
- How to output adaptive bitstreams in VOD (a player can dynamically select the most appropriate bitrate for playback based on the current bandwidth).
- How to set video timestamps.
- How to use image sprite as thumbnail in VOD.
- How to use the player.

Before reading this document, make sure that you have read [Stage 1. Play back a video with superplayer](https://intl.cloud.tencent.com/document/product/266/38098) in the Superplayer Guide and understood the `fileid` concept of VOD.

## Directions
### Step 1. Output adaptive bitstream and image sprite
This step describes how to transcode a video to adaptive bitstream and output image sprite.
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod), select **Video Processing Settings** > **Template Settings** > **Adaptive Bitrate Streaming Template**, and click **Create Template**.
![](https://qcloudimg.tencent-cloud.cn/raw/e941daca088dbf5ca8a40384fc3ade7f.png)
Create the adaptive bitstream through the template as needed. This document creates an adaptive bitrate streaming template named `testAdaptive`, which contains three substreams with a resolution of 480p, 720p, and 1080p respectively. The video bitrate, video frame rate, and audio bitrate remain the same as the original video.
![](https://qcloudimg.tencent-cloud.cn/raw/21ee0dba1c79bde7bea922188d8f5b28.png)
2. Select **Video Processing Settings** > **Template Settings** > **Screencapturing Template** and click **Create Template**.
![](https://qcloudimg.tencent-cloud.cn/raw/8bac06234f924cc2d9327b6e9791157d.png)
Create the image sprite through the template as needed. This document creates an image sprite template named `testSprite`, with a sampling interval of 5%, 10 subimage rows, and 10 subimage columns.
![](https://qcloudimg.tencent-cloud.cn/raw/3f62b3d05600f729baa8fbe0f7f0e98c.png)
3. Add the adaptive bitrate streaming and image sprite templates through the task flow.
Select **Video Processing Settings** > **Task Flow Settings** > **Create Task Flow** and click **Create Task Flow**.
![](https://qcloudimg.tencent-cloud.cn/raw/bc6e4fcd4e53b050fa5f6d59d83608c8.png)
Add a task through the task flow as needed. To demonstrate the process of playing back adaptive bitstreams, this document creates a task flow named `testPlayVideo`, which only adds the adaptive bitrate streaming and image sprite templates.
![](https://qcloudimg.tencent-cloud.cn/raw/29ebf8e33157e9c342848c8f1c54ce6d.png)
4. Select **Video Management** > **Audio/Video Management**, select the video to be processed, and click **Video Processing** > **Adaptive Bitrate Streaming** > **Select Task Flow** to start the task.
![](https://qcloudimg.tencent-cloud.cn/raw/31392ed275f4406b73ceb2d3c866e3ad.png)
5. At this point, you can get the processed task result in **Audio/Video Management** > **Operation** > **Manage**.

### Step 2. Add video timestamps
This step describes how to add a set of video timestamps.
1. Go to VOD Server APIs > **Media Asset Management APIs** > [**ModifyMediaInfo**](https://intl.cloud.tencent.com/document/product/266/37570) and click **Debug** to enter the TencentCloud API console for debugging.
![](https://qcloudimg.tencent-cloud.cn/raw/69cc5e88d5858b25e6a21e59082c946a.png)
2. Add the specified video timestamps through the **AddKeyFrameDescs.N** parameter.
![](https://qcloudimg.tencent-cloud.cn/raw/85eb2701162edf90c309d161af2bff99.png)
At this point, you have completed the operation in the cloud, output the adaptive bitstreams and image sprite, and added the video timestamps.

### Step 3. Integrate the player
This step describes how to play back the adaptive bitstreams, thumbnails, and timestamps in the superplayer for web, iOS, and Android.

<dx-tabs>
::: Web
You need to integrate the RT-Cube Player as instructed in [Superplayer](https://intl.cloud.tencent.com/document/product/266/33976). After importing the player's SDK file, you can get the `appId` and `fileId` of media asset files from **Video Management** for playback.

The construction method of the player is `TCPlayer`, which can be used to create a player instance for playback.

#### 1. Place the player container in the HTML file

Place the player container in the desired place on the page. For example, add the following code to `index.html` (the container ID, width, and height can be customized).

```
<video id="player-container-id" width="414" height="270" preload="auto" playsinline webkit-playsinline>
</video>
```

#### 2. Play back with the fileID

Add the following initialization script to the `index.html` page initialization code to pass in the obtained `fileID` and `appID` for playback.

```
var player = TCPlayer('player-container-id', { // `player-container-id` is the player container ID, which must be the same as that in HTML
    fileID: '5285890799710670616', // Pass in the `fileID` of the video to be played back, which is required
    appID: '1400329073' // Pass in the `appID` of the VOD account, which is required
});
```


:::
::: iOS
You need to integrate the RT-Cube Player as instructed in [Superplayer](https://intl.cloud.tencent.com/document/product/266/33976). After integration, you can get the `appId` and `fileId` of media asset files from **Video Management** for playback.

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

#### Play back with fileId

```java
SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
model.appId = 1400329073;// Configure `AppId`
model.videoId = [[SuperPlayerVideoId alloc] init];
model.videoId.fileId = @"5285890799710670616"; // Configure `FileId`
[_playerView playWithModel:model];
```
:::
::: Android
You need to integrate the RT-Cube Player as instructed in [Superplayer](https://intl.cloud.tencent.com/document/product/266/33975). After integration, you can get the `appId` and `fileId` of media asset files from **Video Management** for playback.

The main class of the player is `SuperPlayerView`, and videos can be played back after it is created.

#### 1. Create the SuperPlayerView in the layout file

```xml
<!-- Superplayer -->
<com.tencent.liteav.demo.superplayer.SuperPlayerView
    android:id="@+id/superVodPlayerView"
    android:layout_width="match_parent"
    android:layout_height="200dp" />
```

#### 2. Play back with the fileId

```java
// Import `SuperPlayerView` into the layout file and create an instance
mSuperPlayerView = (SuperPlayerView) findViewById(R.id.superVodPlayerView);
// Hotlink protection disabled
SuperPlayerModel model = new SuperPlayerModel();
model.appId = 1400329073;// Configure `AppId`
model.videoId = new SuperPlayerVideoId();
model.videoId.fileId = "5285890799710670616"; // Configure `FileId`
mSuperPlayerView.playWithModel(model);
```
:::
</dx-tabs>


## Summary

At this point, you can view the image sprite and video timestamps and automatically switch dynamic adaptive bitstreams in the player. For more features, see [Feature Description](https://intl.cloud.tencent.com/document/product/266/42965).





