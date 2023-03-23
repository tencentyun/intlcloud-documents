The live recording feature is disabled by default. This document describes how to bind a recording template to a push domain to enable the recording feature, as well as how to unbind a template to disable the feature.

[](id:limit)
## Use Limits
- After enabling the recording feature, please make sure that your VOD or COS service is in normal status. If VOD or COS is not activated or is suspended due to overdue payments, live recording will fail. No recording files will be generated. Nor will fees be incurred.
- A template takes effect about 5-10 minutes after it is bound to a domain. 
- After a template is successfully bound to a push domain, recording will be enabled for push addresses under that domain.
- One domain can be bound with only one recording template. After binding, all streams under that domain will be recorded according to the template.
- Mixed-stream recording does not support mixing streams inside the Chinese mainland with those outside. It will cause an error and playback will fail.

## Prerequisites
- You have logged in to the [CSS console](https://console.cloud.tencent.com/live) and added a [push domain](https://intl.cloud.tencent.com/document/product/267/35970).
- You have [created a recording template](https://intl.cloud.tencent.com/document/product/267/34223).


[](id:conect)
## Binding a Recording Template
1. Go to [Domain Management](https://console.cloud.tencent.com/live/domainmanage), and click the target **push domain** or click **Manage** to enter the domain details page.
2. Select the **Template Configuration** tab and click **Edit** in the **Recording configuration** area.
![](https://qcloudimg.tencent-cloud.cn/raw/a56ed2f940b60babab0e2bbbe4eebaab.png)
3. Select a recording template and click **Confirm**.
![](https://qcloudimg.tencent-cloud.cn/raw/b4e5b04ee6e79636e52ae907556cd5d1.png)


[](id:unite)
## Unbinding a Recording Template
1. Go to [Domain Management](https://console.cloud.tencent.com/live/domainmanage), and click the target **push domain** or click **Manage** to enter the domain details page.
2. Select the **Template Configuration** tab and click **Edit** in the **Recording configuration** area.
3. Unselect the template and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/ae44efc51b581100735c7faafe2414e8.png)

>? 
>- Unbinding a recording template will not affect ongoing live streams.
>- To cancel recording for ongoing streams, stop the streams and push them again.


[](id:get_record)
## Obtaining Recording Files
You can obtain recording files in the following ways:
### Recording to VOD
#### From the VOD console
Log in to the VOD console, select the target subapplication, and click [Media Assets](https://console.cloud.tencent.com/vod/media) on the left sidebar. You can view all your recording files on this page.
![](https://main.qcloudimg.com/raw/b41dc459807ac1986d1db04032ea7942.png)

#### From recording callbacks
If you have configured a recording callback address in the console or using an API, after a recording file is generated, a notification will be sent to the callback address configured. For details about the fields of the callback, see [How to Receive Event Notification](https://intl.cloud.tencent.com/document/product/267/38080).
>? The recording callback method is recommended for its reliability and real-timeliness.

#### Using a VOD API
You can also call the [SearchMedia](https://intl.cloud.tencent.com/document/product/266/34179) API of VOD to query recording files.

### Recording to COS
#### From the COS console
Log in to the COS console, click [Bucket List](https://console.cloud.tencent.com/cos/bucket) on the left sidebar, and then click the target bucket. You will be able to find the recording files in the file list.
