标准直播（LVB）是云直播针对普通直播场景下提供的专业稳定快速的直播云端服务，可以配合 [移动直播 SDK](https://intl.cloud.tencent.com/document/product/1071) 来快速实现包括 App、Web 等多平台快速接入。

[](id:app)

## App 接入	
iOS、Android 上的应用可以通过集成移动直播 SDK 来实现 App 端上的直播推流/播放功能。

- **App 端直播推流**：支持采集摄像头画面或者采集手机界面，通过 RTMP 协议快速推流到云直播服务上，详情请参见 [摄像头推流](https://intl.cloud.tencent.com/document/product/1071/38157) 和 [录屏推流](https://intl.cloud.tencent.com/document/product/1071/41878)。
- **App 端直播播放**：支持 RTMP、FLV、HLS 等格式的播放协议，配合云直播服务快速打造直播 APP，详情请参见 [标准直播拉流](https://intl.cloud.tencent.com/document/product/1071/38159)。

>? 移动直播 SDK 借助云直播、即时通信 IM、TRTC 等服务实现了多人音视频低延迟互联互通，可以实现多人连麦的互动效果，不参与连麦的观众仍通过直播服务观看，详情请参见 [直播连麦互动](https://intl.cloud.tencent.com/document/product/1071/39888)。



[](id:web)

## Web 接入
若您有网站需要进行直播推流和播放，推荐您使用以下方式进行接入：
- **Web 端直播推流**：基于浏览器通用的 WebRTC 标准进行设计和封装，通过引入代码片段就能实现在浏览器中进行直播推流，详情请参见 [WebRTC 推流](https://intl.cloud.tencent.com/document/product/267/41620)。
> ! WebRTC 推流时音频编码方式只支持 opus 编码，若使用标准直播的播放协议（RTMP、FLV、HLS）进行播放时，为保证能正常观看，云直播后台会自动发起音频转码转为 aac 编码，从而会产生音频转码费用，详情请参见 [音频转码费用说明](https://intl.cloud.tencent.com/document/product/267/39604)。


