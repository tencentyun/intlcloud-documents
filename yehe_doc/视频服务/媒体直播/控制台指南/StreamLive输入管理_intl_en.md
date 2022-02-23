Inputs are the source of streams for StreamLive channels. An input is usually associated with 1 security group and 1 StreamLive channel.

### Creating an input

Choose **Input Management** on the left sidebar and click **Create Input** to create an input. Currently, the protocols supported for inputs include RTP, RTP-FEC, RTMP, UDP, HLS, and HTTP-MP4. An input is either a push input or a pull input.

Each input can be associated with 1 security group and 1 channel. An input associated with a channel is marked as "attached".
![img](https://main.qcloudimg.com/raw/eed9a73cc25fc646b1f601ac545ccc0e.png)

>?
> - The console supports up to 5 inputs by default.
> - An input source must contain at least 1 video data channel.
> - When MPEG-TS multiplexing is used, a maximum of 8 channels can be transferred simultaneously.
