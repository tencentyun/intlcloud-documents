You can use StreamLive to insert ads into live streams. We offer the following ad insertion solutions:

1. Input switch
Bind a video file or live streaming URL as an input to your channel. On the **Plan** page, create an input switch event to insert the video or live stream at a specified time or immediately after configuration. The figure below shows you how to insert a video file into the live stream at a specified time.
![](https://qcloudimg.tencent-cloud.cn/raw/0e5789754fc7fd86e362f55adbe30e8b.png)
StreamLive will switch to the video file at the specified UTC time to play the ad. After the ad is finished, StreamLive will switch back to the original live stream. The entire process is executed automatically without the need for human intervention.

2. SCTE-35
If your input is MPEG-2 TS streams, you can also include SCTE-35 payloads in the input. StreamLive will recognize the payloads and convert them into information that can be displayed in outputs. A standard method is used for players to recognize the information and switch to the ad. You only need to enable SCTE-35 pass-through for the corresponding output. For details, see the “SCTE-35” document.
