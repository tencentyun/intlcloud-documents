## Overview
This document describes how to encrypt a video and use the player to play back the encrypted video.
Before reading this document, make sure that you have read [Stage 1. Play back a source video](https://www.tencentcloud.com/document/product/266/51564) in the Player Guide. This document uses the account activated and the video uploaded in [stage 1](https://intl.cloud.tencent.com/document/product/266/38098).

## Step 1. Encrypt a video
1. In the VOD console, select **Media Assets** > [Video/Audio Management](https://console.cloud.tencent.com/vod/media) on the left sidebar, select the target video (in this example, the file ID of the video processed is `387xxxxx8142975036`), and click **Process**.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/7ut4367_1.jpg" width="622" />

2. On the **Process** page:
 - Select **Task Flow** as the **Processing Type**.
 * Select **SimpleAesEncryptPreset** for **Task Flow Template**.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/GkuI523_2.jpg" width="" style="zoom:100%;" /><span>

>?
>- **SimpleAesEncryptPreset** is a preset task flow, which uses template 12 for adaptive bitrate streaming, template 10 for thumbnail generating, and template 10 for image sprite capturing.
>- Adaptive bitrate streaming with template 12 is to output an encrypted multi-bitrate stream.

3. Click **Confirm**, and then go to the [Task Management](https://console.cloud.tencent.com/vod/task) page to view the status of the task. When the **Task Status** changes from **Processing** to **Completed**, it indicates that video processing is complete.
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/hUM7408_3.png" style="zoom:80%;" />

4. Go to **Media Assets** > [**Video/Audio Management****](https://console.cloud.tencent.com/vod/media) and click **Manage** on the right of the target video to enter the management page:

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/ETsG597_4.jpg" width="800" />

Select the **Basic Info** tab:
 - You can view the thumbnail generated and outputs of encrypted adaptive bitrate streaming (template ID: 12).

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/KBkV486_5.jpg" width="622" />
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/5NsV447_6.jpg" width="700" />

 Select the **Screenshot Info** tab:
 - You can view the image sprite generated (template ID: 10).

 <img src="https://staticintl.cloudcachetci.com/yehe/backend-news/XTu8560_7.jpg" width="700" />

## Step 2. Generate a Player Signature
In this step, you can use the signature tool to quickly generate a signature for the player to play back the video.
Select **Distribution and Playback** > [**Player Signature Tools**](https://console.cloud.tencent.com/vod/distribute-play/signature) and enter the following information:
 - **Video file ID**: Enter the `FileId` (387xxxxx8142975036) used in **step 1**.
 - **Signature expiration time**: Enter the player signature expiration time. If you leave it empty, the signature will never expire.
 - **Playable video type**: Select **Encrypted adaptive bitrate**.
 - **Encryption type**: Select **Private encryption (SimpleAES)**.
 - **Playable adaptive bitrate streaming template**: Select `Adpative-HLS-Encrypt (12)`.
 - **Image sprite template for thumbnail preview**: Select `SpriteScreenshot (10)`.

Click **Generate** to get the signature string.

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
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/Eapx633_9.png" width="800" />

### Multi-platform player demos
After getting the player signature, you can use the player demos for [web](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html), [Android](https://github.com/LiteAVSDK/Player_Android), and [iOS](https://github.com/LiteAVSDK/Player_iOS) for verification. For more information, see the demo source code.


## Summary

At this point, you have understood how to encrypt a video and use the player to play it back.
