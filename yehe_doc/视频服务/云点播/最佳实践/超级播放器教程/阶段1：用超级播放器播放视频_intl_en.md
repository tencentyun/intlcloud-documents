## Overview
This document describes how to upload a video to VOD, process it, and play it back in the superplayer.

## Prerequisites
Before using VOD, please make sure that you have met the following prerequisites:

### Activating VOD
You need to activate VOD in the following steps:

1. Sign up for a [Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).
2. For more information about VOD service billing, please see [Billing Overview] (https://intl.cloud.tencent.com/document/product/266/2838).
3. Select **Cloud Products** > **Video Services** > **[Video on Demand](https://console.cloud.tencent.com/vod)** to enter the VOD Console.

At this point, you have activated VOD.

### Disabling hotlink protection

You need to make sure that hotlink protection for your default distribution domain name is not enabled:

1. Log in to the VOD Console, select **Distribution and Playback Settings** > **[Domain Management](https://console.cloud.tencent.com/vod/distribute-play/domain)**, and click **Settings** of the "default distribution domain name" to enter the settings page.
<img src="https://main.qcloudimg.com/raw/06259e41a62ea14ce8eb19ef6480182c.png" width="800" />
2. Confirm that the statuses of **Referer Hotlink Protection** and **Key Hotlink Protection** are both "Not Enabled".
![](https://qcloudimg.tencent-cloud.cn/raw/12689eb5bed63fc76cd7d88e38907c09.png)


## Step 1. Upload and process a video
This step describes how to upload a video, transcode it to adaptive bitstream, and capture the cover and image sprite.

1. Log in to the VOD Console, select **Media Assets** > **[Video Management](https://console.cloud.tencent.com/vod/media)**, and click **Upload Video**.
![](https://main.qcloudimg.com/raw/b1ad4f0706ad1cd24044c8420a759868.png)
2. On the upload page, select **Local Upload**, click **Select Video** to upload a local video, and set other items as follows:
 * Select **Automatic Processing After Upload** as **Video Processing**.
 * Select **Task Flow** as **Processing Type**.
 * Select **LongVideoPreset** as **Task Flow Template**.
 >?`LongVideoPreset` is a preset task flow, which uses template 10 for adaptive bitrate streaming, template 10 for cover generating, and template 10 for image sprite capturing.
![](https://main.qcloudimg.com/raw/c5d53f748ce95ab0c8accea42687256a.png)
3. Click **Upload** to enter the "Uploading" page and wait for the upload to complete.
4. Select **Media Assets** > **[Video Management](https://console.cloud.tencent.com/vod/media)** and find the newly uploaded video (FileId: 528xxx3757278095). Here, the ID is the `FileId` of the uploaded video.
![](https://main.qcloudimg.com/raw/f2b3744a3c42a07863db0b7545dd892f.png)
>?Wait until the "video status" changes from **Processing** to **Normal**, which indicates that video processing is completed.
5. Click **Manage** in the "Operation" column of the newly uploaded video to enter the management page:
 - Select the **Basic Info** tab, and you can view the generated cover and output adaptive bitstream (template ID: 10).
 - Select the **Screenshot Info** tab, and you can view the generated image sprite (template ID: 10).

## Step 2. Preview video playback

In the previous step, you have uploaded and processed the video. Now, you can use the superplayer for web, iOS, and Android to quickly preview video playback.

1. Select **Media Assets** > **[Video Management](https://console.cloud.tencent.com/vod/media)**, find the video uploaded and processed in **step 1**, click **Manage** in the "Operation" column, and select **Superplayer Preview**.
2. Select "default" as **Superplayer Configuration**.
>? `default` is a preset superplayer configuration, which is used to output the adaptive bitstream with template 10 and the image sprite with template 10.
 <img src="https://main.qcloudimg.com/raw/17e2552964195c6919239d2d13a0d012.png" width="500" />
4. In **Web Player**, click the button in the middle of the player, and you can play back the video on web.
<img src="https://main.qcloudimg.com/raw/976ec23a988bcb494c4b225e635a5dba.png" width="522" />

## Step 3. Use a demo for verification

You can use the superplayer demos for [web](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html), [Android](https://github.com/tencentyun/SuperPlayer_Android), and [iOS](https://github.com/tencentyun/SuperPlayer_iOS) for verification. For more information, please see the demo source code.
>?In **Media Assets** > **[Video Management](https://console.cloud.tencent.com/vod/media)** > **Superplayer Preview** in the console, you can get the corresponding web player source code for video preview for your reference.
<img src="https://main.qcloudimg.com/raw/c5756910c7958aae198804c91b76a89e.png" width="500" />

## Summary

At this point, you have understood how to upload a video to VOD, process it, and play it back in the superplayer.

- If you want to play back a video after the key hotlink protection is enabled, please see [Stage 2. Play back a video with hotlink protection enabled](https://intl.cloud.tencent.com/document/product/266/38292).
- If you want to customize the content and style of a playback video, please see [Stage 3. Customize playback content and style](https://intl.cloud.tencent.com/document/product/266/38293).
- If you want to encrypt a video and then play back it, please see [Stage 4. Play back an encrypted video](https://intl.cloud.tencent.com/document/product/266/38294).
