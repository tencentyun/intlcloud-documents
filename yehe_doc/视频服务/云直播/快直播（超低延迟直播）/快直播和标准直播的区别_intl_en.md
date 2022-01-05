As a lower-latency version of LVB, LEB provides superb live streaming experience with millisecond playback latency, far lower than that of live stream playback using traditional protocols. LEB is designed for scenarios with high latency requirements. In addition to live shopping and online education, it is also suitable for interactive scenarios such as live sports streaming and live game streaming.

## Protocol Comparison

Common playback protocols used by LVB include RTMP, FLV, and HLS, all of which are based on TCP. With TCP, due to delayed acknowledgement and piggybacking, acknowledgement is not sent immediately after data is received, but only after the data accumulates to a certain size. This leads to perceptible latency. Under poor network conditions, this mechanism will cause data to build up, resulting in data transfer congestion and a latency of several or dozens of seconds.
![](https://qcloudimg.tencent-cloud.cn/raw/911be7d33fbffa34a92b68111810f5d8.png)

Low-latency live streaming services in the industry use protocols such as QUIC, SRT, WebRTC, and ORTC. Among these, the latency of QUIC is relatively high as it does not have the characteristics of streaming media. SRT, WebRTC, and ORTC have streaming media characteristics and can stream with millisecond latency, but SRT and ORTC are not as widely used as WebRTC. As a result, LEB has settled on UDP-based WebRTC to implement low-latency live streaming.
![](https://qcloudimg.tencent-cloud.cn/raw/19ee08b715b3a3e7198881e81f2ea9dd.png)

## Latency Comparison
With LVB, the typical latency of FLV is 2-10 seconds, which is mainly caused by large GOP size and data buildup under poor network conditions. The latency of HLS is higher, usually several to dozens of seconds, and is caused by large GOP size and large TS segments. HLS works by downloading data chunks and generating an index file, so its latency is affected by the size of TS segments. Many players wait until 3 TS segments are received before playback, which may result in a latency of dozens of seconds. HLS delivers the highest latency among the protocols used by LVB.

LEB uses WebRTC to achieve low latency. Most mainstream browsers, including Chrome and Safari, have supported WebRTC, so we can offer standard WebRTC capabilities via browsers. In addition, the well-established, open-source WebRTC SDK makes optimization and customization easy, allowing us to customize an SDK with improved low-latency streaming features. The typical latency of LEB is 300-1000 ms.
![](https://qcloudimg.tencent-cloud.cn/raw/195c8b28f1fc63240f12c1e60f1a1dbe.png)

## LEB Strengths

- More than 2,100 acceleration nodes across the world, covering 25 countries/regions
- Ultra-high bandwidth (supports bandwidth of over 100 Tbps)
- High quality and low cost (30% packet loss tolerance)
- Easy integration and high compatibility (you only need to modify the playback SDK to use a complete set of features)
- Instant streaming and ultra-low latency. As demonstrated by the test below, LEB can keep latency at around 300 ms or even as low as 43 ms.

 ![](https://qcloudimg.tencent-cloud.cn/raw/9a8eb2a10290a8b51e93862a5eb55935.png)
