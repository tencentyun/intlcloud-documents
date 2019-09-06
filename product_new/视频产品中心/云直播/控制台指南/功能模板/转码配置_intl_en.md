You can add and delete transcoding templates by selecting **Function Template** > **Transcoding Configuration** in the left sidebar in the LVB Console.
## Creating a Transcoding Template

The system provides four types of templates, namely Smooth, SD, HD, and Audio. After you select a corresponding template for Smooth, SD, or HD, the system will automatically enter the video bitrate and video height. You can also manually set the video bitrate and video height to customize a transcoding template.

![](https://main.qcloudimg.com/raw/c3208fe3e06c785041954f176960dc8a.png)

>The transcoding template name can contain up to 10 letters and numbers.

## Associating the Template with a Domain Name

After creating a transcoding template, you need to select the corresponding playback domain name in **Manage Domain**, go to **Configure Template**, and click **Edit** to specify the transcoding template for the domain name.
![](https://main.qcloudimg.com/raw/7c78f911a92f05293777f19957695874.png)

>After you specify a transcoding template, the backend will generate different playback addresses with different bitrates for easier use. The original resolution of the stream will be as close as possible to the original aspect ratio of the video to avoid stretched and distorted display.
> When end users access an address with a new bitrate for the first time, it is normal for the first end user triggering the link to experience slower loading.


**Real-time transcoding can be used in the following ways:**

1. If the Tencent Cloud Web Player SDK is used, after transcoding is enabled, the player will automatically display available bitrates in the bottom-right corner according to the channel settings. Users can make adjustments manually. The default settings are as follows:
 - PC: Use the original resolution if possible.
 - Mobile: Use **HD** with a resolution of 900 Kbps if possible. If it is unavailable, the original resolution will be used.
2. Obtain addresses corresponding to different bitrates and play the video with a third-party player.
