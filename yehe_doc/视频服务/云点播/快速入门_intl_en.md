This document guides you through how to quickly upload a video from your local file system to VOD and use VOD features to process it, **so that you can directly watch an accelerated and watermarked output video on a webpage**. The local video file `Tencent Cloud.mp4` is used as an example here.


## Step 1. Activate VOD
1. [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).
2. Purchase the VOD service. For details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/266/2838).
3. Select **Products** > **Video Services** > **[Video on Demand](https://console.cloud.tencent.com/vod)** to enter the VOD console.

>? If the VOD service has already been activated, skip this step.



## Step 2. Upload a video
1. Click **[Media Assets > Video Management](https://console.cloud.tencent.com/vod/media)** on the left sidebar.
2. Click **Upload Video** and select **Local Upload** as the **Upload Method**.
![](https://main.qcloudimg.com/raw/1d54bda88e541f56d8c2fdec162761f0.png)
3. Click **Select Video** and select the local video file `Tencent Cloud.mp4`.
4. For **Process Video**, select **No processing after upload** and click **Upload** in the bottom-left corner.

## Step 3. Create a watermark template
1. Select **Video Processing** > **[Template Settings](https://console.intl.cloud.tencent.com/vod/video-process/template)** on the left sidebar.
2. Select the **Watermark** tab.
3. Click **Create Watermark Template**, configure the following settings, and click **Create**. <br>
<img src="https://main.qcloudimg.com/raw/423f29236a2e12bb8546682db5eb97fc.png" width="450">

## Step 4. Process the video
1. Select **Uploaded** on the **[Media Assets > Video Management](https://console.cloud.tencent.com/vod/media)** page.
2. Check "Tencent Cloud.mp4" and click **Process Video**.
![](https://main.qcloudimg.com/raw/246099e6f6c37bca0f3b4901b4125412.png)
3. In the **Process Video** pop-up, select **Transcoding** as the **Processing Type**.
4. Click **Transcoding Template**, and then select one or more transcoding templates.
5. For **Watermark Template**, click the drop-down list, and then select **p001** under **Select watermark**.
6. Check **Thumbnail**, and then click **Confirm**.
![](https://main.qcloudimg.com/raw/31ecab7ef88cc80f103a16a7dee3deb8.png)

## Step 5. Get a playback URL
1. Click **Manage** in the **Operation** column of `Tencent Cloud.mp4`.
2. In the **Standard Transcoding List** section, click **Copy URL** in the **Operation** column of **MP4-SD-SD**.
<img src="https://main.qcloudimg.com/raw/18a5e92a1200dfcd67dc5d5d0567159c.png" width="1100">
3. Paste the copied URL into the address bar on a web browser and press Enter to play back the video.

## Operations
- [Best Practice - How to Upload Videos over the Web](https://intl.cloud.tencent.com/document/product/266/39106)
- [Best Practice - How to Transcode Video](https://intl.cloud.tencent.com/document/product/266/37546)
- [Best Practice - How to Use Key Hotlink Protection](https://intl.cloud.tencent.com/document/product/266/37544)
- [Best Practice - How to Receive Event Notification](https://intl.cloud.tencent.com/document/product/266/37542)



## FAQs

- [How do I change my VOD billing mode?](https://intl.cloud.tencent.com/document/product/266/18941)
- [What media file formats are supported for upload to VOD?](https://intl.cloud.tencent.com/document/product/266/2846)
- [How can I upload files to VOD? Is checkpoint restart supported?](https://intl.cloud.tencent.com/document/product/266/2846)

