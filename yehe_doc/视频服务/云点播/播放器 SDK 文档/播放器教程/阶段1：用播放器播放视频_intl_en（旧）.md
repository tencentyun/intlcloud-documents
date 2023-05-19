## Overview
This document describes how to upload a video to VOD, process it, and play it back in the player.

## Prerequisites
Before you start, do the following:

### Activate VOD
Follow the steps below to activate VOD:

1. [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).
2. Purchase VOD services. For details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/266/2838).
3. Go to the [VOD console](https://console.cloud.tencent.com/vod).

At this point, you have activated VOD.

### Disabling hotlink protection

You need to make sure that hotlink protection for your default distribution domain name is not enabled:

1. Log in to the VOD console, select **Distribution and Playback** > **[Domain Name](https://console.cloud.tencent.com/vod/distribute-play/domain)**, and click **Set** in the entry of the default distribution domain to enter the settings page.
<img src="https://main.qcloudimg.com/raw/06259e41a62ea14ce8eb19ef6480182c.png" width="800" />
2. Confirm that the statuses of **Referer Hotlink Protection** and **Key Hotlink Protection** are both "Not Enabled".
![](https://qcloudimg.tencent-cloud.cn/raw/12689eb5bed63fc76cd7d88e38907c09.png)


## Step 1. Upload and process a video
This step describes how to upload a video, transcode it to adaptive bitstream, and generate a thumbnail and image sprite.

1. Log in to the VOD console, select **Media Assets** > **[Video Management](https://console.cloud.tencent.com/vod/media)**, and click **Upload Video**.
![](https://main.qcloudimg.com/raw/b1ad4f0706ad1cd24044c8420a759868.png)
2. On the upload page, select **Local Upload**, click **Select Video** to upload a local video, and set other fields as follows:
	- Select **Auto-processing after upload** for **Process Video**.
	- Select **Task Flow** as the **Processing Type**.
	- Select **LongVideoPreset** for **Task Flow Template**.
>? **LongVideoPreset** is a preset task flow, which uses template 10 for adaptive bitrate streaming, thumbnail generation, and image sprite capturing.

![](https://qcloudimg.tencent-cloud.cn/raw/56e6b4249722884eed34b167d6e6d6ed.png)
3. Click **Upload** to enter the **Uploading** page and wait for the upload to complete.
4. Select **Media Assets** > **[Video Management](https://console.cloud.tencent.com/vod/media)** and find the newly uploaded video (FileId: 528xxx3757278095). Here, the ID is the `FileId` of the uploaded video.
![](https://main.qcloudimg.com/raw/f2b3744a3c42a07863db0b7545dd892f.png)
>? Wait until the **Video Status** changes from **Processing** to **Normal**, which indicates that video processing is completed.

5. Click **Manage** in the **Operation** column of the newly uploaded video to enter the management page:
 - Click the **Basic Info** tab, and you can view the generated thumbnail and output adaptive bitstream (template ID: 10).
 - Click the **Screenshot Info** tab to view the generated image sprite (template ID: 10).

## Step 2. Preview video playback

In the previous step, you have uploaded and processed the video. Now, you can use the player for web, iOS, and Android to quickly preview video playback.

1. Select **Media Assets** > **[Video Management](https://console.cloud.tencent.com/vod/media)**, find the video uploaded and processed in **step 1**, click **Manage** in the **Operation** column, and select **Player Preview**.
2. Select **default** for **Player Configuration**.
>? **Default** is a preset player configuration, which is used to output the adaptive bitstream with template 10 and the image sprite with template 10.

 <img src="https://main.qcloudimg.com/raw/17e2552964195c6919239d2d13a0d012.png" width="660" />
4. In **Web Player**, click the button in the middle of the player to play back the video on web.
<img src="https://main.qcloudimg.com/raw/976ec23a988bcb494c4b225e635a5dba.png" width="522" />
5. In **Mobile Player**, click **Scan code to download** and install "Tencent Cloud Toolkit".
<img src="https://qcloudimg.tencent-cloud.cn/raw/439e632cb867b96a3334eb2823b2e235.png" width="522" />
6. Open Tencent Cloud Toolkit on your mobile phone, select **Player**, click the top-right corner to scan the QR code, and you can play back the video on your phone.
<img src="https://qcloudimg.tencent-cloud.cn/raw/06e77f14c2e1020e8936ce1ab30a6ca3.png" width="422" />

## Step 3. Use a demo for verification

You can use the player demos for [web](https://tcplayer.vcube.tencent.com/intl/index.html), [Android](https://github.com/LiteAVSDK/Player_Android), and [iOS](https://github.com/LiteAVSDK/Player_iOS) for verification. For more information, see the demo source code.
>? In **Media Assets** > **[Video Management](https://console.cloud.tencent.com/vod/media)** > **Player Preview** in the console, you can get the corresponding web player source code for video preview for your reference.
<img src="https://main.qcloudimg.com/raw/c5756910c7958aae198804c91b76a89e.png" width="500" />

## Summary

At this point, you have understood how to upload a video to VOD, process it, and play it back in the player.

You can also:
- Enable key hotlink protection for video playback as instructed in [Stage 2. Play back a video with hotlink protection enabled](https://intl.cloud.tencent.com/document/product/266/38292).
- Customize the video playback content and style as instructed in [Stage 3. Customize playback content and style](https://intl.cloud.tencent.com/document/product/266/38293).
- Encrypt a video and play back the encrypted video as instructed in [Stage 4. Play back an encrypted video](https://intl.cloud.tencent.com/document/product/266/38294).
