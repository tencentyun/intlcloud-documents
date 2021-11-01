## Overview

This document describes how to customize the content and style of a video played back by the superplayer, including:

* Set the resolution of a substream to be played back, which ranges from 480p to 1080p.
* Use a video screenshot as the video cover.
* Adjust the preview thumbnail interval on the progress bar to 20%.

Before reading this document, please make sure that you have read [Stage 1. Play back a video with superplayer](https://intl.cloud.tencent.com/document/product/266/38098) and [Stage 2. Play back a video with hotlink protection enabled](https://intl.cloud.tencent.com/document/product/266/38292) in the Superplayer Guide. This document uses the account activated and the video uploaded in [stage 1](https://intl.cloud.tencent.com/document/product/266/38098), and hotlink protection needs to be enabled as instructed in [stage 2](https://intl.cloud.tencent.com/document/product/266/38292).

## Step 1. Create an adaptive bitrate streaming template

1. Log in to the VOD Console, select **Video Processing Settings** > **[Template Settings](https://console.cloud.tencent.com/vod/video-process/template)**, and click **Create Template** on the **Adaptive Bitrate Streaming Template** tab.
<img src="https://qcloudimg.tencent-cloud.cn/raw/19f292b6dbd89cf702ba27b3e9adf042.png" width="800" />
2. Enter the **Template Settings** page, click **Add Substream** to create substreams 1, 2, and 3, and enter the parameters as follows:
	- **Basic information module**
	  - **Template Name**: enter `MyTestTemplate`.
	  - **Encryption Type**: select **Not encrypted**.
	  - **Allow Transcoding from Low Resolution to High Resolution**: disable this option.
	  
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
<td>Video long side: 0 px; video short side: 480 px</td>
<td>24 fps</td>
<td>48 Kbps</td>
<td>Dual</td>
</tr>
<tr>
<td>Substream 2</td>
<td>512 Kbps</td>
<td>Video long side: 0 px; video short side: 720 px</td>
<td>24 fps</td>
<td>48 Kbps</td>
<td>Dual</td>
</tr>
<tr>
<td>Substream 3</td>
<td>1,024 Kbps</td>
<td>Video long side: 0 px; video short side: 1,080 px</td>
<td>24 fps</td>
<td>48 Kbps</td>
<td>Dual</td>
</tr>
</tbody></table>
<img src="https://qcloudimg.tencent-cloud.cn/raw/995fcae82a8d2f1a27f0b128147c285b.png" width="500" />
3. Click **Create**, an adaptive bitrate streaming template containing three substreams will be generated, and the template ID will be `1145464`.

![](https://qcloudimg.tencent-cloud.cn/raw/1b1ffba4a8c37c8d81132e8f93c801b6.png)

## Step 2. Create an image sprite template

1. Log in to the VOD Console, select **Video Processing Settings** > **[Template Settings](https://console.cloud.tencent.com/vod/video-process/template)**, and click **Create Template** on the **Screencapturing Template** tab.
2. On the "Template Settings" page, enter the template parameters:
 * **Template Name**: `MyTestTemplate`.
 * **Template Type**: **Image Sprite Screencapturing**.
 * **Image Dimension**: 726x240.
 * **Sampling Interval**: 20%.
 * **Rows**: 10.
 * **Columns**: 10.
![](https://qcloudimg.tencent-cloud.cn/raw/9c0f52f7a6948f693ddc2e7bda48462a.png)
3. Click **Create**, and an image sprite template whose ID is `113272` will be generated.
![](https://qcloudimg.tencent-cloud.cn/raw/4cf44757d6dbb339aa29c3c29fc480d7.png)

## Step 3. Create a task flow and initiate processing

After creating an adaptive bitrate streaming template (ID: 1145464`) and an image sprite template (ID: 113272), you need to create a task flow.

1. Log in to the VOD Console, select **Video Processing Settings** > **[Task Flow Settings](https://console.cloud.tencent.com/vod/video-process/taskflow)**, and click **Create Task Flow**: **Task Flow Name**: enter `MyTestProcedure`.
 * **Task Type**: check **Adaptive bitrate streaming**, **Screencapturing**, and **Cover capturing**: On the **Adaptive bitrate streaming task configuration** tab, click **Add Template**, and select the custom adaptive bitrate streaming template `MyTestTemplate(1145464)` created in **step 1** as "Adaptive Bitrate Streaming Template/ID".
	 *  On the **Screencapturing task configuration** tab, click **Add Template**, and select **Image Sprite** as "Screencapturing Method" and the custom image sprite template `MyTestTemplate(113272)` created in **step 2** as "Screencapturing Template".
	 *  On the **Cover capturing task configuration** tab, click **Add Template**, select **TimepointScreenshot** as "Screencapturing Template", and select **Percentage** and enter "50%" for "Time Point Selection".
<img src="https://qcloudimg.tencent-cloud.cn/raw/0d91b5aeb8c2fe41d844e4c36c0a3d12.png" width="900" />
2. Click **Submit**, and a task flow named `MyTestProcedure` will be generated.
![](https://main.qcloudimg.com/raw/e33008c55dcc18bed3b41f96d88c5c8c.png)
3. Select **Media Assets** > **[Video Management](https://console.cloud.tencent.com/vod/media)** in the console, select the target video (FileId: 528xxx3757278095), and click **Process Video**.
4. In the video processing pop-up window:
 * Select **Task Flow** as **Processing Type**.
 * Select **MyTestProcedure** as **Task Flow Template**. <span></span>
 <img src="https://qcloudimg.tencent-cloud.cn/raw/649b07dfd248670d057795f3498b61ee.png" width="500" />
5. Click **OK** and wait until the **video status** changes from "Processing" to "Normal", which indicates that video processing is completed.
![](https://main.qcloudimg.com/raw/2894b49729ef223941360f2f814a63fa.png)
6. Click **Manage** in the "Operation" column of the video to enter the management page:
 * In the **Basic Info** column, you can view the generated cover and output adaptive bitstream (template ID: 1145464).
 * In the **Screenshot Info** column, you can view the generated image sprite (template ID: 113272).

## Step 4. Create a superplayer configuration

To play back the custom adaptive bitstream and image sprite, you need to use a custom player configuration.

1. Log in to the VOD Console, select **Distribution and Playback Settings** > **[Superplayer Configuration](https://console.cloud.tencent.com/vod/distribute-play/super-player)**, and click **Create**.
2. On the superplayer configuration page, click **Add Adaptive Bitrate Streaming Template** and **Add Image Sprite Template**, and enter the following parameters for the two templates, respectively:
 * **Template Name**: `MyTestCfg`.
 * On the **Adaptive Bitstream for Playback** tab, select `MyTestTemplate(1145464)` as "Adaptive Bitrate Streaming Template/ID".
 * On the **Image Sprite for Playback** tab, select `MyTestTemplate` as "Screencapturing Template".
<img src="https://main.qcloudimg.com/raw/2459be6bd365e9a5143146d88d44a43c.png" width="400" />
3. Click **OK** to generate the superplayer configuration `MyTestCfg`.

## Step 5. Preview video playback

In the previous step, you have processed the video. Now, you can use the superplayer for web, iOS, and Android to quickly preview video playback.

1. Select the "Uploaded" tab in **[Video Management](https://console.cloud.tencent.com/vod/media)**, find the video uploaded and processed in previous steps, click **Manage** in the "Operation" column, and select the **Superplayer Preview** tab.
2. Select "MyTestCfg" as **Playback Configuration**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/4a9ea4b96588c9a2fef0ac82c5ae27e7.png" width="522" />
3. As hotlink protection is enabled for the default distribution domain name, you can set the hotlink protection expiration time and the preview duration on the **Playback Control** tab. You can use the default parameter settings here (the default expiration time of playback hotlink protection is 1 day, and the preview duration and maximum number of IPs allowed for playback are left empty).
  <img src="https://qcloudimg.tencent-cloud.cn/raw/b5d25e5c5cd9f55cf14be336f4abd967.png" width="522" />
4. In **Web Player**, click the button in the middle of the player, and you can play back the video on web.
<img src="https://main.qcloudimg.com/raw/976ec23a988bcb494c4b225e635a5dba.png" width="522" />

## Step 6. Use a demo for verification

After hotlink protection is enabled, the superplayer requires a signature within its validity period to play back the video. You can use the signature tool to quickly generate a signature as shown below.

1. Enter the [Superplayer - Signature Generation Tool](https://vods.cloud.tencent.com/signature/super-player-sign.html) page and enter the following parameters:
 * **User appId**: `appId` of video `1400xxx357`(if a subapplication is used, enter the subapplication's `appId`).
 * **Video fileId**: video `FileId`, which is `528xxx3757278095`.
 * **Current Unix Timestamp**: current Unix time automatically generated by the tool, which does not need to be entered manually and is `1591756516` here.
 * **Superplayer Configuration**: custom superplayer configuration name, which is `MyTestCfg` here.
 * **Signature Expiration Unix Timestamp**: signature expiration time, which can be left empty. The signature will expire in 1 day by default.
 * **Link Expiration Time**: expiration time of key hotlink protection, which can be set to the hexadecimal Unix time after 6 hours: `5ee09b44`.
 * **Hotlink Protection Key**: previously obtained hotlink protection key, which is `2WExxx48eW`.
2. Click **Generate Signature**, and the generated signature will be displayed in the "Signature Generation Result" text box.

 <img src="https://main.qcloudimg.com/raw/132832fdc9e28f4e1377b6cdaaee5b53.png" width="522" />
After getting the superplayer signature, you can use the superplayer demos for [web](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html), [Android](https://github.com/tencentyun/SuperPlayer_Android), and [iOS](https://github.com/tencentyun/SuperPlayer_iOS) for verification. For more information, please see the demo source code.
>?In **Media Assets** > **[Video Management](https://console.cloud.tencent.com/vod/media)** > **Superplayer Preview** in the console, you can get the corresponding web player source code for video preview for your reference.
<img src="https://main.qcloudimg.com/raw/c5756910c7958aae198804c91b76a89e.png" width="500" />

## Summary

At this point, you have understood how to customize the content and style of a video played back by the superplayer.
If you want to encrypt a video and play back the encrypted video, please see [Stage 4. Play back an encrypted video](https://intl.cloud.tencent.com/document/product/266/38294).
