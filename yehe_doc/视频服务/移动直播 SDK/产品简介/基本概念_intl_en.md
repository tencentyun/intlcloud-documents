### Publishing

This refers to the process in which the host publishes local video and audio to Tencent Video Cloud servers. It is also known as "RTMP publishing" in some cases.

### Playback

This refers to the process of playing audio/video streams via a specified URL after the streams are published to Tencent Video Cloud servers. Since video sources are generated in real time, playback is possible only if streams are being published. Once the host stops streaming, the playback URL becomes invalid. Also, because the streaming takes place in real time, there isn’t a progress bar during playback.

### Publishing domain name

It refers to the domain name used to publish live streams, which is a required setting. You must register a domain name before using it for live streaming. After a publishing domain name is configured, CSS will generate a corresponding publishing URL. For details, please see [How to automatically splice push URLs?](https://intl.cloud.tencent.com/document/product/1071/39359).

### Playback domain name

It refers to the domain name used to play live streams, which is a required setting. You must register a domain name before using it for live streaming. After a playback domain name is configured, CSS will generate a corresponding playback URL. For details, please see [How to automatically splice playback URLs?](https://intl.cloud.tencent.com/document/product/1071/39359).

### UserSig

`UserSig` (user signature) is a security signature designed by Tencent Cloud to authenticate user logins, check whether a user is real, and thus prevent attackers from accessing your Tencent Cloud account. For more information, please see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1071/39471).

### License

The MLVB SDK has trial licenses and international licenses. For how to obtain them, see [Try and Purchase License](https://intl.cloud.tencent.com/document/product/1071/38546). You can unlock different features of the MLVB SDK using different licenses. For details, see [Feature Description](https://intl.cloud.tencent.com/document/product/1071/38149).

### Recording and replay

The recording and replay features are enabled by **VOD**, so before using the features, you need to [activate VOD](https://console.cloud.tencent.com/vod) and complete domain and [recording configuration](https://intl.cloud.tencent.com/document/product/267/31074) in the CSS console. To [view the recording files generated during live streaming](https://intl.cloud.tencent.com/document/product/266/33895), go to **Media Assets** of the VOD console.


### LEB
Live Event Broadcasting (LEB) is the ultra-low-latency version of LVB. It features lower latency than traditional streaming protocols and delivers superior playback experience with millisecond latency. It is suitable for scenarios with high requirements on latency, such as online education, sports streaming, and online quizzes.
