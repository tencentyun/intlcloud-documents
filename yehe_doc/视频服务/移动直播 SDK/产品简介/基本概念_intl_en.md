### Publishing

This refers to the process in which the host pushes local video and audio sources to Tencent Video Cloud servers. It is also known as "RTMP publishing" in some cases.

### Playback

It refers to the process of using a specified URL to play audio/video streams after they are published to Tencent Video Cloud servers. Since video sources are generated in real time, playback is possible only if streams are being published. Once the host stops streaming, the playback URL becomes invalid. Also, because the streaming takes place in real time, there isn’t a progress bar during playback.

### Publishing domain name

It refers to the domain name used to publish live streams, which is a required setting. You must register a domain name before using it for live streaming. After a publishing domain name is configured, CSS will generate a corresponding publishing URL. For details, please see [How to automatically splice push URLs?](https://intl.cloud.tencent.com/document/product/1071/39359).

### Playback domain name

It refers to the domain name used to play live streams, which is a required setting. You must register a domain name before using it for live streaming. After a playback domain name is configured, CSS will generate a corresponding playback URL. For details, please see [How to automatically splice playback URLs?](https://intl.cloud.tencent.com/document/product/1071/39359).

### UserSig

`UserSig` (user signature) is a security signature designed by Tencent Cloud to authenticate user logins, check whether a user is real, and thus prevent attackers from accessing your Tencent Cloud account. For more information, please see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1071/39471).

### License

There are three kinds of licenses for MLVB: trial license, basic edition license, and enterprise edition license. For instructions on how to obtain them, please see [Try and Purchase a License](https://intl.cloud.tencent.com/zh/document/product/1071). You can unlock different features of the MLVB SDK using different licenses. For details, please see [SDK and license](https://intl.cloud.tencent.com/document/product/1071/38149).

### Recording and replay

The recording and replay features are enabled by **VOD**, so before using the features, you need to [activate VOD](https://console.cloud.tencent.com/vod) and complete domain and [recording configuration](https://intl.cloud.tencent.com/document/product/267/31074) in the CSS console. To [view the recording files generated during live streaming](https://intl.cloud.tencent.com/document/product/266/33895), go to **Media Assets** of the VOD console.

### 小直播

小直播 App 是一套开源的完整的在线直播解决方案，它基于云直播服务（LVB）、即时通信（IM）和对象存储服务（COS）构建，并使用云服务器（CVM）提供简单的后台服务，可以实现登录、注册、开播、房间列表、连麦互动、文字互动和弹幕消息等功能。

SDKAppID 是用户在实现小直播 App 中需要填写的信息，主要是在实现聊天室功能时创建 IM 应用产生的， 是腾讯云后台用来区分不同 IM 应用的唯一标识，在 【云直播控制台】>【直播 SDK】>【[应用管理](https://console.cloud.tencent.com/live/license/appmanage)】创建应用时自动生成。不同 SDKAppID 之间的数据不互通。 


### LEB
Live Event Broadcasting (LEB) is the ultra-low-latency version of LVB. It features lower latency than traditional streaming protocols and delivers superior playback experience with millisecond latency. It is suitable for scenarios with high requirements on latency, such as online education, sports streaming, and online quizzes.
