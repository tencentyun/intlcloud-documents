The recording feature is disabled by default for LVB push. This document describes how to bind/unbind a push domain name to/from a recording template to enable/disable the recording feature.


## Use Limits
- The recorded video files are stored in the [VOD console](https://console.cloud.tencent.com/vod/overview) by default. We recommend you activate the VOD service in advance and purchase appropriate resource packages so as to avoid service suspension due to account arrears. For more information, please see [Getting Started with VOD](https://intl.cloud.tencent.com/document/product/266/8757).
- After enabling the recording feature, please make sure that your VOD service is in normal status; if it has not been activated or has been suspended due to account arrears, LVB recording will not be available, no recording files will be generated, and no recording fees will be incurred.
-  The template configuration will take effect in about 5–10 minutes. 
-  After the template is bound successfully, the recording feature will be enabled for push addresses under the specified push domain name.
- One domain name can be bound to only one recording template. After binding, all streams under it will be recorded according to this template.

## Prerequisites
- You have logged in to the [LVB console](https://console.cloud.tencent.com/live) and added a [push domain name](https://intl.cloud.tencent.com/document/product/267/35970).
- You have [created a recording template](https://intl.cloud.tencent.com/document/product/267/34223).

## Binding Recording Template
1. 	Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** and click the **push domain name** to be configured or **Manage** to enter the domain name details page.
2. 	Select the **Template Configuration** tab and click **Edit** in the top-right corner of the **Recording Configuration** block.
![](https://main.qcloudimg.com/raw/29bf30fa3b4ce940a9903c0331fc608e.png)
3. Select a recording configuration template and click **Save**.
![](https://main.qcloudimg.com/raw/8ecacaebb47ab9ae476d9286c1796b46.png)

## Unbinding Recording Template
1. Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** and click the **push domain name** to be configured or **Manage** to enter the domain name details page.
2. Select the **Template Configuration** tab and click **Edit** in the top-right corner of the **Recording Configuration** block.
3. Deselect the target template and click **Save**.
![](https://main.qcloudimg.com/raw/f2c5f091437cd8b873ed6447562fb697.png)


## Getting Recording File
The generated recording files are automatically stored in the VOD system and can be obtained in the following ways:

### VOD console
Log in to the VOD console, select and enter the target subapplication, and click **[Media Assets](https://console.cloud.tencent.com/vod/media)** on the left to browse all recording files.
![](https://main.qcloudimg.com/raw/b41dc459807ac1986d1db04032ea7942.png)
 
### Recording event notification
The recording callback URL can be set in the console or through API calls. A notification will be sent to the callback address after the recording files are generated. After that, you can refer to the [callback protocol content](https://intl.cloud.tencent.com/document/product/267/31566) for recording to take your next step.
>?The event notification mechanism is efficient, reliable, and real-time. Therefore, we recommend you use the callback method to get recording files.

### VOD API query
For more information on how to query and filter recording files, please see [SearchMedia](https://intl.cloud.tencent.com/document/product/266/34179).
