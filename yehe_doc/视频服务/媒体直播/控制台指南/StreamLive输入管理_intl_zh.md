频道输入是StreamLive的媒体流输入通道，通常关联一个安全组和一个StreamLive的频道。

### 创建输入

选择【Input Management】菜单，点击【Create Input】创建频道输入。频道输入目前支持RTP、RTP-FEC、RTMP、UDP、HLS、HTTP-MP4等协议输入，提供PULL和PUSH两种输入方式。

每一个频道输入可以关联一个安全组和一个频道，被频道关联的输入状态会显示attached。
![img](https://main.qcloudimg.com/raw/eed9a73cc25fc646b1f601ac545ccc0e.png)

>?
> - 控制台默认只支持最多5个input的存在。
> - 输入的媒体源目前至少需要包含一个视频数据通道。
> - 当使用MPEG-TS多路复用通道时，最多允许8路通道同时传输。
