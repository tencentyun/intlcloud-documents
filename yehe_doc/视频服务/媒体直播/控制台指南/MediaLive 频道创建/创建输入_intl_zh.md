
频道输入是MediaLive的媒体流输入通道，通常关联一个安全组和一个MediaLive的频道。频道输入目前支持RTP、RTP-FEC、RTMP、UDP、HLS、HTTP-MP4等协议输入，提供PULL和PUSH两种输入方式。
每一个频道输入可以关联一个安全组和一个频道，详情可参见【MediaLive 频道创建】，被频道关联的输入状态会显示attached。
![](https://main.qcloudimg.com/raw/33f00ffaaf22432d973b500228daa947.jpg)
>!
- 控制台默认只支持最多5个input的存在。
- 输入的媒体源目前至少需要包含一个视频数据通道。
- 当使用MPEGTS多路复用通道时，最多允许8路通道同时传输。
