This document describes how to create a [recording configuration](https://intl.cloud.tencent.com/document/product/267/34224) in the [LVB Console](https://console.cloud.tencent.com/live). After the configuration is successfully created, you need to associate it with the corresponding push domain name. The association will take effect in about 5–10 minutes. You can also create recording templates for live channels through APIs. For more information, please see [Creating Recording Templates](https://cloud.tencent.com/document/api/267/32614).

>
>- The recorded video files are stored in the [VOD Console](https://console.cloud.tencent.com/vod/overview) by default. After enabling the recording feature, please make sure that your VOD service is in normal status; if it has not been activated or has been suspended due to account arrears, LVB recording will not be available, no recording files will be generated, and no recording fees will be incurred.
>- You are recommended to activate the VOD service in advance and purchase appropriate resource packages so as to avoid service suspension due to account arrears. For more information, please see [Getting Started with VOD](https://intl.cloud.tencent.com/document/product/266/8757).

## Creating a Recording Template
Log in to the LVB Console, select **Feature Template** > **[Recording Configuration](https://console.cloud.tencent.com/live/config/record)**, click **+**, enter the basic information, and click **Save**.

![](https://main.qcloudimg.com/raw/d5352513fa5b9388a01edd3f37e97c28.png)
The .hls format supports recording resumption after push interruption, and the timeout period for resumption can be set between 0 and 300 seconds.

> 
1. Videos are recorded based on the original bitrate of the live stream and can be outputted in .hls, .mp4, .flv, and .aac formats. The .aac format records the audio only.
1. The maximum length of a single file recorded in .mp4 or .flv format is 120 minutes, and if a file exceeds this limit, a new file will be created to continue recording. There is no upper limit for .hls format.
1. A single recording file can be retained up to 1,080 days. A retention period of 0 means "permanently retained".
1. During the live streaming, you can obtain a recording file in about 5 minutes after the recording process ends. For example, if you start recording a live stream at 12:00, you can get the corresponding clip for 12:00 to 12:30 at around 12:35.
1. Subject to the audio and video file formats (FLV/MP4/HLS), the video encoding format of H.264 and audio encoding format of AAC are supported.

## Associating a Domain Name
After creating a recording template, you need to select the corresponding push domain name in **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** or click **Manage** on the right to enter the domain name details page. Then, select **Template Configuration** to specify the recording template for the domain name.
![](https://main.qcloudimg.com/raw/03810e82a6429ba8ad606b6c02503a9d.png)
>
>- If you want to unbind the recording configuration from the domain name, click **Edit** in **Template Configuration**, deselect the corresponding template, and click **Save**.
>- The recording templates are managed at the domain name level in the console, and rules created by APIs cannot be canceled there for the time being. If you associated the recording configuration with a specified stream through the recording management API and want to unassociate them, you need to call the [DeleteLiveRecordTemplate API](https://cloud.tencent.com/document/product/267/32612).






