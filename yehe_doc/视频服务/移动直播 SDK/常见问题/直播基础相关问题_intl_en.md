[](id:Que1)
### What are the differences among stream pushing, live streaming, and video on demand?
- **Stream pushing**: stream pushing is the process of hosts pushing local video and audio to Tencent Video Cloud servers. It is sometimes called "RTMP publishing" as well.
- **Live streaming**: with live streaming, video streams are generated in real time. It works only if someone is pushing live streams. A live streaming URL becomes invalid the moment the host stops pushing streams. Because live streams are played back in real time, viewers cannot see a progress bar during live streaming.   
**Video on demand**: with video on demand, it is the files in the cloud that are played back. Unless a file is deleted by its provider (e.g., Tencent Video), playback is possible at any time. Because videos are already stored in the server, viewers can see a progress bar during playback.

[](id:Que2)
### What requirements must a playback domain name meet in MLVB? 
If the regions you select for a playback domain name include the Chinese mainland, you need to apply for an ICP filing before submitting the domain name in the console. A domain name can be up to 29 bits in length and cannot contain uppercase letters. For details, see [Adding Domain Name](https://intl.cloud.tencent.com/document/product/267/35970).

[](id:Que3)
### Can I use the same domain name or domain names with different second-level domains for playback and push in MLVB?
You must use different domain names for playback and push, but you can distinguish them by second-level domains.
For example, you can use `123.abc.com` for push, and `456.abc.com` for playback.


[](id:Que4)
### What push protocols does MLVB support?
RTMP may not be a widely adopted protocol for live streaming, but it is the most common protocol used for stream pushing (pushing data from hosts to servers). Most Chinese video cloud services use RTMP as their main push protocol. The MLVB SDK is also known as RTMP SDK because its services start with stream pushing by hosts.

[](id:Que5)
### What playback protocols does MLVB support?
The three widely used live streaming protocols currently are RTMP, FLV and HLS.
- **RTMP** can be used for both push and live streaming. It works by splitting long video and audio chunks into short fragments and transmitting them as small data packets over the internet. RTMP supports encryption and therefore ensures privacy. However, the complicated splitting and reassembling processes add uncertainty to the stability of data transmission in high concurrency scenarios. 
**FLV** is developed by Adobe Systems and is a rather simple video format. It works by adding a header to large video and audio data chunks. This simplicity gives it a notable advantage in terms of delay control and high-concurrency performance. The only drawback is that FLV is poorly supported on mobile browsers, but it is an ideal option for mobile apps.  
- **HLS** is released by Apple. It breaks video streams into fragments of 5-10s and manages them using m3u8 playlists. The protocol ensures smooth playback as it is separate data chunks of 5-10s that the client downloads. However, it comes with high latency, normally about 10-30s. Unlike FLV, HLS is well supported on iPhone and most Android browsers and is therefore often used for URL sharing on QQ and WeChat Moments.

|Protocol|Pro|Con|Playback Latency|
|::|::|::|::|
| FLV | Well established and well suited for high-concurrency scenarios | SDK integration is required for playback. | 2-3s |
| RTMP | Lowest latency in good network conditions| Poor performance in high-concurrency scenarios | 1-3s |
| HLS (m3u8) | Well supported on mobile browsers | High latency |10-30s|

[](id:Que6)
### What is the format of a playback address?   
A Tencent Cloud playback address consists of a playback protocol prefix, domain name (`domain`), application name (`AppName`), stream name (`StreamName`), playback protocol suffix, authentication key, and other custom parameters. Below are a few examples.
```
rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
http://domain/AppName/StreamName.m3u8?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
https://domain/AppName/StreamName.m3u8?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
https://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
```
- **Playback protocol prefix**
- RTMP: **rtmp://**
- HTTP-FLV: **http://** or **https://**
- HLS: **http://** or **https://**
- **Application name (`AppName`)**
Application name specifies where live streaming files are stored. *live* is used by default.
- [](id:streamname">**stream name（`StreamName`）**</span>
Stream name (`StreamName`) is the unique identifier of a live stream.
- **Authentication key and other custom parameters**
Authentication key: **txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)**.


[](id:Que7)
### What are some of the common push methods?
- **Camera on Android/iOS devices**: third-party software or the [MLVB SDK](https://intl.cloud.tencent.com/product/mlvb) captures video data from the camera and pushes it to the push address for live streaming.
- **Camera or screencapturing tool on PCs**: third-party software captures video data from the camera or records the screen and pushes the data to the push address for live streaming. Third-party push applications include [OBS (recommended)](https://intl.cloud.tencent.com/document/product/267/31569), XSplit, FMLE, etc.
- **Video capturing device**: an HD camcorder with HDMI or SDI output can be connected to an encoder and push live RTMP streams to live streaming services. You need to set the push address for live streaming to the RTMP publishing address of the encoder.
You can set the push address for live streaming to the publishing address of a webcam too if it supports RTMP push.
- **Converting video files to RTMP streams**: video files are read and pushed as RTMP streams to the RTMP push address of a live streaming service for publishing. This can be achieved using the `ffmpeg` command, which works on Windows, Linux, and macOS.

[](id:Que8)
### What are the differences between stream interruption and suspension?
- **Stream interruption**: if a live stream is interrupted, the push will stop, and viewers will be unable to watch the stream. However, the host can start the push again to resume the live stream.
- **Stream suspension**: if a live stream is suspended, the push will stop, and viewers will be unable to watch the stream. The host cannot start the push again as long as the stream is suspended. You can suspend a stream on the stream management page of the LVB console. Suspended streams can be found in the list of forbidden streams. You can click **Enable** to resume suspended streams.
