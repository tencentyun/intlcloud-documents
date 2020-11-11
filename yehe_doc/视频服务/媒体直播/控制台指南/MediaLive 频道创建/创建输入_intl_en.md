
A channel input is MediaLive's media stream input channel, which is usually associated with one security group and one MediaLive channel. Currently, channel input supports multiple input protocols such as RTP, RTP-FEC, RTMP, UDP, HLS, HTTP-MP4, etc as well as pull and push input methods.
Each channel can be associated with one security group and one MediaLive channel. For more information, please see [MediaLive Creating channel](https://intl.cloud.tencent.com/document/product/1048/38374). The input associated with a channel will be displayed as “attached”.
![](https://main.qcloudimg.com/raw/33f00ffaaf22432d973b500228daa947.jpg)

>!
>- The console supports up to 5 inputs by default.
>- The input media source currently must contain at least one video data channel.
>- When MPEG-TS multiplexing is used, a maximum of 8 channels can be transferred simultaneously.
