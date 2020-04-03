This document describes how to create a [transcoding configuration](https://intl.cloud.tencent.com/document/product/267/31062) in the [LVB Console](https://console.cloud.tencent.com/live). After the configuration is successfully created, you need to associate it with the corresponding push domain name. The association will take effect in about 5–10 minutes. You can also create transcoding templates for live channels through APIs. 

The system supports two types of transcoding services: general transcoding and top speed codec, each of which provides four templates: LD, SD, HD, and Audio. 

## Creating a Transcoding Template
Log in to the LVB Console, select **Feature Template** > **[Transcoding Configuration](https://console.cloud.tencent.com/live/config/transcode)** on the left sidebar to add or delete transcoding templates.

After you select a corresponding template for LD, SD, or HD, the system will automatically enter the video bitrate and video height. You can also manually set them to create a custom transcoding template.       
![](https://main.qcloudimg.com/raw/c3208fe3e06c785041954f176960dc8a.png)

>The transcoding template name can contain up to 10 letters and digits.


## Associating a Domain Name

After creating a transcoding template, you need to select the corresponding playback domain name in **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, go to **Template Configuration**, and click **Edit** to specify the transcoding template for the domain name. For detailed directions, please see [Transcoding Configuration](https://intl.cloud.tencent.com/document/product/267/31062).
![](https://main.qcloudimg.com/raw/7c78f911a92f05293777f19957695874.png)

>After a transcoding template is specified, the backend will generate different playback addresses with different bitrates for easier use. The original resolution of the stream should be as close as possible to the original aspect ratio of the video in order to avoid stretched and distorted display.
> When end users access an address with a new bitrate for the first time, the first end user triggering the link may experience slower loading, which is normal.


**Real-time transcoding can be used in the following ways:**

1. If the Tencent Cloud Web Player SDK is used, after transcoding is enabled, the player will automatically display the appropriate bitrate in the definition selector in the bottom-right corner according to the channel settings, which can be adjusted manually. The default settings are as follows:
 - PC: the original resolution is prioritized.
 - Mobile: **HD** with a resolution of 900 Kbps is prioritized. If it is unavailable, the original resolution will be used.
2. Addresses with different bitrates can be obtained directly and then embedded into a third-party player for video playback.
