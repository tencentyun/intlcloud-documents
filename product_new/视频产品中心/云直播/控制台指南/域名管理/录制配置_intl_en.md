## Scenario

The recording feature is disabled by default for live push. If you want to set or modify it, you can do so in the recording configuration. Then, you need to associate the change with a specified domain name in domain name management.

## Prerequisites

You have logged in to the [LVB Console](https://console.cloud.tencent.com/live).

## Steps

1. Select **Manage Domain** in the left sidebar, click the push domain name to be configured or click **Manage** in the operation column to enter the domain name management page.
 ![](https://main.qcloudimg.com/raw/62719d1025bf1fd4bb72379242fa8209.png)
2. In the **Configure Template** tab, you can see the recording configuration information of the domain name.
![](https://main.qcloudimg.com/raw/6cf96e702b81cd47511fd508af5e848d.png)
3. By clicking **Edit**, you can select a recording configuration to specify the corresponding recording template for the playback address under the domain name.
![](https://main.qcloudimg.com/raw/0dfcc722c01e7c544aef9f187706e2b6.png)
For more information on how to configure a recording template, see [Recording Configuration](https://cloud.tencent.com/document/product/267/20384).

>? If you want to unbind the recording configuration from the domain name, click **Edit** in **Configure Template**, deselect the corresponding template, and click **Save**.
>![](https://main.qcloudimg.com/raw/d973dc282489f0acb584d5159edbee4b.png)

## Obtaining Recording Files
The generated recording files are automatically stored in the VOD system and can be obtained in the following ways:

### VOD Console

After logging in to the VOD Console, you can browse all the recording files on the [Video Management](https://console.cloud.tencent.com/video/videomanage) page.

 ![](https://main.qcloudimg.com/raw/d3afc2a39fadc9ac889d68cfe52c71ef.png)
 
### Recording Event Notification

The recording callback address can be set in the console or through API calls. A notification will be sent to the callback address after the recording files are generated. After that, you can refer to the [callback protocol content](https://cloud.tencent.com/document/product/267/32744) for recording to take your next step.

The event notification is an efficient, reliable, and real-time mechanism, so it is recommended to use the callback method to get recording files.

### VOD API Query
For detailed instructions, see the VOD API documentation:
- The [SearchMedia] (https://cloud.tencent.com/document/product/266/31813) API can be used to query recording files by live stream name and time range.
- The [DescribeVodPlayInfo](https://cloud.tencent.com/document/product/266/7825) API can be used to get video information by video name prefix.
