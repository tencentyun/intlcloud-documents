[](id:Que1)
### What are publishing, live streaming, and video on demand?
- **Publishing**: Stream publishing is the process of hosts publishing local video and audio to Tencent Video Cloud servers. It is sometimes called "RTMP publishing" as well.
- **Live streaming**: In live streaming, video streams are generated in real time. It works only if someone is publishing live streams. A live streaming URL becomes invalid the moment the host stops publishing streams. Because live streams are played back in real time, audience cannot see a progress bar during live streaming.   
**Video on demand**: In video on demand, it is the files in the cloud that are played back. Unless a file is deleted by its provider (e.g., Tencent Video), playback is possible at any time. Because videos are already stored in the server, audience can see a progress bar during playback.

[](id:Que2)
### What are the requirements for a playback domain name in CSS? 
The domain name can contain up to 29 characters and cannot contain uppercase letters. For more information, please see [Adding Domain Name](https://intl.cloud.tencent.com/document/product/267/35970).

[](id:Que3)
### Can I use the same domain name for playback and publishing? Can I use second-level domains?
You must use different domain names for playback and publishing, but you can distinguish them by second-level domains.
For example, you can use `123.abc.com` for publishing, and `456.abc.com` for playback.


[](id:Que4)
### What publishing protocols can I use?
RTMP may not be a widely adopted protocol for live streaming, but it is the most common protocol used for stream publishing (publishing data from hosts to servers). Most video cloud services in the Chinese mainland use RTMP as their main publishing protocol. The MLVB SDK is also called RTMP SDK because its first feature module is stream publishing.

[](id:Que5)
### What playback protocols can I use?
Common live streaming protocols include RTMP, HTTP-FLV, HLS, and WebRTC.
- **RTMP** can be used for both publishing and playback. It works by splitting long video and audio chunks into short fragments and transmitting them as small data packets over the internet. RTMP supports encryption and therefore ensures privacy. However, the complicated splitting and reassembling processes add uncertainty to the stability of data transmission in high concurrency scenarios. 
- **HTTP-FLV** is developed by Adobe Systems and is a rather simple video format. It works by adding a header to large video and audio data chunks. This simplicity gives it a notable advantage in terms of latency control and high-concurrency performance. The only drawback is that HTTP-FLV is poorly supported on mobile browsers, but it is an ideal option for mobile apps.  
- **HLS** is released by Apple. It breaks video streams into fragments of 5-10s and manages them using M3U8 playlists. The protocol ensures smooth playback as it is separate data chunks of 5-10s that the client downloads. However, it comes with high latency, normally about 10-30s. Unlike HTTP-FLV, HLS is well supported on iPhone and most Android browsers and is therefore often used for URL sharing on QQ and WeChat Moments.
- **WebRTC** is short for Web Real-Time Communication. It is an API that allows real-time audio/video calls on web browsers. Supported by Google, Mozilla, and Opera, WebRTC specifications were published by the World Wide Web Consortium (W3C) on June 1, 2011. WebRTC is adopted by LEB, which is an ultra-low-latency version of LVB and offers streaming with millisecond latency. It is suitable for scenarios with high requirements on latency, such as online education, sports streaming, and online quizzes.

|Protocol|Pro|Con|Playback Latency|
|::|::|::|::|
| HTTP-FLV | Mature, suited for high-concurrency scenarios | SDK integration is required. | 2-3s |
|RTMP|Relatively low latency|Poor performance in high-concurrency scenarios |1-3s |
| HLS (M3U8) | Well supported on mobile browsers | High latency |10-30s|
|WebRTC |Lowest latency |SDK integration is required. |< 1s |

[](id:Que6)
### What is the format of a playback URL?   
A Tencent Cloud playback URL consists of a playback protocol prefix, domain name (`domain`), application name (`AppName`), stream name (`StreamName`), playback protocol suffix, authentication key, and other custom parameters. Below are examples:
```
rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
http://domain/AppName/StreamName.m3u8?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
https://domain/AppName/StreamName.m3u8?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
https://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
webrtc://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
```
- **Prefix**
RTMP: **rtmp://**
HTTP-FLV: **http://** or **https://**
HLS: **http://** or **https://**
WebRTC: **webrtc://**
- **Application name (`AppName`)**
Application name specifies the storage path of a live streaming file. It is **live** by default.
- **Stream name (`StreamName`)**[](id:streamname)
Stream name (`StreamName`) uniquely identifies a live stream.
- **Authentication key and other custom parameters**
Authentication key: **txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)**.


[](id:Que7)
### What are some common publishing methods?
- **Camera on Android/iOS devices**: Third-party software or the [MLVB SDK](https://intl.cloud.tencent.com/product/mlvb) captures video data from the camera and publishes it to the publishing URL.
- **Camera or screen recording tool on PCs**: Third-party software captures video data from the camera or records the screen and publishes the data to the publishing URL. Third-party publishing applications include [OBS (recommended)](https://intl.cloud.tencent.com/document/product/267/31569), XSplit, FMLE, etc.
- **Video capturing device**: Connect an HD camcorder with HDMI or SDI output to an encoder and publish RTMP streams to live streaming applications. You need to set the RTMP publishing address of the encoder to your publishing URL.
If you use a webcam that supports RTMP, you can also set the RTMP publishing address of the webcam to your publishing URL.
- **Converting video files to video streams**: Read video files and publish them as RTMP streams to your RTMP publishing URL. This can be achieved using FFmpeg commands, which works on Windows, Linux, and macOS.

[](id:Que8)
### What are the differences between stream interruption and stream disabling?
- **Stream interruption**: If a live stream is interrupted, publishing will stop, and audience will be unable to watch the stream. However, the host can resume publishing the stream.
- **Stream disabling**: If a live stream is disabled, publishing will stop, and audience will be unable to watch the stream. The host cannot resume publishing the stream. You can disable a stream on the stream management page of the CSS console. Disabled streams can be found in the list of disabled streams. You can click **Enable** to enable a disabled stream.

[](id:Que9)
### How do MLVB V1 APIs correspond to V2 APIs?
We offer a table that lists the relationships between V1 and V2 APIs. For details, please see [Relationships Between MLVB SDK V1 and V2 APIs](https://docs.qq.com/sheet/DRkJUckpGdkNTUmt2?tab=BB08J2).

[](id:Que10)
### Regarding privacy, what data (e.g., MAC address, IMEI) does the MLVB SDK collect?
The MLVB SDK complies with the privacy requirements of app stores. For details, please see [Privacy Policy](https://intl.cloud.tencent.com/document/product/1071/38543).


