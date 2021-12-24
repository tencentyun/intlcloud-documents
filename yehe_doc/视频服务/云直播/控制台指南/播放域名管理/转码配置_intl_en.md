CSS playback is output to the original bitrate by default. If you want to limit or set the playback bitrate, you can associate the playback domain name with a transcoding template. This document describes how to associate/disassociate a playback domain name with/from a transcoding template.

## Note
- The template configuration takes effect in about 5-10 minutes.
- After you specify a transcoding template, the backend will generate playback URLs corresponding to different bitrates. The original resolution of the stream will follow the aspect ratio of the source video as much as possible to avoid image distortion.
- As H.265 is not as compatible as H.264, if a player doesn't support H.265 and the playback fails, you can configure a [transcoding template](https://intl.cloud.tencent.com/document/product/267/31071) to transcode the video to H.264 for playback.
- It is normal that the loading takes longer for the end user who first triggers the URL for a new bitrate.
- One domain name can be bound to multiple transcoding templates. After they are bound, the playback bitrate will be transcoded according to the bound transcoding template.
- You can create up to **50** transcoding templates.



## Prerequisites
- You have logged in to the [CSS console](https://console.cloud.tencent.com/live) and added a [playback domain name](https://intl.cloud.tencent.com/document/product/267/35970).
- You have created a [transcoding template](https://intl.cloud.tencent.com/document/product/267/31071).

[](id:conect)
## Binding Transcoding Template
1. Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** and click the playback domain name to be configured or **Manage** on the right to go to the domain details page.
2. Select **Template Configuration**, and click **Edit** in the top-right corner of the **Transcoding Configuration** tab.
3. Select a transcoding template with the desired codec and bitrate for the playback URL under the domain name.
4. Click **Save**.

![](https://main.qcloudimg.com/raw/8ab50571f4260ba070cf3270f8487e30.png)

[](id:descript)
## Notes on Playback URL
After configuring the transcoding template, add its name in the playback URL in the format of **playback URL_transcoding template name**. If it is not added, the original live stream will be played back. For more information on the playback URL, see [Playback Configuration](https://intl.cloud.tencent.com/document/product/267/31058).

Suppose the name of the transcoding template bound with the playback domain name is **hd**, and the original playback URL is:
<pre>
http://domain/AppName/StreamName.flv?txSecret=Md5(key+<b style="color:yellow;">StreamName</b>+hex(time))&txTime=hex(time) 
</pre>
The following URL needs to be generated for playing back the transcoded video:
<pre>
http://domain/AppName/<b style="color:yellow;">StreamName_hd</b>.flv?txSecret=Md5(key+<b style="color:yellow;">StreamName_hd</b>+hex(time))&txTime=hex(time)
</pre>

[](id:Untie)
## Unbinding Transcoding Template
1. Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, click the playback domain name to be configured or **Manage** on the right to enter the domain details page.
2. Select **Template Configuration** > **Transcoding Configuration**.
3. Click **Edit** on the right and uncheck the corresponding template.
4. Click **Save** to disassociate the template from the domain name.
![](https://main.qcloudimg.com/raw/497478a836b8017c7e8be177b26af24d.png)

>? To delete a template, you need to disassociate it first and then go to **Feature Template** > **[Transcoding Configuration](https://console.cloud.tencent.com/live/config/transcode)** to delete it. For more information, see [Transcoding Configuration](https://intl.cloud.tencent.com/document/product/267/31071#delect).
