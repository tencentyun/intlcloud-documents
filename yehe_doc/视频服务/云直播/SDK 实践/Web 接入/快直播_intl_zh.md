## WebRTC 推流

[TXLivePusher 推流 SDK](https://intl.cloud.tencent.com/document/product/267/41620) 主要用于视频云的快直播（超低延时直播）推流，负责将浏览器采集的音视频画面通过 WebRTC 推送到直播服务器。目前支持摄像头推流、屏幕录制推流和本地媒体文件推流。

>? WebRTC 推流的音频编码方式为 opus 编码，若使用标准直播协议（RTMP、FLV、HLS）播放，系统会自动转为 aac 编码，从而会产生音频转码费用，详情请参见 [音频转码费用说明](https://intl.cloud.tencent.com/document/product/267/39604)。

