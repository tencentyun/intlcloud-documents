
[](id:push)
### Push
 This refers to the process in which the host pushes local video and audio sources to Tencent video cloud servers. It is also known as "RTMP publishing" in some cases. 



[](id:play)

### Pull
It refers to live playback where the source video and audio are pulled from the Tencent video cloud servers and played back at the specified address after live push is implemented. The video source is generated in real time. It is only meaningful if someone pushes a live stream. Once the host stops streaming, the live stream URL will become invalid, and since the live streams are played back in real time, no progress bar will be displayed on the player during the playback. 


[](id:push_domain)
### Push Domain Name
It refers to the domain name used to push live streams, which is required. It must be registered and get an ICP filing before you can use the CSS service. After a push domain name is configured, CSS will generate the corresponding push address. For splicing rules, please see [Splicing Live Stream URLs](https://intl.cloud.tencent.com/document/product/267/38393).

[](id:play_domain)
### Playback Domain Name
It refers to the domain name used to play back live streams, which is required. It must be registered and get an ICP filing before you can use the CSS service. After a playback domain name is configured, CSS will generate the corresponding playback address. For splicing rules, please see [Splicing Live Stream URLs](https://intl.cloud.tencent.com/document/product/267/38393).


[](id:cname)
### Domain Name CNAME
A CNAME domain name is a domain name suffixed with `.liveplay.myqcloud.com` that is assigned by the system to the connected acceleration domain name configured in the CSS console. You need to configure a CNAME record at your domain name service provider. After the record takes effect, CSS will take care of domain name resolution, and all requests made to this domain name will be forwarded to the edge servers of CSS.

[](id:streamname)
### StreamName
`StreamName` is the ID of a stream, which is usually used to uniquely identify the stream together with a domain name.

[](id:appname)
### AppName
`AppName` is a live streaming application name used to identify the storage path of a live streaming media file. It is `live` by default and customizable.

[](id:trans)
### Transcoding
Transcoding is an offline task that converts a video bitstream. It changes parameters of the source bitstream, such as codec, resolution, and bitrate, to adapt it to different devices and network conditions. The following benefits can be achieved with transcoding:
- Increased compatibility: a source video can be transcoded to formats that are compatible with more types of devices for smooth playback.
- Increased bandwidth adaptability: a source video can be transcoded for output in multiple definitions such as LD, SD, HD, and FHD. End users can select the most appropriate bitrate depending on their network conditions.
- Reduced bandwidth consumption: with a more advanced codec, the bitrate of a video can be substantially reduced while retaining the original quality, which helps reduce the bandwidth consumption.

[](id:h264)
### H.264
Developed by the Joint Video Team (JVT) established by ITU-T Video Coding Experts Group (VCEG) and ISO/IEC Moving Picture Experts Group (MPEG), H.264 is a codec standard for highly-compressed digital video and also part 10 of MPEG-4. It has the following advantages in transcoding:
- SD digital image (at a resolution below 1280*720) can be transferred at a speed below 1 Mbps.
- Compared with other existing video encoding standards, it delivers better image quality under the same bandwidth.
- It has the advantages and best features of previous compression technologies while surpassing them with its unique strengths.


[](id:h265)
### H.265
H.265 makes optimizations and improvements on the existing video encoding standard H.264 while reserving part of H.264 features. It has the following advantages in transcoding:
- General HD audio/video (720p at a resolution of 1280x720) can be transferred at a 1–2 Mbps speed.
- It achieves a better balance between the bitstream, encoding quality, latency, and algorithm complexity for optimal configuration.


[](id:message)
### Event Message Notification
It refers to the process where an event notification is triggered by a live stream during push, Tencent Cloud proactively sends the request to your server according to the configured message template, and your server authenticates and responds to the request. For more information on the response protocol, please see [How to Receive Event Notification](https://intl.cloud.tencent.com/document/product/267/38080). After the authentication is passed, a JSON packet containing the callback information can be obtained for parsing and information logging. 


[](id:link)
### Hotlink Protection
 It refers to the `txSecret` field in the push and playback URLs, which can prevent attackers from forging your backend for push URL generation or stealing your playback address for illegal profit.

[](id:record)
 ### Live Recording
During the push, video files generated by muxing original streams (without modifying such information as audio and video data and corresponding timestamps) can be stored on the VOD platform. To use this feature, you need to activate [VOD](https://intl.cloud.tencent.com/product/vod) first.

[](id:watermark)
### Watermarking
To avoid your video copyright from being infringed during live push, you can add a configured watermark to the video stream during transcoding to output a watermarked video stream. The watermark can be either text or image.

[](id:screenshot)
### Screencapture
You can capture screenshots of videos in a pushed live stream at a fixed interval and store the generated image files into COS. To enable the screencapture feature, you must first grant CSS the permission to write to your COS bucket. For more information, please see [How to Authorize CSS to Store Screenshots in a COS Bucket](https://intl.cloud.tencent.com/document/product/267/33384). 

[](id:yellow_confidence)
### Porn Detection
Based on the screencapture feature, the system can recognize screenshots and call back results based on the screencapture and porn detection template bound to the push domain name. For more information, please see [Live Screencapture & Porn Detection](https://intl.cloud.tencent.com/document/product/267/31072).

 
