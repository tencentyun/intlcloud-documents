This document describes how to use the player to play back long videos common on audio/video platforms. It covers the web, iOS, and Android versions of the player and also details the features of [key hotlink protection](https://www.tencentcloud.com/document/product/266/49274), adaptive bitrate streaming, video thumbnail preview, and video timestamping.

## Overview
After reading this document, you will know:
- How to configure key hotlink protection, which allows you to set the validity period, number of viewers, playback duration, etc.
- How to output adaptive bitstreams in VOD (a player can dynamically select the most appropriate bitrate for playback based on the current bandwidth).
- How to set video timestamps.
- How to use an image sprite as a thumbnail in VOD.
- How to use the player.

Before reading this document, make sure that you have read [Stage 1. Play back a video with Player](https://intl.cloud.tencent.com/document/product/266/38098) in the Player Guide and understand the concept of `fileid` in VOD.

## Directions
### Step 1. Enable key hotlink protection
The following takes enabling key hotlink protection for the default distribution domain name under your account as an example:
>!Do not directly enable hotlink protection for the domain name in your production environment; otherwise, playback of videos in the production environment may fail.

1. Log in to the VOD console, select **Distribution and Playback** > **[Domain Name](https://console.cloud.tencent.com/vod/distribute-play/domain)** to enter the settings page.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/pyHf434_1.png" width="800" />

2. Click the **Access Control** tab, find **Key Hotlink Protection**, click the gray button to enable it, click **Generate** in the pop-up window to generate a random key, and click **OK** to save the configuration and make it take effect.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/azQ5558_2.jpg" width="522" />

### Step 2. Output adaptive bitstream and image sprite
This step describes how to transcode a video to adaptive bitstream and output image sprite.
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod), select **Video Processing Settings** > **Template Settings** > **Adaptive Bitrate Streaming Template**, and click **Create Template**.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/3gkP770_3.png)

Create the adaptive bitstream through the template as needed. The following example shows an adaptive bitrate streaming template named `testAdaptive`, which contains three substreams with a resolution of 480p, 720p, and 1080p. The video bitrate, video frame rate, and audio bitrate are the same as the original video.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/XIga303_4.jpg)

2. Select **Video Processing Settings** > **Template Settings** > **Screenshot Template** and click **Create Template**.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/mVrf686_5.png)

Create the image sprite through the template as needed. The following example shows an image sprite template named `testSprite`, with a sampling interval of 5%, 10 rows, and 10 columns.

![](https://qcloudimg.tencent-cloud.cn/raw/3f62b3d05600f729baa8fbe0f7f0e98c.png)

3. Add the adaptive bitrate streaming and image sprite templates through the task flow.
Select **Video Processing** > **Task Flow Settings** and click **Create Task Flow**.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/sUGF476_7.jpg)

Add a task through the task flow as needed. The following example shows a task flow named `testPlayVideo`, which only adds the adaptive bitrate streaming and image sprite templates from the previous examples.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/4e45517_8.jpg)

4. Select **Media Assets** > **Video/Audio Management**, select the target video (FileId: 387xxxxx8142975036), click **Task Flow**, and select a task flow template to start the task.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/LAPx726_9.png)

