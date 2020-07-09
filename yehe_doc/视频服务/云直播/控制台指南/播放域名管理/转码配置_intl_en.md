LVB outputs playback streams with the original bitrate by default. To limit or set the playback bitrate, you can associate a transcoding template with a playback domain name. This document describes how to associate/unassociate a transcoding template with/from a playback domain name.

## Notes
- The template configuration will take effect in about 5–10 minutes.
- After you specify a transcoding template, the backend will generate different playback addresses with different bitrates for easier use. The original resolution of the stream will be as close as possible to the original aspect ratio of the video to avoid stretched and distorted display.
- When end users access an address with a new bitrate for the first time, it is normal for the first end user triggering the link to experience slower loading.



## Prerequisites
- You have logged in to the [LVB Console](https://console.cloud.tencent.com/live) and added a [playback domain name](https://intl.cloud.tencent.com/document/product/267/35970).
- You have created a [transcoding template](https://intl.cloud.tencent.com/document/product/267/31071)


## Associating a Transcoding Template
1. Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, click the **playback domain** to be configured or **Manage** on the right to enter the domain details page.
2. Select the **Template Configuration** tab, and click **Edit** in the top-right corner of the **Transcoding Configuration** tab.
3. Select a transcoding configuration to specify the encoding mode and bitrate set by the transcoding template for the playback address under the domain name.
4. Click **Save**.

![](https://main.qcloudimg.com/raw/8ab50571f4260ba070cf3270f8487e30.png)

## Playback Address of a Transcoded Video
After you configure the transcoding template, you need to add the transcoding template name to the playback URL. The format is **playback address_transcoding template name**. Otherwise, you will only be able to play back the original live stream content. For more information, please see [Playback Configuration](https://intl.cloud.tencent.com/document/product/267/31058).

**For example,** if the name of the transcoding template associated with the playback domain name is **hd**, and the original playback address is:
<pre>
http://domain/AppName/StreamName.flv?txSecret=Md5(key+<b style="color:yellow;">StreamName</b>+hex(time))&txTime=hex(time) 
</pre>
Then, if you want to get the output video, the following new playback address needs to be generated:
<pre>
http://domain/AppName/<b style="color:yellow;">StreamName_hd</b>.flv?txSecret=Md5(key+<b style="color:yellow;">StreamName_hd</b>+hex(time))&txTime=hex(time)
</pre>

<span id="Untie"></span>
## Unassociating a Transcoding Template
1. Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, click the **playback domain** to be configured or **Manage** on the right to enter the domain details page.
2. Select **Template Configuration** > **Transcoding Configuration**.
3. Click **Edit** on the right and uncheck the corresponding template.
4. Click **Save** to unassociate the template from the domain name.
![](https://main.qcloudimg.com/raw/497478a836b8017c7e8be177b26af24d.png)

>? To delete a template, you need to unassociate it first and then go to **Feature Template** > **[Transcoding Configuration](https://console.cloud.tencent.com/live/config/transcode)** to delete it. For more information, please see [Transcoding Configuration](https://intl.cloud.tencent.com/document/product/267/31071#delect).
