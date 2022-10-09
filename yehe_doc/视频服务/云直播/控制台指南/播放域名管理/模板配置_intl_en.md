With CSS, the bitrate of the original stream is used for playback by default. To use a different playback bitrate, you can bind your domain with a transcoding or adaptive bitrate template. This document shows you how to bind a template to and unbind a template from a playback domain.

## Notes
- A template takes effect about 5-10 minutes after it is bound to a domain.
- After you specify a transcoding template, the backend will generate playback URLs of different formats for the transcoded stream. To avoid image distortion, push the stream at a resolution as close as possible to the original resolution.
- H.265 is supported by fewer players than H.264. Playback may fail if a player does not support H.265. To solve this issue, you can [configure a transcoding template](https://intl.cloud.tencent.com/document/product/267/31071) to transcode your video to H.264.
- Loading may take some time for the first user accessing the URL that uses a different playback bitrate.
- One domain can be bound with multiple transcoding templates. After you bind a template, videos will be transcoded as specified in the template.
- You can create up to **50** transcoding templates.



## Prerequisites
- You have logged in to the [CSS console](https://console.cloud.tencent.com/live) and added a [playback domain name](https://intl.cloud.tencent.com/document/product/267/35970).
- You have created a [transcoding template](https://intl.cloud.tencent.com/document/product/267/31071) or an [adaptive bitrate template](https://intl.cloud.tencent.com/document/product/267/50271).

[](id:conect)
## Binding a Transcoding Template
1. Go to [Domain Management](https://console.tencentcloud.com/live/domainmanage). Click the name of your playback domain or **Manage** on the right.
2. Select the **Template Configuration** tab and click **Edit** in the **Transcoding Configuration** area.
3. Select a transcoding template. Videos under the current domain will be transcoded using the codec and bitrate specified in the template.
4. Click **Confirm**.

![](https://qcloudimg.tencent-cloud.cn/raw/2d8cb5be76debfbd04d60329891c5830.png)

[](id:descript)
## URL Format for Transcoded Streams
After binding a transcoding template, append its name to your playback URL (**playback URL_transcoding template name**). If you do not append the template name, the original stream will be played. For more information on playback URLs, see [Playback Configuration](https://intl.cloud.tencent.com/document/product/267/31058).

Suppose the name of the transcoding template bound is **hd**, and the original playback URL is as follows:
<pre>
http://domain/AppName/StreamName.flv?txSecret=Md5(key+<b style="color:yellow;">StreamName</b>+hex(time))&txTime=hex(time) 
</pre>
To play the transcoded stream, you need to use the following URL:
<pre>
http://domain/AppName/<b style="color:yellow;">StreamName_hd</b>.flv?txSecret=Md5(key+<b style="color:yellow;">StreamName_hd</b>+hex(time))&txTime=hex(time)
</pre>
[](id:Untie)

## Unbinding a Transcoding Template
1. Go to [Domain Management](https://console.tencentcloud.com/live/domainmanage). Click the name of your playback domain or click **Manage** on the right.
2. Select the **Template Configuration** tab.
3. In the **Transcoding Configuration** area, click **Edit** on the right and unselect the template you want to unbind.
4. Click **Confirm**.
![](https://qcloudimg.tencent-cloud.cn/raw/ff6e5f8038124c95fb29d0ffb5745890.png)

>? To delete a template, you need to unbind it first and then go to **Feature Configuration** > [Live Transcoding](https://console.tencentcloud.com/live/config/transcode) to delete it. For details, see [Deleting a Template](https://intl.cloud.tencent.com/document/product/267/31071#delect).


## Binding an Adaptive Bitrate Template

1. Go to [Domain Management](https://console.tencentcloud.com/live/domainmanage). Click the name of your playback domain or **Manage** on the right.
2. Select the **Template Configuration** tab and click **Edit** in the **Adaptive bitrate configuration** area.
3. Select an adaptive bitrate template. Streams of different bitrates will be generated for videos under the current domain according to the template.
4. Click **Confirm**.
![](https://qcloudimg.tencent-cloud.cn/raw/df2db1fd5b8f9beb5eda4eb989557c51.png)

## Adaptive Bitrate URL Format
Only HLS and WebRTC are supported for adaptive bitrate playback. The URL formats for the two protocols are different. For details, see [Playback Configuration](https://intl.cloud.tencent.com/document/product/267/31058).
**HLS URL**：
**Suppose** the name of the adaptive bitrate template bound is **autobitrate**, and the original playback URL is as follows:

<pre>
http://domain/AppName/StreamName.m3u8?txSecret=Md5(key+<b style="color:yellow;">StreamName</b>+hex(time))&txTime=hex(time) 
</pre>
The following URL needs to be generated for playing back the transcoded video:
<pre>
http://domain/AppName/<b style="color:yellow;">StreamName_autobitrate</b>.m3u8?txSecret=Md5(key+<b style="color:yellow;">StreamName_autobitrate</b>+hex(time))&txTime=hex(time)
</pre>
**WebRTC URL**:
**Suppose** the adaptive bitrate template bound has three streams. Their names are "test 1", "test 2", and "test 3", and their bitrates are 200 Kbps, 300 Kbps, and 400 Kbps respectively.
The adaptive bitrate playback URL would be as follows:

webrtc://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)&tabr_bitrates=test3,test2,test1&tabr_start_bitrate=test1&tabr_control=auto

## Unbinding an Adaptive Bitrate Template
1. Go to [Domain Management](https://console.tencentcloud.com/live/domainmanage). Click the name of your playback domain or click **Manage** on the right.
2. Select the **Template Configuration** tab.
3. In the **Adaptive bitrate configuration** area, click **Edit** on the right and unselect the template you want to unbind.
4. Click **Confirm**.
![](https://qcloudimg.tencent-cloud.cn/raw/872b71589554e8d89abf50db40f75777.png)

>? To delete a template, you need to unbind it first and then go to **Feature Configuration** > [Live Transcoding](https://console.tencentcloud.com/live/config/transcode) to delete it. For details, see [Deleting a Template](https://intl.cloud.tencent.com/document/product/267/31071#delect).