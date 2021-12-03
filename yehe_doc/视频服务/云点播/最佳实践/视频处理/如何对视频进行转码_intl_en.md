

## Instructions

### Overview

This document describes how to transcode videos stored in VOD and how to get the outputs.

### Costs

The open-source code provided here is free of charge, but the following costs may be incurred.

- Fees for purchasing a Tencent Cloud CVM instance to implement the request script of TencentCloud APIs. For more information, please see [CVM Billing Plans](https://intl.cloud.tencent.com/document/product/213/2180).
- Fees for VOD storage of uploaded videos. For more information, please see [Video Storage](https://intl.cloud.tencent.com/document/product/266/14666).
- Fees for VOD transcoding duration of uploaded videos. For more information, please see [Video Transcoding](https://intl.cloud.tencent.com/document/product/266/14666).
- Fees for VOD traffic consumed by video playback. For more information, please see [Video Acceleration](https://intl.cloud.tencent.com/document/product/266/14666).

### Parameters
VOD video transcoding supports the following formats:
<table>
   <tr>
      <th width="0px" style="text-align:center">Parameter</td>
      <th width="0px" style="text-align:center">Type</td>
      <th width="0px"  style="text-align:center">Description</td>
   </tr>
   <tr>
      <td rowspan='2' style="text-align:center">Input format</td>
      <td> Container format </td>
      <td>WMV, RM, MOV, MPEG, MP4, 3GP, FLV, AVI, RMVB, TS, ASF, MPG, WebM, MKV, M3U8, WM, ASX, RAM, MPE, VOB, DAT, MP4V, M4V, F4V, MXF, QT, Ogg</td>
   </tr>
   <tr>
      <td>Video codec</td>
      <td>AV1, AVS2, H.264/AVC, H.263, H.263+, H.265, MPEG-1, MPEG-2, MPEG-4, MJPEG, VP8, VP9, QuickTime, RealVideo, Windows Media Video</td>
   </tr>
   <tr>
      <td rowspan='4' style="text-align:center">Output format</td>
      <td rowspan="3">Container format</td>
      <td>Video: FLV, MP4, HLS (M3U8 + TS)</td>
   </tr>
   <tr>
      <td>Audio: MP3, MP4, Ogg, FLAC, M4A</td>
   </tr>
   <tr>
      <td>Image: GIF, WebP</td>
   </tr>
   <tr>
      <td>Video codec</td>
      <td>H.264/AVC, H.265/HEVC, AV1</td>
   </tr>
</table>

The target specification of an output video after transcoding is specified by parameters such as codec, resolution, and bitrate. VOD integrates these parameters in the transcoding template as shown below. For details, please see [Video Processing Overview](https://intl.cloud.tencent.com/document/product/266/33930).
<table>
   <tr>
      <th width="108px" style="text-align:center">Type</td>
      <th width="200px" style="text-align:center">Parameter</td>
      <th width="0px"  style="text-align:center">Description</td>
   </tr>
   <tr>
      <td rowspan='7' width="0px" style="text-align:center">Video encoding</td>
      <td>Codec</td>
      <td>Supported codecs: H.264, H.265, and AV1</td>
   </tr>
	  <tr>
      <td>Bitrate</td>
      <td>Supported bitrate range: 10 Kbps - 35 Mbps   </td>
   </tr>
	    <tr>
      <td>Frame rate</td>
      <td>Supported frame rate range: 1-60 fps; common values: 24, 25, 30</td>
   </tr>
	    <tr>
      <td>Resolution</td>
      <td><li>Value range of width: 128-4096 px</li><br><li>Value range of height: 128-4096 px</li><br></td>
   </tr>
	    <tr>
      <td>GOP length</td>
      <td>Value range: 1-10s </td>
   </tr>
	    <tr>
      <td>Profile</td>
      <td><li>When the video codec is H.264, the Baseline, Main, and High profiles are supported.</li><br><li>When the video codec is H.265, only the Main profile is supported.</li><br></td>
   </tr>
	    <tr>
      <td>Color space</td>
      <td> YUV420P is supported </td>
   </tr>
</table>

>?
>- **Codec**: a method of converting video files from a certain format into another using specific compression technology. With advanced encoding mode for transcoding, an H.265 video has far lower bitrate than an H.264 video while the original quality is retained, which lowers the playback bandwidth usage.
>-**Bitrate**: it refers to the size of data encoded by the encoder each second, in Kbps. For example, 800 Kbps indicates that the encoder generates 800 Kb of data per second.
>- **Frame rate**: the number of frames that appear within a second
>- **Resolution**: the number of pixels per inch
>- **GOP**: the number of frames between two I-frames

Recommended bitrates, resolutions, and configuration ranges are shown below:

| **Clarity** | **Recommended Bitrate** | **Recommended Resolution** | **Resolution Range**            |
| ------- | -------- | --------- | -------------------- |
| SD      | 600      | 640 x 480   | SD (Image short side ≤ 480 px)   |
| HD      | 2000     | 1280 x 720  | HD (Image short side ≤ 720 px)     |
| FHD     | 4000     | 1920 x 1080 | FHD (Image short side ≤ 1080 px)  |
| 2K      | 6000     | 2560 x 1440 | 2K (Image short side ≤ 1440 px)      |
| 4K      | 8000     | 3840 x 2160 | 4K (Image short side ≤ 2160 px)     |

Tencent Cloud VOD's unique TESHD is a solution integrating image quality repair and enhancement, adaptive parameter selection, and V265 encoder among other video processing features. It provides granular transcoding methods and ensures higher definition, and this solution requires low consumption of network resources while delivering better watch experience. VOD provides a wide range of preset clarity settings, with parameters detailed as follows:

| **Clarity** | **Recommended Bitrate** | **Recommended Resolution** | **Resolution Range**            |
| ------- | -------- | --------- | -------------------- |
| SD      | 350 or leave it empty      | 640 x 480   | SD (Image short side ≤ 480 px)     |
| HD      | 1350 or leave it empty    | 1280 x 720  | HD (Image short side ≤ 720 px)    |
| FHD     | 2700 or leave it empty  | 1920 x 1080 | FHD (Image short side ≤ 1080 px)  |
| 2K      | 3500 or leave it empty  | 2560 x 1440 | 2K (Image short side ≤ 1440 px)    |
| 4K      | 7500 or leave it empty  | 3840 x 2160 | 4K (Image short side ≤ 2160 px)    |

>? If the bitrate is left empty, TESHD will set the minimum bitrate based on intelligent analysis of the source video.

## Initiating Transcoding Through the Console

### Step 1. Activate VOD[](id:p11)

See [Getting Started - Step 1. Activate VOD](https://intl.cloud.tencent.com/document/product/266/8757) for details.

### Step 2. Upload a video[](id:p12)

See [Getting Started - Step 2. Upload a video](https://intl.cloud.tencent.com/document/product/266/8757) for details. Click [here](http://1400329073.vod2.myqcloud.com/ff439affvodcq1400329073/e968a7e55285890804162014755/LKk92603oW0A.mp4) to view the test video (FileId: 3701925921390170339) for this demo.
![](https://qcloudimg.tencent-cloud.cn/raw/9d10415aff42613a6b9899c552d053d2.png)
>?You’re advised to use a short video (dozens of seconds) for test to avoid long transcoding duration.

### Step 3. Initiate transcoding[](id:p13)

Check the uploaded test video on the [Video Management](https://console.cloud.tencent.com/vod/media) page, and then click **Process Video**.
![](https://qcloudimg.tencent-cloud.cn/raw/9d10415aff42613a6b9899c552d053d2.png)
In the pop-up, select **Transcoding** as the processing type, and then click **Transcoding Template**:
![](https://qcloudimg.tencent-cloud.cn/raw/bb552a5454fe649f2b61edf2d5fe50fa.png)
Select the desired transcoding template, and then click **Confirm**. This demo uses the system preset templates `STD-H264-MP4-360P` (template ID 100010) and `STD-H264-MP4-540P` (template ID 100020) as examples. If you need to use custom transcoding templates, please see [Template Settings](https://intl.cloud.tencent.com/document/product/266/14059).
![](https://qcloudimg.tencent-cloud.cn/raw/d26764d535ee63e216969e21ee7e6e46.png)
Click **Confirm** to initiate the transcoding.
![](https://qcloudimg.tencent-cloud.cn/raw/e370f7ee3ae245e5b97d47fa383e2be8.png)
If the status of the test video is **Processing** on the **Video Management** page, the video is being transcoded.
![](https://qcloudimg.tencent-cloud.cn/raw/9c329fbf018cd251c2280d2df453f041.png)

### Step 4. View the transcoding result [](id:p14)

When the status of the test video changes to **Normal** on the [Video Management](https://console.cloud.tencent.com/vod/media) page, the transcoding is finished. Click **Manage** on the right to enter the video management page.
![](https://qcloudimg.tencent-cloud.cn/raw/be5fa72994d786fa6737bf3590d4324f.png)
In the **Standard Transcoding List** under the **Basic Info** tab, videos of `STD-H264-MP4-360P` and `STD-H264-MP4-540P` specifications are the transcoding outputs. You can click **Preview** on the right to watch them, or click **Copy URL** and then publish them through other channels.
![](https://qcloudimg.tencent-cloud.cn/raw/48867ad69971690bc6a528cf9f14473c.png)

## Calling TencentCloud APIs to initiate transcoding

### Step 1. Prepare a CVM[](id:p21)

The TencentCloud API script needs to be executed on a CVM instance meeting the following requirements:

- Region: not limited.
- Model: the minimum official configuration (1 CPU core and 1 GB memory) is sufficient.
- Public network: a public IP is required, and the bandwidth should be at least 1 Mbps.
- Operating system: official public image `Ubuntu Server 16.04.1 LTS 64-bit` or `Ubuntu Server 18.04.1 LTS 64-bit`.

For detailed directions on how to purchase a CVM instance and reinstall the system, please see [Operation Guide - Creating Instances via CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855) and [Operation Guide - Reinstalling System](https://intl.cloud.tencent.com/document/product/213/4933), respectively.

>!If you do not have a CVM instance satisfying the above conditions, you can also run the script on another Linux (such as CentOS or Debian) or macOS server with public network access, but you need to modify certain commands in the script based on the operating system. Please search for the specific modification method by yourself.

### Step 2. Get an API key[](id:p22)

The API key (`SecretId` and `SecretKey`) is required for calling TencentCloud APIs. If you have not created an API key yet, generate one as instructed in [Root Account Access Key](https://intl.cloud.tencent.com/document/product/598/34228). If you have already created a key, get it as instructed in the same document.

### Step 3. Activate VOD[](id:p23)

See [Getting Started - Step 1. Activate VOD](https://intl.cloud.tencent.com/document/product/266/8757) for details.

### Step 4. Upload a video[](id:p24)
See [Getting Started - Step 2. Upload a video](https://intl.cloud.tencent.com/document/product/266/8757) for details. Click [here](http://1400329073.vod2.myqcloud.com/ff439affvodcq1400329073/e968a7e55285890804162014755/LKk92603oW0A.mp4) to view the test video (FileId: 5285890804162014755) for this demo.
![](https://qcloudimg.tencent-cloud.cn/raw/fb2ac8243834a909cee60aaf19426bea.png)
>?You’re advised to use a short video (dozens of seconds) for test to avoid long transcoding duration.


### Step 5. Initiate transcoding[](id:p25)

Log in to the [CVM instance prepared in step 1](#p21) as instructed in [Logging In to Linux Instance in Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436) and enter and run the following command on the remote terminal:
```
ubuntu@VM-69-2-ubuntu:~$ export SECRET_ID=AKxxxxxxxxxxxxxxxxxxxxxxx; export SECRET_KEY=xxxxxxxxxxxxxxxxxxxxx;git clone https://github.com/tencentyun/vod-server-demo.git ~/vod-server-demo; bash ~/vod-server-demo/installer/transcode_api.sh
```
>?Please assign the corresponding values obtained in [step 2](#p22) to `SECRET_ID` and `SECRET_KEY` in the command.

This command will download the demo source code from GitHub and automatically run the installation script. The installation process will take several minutes (subject to the CVM network conditions), during which the remote terminal will print the following information:
```
  [2020-06-15 20:39:56] Start installing pip3.
  [2020-06-15 20:40:06] pip3 is successfully installed.
  [2020-06-15 20:40:06] Start installing TencentCloud API Python SDK.
  [2020-06-15 20:40:07] TencentCloud API Python SDK is installed.
  [2020-06-15 20:40:07] Start configuring API parameters.
  [2020-06-15 20:40:07] API parameters are configured.
```
Execute the `process_media.py` script to initiate transcoding.
```
ubuntu@VM-69-2-ubuntu:~$ cd ~/vod-server-demo/transcode_api/; python3 process_media.py 5285890804162014755
```
>? Replace `5285890804162014755` in the command with the actual `FileId` obtained in [Step 4](#p24).

This command will initiate a [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) request for the video `5285890804162014755`, perform transcoding according to specifications `100010` and `100020` as defined in the VOD [preset transcoding template](https://intl.cloud.tencent.com/document/product/266/33932), and print the response.
```
{"TaskId": "1400329073-procedurev2-f6bf6f01612369b6db30f2224792a2aft0", "RequestId": "809918fb-791c-4937-b684-5027ba6bc5f0"}
```

### Step 6. View the transcoding result [](id:p14)

If the status of the test video is **Processing** on the **Video Management** page, the video is being transcoded.
![](https://qcloudimg.tencent-cloud.cn/raw/5fcd99f766d6587f1644daac23c10d4d.png)
When the status of the test video changes to **Normal**, the transcoding is finished. Click **Manage** on the right to enter the video management page.
![](https://qcloudimg.tencent-cloud.cn/raw/be5fa72994d786fa6737bf3590d4324f.png)
In the **Standard Transcoding List** under the **Basic Info** tab, videos of desired specifications are the transcoding outputs. You can click **Preview** on the right to watch them, or click **Copy URL** and then publish them through other channels.
![](https://qcloudimg.tencent-cloud.cn/raw/9067b71ebcac7658c58222499f47fcf0.png)

## Auto Transcoding After Uploading (Task Flow)

VOD supports uploading videos through the console, from the server, from the client, and by pulling from URLs, etc. (see [Media Upload](https://intl.cloud.tencent.com/document/product/266/9760) for details). Each upload method supports specifying a [task flow](https://intl.cloud.tencent.com/document/product/266/33931) that automatically triggers transcoding after the uploading is finished.

## Auto Transcoding After Uploading (Event Notification)

The VOD backend will initiate [event notification](https://intl.cloud.tencent.com/document/product/266/33948) requests after completing both uploading and transcoding. Developers can initiate transcoding for newly uploaded videos based on the event notifications and can also get transcoding results from such notifications (the method above is to view transcoding results from the console). For details about how to use event notifications, please see [How to Receive Event Notification](https://intl.cloud.tencent.com/document/product/266/37542).

