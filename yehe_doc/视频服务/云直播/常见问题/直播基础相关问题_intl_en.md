### What are the differences between push, LVB, and VOD?
- **Push**: this refers to the process in which the host pushes local video and audio sources to Tencent Video Cloud servers. It is also known as "RTMP publishing" in some cases.
- **LVB**: LVB video source is generated in real time. It is only meaningful if someone pushes a live stream. Once the host stops broadcasting, the LVB URL will become invalid, and since the live streams are played back in real time, no progress bar will be displayed on the player during the playback.   
- **VOD**: a video source in VOD is a file in the cloud, which can be played back at any time as long as it is not deleted by the provider (such as Youku Tudou, iQIYI, and Tencent Video). Since the entire video file is stored on the server, a progress bar will be displayed during the playback.

### What push protocols are supported?
Although RTMP is not commonly used in live broadcasting, it is dominant in push service (pushing data from "host" to "server"). Most Chinese video cloud services use RTMP as the main push protocol. MLVB SDK's first module is host push, so the SDK is also called RTMP SDK.

### What playback protocols are supported?
Three LVB protocols are commonly used: RTMP, FLV, and HLS.
- **RTMP**: the RTMP protocol can be used for both push and live broadcasting. It involves breaking large video and audio frames into smaller fragments and transmitting them as small packets over the internet. RTMP supports encryption and thus ensures privacy. However, its complicated fragmentation and reassembling process brings about some unforeseeable stability issues in high-concurrency scenarios. 
- **FLV**: the FLV protocol is mainly implemented by Adobe. It simply places header information into large video and audio frame headers. This simplicity makes it a sophisticated format in terms of delay control and high-concurrency performance. Its only disadvantage is the limited capability on mobile browsers. However, it is especially suitable for LVB on mobile apps.  
- **HLS**: this solution is provided by Apple. It divides a video into video segments of 5–10s in length and then manages them with an m3u8 index table. As the video segments downloaded by the client contain full data of 5–10s, video playback can be very smooth. However, this causes a high delay (about 10–30s in general). Compared with FLV, HLS features better compatibility with iPhone and most Android browsers, so it is often used for URL-based sharing on QQ and WeChat Moments.

| LVB Protocol | Advantage | Disadvantage | Playback Delay |
|::|::|::|::|
| FLV | High maturity and performance in high-concurrency scenarios | SDK integration is required for playback | 2–3s |
| RTMP | Lowest delay on high-quality connections in theory | Poor performance in high-concurrency scenarios | 1–3s |
| HLS (m3u8) | Highest compatibility with mobile browsers | Extremely high delay |10–30s|

### What does a playback address consist of?
A Tencent Cloud playback address is mainly composed of playback prefix, playback domain name (`domain`), application name (`AppName`), stream name (`StreamName`), playback protocol suffix, authentication parameter, and other custom parameters as shown below:
```
rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
http://domain/AppName/StreamName.m3u8?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
https://domain/AppName/StreamName.m3u8?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
https://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
```
- **Playback prefix**
RTMP playback protocol: **rtmp://**.
HTTP-FLV playback protocol: **http://** or **https://**.
HLS playback protocol: **http://** or **https://**.

- **Application name (`AppName`)**
Application name refers to the storage path of a live streaming media file. By default, LVB assigns a unified path: **live**.

- <span id="streamname">**Stream name (`StreamName`)**</span>
Stream name (`StreamName`) is the unique identifier of a live stream.

- **Authentication parameter and other custom parameters**
Authentication parameter: **txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)**.

