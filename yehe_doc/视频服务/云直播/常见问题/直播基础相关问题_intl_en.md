<span id="Que1"></span>
### What are the differences between push, LVB, and VOD?
- **Push**: this refers to the process in which the host pushes local video and audio sources to Tencent Video Cloud servers. It is also known as "RTMP publishing" in some cases.
- **LVB**: LVB video source is generated in real time. It is only meaningful if someone pushes a live stream. Once the host stops streaming, the LVB URL will become invalid, and since the live streams are played back in real time, no progress bar will be displayed on the player during the playback.   
- **VOD**: a video source in VOD is a file in the cloud, which can be played back at any time as long as it is not deleted by the provider (such as Youku Tudou, iQIYI, and Tencent Video). Since the entire video file is stored on the server, a progress bar will be displayed during the playback.

<span id="Que2"></span>
### What are the requirements for a playback domain name in LVB?	
You need to apply for an ICP filing for your domain name for service in Mainland China before submitting it to the console for management. The domain name can contain up to 29-bit characters and cannot contain uppercase letters.

<span id="Que3"></span>
### Can the playback and push domain names in LVB be the same? Can I use second-level domain names for them?
The connected playback and push domain names must be different, but they can be distinguished between with second-level domain names.
For example, `123.abc.com` can be used as the push domain name, while `456.abc.com` the playback domain name.


<span id="Que4"></span>
### What push protocols are supported?
Although RTMP is not commonly used in live streaming, it is dominant in push service (pushing data from "host" to "server"). Most Chinese video cloud services use RTMP as the main push protocol. MLVB SDK's first module is host push, so the SDK is also called RTMP SDK.

<span id="Que5"></span>
### What playback protocols are supported?
Three LVB protocols are commonly used: RTMP, FLV, and HLS.
- **RTMP**: the RTMP protocol can be used for both push and live streaming. It involves breaking large video and audio frames into smaller fragments and transmitting them as small packets over the internet. RTMP supports encryption and thus ensures privacy. However, its complicated fragmentation and reassembling process brings about some unforeseeable stability issues in high-concurrency scenarios. 
- **FLV**: the FLV protocol is mainly implemented by Adobe. It simply places header information into large video and audio frame headers. This simplicity makes it a sophisticated format in terms of delay control and high-concurrency performance. Its only disadvantage is the limited capability on mobile browsers. However, it is especially suitable for LVB on mobile apps.  
- **HLS**: this solution is provided by Apple. It divides a video into video segments of 5–10s in length and then manages them with an m3u8 index table. As the video segments downloaded by the client contain full data of 5–10s, video playback can be very smooth. However, this causes a high delay (about 10–30s in general). Compared with FLV, HLS features better compatibility with iPhone and most Android browsers, so it is often used for URL-based sharing on QQ and WeChat Moments.

| LVB Protocol | Advantage | Disadvantage | Playback Delay |
|::|::|::|::|
| FLV | High maturity and performance in high-concurrency scenarios | SDK integration is required for playback | 2–3s |
| RTMP | Lowest delay on high-quality connections in theory | Poor performance in high-concurrency scenarios | 1–3s |
| HLS (m3u8) | Highest compatibility with mobile browsers | Extremely high delay |10–30s|

<span id="Que6"></span>
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


<span id="Que7"></span>
### What are common push methods?
- **Camera on Android/iOS devices**: use third-party software or MLVB SDK to capture camera video and push the video stream to the push address.
- **Camera or screencapturing tool on desktops/laptops**: use third-party software to capture camera video or screen and push the video or screen content to the push address. Third-party push applications include [OBS (recommended)](https://intl.cloud.tencent.com/document/product/267/31569), XSplit, FMLE, etc.
- **Video capturing device**: if an HD camcorder has an HDMI or SDI output interface, it can be connected to an encoder to push live content to LVB through RTMP push. You need to configure the push address as the RTMP publishing address of the encoder.
For a webcam, if it supports RTMP push, you can configure the LVB push address as its RTMP publishing address.
- **Video file converted to video stream**: read a video file and use RTMP stream output as a video source to push the video to the RTMP push address of LVB for video publishing. This can be done with the `ffmpeg` command (which works on Windows, Linux, and macOS).

<span id="Que8"></span>
### What are the differences between stream interruption and stream forbidding?
- **Stream interruption**: if a stream that is being streamed is interrupted, the push will stop, and viewers will be unable to watch the stream. When a stream interruption occurs, the host can initiate the push again to resume the stream.
- **Stream forbidding**: if a stream that is being streamed is forbidden, the push will stop, and viewers will be unable to watch the stream. When a stream forbidding occurs, the host cannot initiate the push again during the forbidding duration. The stream forbidding feature can be configured on the stream management page in the LVB Console. The forbidden stream will be displayed in the forbidden stream list, and it can be recovered by clicking **Enable**.
