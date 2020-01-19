This document guides you through how to quickly upload a video from your local file system to VOD and use VOD features to process it, **so that you can directly watch an accelerated and watermarked output video on a webpage**. The local video file "Tencent Cloud.mp4" is used as an example here.


## Step 1. Activate VOD
1. Sign up for a [Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and [verify your identity](https://intl.cloud.tencent.com/document/product/378/3629).
2. Purchase the VOD service. For more information, please see [Billing Overview](https://cloud.tencent.com/document/product/266/2838).
3. Select **Cloud Products** > **Video Services** > **[Video on Demand](https://console.cloud.tencent.com/vod)** to enter the VOD Console.

> If the VOD service has already been activated, please proceed directly to the next step.



## Step 2. Upload a video
1. Click **[Media Assets](https://console.cloud.tencent.com/vod/media)** on the left sidebar.
2. Click **Upload Video** and select **Local Upload** for **Upload method**.
3. Click **Select Video** and select the local video file "Tencent Cloud.mp4".
4. In the **Video Processing** configuration item, select **No Processing After Upload** and click **Start Upload** in the bottom-left corner.

## Step 3. Create a watermarking template
1. Select **Video Processing** > **[Templates](https://console.cloud.tencent.com/vod/video-process/template)** on the left sidebar.
2. Select the **Watermarking Template** tab.
3. Click **Create Watermarking Template**, make the following settings on this page, and click **Create**. <br>
<img src="https://main.qcloudimg.com/raw/b102d1663cd1446d9436a9e818235c4a.png" width="450">
	
## Step 4. Process the video
1. Select **Uploaded** on the "[Media Assets](https://console.cloud.tencent.com/vod/media)" page.
2. Check "Tencent Cloud.mp4" and click **Video Processing**.
![](https://main.qcloudimg.com/raw/82af82fefe1d35d420ebba92894fae37.png)
3. In the **Video Processing** pop-up box, select **Transcode** for **Processing Type**.
4. In the **Transcoding Template** configuration item, click the drop-down list on the left to select **Select Transcoding Template**, and then click the drop-down list on the right to select **MP4-SD-SD(20)** and **MP4-HD-HD(30)** (multiple transcoding templates can be selected).
5. In the **Watermarking Template** configuration item, click the drop-down list and select **Select Watermarking Template**. A drop-down list will pop up on the right where you can select **p001**.
6. In the **Video Cover** configuration item, check **Use First Frame as Cover** and click **OK**.
<img src="https://main.qcloudimg.com/raw/788dfb8ef9fc14b729185560657f8634.png">

## Step 5. Get a playback link
1. Click **Manage** in the "Operation" column at the row of "Tencent Cloud.mp4".
2. Click **MP4-SD-SD** in the **Standard Transcoding List** module and click **Copy address** in the "Operation" column.
<img src="https://main.qcloudimg.com/raw/f14b31cb27614df1597850e902a0fdd9.png" width="850">
3. Paste the copied URL into the address bar on a web browser and press Enter to play back the video.


