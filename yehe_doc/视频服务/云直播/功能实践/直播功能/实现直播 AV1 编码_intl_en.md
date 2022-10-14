AOMedia Video 1 (AV1) is a free, open source video coding format. It encodes videos at a bitrate 30%+ lower than H.265 (HEVC) does while delivering the same video quality. This means that with the same bandwidth, AV 1-encoded videos have higher quality than H.265-encoded videos. This document shows you how to encode videos using AV1 and how to play AV1-encoded videos.

## How to Use AV1

### Prerequisites

- You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985).
- You have activated CSS and added [a playback domain and a push domain](https://intl.cloud.tencent.com/document/product/267/35970).

[](id:step1)
### Step 1. Create a transcoding template
1. Log in to the CSS console and select **Feature Configuration** > [Live Transcoding](https://console.cloud.tencent.com/live/config/transcode) on the left sidebar.
2. Click **Create Transcoding Template**, select **Standard Transcoding** or **Top Speed Codec Transcoding** as the transcoding type, and expand **Advanced Configuration**.
3. Select **AV1** as the codec.
![](https://qcloudimg.tencent-cloud.cn/raw/9cd4c835c3cc37f3da93c07805ce4e5f.png) 
4. Click **Save**.

[](id:step2)
### Step 2. Bind a domain
Select the transcoding template created and click **Bind Domain Name**. In the pop-up window, select a **playback domain** and click **Confirm**.
![](https://qcloudimg.tencent-cloud.cn/raw/a7d945597ae3ff71557720b4e6eeae43.png)

[](id:step3)
### Step 3. Generate a playback URL
Select **Address Generator** on the left sidebar. Select the playback domain bound in step 2 and the transcoding template created in [step 1](#step1), and click **Generate Address** to generate a playback URL.

[](id:step4)
### Step 4. Play AV1-encoded videos

Play the AV1-encoded videos with a player that supports AV1 using the playback URL generated in step 3. You can either use a third-party player that supports AV1 or rebuild your own player.

- **Third-party players that support AV1**
	- **App**
		- [ExoPlayer](https://github.com/google/ExoPlayer) (use `libgav1`)
		- [ijkplayer](https://github.com/bilibili/ijkplayer) FFmpeg (update FFmpeg and integrate [dav1d](https://code.videolan.org/videolan/dav1d))
	- **Web**
		- [dash.js](http://cdn.dashjs.org/v2.4.0/jsdoc/index.html). The player supports AV1, but whether AV1 videos can be decoded depends on the browser. Chrome supports AV1 decoding.
		- [shaka-player](https://github.com/shaka-project/shaka-player). The player supports AV1, but whether AV1 videos can be decoded depends on the browser. Chrome supports AV1 decoding.
	- **PC**
	VLC for [Windows](https://share.weiyun.com/haPT1L0W) and [macOS](https://share.weiyun.com/W2btBASt) support AV1 in FLV and HEVC in FLV.
- **Rebuilding your own player**
If your player cannot play AV1 videos, we can [help](https://intl.cloud.tencent.com/contact-us) you rebuild your player to support AV1.
