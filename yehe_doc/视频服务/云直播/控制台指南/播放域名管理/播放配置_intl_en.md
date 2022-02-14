After the push via a domain name is successful, you can go to the CSS console, copy the `StreamName` in the push URL and then enter it in the playback address generator to generate a playback URL for the stream.

## Prerequisites
 - You have logged in to the [CSS console](https://console.cloud.tencent.com/live).
 - You have added a **playback domain name**. For more information, please see [Adding Domain Name](https://intl.cloud.tencent.com/document/product/267/35970).

## Directions
1. Select **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, and click the target **playback domain** or click **Manage** on the right to enter the domain management page.
2. Select **Playback Configuration** and, in **Playback Address Generator**, complete the following settings:
	1. Select whether you want to play the **original stream** or **transcoded stream**. If you select the latter, the stream will be transcoded according to the selected transcoding template before playback.
	2. Enter a custom `StreamName`, such as `liveteststream`. To play back the stream corresponding to the push URL, you need to enter the `StreamName` in the push URL.
	3. Select an expiration time, such as `2021-06-30 19:00:44`.
	4. Click **Generate Address**.
![](https://main.qcloudimg.com/raw/6bea977acb754ec9c36422aef3189f39.png)
3. If you haven’t enabled authentication for your playback domain, you can find four playback URLs in the **Playback URL** section, namely RTMP, FLV, HLS, and UDP URLs. Replace `StreamName` with your stream name and you can use the URLs to play the stream.
![](https://main.qcloudimg.com/raw/8d8a9ee63dc12045da418c1539051eb6.png)
>?For more information, please see [Live Playback](https://intl.cloud.tencent.com/document/product/267/31559).




## Playback URL
### Playback URL format
```
RTMP format: `rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`
FLV format: `http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`
M3U8 format: `http://domain/AppName/StreamName.m3u8?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`
UDP format: webrtc://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
```
- `domain`: your playback domain with an ICP license
- `AppName`: live streaming application name, which is `live` by default and customizable
- `StreamName`: custom stream name used to identify a live stream
- `txSecret`: authentication string generated after playback authentication is enabled
- `txTime`: timestamp in the playback URL added in the console. It indicates the expiration time of the URL.

>!
>- If you have enabled authentication, the actual expiration time of a URL will be `txTime` plus the validity period of the key.
>- For the sake of convenience, the time you set in the console is the actual expiration time. If you have enabled authentication, the system will calculate the `txTime` when generating playback URLs.
>- As long as you start push or playback before the expiration time and the stream is not interrupted, the push or playback can continue even after the URL expires.

### Playback URL of transcoded stream
If a transcoding template is configured for the playback domain name, `_transcoding template name` will be added after the `StreamName` in the original playback URL for the transcoded stream.

For example, if the original playback URL is `http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)` and the name of the transcoding template bound with the domain name is `hd`, the playback URL of the transcoded stream should be `http://domain/AppName/StreamName_hd.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`.

### Playback URL of H.265 stream
CSS supports pushing and playing back H.265 streams. If the original stream is an H.264 stream, you can use a transcoding template to transcode it into an H.265 stream. For details about transcoding via the console and through APIs, please see [Transcoding via the CSS console](https://intl.cloud.tencent.com/document/product/267/31561) and [Transcoding through APIs](https://intl.cloud.tencent.com/document/product/267/31561).
