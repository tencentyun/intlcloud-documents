You can add and delete transcoding templates by selecting **Feature Template** > **Transcoding Configuration** in the left sidebar in the LVB Console.
## Creating a Transcoding Template

The system provides four templates for Smooth, SD, HD, and Audio. After you select a corresponding template for Smooth, SD, or HD, the system will automatically enter the video bit rate and video height. You can also manually set the video bit rate and video height to create a custom transcoding template.

![](https://main.qcloudimg.com/raw/c3208fe3e06c785041954f176960dc8a.png)

>The transcoding template name can contain up to 10 letters and numbers.

## Associating a Domain Name

After creating a transcoding template, you need to select the corresponding playback domain name in **Domain Name Management**, go to **Template Configuration**, and click **Edit** to specify the transcoding template for the domain name. 
![](https://main.qcloudimg.com/raw/7c78f911a92f05293777f19957695874.png)

>After a transcoding template is specified, the backend will generate different playback addresses with different bit rates for easier use. The original resolution of the stream should be as close as possible to the original aspect ratio of the video to avoid stretched and distorted display.
> When end users access an address with a new bit rate for the first time, the first end user triggering the link may experience slower loading, which is normal.


**Real-time transcoding can be used in the following ways:**

1. If the Tencent Cloud Web Player SDK is used, after transcoding is enabled, the player will automatically display the appropriate bit rate in the quality selector in the bottom-right corner according to the channel settings, which can be adjusted manually. The default settings are as follows:
 - PC: The original resolution is prioritized.
 - Mobile: **HD** with a resolution of 900 Kbps is prioritized. If it is unavailable, the original resolution will be used.
2. Addresses with different bit rates can be obtained directly and then embedded into a third-party player for video playback.
