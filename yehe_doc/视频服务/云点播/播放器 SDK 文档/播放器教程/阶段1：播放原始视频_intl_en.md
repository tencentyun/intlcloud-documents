## Overview
This document describes how to upload a video to VOD and play it back in the player.

## Prerequisites
Before you start, do the following:

### Activating VOD
Follow the steps below to activate VOD:

1. [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).
2. Purchase VOD services. For details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/266/2838).
3. Go to the [VOD console](https://console.cloud.tencent.com/vod).

At this point, you have activated VOD.

## Step 1. Upload a video
This step describes how to upload a video.

1. Log in to the VOD console, select **Media Assets** > **[Video/Audio Management](https://console.cloud.tencent.com/vod/media)**, and click **Upload**.
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/eDZY097_1.jpg" width="722" />

2. On the upload page, select **Local Upload**, click **Select** to upload a local video, and set other fields as follows:
	- Select **No processing after upload** for **Process Video**.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/zB6K038_2.jpg)

3. Click **Upload** to enter the **Uploading** page. When **Status** changes to **Uploaded successfully**, the upload is completed. **File ID** is the `FileId` of the uploaded file (387xxxxx8142975036 here).
![](https://staticintl.cloudcachetci.com/yehe/backend-news/nMEx197_3.jpg)

## Step 2. Generate a Player Signature
In this step, you can use the signature tool to quickly generate a signature for the player to play back the video.
Select **Distribution and Playback** > [**Player Signature Tools**](https://console.cloud.tencent.com/vod/distribute-play/signature) and enter the following information:
 - **Video file ID**: Enter the `FileId` (387xxxxx8142975036) used in **step 1**.
 - **Signature expiration time**: Enter the player signature expiration time. If you leave it empty, the signature will never expire.
 - **Playable video type**: Select **Original**.

Click **Generate** to get the signature string.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/3pgW155_4.jpg" width="800" />

## Step 3. Play back the video
After step 2, you have obtained the three parameters needed for video playback: `appId`, `fileId` and `psign` (player signature). The following describes how to play back the video on the web.

### Playback on the web
Open the [web player demo](https://tcplayer.vcube.tencent.com/) and configure it as follows:
 - **Player feature**: Select **Video playback**.
 - Click the **Play by FileID** tab.
 - **fileID**: Enter the `FileId` in the previous step (387xxxxx8142975036).
 - **appID**: Enter the `appId` to which the file belongs, i.e., the `appID` on the player signature generation page in the previous step.
 - **psign**: Enter the signature string generated in the previous step.

Click **Preview** to play back the video.
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/SfPg988_5.png" width="800" />

### Multi-platform player demos
After getting the player signature, you can use the player demos for [web](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html), [Android](https://github.com/LiteAVSDK/Player_Android), and [iOS](https://github.com/LiteAVSDK/Player_iOS) for verification. For more information, see the demo source code.


## Summary

At this point, you have understood how to upload a video to VOD and play it back in the player.

You can also:
- Play back a transcoded video as instructed in [Stage 2. Play back a transcoded video](https://www.tencentcloud.com/document/product/266/51565).
- Play back an adaptive bitrate streaming video as instructed in [Stage 3. Play back an adaptive bitrate streaming video](https://www.tencentcloud.com/document/product/266/51566).
- Play back an encrypted video as instructed in [Stage 4. Play back an encrypted video](https://www.tencentcloud.com/document/product/266/51556).
- Play back a long video as instructed in [Stage 5. Play back a long video](https://www.tencentcloud.com/document/product/266/51557)
