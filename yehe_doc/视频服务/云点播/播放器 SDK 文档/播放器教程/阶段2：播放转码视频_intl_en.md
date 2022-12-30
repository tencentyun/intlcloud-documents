## Overview
This document describes how to transcode a video and use the player to play back the output video.
Before reading this document, make sure that you have read [Stage 1. Play back a source video](https://www.tencentcloud.com/document/product/266/51564) in the Player Guide. This document uses the account activated and the video uploaded in [stage 1](https://intl.cloud.tencent.com/document/product/266/38098).

## Step 1. Transcode a video
1. In the VOD console, select **Media Assets** > [Video/Audio Management](https://console.cloud.tencent.com/vod/media) on the left sidebar, select the target video (in this example, the file ID of the video encrypted is `387xxxxx8142975036`), and click **Process**.
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/3unX216_1.png" width="800" />

2. On the **Process** page:
 - Select **Transcoding** for **Processing Type**.
 - Click **Select template** for **Transcoding Template**.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/U4VK178_2.png" width="522" />

On the transcoding template selection page that pops up, select template `STD-H264-MP4-540P` (ID: `100020`):
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/xtzd936_3.png" width="622" />

Click **Confirm** to start the transcoding task.
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/pahm058_4.png" width="550" />

3. Go to the [**Task Management**](https://console.cloud.tencent.com/vod/task) page to view the status of the task. When the **Task Status** changes from **Processing** to **Completed**, it indicates that video processing is completed.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/Q4bA978_5.png" width="800" />

4. Go to **Media Assets** > [**Video/Audio Management****](https://console.cloud.tencent.com/vod/media) and click **Manage** on the right of the target video to enter the management page:

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/Mfdx017_6.png" width="800" />

Select the **Basic Info** tab:
 - You can see the list of templates that have been successfully used for transcoding in the **Standard Transcoding List**.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/LJcj256_7.jpg" width="700" />

## Step 2. Generate a Player Signature
In this step, you can use the signature tool to quickly generate a signature for the player to play back the video.
Select **Distribution and Playback** > [**Player Signature Tools**](https://console.cloud.tencent.com/vod/distribute-play/signature) and enter the following information:
 - **Video file ID**: Enter the `FileId` (387xxxxx8142975036) used in **step 1**.
 - **Signature expiration time**: Enter the player signature expiration time. If you leave it empty, the signature will never expire.
 - **Playable video type**: Select **Transcoding**.
 - **Playable transcoding template**: Select `STD-H264-MP4-540P (100020)`.

Click **Generate** to get the signature string.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/SpCE136_8.png" width="800" />

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
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/kzkm097_9.png" width="800" />

### Multi-platform player demos
After getting the player signature, you can use the player demos for [web](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html), [Android](https://github.com/LiteAVSDK/Player_Android), and [iOS](https://github.com/LiteAVSDK/Player_iOS) for verification. For more information, see the demo source code.


## Summary

At this point, you have understood how to transcode a video and use the player to play it back.
