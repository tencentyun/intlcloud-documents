CSS playback is output to the original bitrate by default. If you want to limit or set the playback bitrate, you can bind the playback domain name to a transcoding template. This document describes how to bind/unbind a playback domain name to/from a transcoding template.

## Notes
- The template configuration will take effect in about 5–10 minutes.
- After you specify a transcoding template, the backend will generate different playback addresses with different bitrates for easier use. The original resolution of the stream will be as close as possible to the original aspect ratio of the video to avoid stretched and distorted display.
- When end users access an address with a new bitrate for the first time, it is normal for the first end user triggering the link to experience slower loading.
- One domain name can be bound to multiple transcoding templates. After binding, the playback bitrate will be transcoded according to the bound transcoding template.



## Prerequisites
- You have logged in to the [CSS console](https://console.cloud.tencent.com/live) and added a [playback domain name](https://intl.cloud.tencent.com/document/product/267/35970).
- You have created a [transcoding template](https://intl.cloud.tencent.com/document/product/267/31071).


## Binding Transcoding Template
1. Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** and click the **playback domain name** to be configured or **Manage** on the right to enter the domain details page.
2. Select the **Template Configuration** tab and click **Edit** in the top-right corner of the **Transcoding Configuration** tab.
3. Select a transcoding configuration to specify the encoding mode and bitrate set by the transcoding template for the playback address under the domain name.
4. Click **Save**.

![](https://main.qcloudimg.com/raw/8ab50571f4260ba070cf3270f8487e30.png)

## Playback Address Description
After the transcoding template is configured, the transcoding template name needs to be added to the playback URL. The splicing format is **playback address_transcoding template name**. If it is not added, the original live stream content will be played back. For more information on the playback address, please see [Playback Configuration](https://intl.cloud.tencent.com/document/product/267/31058).

**For example,** if the name of the transcoding template bound to the playback domain name is **hd**, and the original playback address is:
<pre>
http://domain/AppName/StreamName.flv?txSecret=Md5(key+<b style="color:yellow;">StreamName</b>+hex(time))&txTime=hex(time) 
</pre>
Then, if you want to get the output video, the following new playback address needs to be generated:
<pre>
http://domain/AppName/<b style="color:yellow;">StreamName_hd</b>.flv?txSecret=Md5(key+<b style="color:yellow;">StreamName_hd</b>+hex(time))&txTime=hex(time)
</pre>

<span id="Untie"></span>
## Unbinding Transcoding Template
1. Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** and click the **playback domain name** to be configured or **Manage** on the right to enter the domain details page.
2. Select **Template Configuration** > **Transcoding Configuration**.
3. Click **Edit** on the right and deselect the corresponding template.
4. Click **Save** to unbind the template from the domain name.
![](https://main.qcloudimg.com/raw/497478a836b8017c7e8be177b26af24d.png)

>? To delete a template, you need to unbind it first and then go to **Feature Template** > **[Transcoding Configuration](https://console.cloud.tencent.com/live/config/transcode)** to delete it. For more information, please see [Transcoding Configuration](https://intl.cloud.tencent.com/document/product/267/31071#delect).
