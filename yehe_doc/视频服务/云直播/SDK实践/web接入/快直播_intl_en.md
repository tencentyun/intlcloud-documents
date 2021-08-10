## WebRTC Push

The [TXLivePusher SDK](https://intl.cloud.tencent.com/zh/document/product/267/) is mainly used for stream pushing for LEB (ultra-low latency streaming). It can push audio and video captured by the browser from the camera, screen, or a local media file to live streaming servers via WebRTC.

>? WebRTC push uses the Opus audio codec. If you use a standard live streaming protocol (RTMP, HTTP-FLV, or HLS) for playback, the system will automatically convert the streams to AAC, which will incur transcoding fees. For details, please see [Live Transcoding > Audio Transcoding](https://intl.cloud.tencent.com/document/product/267/39604).



## WebRTC Playback

Tencent Cloud’s web superplayer [TCPlayerLite](https://intl.cloud.tencent.com/zh/document/product/1071/39888) supports **LEB playback via WebRTC** on mobile and desktop browsers, which features lower latency than traditional live streaming protocols and delivers a superb streaming experience with millisecond latency.

>? 
> - If a browser does not support WebRTC, a WebRTC URL passed into the player will be converted automatically to better support playback. By default, WebRTC is converted to HLS on mobile browsers and HTTP-FLV on desktop browsers.
> - For billing details of LEB, please see [LEB Billing Overview](https://intl.cloud.tencent.com/document/product/267/39969).