5. At this point, you can view the task execution status in the [**Task Managment**](https://console.cloud.tencent.com/vod/task) page and get the task result after completion.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/wrMs396_10.jpg" width="800" />

### Step 3. Add video timestamps
This step describes how to add a set of video timestamps.
1. Go to VOD Server APIs > **Media Asset Management APIs** > [**ModifyMediaInfo**](https://intl.cloud.tencent.com/document/product/266/37570) and click **Debug** to enter the TencentCloud API console for debugging.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/3hHA645_11.jpg)
2. Add the specified video timestamps through the **AddKeyFrameDescs.N** parameter.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/dpvW350_12.jpg)
At this point, you have completed the operation in the cloud, output the adaptive bitstreams and image sprite, and added the video timestamps.

### Step 4. Generate a player signature
In this step, you can use the signature tool to quickly generate a signature for the player to play back the video.
Select **Distribution and Playback** > [**Player Signature Tools**](https://console.cloud.tencent.com/vod/distribute-play/signature) and enter the following information:
 - **Video file ID**: Enter the `FileId` (387xxxxx8142975036) used in **step 2**.
 - **Signature expiration time**: Enter the player signature expiration time. If you leave it empty, the signature will never expire.
 - **Playable video type**: Select **Unencrypted adaptive bitrate**.
 - **Playable adaptive bitrate streaming template**: Select `testAdaptive (1429229)`.
 - **Image sprite template for thumbnail preview**: Select `testSprite (131353)`.
 - **Hotlink protection and encryption**: Toggle it on and configure as follows:
  - **Link expiration time**: Set it to the expiration time of the obtained hotlink protection signature.
  - **Maximum playback IPs**: Set the maximum number of IPs allowed for playback.

Click **Generate** to get the signature string.


### Step 5. Integrate the player
After step 4, you have obtained the three parameters needed for video playback: `appId`, `fileId` and `psign` (player signature).
This step describes how to play back the adaptive bitstreams, thumbnails, and timestamps in the player for web, iOS, and Android.

<dx-tabs>
::: Web
You need to integrate the RT-Cube Player as instructed in [Web integration](https://intl.cloud.tencent.com/document/product/266/33977). After importing the player's SDK file, you can play back the video by using the `appId`, `fileId`, and `psign`.

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
var player = TCPlayer('player-container-id', { // player-container-id is the player container ID, which must be the same as that in HTML
    fileID: '387xxxxx8142975036', // `fileID` of the video to be played back
    appID: '1400329073', // `appID` of the VOD account to play back the video
    psign:'psignxxxx'   // `psign` is a player signature. For more information on the signature and how to generate it, see [Player Signature](https://www.tencentcloud.com/document/product/266/38099).
});
```


:::
::: iOS
You need to integrate the RT-Cube Player as instructed in [iOS Integration](https://www.tencentcloud.com/document/product/266/49649). Then, you can play back the video by using the `appId`, `fileId`, and `psign`.

The main class of the player is `SuperPlayerView`, and videos can be played back after it is created.

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

#### Playing back with the `fileId`

```java
SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
model.appId = 1400329073;// Configure AppId
model.videoId = [[SuperPlayerVideoId alloc] init];
model.videoId.fileId = @"387xxxxx8142975036"; // Configure `FileId`
// `pSign` is a player signature. For more information on the signature and how to generate it, see [Player Signature](https://www.tencentcloud.com/document/product/266/38099).
model.videoId.pSign = @"psignxxxx";
[_playerView playWithModelNeedLicence:model];
[_playerView playWithModel:model];
```
:::
:::  Android
You need to integrate the RT-Cube Player as instructed in [Android integration](https://intl.cloud.tencent.com/document/product/266/33975). Then, you can play back the video by using the `appId`, `fileId`, and `psign`.

The main class of the player is `SuperPlayerView`, and videos can be played back after it is created.

#### 1. Create the SuperPlayerView in the layout file

```xml
<!-- Player -->
<com.tencent.liteav.demo.superplayer.SuperPlayerView
    android:id="@+id/superVodPlayerView"
    android:layout_width="match_parent"
    android:layout_height="200dp" />
```

#### 2. Play back with the fileId

```java
// Import `SuperPlayerView` into the layout file and create an instance
mSuperPlayerView = (SuperPlayerView) findViewById(R.id.superVodPlayerView);

SuperPlayerModel model = new SuperPlayerModel();
model.appId = 1400329073;// Configure AppId
model.videoId = new SuperPlayerVideoId();
model.videoId.fileId = "387xxxxx8142975036"; // Configure `FileId`
// `pSign` is a player signature. For more information on the signature and how to generate it, see [Player Signature](https://www.tencentcloud.com/document/product/266/38099).
model.videoId.pSign = "psignxxxx";

mSuperPlayerView.playWithModel(model);
```
:::
</dx-tabs>


## Summary

At this point, you can play back media files with hotlink protection enabled, view the image sprite and video timestamps, and automatically switch dynamic adaptive bitstreams in the player.
For more features, see [Feature Description](https://intl.cloud.tencent.com/document/product/266/42965).