### What are common push methods?
- **Camera on Android/iOS devices**: use third-party software or MLVB SDK to capture camera video and push the video stream to the push address.
- **Camera or screencapturing tool on desktops/laptops**: use third-party software to capture camera video or screen and push the video or screen content to the push address. Third-party push applications include [OBS (recommended)](https://intl.cloud.tencent.com/document/product/267/31569), XSplit, FMLE, etc.
- **Video capturing device**: if an HD camcorder has an HDMI or SDI output interface, it can be connected to an encoder to push live content to LVB through RTMP push. You need to configure the push address as the RTMP publishing address of the encoder.
For a webcam, if it supports RTMP push, you can configure the LVB push address as its RTMP publishing address.
- **Video file converted to video stream**: read a video file and use RTMP stream output as a video source to push the video to the RTMP push address of LVB for video publishing. This can be done with the `ffmpeg` command (which works on Windows, Linux, and macOS).

### What are the differences between stream interruption and stream forbidding?
- **Stream interruption**: if a stream that is being broadcasted is interrupted, the push will stop, and viewers will be unable to watch the stream. When a stream interruption occurs, the host can initiate the push again to resume the stream.
- **Stream forbidding**: if a stream that is being broadcasted is forbidden, the push will stop, and viewers will be unable to watch the stream. When a stream forbidding occurs, the host cannot initiate the push again during the forbidding duration. The stream forbidding feature can be configured on the stream management page in the LVB Console. The forbidden stream will be displayed in the forbidden stream list, and it can be recovered by clicking **Enable**.

### How can I use live transcoding?
In consideration of different network factors and to meet your needs for different resolutions at different bitrates, you can set transcoding templates with different bitrates and resolutions in [Transcoding Configuration](https://console.cloud.tencent.com/live/config/transcode). For more information on transcoding, please see [Best Practice - LVB Remuxing and Transcoding](https://intl.cloud.tencent.com/document/product/267/31561).

 #### <span id="multirate">Original, HD, and SD</span>
In a real playback scenario, three bitrates are generally used: original, HD, and SD.
 - For an original stream, the push bitrate is the same as the original resolution.
 - For an HD stream, bitrate of 2,000 Kbps and resolution of 1080p are recommended.
 - For an SD stream, bitrate of 1,000 Kbps and resolution of 720p are recommended.

### How can I use time shifting for replay?
If you want to replay highlights, you can use the time shifting feature which only supports the HLS protocol. 

### How can I use HTTPS for playback?
If your playback domain name needs to support HTTPS, you should prepare a valid certificate and a valid private key, go to [Domain Management](https://console.cloud.tencent.com/live/domainmanage), and select **Playback Domain Name Management** > **Advanced Configuration** > **HTTPS Configuration** to add a configuration. After the configuration is successfully added, it will take effect in 2 hours, and then, your stream can be played back with the HTTPS protocol.

### How can I use a global cache node for playback?
LVB has CDN nodes across Mainland China and around the world with wide coverage and high stability. If your end users are located outside Mainland China, you can select **Global Acceleration** or **Hong Kong/Macao/Taiwan (China Region) and other regions** as the acceleration region when configuring a domain name in [Domain Management](https://console.cloud.tencent.com/live/domainmanage) to enjoy coverage by global nodes.
> The global acceleration of LVB supports only HTTP-FLV and HLS protocols.

### How can I enable hotlink protection?
In order to prevent malicious users from stealing your playback URL for use elsewhere that may cause traffic losses, you are strongly recommended to enable hotlink protection for your playback address to avoid potential losses caused by hotlinking. A hotlink protection-enabled playback URL in LVB is mainly controlled by four parameters: `txTime`, `key` (hash key), `txSecret`, and validity period.

| Hotlink Protection Parameter | Description | Remarks |
|---------|---------|---------|
| txTime | Effective time of playback URL | This parameter is in hexadecimal UNIX time. <br>If the current value of `txTime` is greater than the current request time, the stream can be played back normally; otherwise, the playback will be rejected by the backend. |
| key | Key for MD5 calculation | This parameter can be customized. You can set a master key and a slave key, <br>so that if your master key is accidentally leaked, you can use the slave key to splice the playback URL and change the value of the master key. |
| txSecret | Encryption parameter in playback URL | The value of this parameter is obtained by performing MD5 encryption on the spiced string by `key`, `StreamName`, and `txTime`. <br>txSecret = MD5(key+StreamName+txTime). |
| Validity period | Validity period of address | The validity period must be set to greater than 0. <br>If `txTime` is set to the current time and the validity period is 300 seconds, then the playback URL expiration time is the current time + 300 seconds. |

#### Hotlink protection URL calculation
The calculation of a hotlink protection URL requires three parameters: `key` (a random string), stream name (`StreamName`), and `txTime` (in hexadecimal format).
Suppose that the `key` you set is **somestring**, the stream name (`StreamName`) is **test**, the `txTime` is **5c2acacc** (2019-01-01 10:05:00), the HD bitrate is **900 Kbps**, and the transcoding template name is **900**, then:
Original stream playback address:
```
txSecret = MD5(somestringtest5c2acacc) = b77e812107e1d8b8f247885a46e1bd34
http://domain/live/test.flv?txTime=5c2acacc&txSecret=b77e812107e1d8b8f247885a46e1bd34
http://domain/live/test.m3u8?txTime=5c2acacc&txSecret=b77e812107e1d8b8f247885a46e1bd34
```
HD stream playback address:
```
txSecret = MD5(somestringtest_9005c2acacc) = 4beae959b16c77da6a65c7edda1dfefe
http://domain/live/test_900.flv?txTime=5c2acacc&txSecret=4beae959b16c77da6a65c7edda1dfefe
http://domain/live/test_900.m3u8?txTime=5c2acacc&txSecret=4beae959b16c77da6a65c7edda1dfefe
```

#### Enabling hotlink protection
1. Go to [Domain Management](https://console.cloud.tencent.com/live/domainmanage).
2. Select a playback domain name or click **Manage** to enter its details page.
3. Select **Access Control** and click **Edit**.
4. Set **Playback Authentication** to "On" and click **Save**.

>
>- It takes **30 minutes** for the authentication configuration to take effect.
>- HTTP-FLV: the URL of the current playback will be able to continue playing back the stream after `txTime` expires but will be rejected when it requests a playback again.
>- HLS: as HLS uses a short link, it will continuously request .m3u8 files to get the latest ts segment. For example, if you set the value of `txTime` to the current time + 10 minutes, the HLS playback URL request will be rejected after 10 minutes. To solve this problem, you can dynamically update the HLS request address on the server or set the expiration time of the HLS playback address to be longer.

### How can I view the sample push code?
1. Log in to the LVB Console and enter **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**.
2. Select a push domain name or click **Manage** on the right to enter its details page.
3. Select **Push Configuration** and scroll down to find **Push Address Sample Code**. You can view the PHP/Java sample code by switching tabs.

