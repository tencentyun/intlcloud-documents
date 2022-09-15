## Overview

This document describes how to customize the content and style of a video played back by the player, including:

* Set the resolution of a substream to be played back, which ranges from 480p to 1080p.
* Use a video screenshot as the video thumbnail.
* Adjust the preview thumbnail interval on the progress bar to 20%.

Before reading this document, make sure that you have read [Stage 1. Play back a video with Player](https://intl.cloud.tencent.com/document/product/266/38098) and [Stage 2. Play back a video with hotlink protection enabled](https://intl.cloud.tencent.com/document/product/266/38292) in the Player Guide. This document uses the account activated and the video uploaded in [stage 1](https://intl.cloud.tencent.com/document/product/266/38098), and hotlink protection needs to be enabled as instructed in [stage 2](https://intl.cloud.tencent.com/document/product/266/38292).

## Step 1. Create an adaptive bitrate streaming template

1. Log in to the VOD console, select **Video Processing** > **[Template Settings](https://console.cloud.tencent.com/vod/video-process/template)**, and click **Create Template** on the **Adaptive Bitrate Streaming** tab.
<img src="https://qcloudimg.tencent-cloud.cn/raw/19f292b6dbd89cf702ba27b3e9adf042.png" width="800" />
2. On the **Template Settings** page, click **Add Substream** to create substreams 1, 2, and 3, and enter the parameters as follows:
	- **Basic information module**
	  - **Template Name**: Enter `MyTestTemplate`.
	  - **Encryption Type**: Select **Not encrypted**.
	  - **Switch from Low Resolution to High Resolution**: Disable this option.

 - **Substream information module**
<table>
<thead>
<tr>
<th>Substream ID</th>
<th>Video Bitrate</th>
<th>Resolution</th>
<th>Frame Rate</th>
<th>Audio Bitrate</th>
<th>Sound Channel</th>
</tr>
</thead>
<tbody><tr>
<td>Substream 1</td>
<td>512 Kbps</td>
<td>The video long side: 0 px; the video short side: 480 px</td>
<td>24 fps</td>
<td>48 Kbps</td>
<td>Dual</td>
</tr>
<tr>
<td>Substream 2</td>
<td>512 Kbps</td>
<td>The video long side: 0 px; the video short side: 720 px</td>
<td>24 fps</td>
<td>48 Kbps</td>
<td>Dual</td>
</tr>
<tr>
<td>Substream 3</td>
<td>1024 Kbps</td>
<td>The video long side: 0 px; the video short side: 1,080 px</td>
<td>24 fps</td>
<td>48 Kbps</td>
<td>Dual</td>
</tr>
</tbody></table>

<img src="https://qcloudimg.tencent-cloud.cn/raw/995fcae82a8d2f1a27f0b128147c285b.png" width="500" />
3. Click **Create**. An adaptive bitrate streaming template containing three substreams will be generated, and the template ID will be `125866`.
![](https://qcloudimg.tencent-cloud.cn/raw/1b1ffba4a8c37c8d81132e8f93c801b6.png)

## Step 2. Create an image sprite template

1. Log in to the VOD console, select **Video Processing** > **[Template Settings](https://console.cloud.tencent.com/vod/video-process/template)**, and click **Create Screenshot Template** on the **Screenshot** tab.
2. On the **Template Settings** page, enter the template parameters:
 * **Template Name**: `MyTestTemplate`.
 * **Screenshot Type**: **Image sprite screenshot**.
 * **Image Dimension**: 726x240.
 * **Sampling Interval**: 20%.
 * **Rows**: 10.
 * **Columns**: 10.
![](https://qcloudimg.tencent-cloud.cn/raw/7ec21a1d127a0b5284a491fcac90c3a9.png)
3. Click **Create**. An image sprite template with the ID of `41377` will be generated.
![](https://qcloudimg.tencent-cloud.cn/raw/4cf44757d6dbb339aa29c3c29fc480d7.png)

## Step 3. Create a task flow and initiate processing

After creating an adaptive bitrate streaming template (ID: 125866) and an image sprite template (ID: 41377), you need to create a task flow.

1. Log in to the VOD console, select **Video Processing** > **[Task Flow Settings](https://console.cloud.tencent.com/vod/video-process/taskflow)**, and click **Create Task Flow**:
 * **Task Flow Name**: Enter `MyTestProcedure`.
 * **Task Type Configuration**: Select **Adaptive bitrate streaming**, **Screenshot*, and **Thumbnail**.
	 *  In the **Adaptive bitrate streaming task configuration** area, click **Add Template**, and select the custom adaptive bitrate streaming template **MyTestTemplate(126866)** created in **step 1** for **Adaptive Bitrate Streaming Template/ID**.
	 *  In the **Screenshot task configuration** area, click **Add Template**, and select **Image sprite** for **Method for Taking Screenshot** and the custom image sprite template **MyTestTemplate(41377)** created in **step 2** for **Screenshot/ID**.
	 *  In the **Configuration of task of capturing cover screenshot** area, click **Add Template**, select **TimepointScreenshot** for **Screenshot Template/ID**, and select **Percent** and enter "50%" for **Select by time points**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/0d91b5aeb8c2fe41d844e4c36c0a3d12.png" width="900" />
2. Click **Submit**. A task flow named `MyTestProcedure` will be generated.
![](https://main.qcloudimg.com/raw/e33008c55dcc18bed3b41f96d88c5c8c.png)
3. Select **Media Assets** > **[Video Management](https://console.cloud.tencent.com/vod/media)** in the console, select the target video (FileId: `528xxx3757278095`), and click **Process Video**.
4. In the video processing pop-up window:
 * Select **Task Flow** for **Processing Type**.
 * Select **MyTestProcedure** for **Task Flow Template**. <span></span>
 <img src="https://qcloudimg.tencent-cloud.cn/raw/649b07dfd248670d057795f3498b61ee.png" width="500" />
5. Click **Confirm** and wait until the **Video Status** changes from "Processing" to "Normal", which indicates that video processing is completed.
![](https://main.qcloudimg.com/raw/2894b49729ef223941360f2f814a63fa.png)
6. Click **Manage** in the **Operation** column of the video to enter the management page:
 * In the **Basic Info** tab, you can view the generated thumbnail and output adaptive bitstream (template ID: 125866).
 * In the **Screenshot Info** tab, you can view the generated image sprite (template ID: 41377).

## Step 4. Create a player configuration

To play back the custom adaptive bitstream and image sprite, you need to use a custom player configuration.

1. Log in to the VOD console, select **[Player Configuration](https://console.cloud.tencent.com/vod/distribute-play/super-player)**, and click **Create**.
2. On the player configuration page, add an adaptive bitrate streaming template and an image sprite template:
 * **Configuration Name**: `MyTestCfg`.
 * Select **MyTestTemplate(125866)** for **Adaptive Bitrate Streaming Template/ID**.
 * Select **MyTestTemplate(41377)** for **Screenshot Template**.
<img src="https://main.qcloudimg.com/raw/2459be6bd365e9a5143146d88d44a43c.png" width="400" />
3. Click **Confirm** to generate the player configuration `MyTestCfg`.

## Step 5. Preview video playback

In the previous step, you have processed the video. Now, you can use the player for web, iOS, and Android to quickly preview video playback.

1. Select the **Uploaded** tab in **[Video Management](https://console.cloud.tencent.com/vod/media)**, find the video uploaded and processed in previous steps, click **Manage** in the **Operation** column, and select the **Player Preview** tab.
2. Select **MyTestCfg** for **Playback Configuration**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/4a9ea4b96588c9a2fef0ac82c5ae27e7.png" width="522" />
3. As hotlink protection is enabled for the default distribution domain name, you can set the hotlink protection expiration time and the preview duration on the **Playback Control** tab. You can use the default parameter settings here (the default expiration time of playback hotlink protection is one day, and the preview duration and maximum number of IPs allowed for playback are left empty).
 <img src="https://qcloudimg.tencent-cloud.cn/raw/b5d25e5c5cd9f55cf14be336f4abd967.png" width="522" />
4. In **Web Player**, click the button in the middle of the player to play back the video on web.
<img src="https://main.qcloudimg.com/raw/976ec23a988bcb494c4b225e635a5dba.png" width="522" />
5. In **Mobile Player**, click **Scan code to download** and install "Tencent Cloud Toolkit".
<img src="https://qcloudimg.tencent-cloud.cn/raw/f0e72b414ee3dc8084dda39d8a5d5c91.png" width="522" />
6. Open Tencent Cloud Toolkit on your mobile phone, select **Player**, click the top-right corner to scan the QR code, and you can play back the video on your phone.
 <img src="https://qcloudimg.tencent-cloud.cn/raw/06e77f14c2e1020e8936ce1ab30a6ca3.png" width="422" />

## Step 6. Use a demo for verification

After hotlink protection is enabled, the player requires a signature within its validity period to play back the video. You can use the signature tool to quickly generate a signature as detailed below.

1. Enter the [Player - Signature Generation Tool](https://vods.cloud.tencent.com/signature/super-player-sign.html) page and enter the following parameters:
 * **User appId**: `appId` of video `1400xxx357`(if a subapplication is used, enter the subapplication's `appId`).
 * **Video fileId**: Video `FileId`, which is `528xxx3757278095`.
 * **Current Unix Timestamp**: Current Unix time automatically generated by the tool, which does not need to be entered manually and is `1591756516` here.
 * **Player Configuration**: Custom player configuration name, which is `MyTestCfg` here.
 * **Signature Expiration Unix Timestamp**: Signature expiration time, which can be left empty. The signature will expire in one day by default.
 * **Link Expiration Time**: Expiration time of key hotlink protection, which can be set to the hexadecimal Unix time after six hours: `5ee09b44`.
 * **Hotlink Protection Key**: Previously obtained hotlink protection key, which is `2WExxx48eW`.
2. Click **Generate Signature**, and the generated signature will be displayed in the "Signature Generation Result" text box.

After getting the player signature, you can use the player demos for [web](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html), [Android](https://github.com/LiteAVSDK/Player_Android), and [iOS](https://github.com/LiteAVSDK/Player_iOS) for verification. For more information, see the demo source code.
>? In **Media Assets** > **[Video Management](https://console.cloud.tencent.com/vod/media)** > **Player Preview** in the console, you can get the corresponding web player source code for video preview for your reference.
<img src="https://main.qcloudimg.com/raw/c5756910c7958aae198804c91b76a89e.png" width="500" />

## Summary

At this point, you have understood how to customize the content and style of a video played back by the player.
If you want to encrypt a video and play back the encrypted video, see [Stage 4. Play back an encrypted video](https://intl.cloud.tencent.com/document/product/266/38294).
