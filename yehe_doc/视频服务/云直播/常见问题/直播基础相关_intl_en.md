<span id="Que1"></span>
### What are push, live streaming, and video on demand?
- **Push**: the process of hosts pushing local video and audio to Tencent Video Cloud servers. It is called "RTMP publishing" in some scenarios.
- **Live streaming**: during live streaming, video streams are generated in real time. It works only if someone is pushing. A live streaming URL becomes invalid the moment the host stops pushing. As live streams are played back in real time, viewers cannot see a progress bar during live streaming.   
**Video on demand (VOD)**: VOD allows you to play files in the cloud. A file can be played at any time unless it is deleted by its provider (e.g., Tencent Video). Because videos are already stored in the server, viewers can see a progress bar during playback.

<span id="Que2"></span>
### What are the requirements for a playback domain name in CSS?	
The domain name can contain up to 29 characters and cannot contain uppercase letters. For more information, please see [Adding Domain Name](https://intl.cloud.tencent.com/document/product/267/35970).

<span id="Que3"></span>
### Can I use the same domain name for playback and push? Can I use second-level domain names?
You must use different domain names for playback and push, but you can use the same second-level domain to indicate that the stream is the same.
For example, you can use `123.abc.com` for push, and `456.abc.com` for playback.

<span id="Que4"></span>

### What push protocols are supported?
RTMP may not be a widely adopted protocol for live streaming, but it is the most common protocol used for stream pushing (pushing data from hosts to servers). Most video cloud services in the Chinese mainland use RTMP as their main push protocol. The MLVB SDK is also called RTMP SDK because its first feature module is stream publishing.

<span id="Que5"></span>

### What playback protocols are supported?
Common live streaming protocols include RTMP, HTTP-FLV, and HLS.
- **RTMP** can be used for both live push and live playback. It works by splitting long video and audio chunks into short fragments and transporting them as small data packets over the internet. RTMP supports encryption and therefore ensures privacy. However, the complicated splitting and splicing processes add uncertainty to the stability of data transmission in high concurrency scenarios. 
- **HTTP-FLV** is developed by Adobe Systems and is a rather simple video format. It works by adding a header to large video and audio data chunks. This simplicity makes it superb in delay control and high-concurrency performance. The only drawback is that HTTP-FLV is poorly supported on mobile browsers, but it is an ideal option for mobile apps.  
- **HLS** is released by Apple. It splits video streams into segments of 5-10s and manages them using M3U8 playlists. The protocol ensures smooth playback as clients download data chunks of 5-10s. However, it comes with high latency of about 10-30s. Unlike HTTP-FLV, HLS is well supported on iPhone and most Android browsers and is therefore often used for URL sharing on QQ and WeChat Moments.
- **WebRTC** is short for Web Real-Time Communication. It is an API that allows real-time audio/video calls on web browsers. Supported by Google, Mozilla, and Opera, WebRTC specifications were published by the World Wide Web Consortium (W3C) on June 1, 2011. WebRTC is adopted by LEB, which is an ultra-low-latency version of LVB and offers streaming with millisecond latency. It is suitable for scenarios with high requirements on latency, such as online education, sports streaming, and online quizzes.

|Protocol|Pro|Con|Playback Latency|
| --------- | ---------------------- | -------------------- | --------- |
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
```
- **Prefix**
RTMP: **rtmp://**
HTTP-FLV: **http://** or **https://**
HLS: **http://** or **https://**
WebRTC: **webrtc://**
- **Application name (`AppName`)**
Application name specifies the storage path of a live streaming file. It is **live** by default.
- <span id="streamname">**stream name (`StreamName`)**</span>
Stream name (`StreamName`) uniquely identifies a live stream.
- **Authentication key and other custom parameters**
Authentication key: **txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)**.


<span id="Que7"></span>
### What are the common push methods?
- **Camera on Android/iOS devices**: use third-party software or the [MLVB SDK](https://intl.cloud.tencent.com/product/mlvb) to capture camera video and push the video stream to your push URL.
- **Camera or screen recorder on PCs**: use third-party software to capture camera video or record the screen and then push the data to your push URL. Such third-party software includes [OBS (recommended)](https://intl.cloud.tencent.com/document/product/267/31569), XSplit, FMLE, etc.
- **Video capturing device**: connect an HD camcorder with HDMI or SDI output to an encoder and push RTMP streams to live streaming applications. You need to set the RTMP publishing address of the encoder to your push URL.
If you use a webcam that supports RTMP, you can also set the RTMP publishing address of the webcam to your push URL.
- **Converting video files to video streams**: read video files and push them as RTMP streams to your RTMP push URL. This can be achieved using the `FFmpeg` command, which works on Windows, Linux, and macOS.

<span id="Que8"></span>
### What are the differences between stream interruption and stream disabling?
- **Stream interruption**: if a live stream is interrupted, the push will stop, and viewers will be unable to watch the stream. However, the host can start the push again to resume the live streaming.
- **Stream disabling**: if a live stream is disabled, the push will stop, and viewers will be unable to watch the stream. The host cannot start the push again. You can disable a stream on the stream management page of the CSS console. Disabled streams can be found in the list of disabled streams. You can click **Enable** to enable a disabled stream.
[](id:Que10)
### Can I enable text chat for live streaming?
Yes. You can use the Instant Messaging (IM) component to realize text chat for live streaming. In addition, IM provides on-screen comments, likes, gifts, repeat notifications and other interactive features. You can also use the room management feature to realize co-anchoring, manage user identities and the permission to mute members, among others.
[](id:Que11)
### Can I activate CSS with a new account after using the service? 
Any account can activate CSS as long as it has completed identify verification. 
[](id:Que13)

### Is CSS a software?
 No. CSS provides APIs for you to develop live streaming applications. 

[](id:Que16)
### How do I get the number of live streaming viewers?
You can call the CSS v3.0 API [DescribeStreamPlayInfoList](https://intl.cloud.tencent.com/document/product/267/37297) to get the number of online viewers.