[](id:que1)
### Is there an upper limit on the number of concurrent viewers?   
By default, CSS does not limit the number of online viewers for a live stream as long as the network and other conditions permit. However, if you have configured a bandwidth limit, new viewers cannot watch the live stream if there are so many existing viewers that the bandwidth limit is exceeded. In this case, the number of online viewers is limited.

[](id:que2)
### How do I use the live transcoding feature?
You can go to [Live Transcoding](https://console.cloud.tencent.com/live/config/transcode) to configure transcoding templates with different bitrates and resolutions for different network conditions. For more information on transcoding, see [Live Remuxing and Transcoding](https://intl.cloud.tencent.com/document/product/267/31561).

[](id:multirate)
#### Original definition, HD, and SD
The three commonly used playback bitrates for original, HD, and SD streams are as follows:
 - For original, the playback bitrate is the same as the bitrate used for push.
 - For HD, the recommended playback bitrate and resolution are 2,000 Kbps and 1080p.
 - For SD, the recommended bitrate and resolution are 1,000 Kbps and 720p.

[](id:que3)
### How do I use time shifting?
You can use the time shifting feature to rewind and play a video stream from earlier time points. The feature currently only supports the HLS protocol. For more information on time shifting and how to activate it, see [Time Shifting](https://intl.cloud.tencent.com/document/product/267/31565).

[](id:que4)
### How can I use HTTPS for playback?
To make your playback domain support HTTPS, make sure you have a valid certificate and private key, go to [Domain Management](https://console.cloud.tencent.com/live/domainmanage), find the target playback domain, click **Manage**, and select **Advanced Configuration** > **HTTPS Configuration** to add an HTTPS configuration. The configuration takes effect in about 2 hours.

[](id:que5)
### How can I use a cache node outside the Chinese mainland for playback?
CSS provides stable CDN nodes across the Chinese mainland and around the world. If your end users are located outside the Chinese mainland, you can select **Global** or **Outside Chinese mainland** for **Acceleration region** when adding domains in [Domain Management](https://console.cloud.tencent.com/live/domainmanage).


[](id:que6)
### How can I enable hotlink protection?
To prevent potential losses caused by unauthorized users using your URLs for playback and stealing your Tencent Cloud traffic, we strongly recommend you enable hotlink protection for your playback URLs. Hotlink protection is determined by four parameters: `txTime`, `key` (hash key), `txSecret`, and the validity period.

| Hotlink Protection Parameter | Description | Remarks |
|---------|---------|---------|
| txTime | The expiration time of the playback URL. |It must be a Unix hexadecimal timestamp.<br> Playback is allowed only if `txTime` is later than when a request is sent.|
| key | The MD5 key. | This parameter is customizable. You can set a primary and a backup key.<br> If your primary key is disclosed, you can use the backup key to splice playback URLs while changing the primary key.|
| txSecret | The encryption parameter in the playback URL. | The value of this parameter is calculated based on `key`, `StreamName`, and `txTime` using the MD5 algorithm. <br>`txSecret` = MD5 (key+StreamName+txTime) |
| Validity period | The authentication validity period. | It must be greater than 0.<br> If you set `txTime` to the current time and the validity period to 300s, the URL expiration time is the current time plus 300s.|

[](id:calculate)
#### Hotlink protection URL calculation
Three parameters are needed to generate a hotlink protection URL: `key` (a random string), `StreamName` (the stream name), and `txTime` (in hexadecimal format).
Assume that you set `key` to **somestring**, `StreamName` to **test**, `txTime` to **5c2acacc** (2019-01-01 10:05:00), the HD bitrate to **900 Kbps**, and the name of the transcoding template to **900**.
The playback URL of the original stream is:
```
txSecret = MD5(somestringtest5c2acacc) = b77e812107e1d8b8f247885a46e1bd34
http://domain/live/test.flv?txTime=5c2acacc&txSecret=b77e812107e1d8b8f247885a46e1bd34
http://domain/live/test.m3u8?txTime=5c2acacc&txSecret=b77e812107e1d8b8f247885a46e1bd34
```
The playback URL of the HD stream is:
```
txSecret = MD5(somestringtest_9005c2acacc) = 4beae959b16c77da6a65c7edda1dfefe
http://domain/live/test_900.flv?txTime=5c2acacc&txSecret=4beae959b16c77da6a65c7edda1dfefe
http://domain/live/test_900.m3u8?txTime=5c2acacc&txSecret=4beae959b16c77da6a65c7edda1dfefe
```

[](id:open)
#### Enabling hotlink protection
1. Select [Domain Management](https://console.cloud.tencent.com/live/domainmanage), and click the target playback domain name or click **Manage** on the right to enter the domain management page.
2. Select the **Access Control** tab. In the **Key Authentication** area, toggle on **Playback Authentication**.
3. Complete the settings in the pop-up window.
4. Click **Save** to save the configuration.

>!
>- It takes **30 minutes** for the configuration to take effect.
>- HTTP-FLV: Ongoing playback can continue even after `txTime`, but new playback requests will be rejected.
>- HLS: With HLS, a stream is broken into short chunks, and TS segments are requested as playback continues. Therefore, if you set `txTime` to 10 minutes after the current time, playback will be rejected after 10 minutes. To avoid this, you can update the HLS request URL dynamically on the server or set a longer validity period.

[](id:que7)
### What are the format requirements for a primary key for playback authentication? Is there any limit on its validity period?
The primary key can contain only letters and digits, with up to 256 characters. For details, please see [Playback Authentication Configuration](https://intl.cloud.tencent.com/document/product/267/31060).
We recommend that you set its validity period to the duration of a live streaming session.


[](id:que8)
### Can I generate a push URL that is valid for a long time? What is the upper limit of the validity period?
If you set the validity period too long, others may use your URL for push without your authorization.
There is no limit on the validity period of a push address. You can have your server automatically splice push URLs to generate URLs with longer validity periods. For detailed directions, see [Splicing Live Streaming URLs](https://intl.cloud.tencent.com/document/product/267/38393).

>? We do not recommend you set a very long validity period. It may cause errors and authentication failures.

[](id:que9)
### Will the Tencent Cloud logo be displayed on the live streaming image? 
No. 

[](id:que10)
### How long is the latency in live streaming? 
Normally, the latency of playing an FLV stream that is pushed over RTMP is around 2-3 seconds. If your playback latency is exceptionally high, please refer to [Troubleshooting High Latency](https://intl.cloud.tencent.com/document/product/267/7971) to troubleshoot the issue.

[](id:que11)
### Can I modify the maximum bitrate during live streaming?
 No. You can set it only before pushing a stream. The bitrate depends on your upload speed. Setting it too high may cause dropped frames and stuttering. 

[](id:que12)
### How do I delete a live streaming room which is no longer used? 
Live push and playback are bound with stream IDs, so you do not need to delete rooms. If you are using the IM service and want to delete IM rooms to avoid reaching the maximum number of rooms, see [Disbanding a Group](https://intl.cloud.tencent.com/document/product/1047/34896).
If you are using channel mode, you can call the `DeleteLVBChannel` API to delete channels (you need to pass in the IDs of the channels you want to delete).

> ! Channel mode is a legacy mode which is no longer updated or maintained.

[](id:que13)
 ### When do I use the push enabling/disabling API? 
You can use the API to disable a live stream when pornographic or other inappropriate content is detected. For details, see [ForbidLiveStream](https://intl.cloud.tencent.com/document/product/267/30794).


[](id:que14)
### How do I implement playback in the background?
Background playback allows the audio of a live stream to continue even when your app runs in the background. This feature depends on the playback device and should be implemented based on your actual business logic.


[](id:que15)
### What should I do if the "incorrect certificate" error occurs when I modify my HTTPS configuration? 
 CSS uses Nginx for encryption, so make sure your certificate type is Nginx.

[](id:que16)
### Why do my playback URLs stop working after I disable playback authentication? 
 An authentication-enabled playback URL will become invalid after authentication is disabled, even if the validity period has not elapsed. 

[](id:que17)
### What are API rate limits?
CSS sets an upper limit on the total number of requests sent by all `SecretId` under an account. After the limit is reached, new requests will not be responded to.
For example, an upper limit of 200 requests per second indicates that the Tencent Cloud server can receive up to 200 requests sent by all `SecretId` under your account within one second. It doesn’t matter whether the requests are sent by one or more users, or whether they query one or multiple streams. 

[](id:que18)
### The "RTMP close" error occurs when I push streams, but the log says the push is successful. What should I do? 
The problem may lie in your push URL. You can use our [TCToolkit app](https://intl.cloud.tencent.com/document/product/1071/38147) to test whether the URL works normally. For more solutions, see [Troubleshooting Push Failure](https://intl.cloud.tencent.com/document/product/267/33383).

[](id:que19)
### I failed to push streams after changing the frame rate, had to restart the service multiple times, and was frequently disconnected. What should I do? 
You may have set the frame rate too high. A frame rate higher than 15 fps is enough to ensure smooth playback. Try reducing the frame rate.  

[](id:que20)
### If a stream has no data for a long time, when will it be disconnected? 
A stream may have no data for a long time when there is a push problem, for example, if the app crashes or the phone is turned off.
In such cases, if the backend doesn’t receive any data for 70 seconds, it will disconnect the stream.

[](id:que21)
### How do I configure an API key in the new console?
API keys are used for the authentication of legacy APIs. We have updated our APIs to v3.0. To use the new APIs, go to [Manage API Key](https://console.cloud.tencent.com/cam/capi) to get the `SecretId` and `Secretkey`.

[](id:que21)
### Why can’t I play a H.265-encoded video?
H.265 is supported by fewer browsers than H.264, and playback may fail if your browser does not support H.265. You can [configure a transcoding template](https://intl.cloud.tencent.com/document/product/267/31071) to transcode the video to H.264.

[](id:que22)
### Can the names of M3U8 files contain Chinese characters?
M3U8 files are named automatically based on stream names. Stream names **do not support** Chinese characters.

[](id:que23)
### How do I view the number of online viewers?
You can get the number of online viewers by calling the [DescribeStreamPlayInfoList](https://intl.cloud.tencent.com/document/product/267/37297) API, but the result may not be 100% accurate. For example, if three users use the same IP address for playback at the same time, they will be counted as one viewer. Note that the data returned by this API is relevant only if your playback protocol is RTMP or FLV, not if it is HLS.

[](id:que24)
### Does CSS support backup streams?
Backup streams are enabled by default with CSS. If you push two streams using the same stream name at the same time, during playback, only the first stream will be visible. If this stream is interrupted, the second stream will become visible.

[](id:que25)
### Can I add different watermarks for the same push domain?
No, you can’t. You can bind only one watermark template to each push domain.

[](id:que26)
### How do I view users’ playback durations?
You cannot view users’ playback durations currently.

[](id:que27)
### Can users watch my live streams if I don’t transcode the streams?
Yes. Playback is based on playback URLs and is possible even if you don’t transcode the streams (as long as the URL is valid).

[](id:que28)
### What factors affect the time to the first frame?
The time to the first frame depends mainly on the number of viewers. The more viewers, the higher the cache hit ratio and the shorter the time to the first frame.

[](id:que9)
### Can I create a blocklist/allowlist for playback?
You can configure a custom IP allowlist or blocklist to control access to your live streams based on IP addresses. For detailed directions, see [Configuring IP Allowlist/Blocklist](https://intl.cloud.tencent.com/document/product/267/46767#configuring-ip-allowlist.2Fblocklist).
- **IP allowlist**: Only IP addresses on the list can access your streaming content.
- **IP blocklist**: IP addresses on the list cannot access your streaming content.

[](id:que30)
### How many screenshots are taken for porn detection?
CSS identifies pornographic content based on screenshots. The number of screenshots taken for porn detection depends on the screenshot interval, which you can set in [Live Screencapture & Porn Detection](https://console.cloud.tencent.com/live/config/jtjh) of the CSS console.
>? The default screenshot interval during push is two seconds. Value range: 2-300 (seconds).

[](id:que31)
### How do I query my billable bandwidth and traffic?
You can use the [DescribeBillBandwidthAndFluxList](https://intl.cloud.tencent.com/document/product/267/36098) API to query the data.

[](id:que32)
### How do I know if push is successful?
- If push is successful, the stream generated will appear in [Stream Management](https://console.cloud.tencent.com/live/streammanage) > **Live Streams** of the CSS console.
- You can also call the [DescribeLiveStreamState](https://intl.cloud.tencent.com/document/product/267/30796) API to query stream status.

>? When push or playback fails, you can use the [self-diagnosis tool](https://console.cloud.tencent.com/live/tools/selfcheck) of the CSS console to troubleshoot the issue. For details, see [Self-Diagnosis](https://intl.cloud.tencent.com/document/product/267/39467).

[](id:que33)
### Can I push audio-only streams?
CSS supports pushing audio-only streams (streaming software is required). You can also create audio-only transcoding templates.
- [Pushing audio-only streams with OBS](https://intl.cloud.tencent.com/document/product/267/31569).
- [Creating a transcoding template](https://intl.cloud.tencent.com/document/product/267/30790)

[](id:que34)
### How do I query live streaming durations?
You can call an RESTful API to query the data. For details, see [DescribeStreamPlayInfoList](https://intl.cloud.tencent.com/document/product/267/37297).

[](id:que35)
### How do I query the duration of an active stream?
CSS does not offer an API to query the duration of an active stream. You can calculate the duration based on the callbacks for push and stream interruption.

[](id:que37)
### How do I query the viewers of a live stream?
You can query the viewers of a live stream using either of two methods:
- Go to the CSS console, select **Data Center** > **Stream Data Query** on the left sidebar, and click **Playback Data** to view the number of concurrent connections.
>? The number of concurrent connections equals the number of online viewers only if the playback protocol is RTMP or FLV.

- Call the [DescribeStreamPlayInfoList](https://intl.cloud.tencent.com/document/product/267/37297) API to get the number of online viewers.

[](id:que38)
### If I’m disconnected after pushing a stream, will I receive the callback for stream interruption?
You need to configure the callback for stream interruption first. If a stream is interrupted by a network disconnection, the system will try to resume the stream automatically. If the stream is resumed within 70 seconds, you will not receive the callback for stream interruption. If the system fails to resume the stream within 70 seconds, it will disconnect the stream, and you will receive the stream interruption callback.

[](id:que39)
### Do I need to use the same protocol for push and playback?
No. You can use RTMP for push and RTMP, FLV, HLS, or UDP for playback.

[](id:que40)
### Why can’t I play videos from CDNs when I use a wireless network?
Check the following:
- Check whether your wireless network has blocked Tencent Cloud’s IP addresses.
- If you use iPhone, make sure you have allowed the app to use Wi-Fi.

If the above does not solve your problem, please contact Tencent Cloud technical support.

[](id:que41)
### I configured HTTPS for my playback domain, so why did playback fail?
Check the following:
- Make sure you have uploaded a certificate.
- Check your certificate upload time. After configuring HTTPS, please wait about two hours before accessing the domain.

>? If the above does not solve your problem, try using the [self-diagnosis tool](https://console.cloud.tencent.com/live/tools/selfcheck) of the CSS console to identify the issue. For detailed directions, see [Self-Diagnosis](https://intl.cloud.tencent.com/document/product/267/39467).



[](id:que42)
### With LEB, how do I change the resolution of hosts during live streaming?
LEB is a playback solution, while hosts are at the push end. To change the resolution of hosts, you need to create a [transcoding template](https://intl.cloud.tencent.com/document/product/267/31071) and bind it to your domain before playback.
