This document guides you through how to quickly upload a video from your local file system to VOD and use VOD features to process it, **so that you can directly watch an accelerated and watermarked output video on a webpage**. The local video file `Tencent Cloud.mp4` is used as an example here.


## Step 1. Activate VOD
1. Sign up for a [Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).
2. Purchase the VOD service. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/zh/document/product/266/2838).
3. Select **Cloud Products** > **Video Services** > **[Video on Demand](https://console.cloud.tencent.com/vod)** to enter the VOD console.

>?If the VOD service has already been activated, please proceed directly to the next step.



## Step 2. Upload a video
1. Click **[Media Assets](https://console.cloud.tencent.com/vod/media)** on the left sidebar.
2. Click **Upload Video** and select **Local Upload** for **Upload method**.
3. Click **Select Video** and select the local video file `Tencent Cloud.mp4`.
4. In the **Video Processing** configuration item, select **No Processing After Upload** and click **Start Upload** in the bottom-left corner.

## Step 3. Create a watermarking template
1. Select **Video Processing** > **[Templates](https://console.cloud.tencent.com/vod/video-process/template)** on the left sidebar.
2. Select the **Watermarking Template** tab.
3. Click **Create Watermarking Template**, make the following settings on this page, and click **Create**. <br>
<img src="https://main.qcloudimg.com/raw/c85044cca9840a8f83bc5747e87985a9.png" width="450">
	
## Step 4. Process the video
1. Select **Uploaded** on the **[Media Assets](https://console.cloud.tencent.com/vod/media)** page.
2. Check `Tencent Cloud.mp4` and click **Video Processing**.
![](https://main.qcloudimg.com/raw/535b71cfc6374ff65bc46c1ab07eccd1.png)
3. In the **Video Processing** pop-up box, select **Transcode** for **Processing Type**.
4. In the **Transcoding Template** configuration item, click **Transcoding Template** and select **MP4-SD** and **MP4-HD** (you can select multiple transcoding templates).
5. In the **Watermarking Template** configuration item, click the drop-down list and select **Select Watermarking Template**. A drop-down list will pop up on the right where you can select **p001**.
6. In the **Video Cover** configuration item, check **Use First Frame as Cover** and click **OK**.
<img src="https://main.qcloudimg.com/raw/69abe9f386f0e12a79ae6596d6a994e4.png">

## Step 5. Get a playback link
1. Click **Manage** in the **Operation** column at the row of `Tencent Cloud.mp4`.
2. Click **MP4-SD-SD** in the **Standard Transcoding List** module and click **Copy address** in the **Operation** column.
<img src="https://main.qcloudimg.com/raw/d6936a55fcc0a1e7df5fdf9265c25f7a.png" width="850">
3. Paste the copied URL into the address bar on a web browser and press Enter to play back the video.

## Relevant Operations
- [How to Transcode Video](https://intl.cloud.tencent.com/zh/document/product/266/37546)
- [How to Use Key Hotlink Protection](https://intl.cloud.tencent.com/zh/document/product/266/37544)
- [How to Receive Event Notification](https://intl.cloud.tencent.com/zh/document/product/266/37542)



## FAQs

- [How do I change my VOD billing mode?](https://intl.cloud.tencent.com/zh/document/product/266/18941#.E4.BA.91.E7.82.B9.E6.92.AD.E8.AE.A1.E8.B4.B9.E6.96.B9.E5.BC.8F.E5.A6.82.E4.BD.95.E6.9B.B4.E6.94.B9.EF.BC.9F)
- [Why are fees still incurred after I purchase a resource package?](https://intl.cloud.tencent.com/zh/document/product/266/18941#.E8.B4.AD.E4.B9.B0.E8.B5.84.E6.BA.90.E5.8C.85.E5.90.8E.EF.BC.8C.E4.B8.BA.E4.BB.80.E4.B9.88.E8.BF.98.E5.9C.A8.E4.BA.A7.E7.94.9F.E8.B4.B9.E7.94.A8.EF.BC.9F)
- [What media file formats are supported for upload to VOD?](https://intl.cloud.tencent.com/zh/document/product/266/2846?from_cn_redirect=1#.E4.BA.91.E7.82.B9.E6.92.AD.E6.94.AF.E6.8C.81.E4.B8.8A.E4.BC.A0.E5.93.AA.E4.BA.9B.E6.A0.BC.E5.BC.8F.E7.9A.84.E5.AA.92.E4.BD.93.E6.96.87.E4.BB.B6.EF.BC.9F)
- [How can I upload files to VOD? Is checkpoint restart supported?](https://intl.cloud.tencent.com/zh/document/product/266/2846?from_cn_redirect=1#.E4.BA.91.E7.82.B9.E6.92.AD.E4.B8.8A.E4.BC.A0.E6.96.87.E4.BB.B6.E6.9C.89.E5.93.AA.E4.BA.9B.E6.96.B9.E5.BC.8F.EF.BC.8C.E8.83.BD.E5.90.A6.E6.96.AD.E7.82.B9.E7.BB.AD.E4.BC.A0.EF.BC.9F)
