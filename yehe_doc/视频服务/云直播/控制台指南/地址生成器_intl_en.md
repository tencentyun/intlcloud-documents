The CSS console provides an address generator. You can enter URL information in the generator to quickly generate push/playback URLs. The live streaming URL is mainly composed of a domain name (`domain`), an application name (`AppName`), a stream name (`StreamName`) and an authentication key (`Key`).
![](https://main.qcloudimg.com/raw/55879651fe2ca61a3699ab4ed9de41d4.jpg)
After an URL is generated, you can **select the URL and copy it**, **click the button next to it to copy it**, or **scan the QR code next to it to get it**.


## Notes
- CSS does not record previously generated URLs. Please copy a URL once it is generated.
- If you need to generate multiple live streaming URLs, we recommend that you splice them as instructed in [Splicing Live Streaming URLs](https://intl.cloud.tencent.com/document/product/267/38393).
- CSS provides a test domain name `xxxx.livepush.myqcloud.com`. You can use it for push testing, but we do not recommend using it as the push domain name for your real business.
- You can get a URL by scanning the QR code with [Tencent Cloud Toolkit](https://intl.cloud.tencent.com/document/product/1071/38147).
- If the stream name suffix is the same as the transcoding template ID, the stream cannot be played back. Under this situation, please change the stream name.



## Prerequisites
You have logged in to the [CSS console](https://console.cloud.tencent.com/live/livestat), and have added a [push domain name](https://intl.cloud.tencent.com/document/product/267/35970).

## Parameter Description

<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Domain Type</td>
<td>Select <strong>push domain</strong> or <strong>playback domain</strong>.</td>
</tr><tr><td>AppName</td>
<td>Live streaming application name, used to identify the live stream file storage path. Default value: `live`.<br>Only letters, digits, and symbols are allowed.</td>
</tr><tr><td>StreamName</td>
<td>Custom stream name. It is a unique identifier of a live stream.<br>Only letters, digits, and symbols are allowed.</td>
</tr><tr><td>Expiration Time</td>
<td><li>The expiration time of a playback URL is the configured time plus the playback authentication valid period.<li>The push URL expiration time is the same as the configured expiration time.</td>
</tr><tr><td>Transcoding Template</td>
<td><li>Applicable only when you select a <strong>playback domain</strong>.<li>If you select a <a href="https://intl.cloud.tencent.com/document/product/267/31071">transcoding template</a>, the generated URL will be the one for the transcoded stream. To play back the original live stream, you don't need to select a transcoding template.</td>
</tr>
</tbody></table>

[](id:push)
## Generating Push URL
### Directions
1. Log in to the CSS console and click **[Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)**.
2. Select **Push Domain** as the domain type, and select a push domain name that you have added on the domain management page.
3. Enter an **AppName**. It is `live` by default.
4. Enter a **StreamName**, such as `liveteststream`.
5. Select the expiration time of the URL, such as `2021-12-15 10:06:22`.
6. Click **Generate Address**.

![](https://qcloudimg.tencent-cloud.cn/raw/68d6cc91bb1092b418f5863f7d91e832.png)

[](id:pushurl)
### Notes
As the protocols RTMP, WebRTC, and SRT are supported for push, the push URLs generated start with `rtmp://`, webrtc://, or `srt://`.
![](https://qcloudimg.tencent-cloud.cn/raw/d866991901d2c780112da709d4e0ba3c.png)


[](id:play)
## Generating Playback URL
### Directions
1. Log in to the CSS console and click **[Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)**.
2. Select **Playback Domain** as the domain type, and select a playback domain name that you have added on the domain management page.
3. Enter an **AppName**. It is `live` by default.
4. Enter a **StreamName**, such as `liveteststream`.
5. Select the URL expiration time, such as `2021-12-15 10:20:26`.
6. Select whether to use a created transcoding template.
6. Click **Generate Address**.

![](https://qcloudimg.tencent-cloud.cn/raw/838b4bc6cf9df0c308f9636b1d7c06af.png)

[](id:playurl)
### Notes
If you select a transcoding template, the address generator will generate a URL for the transcoded stream. As the protocols RTMP, HTTP-FLV, HLS, and WebRTC are supported for playback, the playback URLs generated start with `rtmp://` `http://`, or `webrtc://`.
>! UDP playback URLs are for [LEB](https://intl.cloud.tencent.com/document/product/267/41030). To learn about the billing of LEB, see [Pricing Overview](https://intl.cloud.tencent.com/document/product/267/2819).

![](https://qcloudimg.tencent-cloud.cn/raw/345cc01a3d77d6816d1789fe60b7184e.png)
