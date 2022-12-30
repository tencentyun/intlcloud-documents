## Overview
This document describes how to play back an adaptive bitrate streaming video, including:

* Set the resolution of a substream to be played back, which ranges from 480p to 1080p.
* Use a video screenshot as the video thumbnail.
* Adjust the preview thumbnail interval on the progress bar to 20%.

Before reading this document, make sure that you have read [Stage 1. Play back a source video](https://www.tencentcloud.com/document/product/266/51564) in the Player Guide. This document uses the account activated and the video uploaded in [stage 1](https://intl.cloud.tencent.com/document/product/266/38098).

## Step 1. Create an adaptive bitrate streaming template
1. Log in to the VOD console, select **Media Processing** > **[Template Settings](https://console.cloud.tencent.com/vod/video-process/template)**, and click **Create Template** on the **Adaptive Bitrate Streaming** tab.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/PEXG353_1.png" width="800" />

2. On the **Template Settings** page, click **Add Substream** to create substreams 1, 2, and 3, and enter the parameters as follows:
	- **Basic information**
	  - **Template Name**: Enter `MyTestTemplate`.
	  - **Muxing Format**: Select **HLS**.
	  - **Encryption Type**: Select **Not encrypted**.
	  - **Switch from Low Resolution to High Resolution**: Disable this option.
	  - **Transcoding Method**: Select **General Transcoding**.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/9InI915_2.png" width="622" />

 - **Substream info**
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
<td>1024 Kbps</td>
<td>Video long side: 0 px; video short side: 1,080 px</td>
<td>24 fps</td>
<td>48 Kbps</td>
<td>Dual</td>
</tr>
</tbody></table>
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/MxKn964_3.jpg" width="700" />

3. Click **Create**. An adaptive bitrate streaming template containing three substreams will be generated, and the template ID will be `1429212`.

![](https://qcloudimg.tencent-cloud.cn/raw/1b1ffba4a8c37c8d81132e8f93c801b6.png)

## Step 2. Create an image sprite template
1. Log in to the VOD console, select **Media Processing** > **[Template Settings](https://console.cloud.tencent.com/vod/video-process/template)**, and click **Create Screenshot Template** on the **Screenshot** tab.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/hrUE650_5.png" width="700" />

2. On the **Template Settings** page, enter the template parameters:
 * **Template Name**: `MyTestTemplate`.
 * **Screenshot Type**: **Image sprite screenshot**.
 * **Small Image Dimension**: 726x240 px.
 * **Sampling Interval**: 20%.
 * **Rows**: 10.
 * **Columns**: 10.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/LIw5399_6.png)

3. Click **Create**. An image sprite template with the ID of `131342` will be generated.

![](https://qcloudimg.tencent-cloud.cn/raw/4cf44757d6dbb339aa29c3c29fc480d7.png)

## Step 3. Create a task flow and initiate processing
After creating an adaptive bitrate streaming template (ID: 1429212) and an image sprite template (ID: 131342), you need to create a task flow.

1. Log in to the VOD console, select **Media Processing** > **[Task Flow Settings](https://console.cloud.tencent.com/vod/video-process/taskflow)**, and click **Create Task Flow**:
 * **Task Flow Name**: Enter `MyTestProcedure`.
 * **Task Type Configuration**: Select **Adaptive bitrate streaming**, **Screenshot*, and **Thumbnail**.
	 *  In the **Adaptive bitrate streaming task configuration** area, click **Add Template**, and select the custom adaptive bitrate streaming template **MyTestTemplate(1429212)** created in **step 1** for **Adaptive Bitrate Streaming Template/ID**.
	 *  In the **Screenshot task configuration** area, click **Add Template**, and select **Image sprite** for **Method for Taking Screenshot** and the custom image sprite template **MyTestTemplate(131342)** created in **step 2** for **Screenshot/ID**.
	 *  In the **Configuration of task of capturing cover screenshot** area, click **Add Template**, select **TimepointScreenshot** for **Screenshot Template/ID**, and select **Percent** and enter "50%" for **Select by time points**.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/Q6nQ449_8.png" width="900" />

2. Click **Submit**. A task flow named `MyTestProcedure` will be generated.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/y7xz109_9.jpg)

3. Select **Media Assets** > **[Video/Audio Management](https://console.cloud.tencent.com/vod/media)** in the console, select the target video (FileId: `387xxxxx8142975036`), and click **Process**.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/Mpj9208_10.jpg" width="622" />

4. In the video processing pop-up window:

 * Select **Task Flow** for **Processing Type**.
 * Select **MyTestProcedure** for **Task Flow Template**.

 <img src="https://staticintl.cloudcachetci.com/yehe/backend-news/ctNZ059_11.png" width="500" />

5. Click **Confirm**, and then go to the [Task Management](https://console.cloud.tencent.com/vod/task) page to view the status of the task. When the **Task Status** changes from **Processing** to **Completed**, it indicates that video processing is complete.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/IuU9256_12.jpg" width="800" />

6. Go to **Media Assets** > [**Video/Audio Management****](https://console.cloud.tencent.com/vod/media) and click **Manage** on the right of the target video to enter the management page:

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/UBpg014_13.png" width="800" />

Select the **Basic Info** tab:
 - You can view the thumbnail generated and outputs of adaptive bitrate streaming (template ID: 1429212).

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/gtLx554_14.jpg" width="522" />
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/358v600_15.jpg" width="700" />

 Select the **Screenshot Info** tab:
 - You can view the image sprite generated (template ID: 131342).

 <img src="https://staticintl.cloudcachetci.com/yehe/backend-news/KiVV307_16.jpg" width="700" />

## Step 4. Generate a Player Signature
In this step, you can use the signature tool to quickly generate a signature for the player to play back the video.
Select **Distribution and Playback** > [**Player Signature Tools**](https://console.cloud.tencent.com/vod/distribute-play/signature) and enter the following information:
 - **Video file ID**: Enter the `FileId` (387xxxxx8142975036) used in **step 3**.
 - **Signature expiration time**: Enter the player signature expiration time. If you leave it empty, the signature will never expire.
 - **Playable video type**: Select **Unencrypted adaptive bitrate**.
 - **Playable adaptive bitrate streaming template**: Select `MyTestTemplate (1429212)`.
 - **Image sprite template for thumbnail preview**: Select `MyTestTemplate (131342)`.

Click **Generate** to get the signature string.

## Step 5. Play back the video
After step 4, you have obtained the three parameters needed for video playback: `appId`, `fileId` and `psign` (player signature). The following describes how to play back the video on the web.

### Playback on the web
Open the [web player demo](https://tcplayer.vcube.tencent.com/) and configure it as follows:
 - **Player feature**: Select **Video playback**.
 - Click the **Play by FileID** tab.
 - **fileID**: Enter the `FileId` in the previous step (387xxxxx8142975036).
 - **appID**: Enter the `appId` to which the file belongs, i.e., the `appID` on the player signature generation page in the previous step.
 - **psign**: Enter the signature string generated in the previous step.

Click **Preview** to play back the video.
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/V98D696_18.png" width="800" />

### Multi-platform player demos
After getting the player signature, you can use the player demos for [web](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html), [Android](https://github.com/LiteAVSDK/Player_Android), and [iOS](https://github.com/LiteAVSDK/Player_iOS) for verification. For more information, see the demo source code.

## Summary
At this point, you have understood how to play back an adaptive bitrate streaming video.
If you want to encrypt a video and play back the encrypted video, see [Stage 4. Play back an encrypted video](https://www.tencentcloud.com/document/product/266/51556).
