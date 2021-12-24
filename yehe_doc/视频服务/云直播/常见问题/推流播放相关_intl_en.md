[](id:que1)
### Is there an upper limit on the number of concurrent viewers?   
By default, CSS does not limit the number of online viewers for a live stream as long as the network and other conditions permit. However, if you have configured a bandwidth limit, new viewers cannot watch the live stream if there are so many existing viewers that the bandwidth limit is exceeded. In this case, the number of online viewers is limited.

[](id:que2)
### How do I use transcoding for playback?
You can go to [Live Transcoding](https://console.cloud.tencent.com/live/config/transcode) to configure transcoding templates with different bitrates and resolutions for different network conditions. For more information on transcoding, see [Live Remuxing and Transcoding](https://intl.cloud.tencent.com/document/product/267/31561).

[](id:multirate)
#### Original definition, HD, and SD
Streams of original definition, HD, and SD streams are commonly used in business scenarios.
 - For the original stream, playback bitrates and resolutions are the original values.
 - For an HD stream, the bitrate of 2,000 Kbps and resolution of 1080p are recommended for playback.
 - For an SD stream, the bitrate of 1,000 Kbps and resolution of 720p are recommended for playback.

[](id:que3)
### How can I use time shifting for playback?
You can use the time shifting feature to replay highlights. The feature supports only the HLS protocol for the time being. For more information on time shifting and how to activate it, see [CSS Time Shifting](https://intl.cloud.tencent.com/document/product/267/31565).

[](id:que4)
### How can I use HTTPS for playback?
To make your playback domain support HTTPS, you should prepare a valid certificate and a valid private key, go to [Domain Management](https://console.cloud.tencent.com/live/domainmanage), find the desired playback domain name, click **Manage**, and select **Advanced Configuration** > **HTTPS Configuration** to add a configuration. After the configuration is successfully added, it will take effect in 2 hours, and then, your stream can be played back using the HTTPS protocol.

[](id:que5)
### How can I use an acceleration node outside the Chinese mainland for playback?
CSS provides stable CDN cache nodes across Chinese mainland and around the world. If your end users are located outside the Chinese mainland, you can select **Global** or **Outside Chinese mainland** as the acceleration region when configuring a domain name in [Domain Management](https://console.cloud.tencent.com/live/domainmanage).


[](id:que6)
### How can I enable hotlink protection?
You are strongly advised to enable hotlink protection for your playback URLs to prevent unauthorized users from using your playback URLs, which would consume your Tencent Cloud traffic and thus cause losses. CSS hotlink protection for playback URLs is controlled by `txTime`, `key` (hash key), `txSecret`, and validity period.

| Hotlink Protection Parameter | Description | Remarks |
|---------|---------|---------|
| txTime | Expiration time of the playback URL |It is a Unix hexadecimal time.<br> If `txTime` is greater than the time of a request, the stream can be played back successfully; otherwise, the request will be rejected.|
| key | MD5 key | You can customize this parameter, and you can set a primary and a backup key.<br> If your primary key is leaked, you can use the backup key to splice playback URLs and change the value of the primary key.|
| txSecret | Encryption parameter in the playback URL | The value of this parameter is calculated based on `key`, `StreamName`, and `txTime` using the MD5 algorithm. <br>`txSecret` = MD5 (key+StreamName+txTime) |
| Validity period | Authentication validity period | It must be greater than 0.<br> If you set `txTime` to the current time and the validity period to 300s, the playback URL expiration time is the current time plus 300s.|

[](id:calculate)
#### Hotlink protection URL calculation
The calculation of a hotlink protection URL requires three parameters: `key` (a random string), `StreamName` (stream name), and `txTime` (in hexadecimal format).
Suppose you set `key` to **somestring**, `StreamName` to **test**, `txTime` to **5c2acacc** (2019-01-01 10:05:00), the HD bitrate to **900 Kbps**, and the name of the transcoding template to **900**.
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
1. Log in to the CSS console and click [Domain Management](https://console.cloud.tencent.com/live/domainmanage).
2. Find and click your playback domain name, or click **Manage** to enter the domain name details page.
3. Select **Access Control** and click **Edit**.
4. Enable **Playback Authentication** and click **Save**.

>!
>- It takes **30 minutes** for the configuration to take effect.
>- HTTP-FLV: after the `txTime` of the URL is reached, ongoing playback will continue, but new requests for playback via the URL will be rejected.
>- HLS: as HLS breaks a stream into short chunks, it keeps requesting M3U8 files to get the latest TS segments. Suppose you set `txTime` to the current time and the validity period to 10 minutes, then an HLS playback URL request sent 10 minutes after the current time will be rejected. To avoid this, you can update the HLS request URL dynamically on the server or set a greater expiration time point.

[](id:que7)
### What format requirements must a primary key for playback authentication meet? Is there any limit on its validity period?
The primary key can contain only letters and digits, with up to 256 characters. For details, see [Playback Authentication Configuration](https://intl.cloud.tencent.com/document/product/267/31060).
We recommend that you set its validity period to the duration of a live streaming session.


[](id:que8)
### Can I create a push URL that is valid for a long time? What is the maximum duration of the validity period?
Setting a push URL validity period is for authentication and protection. A permanently valid push URL can hardly prevent unauthorized push and may result in business losses.
There is no limit on the validity period of a push address, which can be set according to your business needs. You can also splice addresses to generate a push URL with a longer validity period. For more information about splicing rules, see [How to Splice a Push URL](https://intl.cloud.tencent.com/document/product/267/38393).

>? We do not recommend setting a very long validity period for the push URL, which may cause an error to occur and failed authentication to be reported when the URL is used.

[](id:que9)
### Will the Tencent Cloud logo be displayed on the live streaming image? 
No. 

[](id:que10)
### How long is the latency in live streaming? 
Under normal circumstances, playback of an FLV stream pushed over the RTMP protocol has a latency of around 2–3 seconds. A higher latency generally means that there is a problem. For more information on troubleshooting, see [High Latency](https://intl.cloud.tencent.com/document/product/267/7971).

[](id:que11)
### Can I modify the maximum bitrate during live streaming?
 No. You can set it only before pushing the stream according to the upload speed of the network. Besides, setting it too high may cause dropped frames and stuttering. 

[](id:que12)
### How do I delete a live streaming room which is no longer used? 
Live push and playback are bound with stream IDs, so you do not need to delete rooms. If you are using the IM service and want to delete IM rooms to avoid reaching the upper limit of room number, see [Disbanding a Group](https://intl.cloud.tencent.com/document/product/1047/34896).
If you are using the channel mode, you can call the `DeleteLVBChannel` API and pass in IDs of live streaming channels to delete them in batches.

> ! Channel mode is a legacy mode which is no longer updated or maintained.

[](id:que13)
 ### What is the usage of the API for enabling/disabling push? 
This API is used to disable a stream when porn detection is performed. For example, if a live stream is detected to contain pornographic or terroristic contents, you can interrupt or disable this stream at any time.


[](id:que14)
### How do I develop the audio playback feature in the background?
The background audio playback feature is provided by devices. You can develop this feature according to the actual business logic. As long as the live stream is not interrupted, its audio can be played back in the background.


[](id:que15)
### What should I do if the "incorrect certificate" message is displayed when I modify HTTPS configuration? 
 Make sure your current certificate type is Nginx as CSS uses Nginx for encryption.

[](id:que16)
### After authentication is disabled for a playback URL, why cannot it be used for playback? 
 An authentication-enabled playback URL will become invalid after authentication is disabled, even when its expiration time is not reached. 

[](id:que17)
### What is the upper limit of the total number of API requests?
CSS sets an upper limit on the total number of requests sent by all `SecretId` under an account. After the limit is reached, new requests will not be responded.
For example, an upper limit of 200 requests per second indicates that Tencent Cloud server can receive up to 200 requests sent by all `SecretId` under your account within 1s. The 200 requests can be sent by one or more customers, and can be used to query one or more streams. 

[](id:que18)
### What should I do if "RTMP close" is displayed during push and the push fails, but the log notifies a successful push? 
It may be that there is a problem with your current push URL. We recommend you use the [trial demo](https://intl.cloud.tencent.com/document/product/1071/38147) to test whether the URL works normally. For more information on troubleshooting, see [Troubleshooting Push Failure](https://intl.cloud.tencent.com/document/product/267/33383).

[](id:que19)
### What should I do if the stream cannot be pushed normally after I modify the frame rate, the push needs to be restarted several times, and the stream is frequently interrupted? 
Maybe the current frame rate is too high. A frame rate higher than 15 fps is enough to ensure smooth video playback. You’re advised to set a lower frame rate.  

[](id:que20)
### When will the system interrupt a stream with no data generated for a long time? 
The system will interrupt a stream when exceptions occur on the push device.
Such exceptions may be application crash, mobile phone shutdown and other external reasons, which cause no data of the stream to be collected in the backend within 70s, and then the system will interrupt the stream.

[](id:que21)
### How do I configure the API key in the new console?
The API key is used for authentication of legacy APIs, which have been upgraded to v3.0 at the official website. You can get the `SecretId` and `Secretkey` on the **[API Key Management](https://console.cloud.tencent.com/cam/capi)** page to use API 3.0.

[](id:que21)
### Why can't an H.265 video be played back?
As H.265 is not as compatible as H.264, if a player doesn't support H.265 and the playback fails, you can configure a [transcoding template](https://intl.cloud.tencent.com/document/product/267/31071) to transcode the video to H.264 for playback.

