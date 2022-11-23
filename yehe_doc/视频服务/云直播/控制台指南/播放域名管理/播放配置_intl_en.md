After pushing a stream successfully, you can use the address generator of the CSS console to generate a playback URL (you need to enter the `StreamName`, which should be the same as the stream ID in the push URL).

## Prerequisites
 - You have logged in to the [CSS console](https://console.tencentcloud.com/live).
 - You have added a **playback domain**. For directions on how to add a domain, see [Adding Your Own Domain Name](https://intl.cloud.tencent.com/document/product/267/35970).

## Directions
1. Select [Domain Management](https://console.tencentcloud.com/live/domainmanage) on the left sidebar and click the name of your playback domain or click **Manage** on the right.
2. Select **Playback Configuration** and, in **Playback Address Generator**, complete the following settings:
	1. Select the type of stream to play, which can be the **original stream**, the **transcoded stream**, or **adaptive bitrate streams**. If you select **Transcoded stream**, you need to specify a transcoding template. If you select **Adaptive bitrate streams**, you need to specify an adaptive bitrate template.
	2. Enter the `StreamName`, such as `liveteststream`. Make sure it’s the same as the `StreamName` in your push URL.
	3. After you select an adaptive bitrate template, the names of the streams in the template will be listed in descending order by bitrate.
	4. Select an expiration time, such as `2021-06-30 19:00:44`.
5. Click **Generate Address**.
![](https://qcloudimg.tencent-cloud.cn/raw/ae67aa5386d9f47d7bd20d7cce7c7603.png)
3. If you haven’t enabled authentication for your playback domain, in the **Playback URL** area on the same page, you can find playback URLs for RTMP, FLV, HLS, and UDP. Replace `StreamName` in the URLs with the stream ID in your push URL, and you can use the URLs to play the stream.
![](https://qcloudimg.tencent-cloud.cn/raw/16a192a0090e8f4f470ace2b78cac52e.png)
>? For more information, see [Live Playback](https://intl.cloud.tencent.com/document/product/267/31559).




## Playback URL Format
### Playback URL for the original stream
```
RTMP format: `rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`
FLV format: `http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`
M3U8 format: `http://domain/AppName/StreamName.m3u8?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`
UDP format: webrtc://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
```
- `domain`: Your playback domain name.
- `AppName`: The live streaming application name, which is `live` by default and is customizable.
- `StreamName`: The stream ID, which uniquely identifies a stream and is customizable.
- `txSecret`: The authentication string generated after playback authentication is enabled.
- `txTime`: The expiration timestamp of the playback URL configured in the console.

>!
>- If you have enabled authentication, the actual expiration time of a URL will be `txTime` plus the validity period of the authentication key.
>- For the sake of convenience, the console allows you to specify the URL expiration time in human-readable format. If you enable authentication, when generating playback URLs, the system will convert it to a hex timestamp (the value of `txTime`).
>- As long as you start push or playback before the expiration time and the stream is not interrupted, the push or playback can continue even after the URL expires.

### Playback URL for the transcoded stream
If a transcoding template is bound to your playback domain, and you want to play the transcoded stream, you need to append the template name (`_transcoding template name`) to the original playback URL.

For example, if the original playback URL is `http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)` and the name of the transcoding template bound is `hd`, the playback URL of the transcoded stream would be `http://domain/AppName/StreamName_hd.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`.

### Adaptive bitrate playback URL

Only HLS and WebRTC are supported for adaptive bitrate playback. The URL formats for the two protocols are different.
- To get an **HLS adaptive bitrate URL**, add the template name (`_adaptive bitrate template name`) after `StreamName` of the original playback URL.
For example, suppose the original playback URL is `http://domain/AppName/StreamName.m3u8?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)` and the name of the adaptive bitrate template bound is `autobitrate`.
The HLS adaptive bitrate URL would be `http://domain/AppName/StreamName_autobitrate.m3u8?txSecret=Md5(key+StreamName_autobitrate+hex(time))&txTime=hex(time)`.
- The format of a **WebRTC adaptive bitrate URL** is `Playback domain (`domain) + Application name (`AppName`, which is `live` by default)`, Stream ID (`StreamName`) + Authentication information + Adaptive bitrate stream names + Name of the initially played stream + Bitrate control mode`. The adaptive stream names are listed in descending order by bitrate.
Suppose the adaptive bitrate template bound has three streams. Their names are "test 1", "test 2", and "test 3", and their bitrates are 200 Kbps, 300 Kbps, and 400 Kbps respectively.
The WebRTC adaptive bitrate URL would be `webrtc://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)&tabr_bitrates=test3,test2,test1&tabr_start_bitrate=test1&tabr_control=auto`.




### H.265 playback URL
CSS supports pushing and playing H.265 streams. If the original stream is an H.264 stream, you can configure a transcoding template to transcode it into an H.265 stream. For details about how to do this in the console or by calling an API, see [Live Remuxing and Transcoding](https://intl.cloud.tencent.com/document/product/267/31561).
