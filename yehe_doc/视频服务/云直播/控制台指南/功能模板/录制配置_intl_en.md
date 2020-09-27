LVB supports recording live streams and storing recording files in VOD for download and preview. This document describes how to create, modify, and delete recording templates.
You can create a recording template in the following two methods:
- Create a recording template in the LVB Console. For detailed directions, please see [Creating Recording Template](#C_record).
- Create a recording template via API. For more information about the parameters and samples, see [CreateLiveRecordTemplate](https://intl.cloud.tencent.com/document/product/267/30845).

## Notes
- The recorded video files are stored in the [VOD Console](https://console.cloud.tencent.com/vod/overview) by default. You are recommended to activate the VOD service in advance and purchase appropriate resource packages so as to avoid service suspension due to account arrears. For more information, please see [Getting Started with VOD](https://intl.cloud.tencent.com/document/product/266/8757).
- After enabling the recording feature, please make sure that your VOD service is in normal status; if it has not been activated or has been suspended due to account arrears, LVB recording will not be available, no recording files will be generated, and no recording fees will be incurred.
- During the live streaming, you can get a recording file in about 5 minutes after the recording process ends. For example, if you start recording a live stream at 12:00, you can get the corresponding clip for 12:00 to 12:30 at around 12:35.
- Subject to the audio and video file formats (FLV/MP4/HLS), the video encoding format of H.264 and audio encoding format of ACC are supported.
- After a recording template is created successfully, it can be associated with a push domain name. For more information, please see [Recording Configuration](https://intl.cloud.tencent.com/document/product/267/34224). The association will take effect in about 5–10 minutes.
- For more information about the recording filenames, see the `VodFileName` parameter in [Data Types](https://intl.cloud.tencent.com/document/product/267/30767#RecordParam).

## Prerequisites
- You have activated the LVB service and added a [push domain name](https://intl.cloud.tencent.com/document/product/267/35970).
- You have activated the [VOD service](https://intl.cloud.tencent.com/document/product/266/8757#.E6.AD.A5.E9.AA.A41.EF.BC.9A.E5.BC.80.E9.80.9A.E4.BA.91.E7.82.B9.E6.92.AD).

<span id="C_record"></span>
## Creating Recording Template
1. Log in to the LVB Console and go to **Feature Template** > **[Recording Configuration](https://console.cloud.tencent.com/live/config/record)**.
2. Click **+** to set basic information and configure as follows:
![](https://main.qcloudimg.com/raw/93c0660fe1c5eaf8bfc2a72e7c7944dc.png)
   
   <table>
   <thead><tr><th>Configuration Item</th><th>Configuration Description</th></tr></thead>
   <tbody><tr>
   <td>Default template</td>
   <td>Default template type for LVB recording, which can be FLV, MP4, or HLS.</td>
   </tr><tr>
   <td>Template name</td>
   <td>Custom LVB recording template name, which can contain letters, digits, underscores, and hyphens.</td>
   </tr><tr>
   <td>Template description</td>
   <td>Custom LVB recording template description, which can contain letters, digits, underscores, and hyphens.</td>
   </tr><tr>
   <td>Recording file type</td>
   <td>Videos are recorded based on the original bitrate of the live stream and can be output in .hls, .mp4, .flv, and .aac formats. The .aac format records the audio only.</td>
   </tr><tr>
   <td>Length of a single recording file (in minutes)</td>
   <td><ul style="margin-bottom:0px">
<li>There is no upper limit for HLS format. If a file exceeds the recording resumption timeout period, a new file will be created to continue recording.</li>
       <li>The length of a single file recorded in .mp4, .flv, or .aac format ranges from 5 to 120 minutes.</li>
       </ul></td>
   </tr><tr>
   <td>File retention duration (in days)</td>
   <td>A single recording file can be retained for up to 1,080 days. A retention period of 0 means "never expire".</td>
   </tr><tr>
   <td>Recording resumption timeout period (in seconds)</td>
   <td>Only the .hls format supports recording resumption after push interruption, and the timeout period for resumption can be set between 0 and 1,800 seconds.</td>
   </tr><tr>
   <td>Recording to subapplication</td>
   <td>Live streams can be recorded to a specified <a href="https://console.cloud.tencent.com/vod/app-manage">subapplication</a> in VOD. They are recorded to the primary application under the account by default. Only writable subapplications are supported.</td>
   </tr>
   </tbody></table>
3. Click **Save**.



## Modifying Recording Template
1. Go to **Feature Template** > **[Recording Configuration](https://console.cloud.tencent.com/live/config/record)**.
2. Select the target recording template and click **Edit** on the right to modify the template information.
3. Click **Save**.

![](https://main.qcloudimg.com/raw/68f4dd1a6452a3e97e7ff4dea6493d7b.png)

## Deleting Recording Template
1. Go to **Feature Template** > **Recording Configuration**.
2. Select the target recording template and click ![](https://main.qcloudimg.com/raw/220ada95a4b631349543cc8cde96226e.png) above.
3. Confirm whether to delete the selected recording template and click **OK** to delete it.
![](https://main.qcloudimg.com/raw/e25f0566348f69e8c6afb64439c5e40f.png)

>! The recording templates are managed at the domain name level in the console, and rules created by APIs cannot be canceled there for the time being. If you associated the recording configuration with a specified stream through the recording management API and want to unassociate them, you need to call the [DeleteLiveRecordTemplate API](https://intl.cloud.tencent.com/document/product/267/30842). 
## Associating and Disassociating Push Domain Name
For detailed directions, please see [Recording Configuration](https://intl.cloud.tencent.com/document/product/267/34224).
