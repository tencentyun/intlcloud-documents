## Operation Scenarios

The recording feature is disabled by default for live push. If you want to set or modify it, you can do so in the recording configuration. Then, you need to associate the change with a specified push domain name in domain management. After that, the recording feature will be enabled for all live streams under the domain name.

## Prerequisites

- You have logged in to the [LVB Console](https://console.cloud.tencent.com/live).
- You have added a **push domain name**.

>
>- The recorded video files are stored in the [VOD Console](https://console.cloud.tencent.com/vod/overview) by default. After enabling the recording feature, please make sure that your VOD service is in normal status; if it has not been activated or has been suspended due to account arrears, LVB recording will not be available, no recording files will be generated, and no recording fees will be incurred.
>- You are recommended to activate the VOD service in advance and purchase appropriate resource packages so as to avoid service suspension due to account arrears. For more information, please see [Getting Started with VOD](https://intl.cloud.tencent.com/document/product/266/8757).

## Directions

1. 	Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, click the **push domain** to be configured or **Manage** to enter the domain management page.
2. 	Select **Template Configuration** and view the **Recording Configuration** tab.
3. Click **Edit** on the tab to select a recording configuration which specifies the corresponding recording template for the playback address under the domain name.
4. Click **Save**.

>The template configuration will take effect in about 5–10 minutes. For more information on how to configure a recording template, please see [Recording Configuration](https://intl.cloud.tencent.com/document/product/267/34223).

![](https://main.qcloudimg.com/raw/29bf30fa3b4ce940a9903c0331fc608e.png)

>If you want to unbind the recording configuration from the domain name, click **Edit** in **Template Configuration**, deselect the corresponding template, and click **Save**.

## Getting Recording Files
The generated recording files are automatically stored in the VOD system and can be obtained in the following ways:

### VOD Console

Log in to the VOD Console and enter **[Media Assets](https://console.cloud.tencent.com/vod/media)** to browse all recording files.

![](https://main.qcloudimg.com/raw/b41dc459807ac1986d1db04032ea7942.png)



### Recording event notification

The recording callback address can be set in the console or through API calls. A notification will be sent to the callback address after the recording files are generated. After that, you can refer to the [callback protocol content](https://intl.cloud.tencent.com/document/product/267/31566) for recording to take your next step.

The event notification is an efficient, reliable, and real-time mechanism, so it is recommended to use the callback method to get recording files.

### VOD API query
For detailed instructions, please see the VOD API documentation:
- The [SearchMedia](https://intl.cloud.tencent.com/document/product/266/34179) API can be used to query recording files by live stream name and time range.
- The **DescribeVodPlayInfo** API can be used to get video information by video name prefix.

