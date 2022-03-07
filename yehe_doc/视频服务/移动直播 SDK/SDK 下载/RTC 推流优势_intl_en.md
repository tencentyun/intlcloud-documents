In order to improve publishing performance under poor network conditions, we have added support for RTC publishing in addition to the traditional RTMP protocol. This document compares the performance of publishing under different network conditions using the two protocols. The video below shows the effects of watching streams published over different methods.
<video width="610" controls><source src="https://qcloudimg.tencent-cloud.cn/raw/2d2ebf53ef568e33c6397c807313d5ce.mp4">
  Sorry, your browser does not support preview.
</video>

>? For instructions on how to publish streams, please see [Publishing from Camera](https://intl.cloud.tencent.com/document/product/1071/38157).

## Performance Under Normal and Poor Network Conditions

### Test method
We simulated different network conditions at the publishing end and observed the playback effects (the streams were played over CDNs, and network conditions at the playback end were normal).

### Parameter configuration
To prevent the use of different sources from affecting the results, we used [V2TXLivePusher](https://intl.cloud.tencent.com/document/product/1071/41270) to publish the same video over RTMP and RTC.
Video parameters:

| Parameter | Value |
|---------|---------|
| Resolution| 720 x 1280 |
| Bitrate| 1800 Kbps |
| Frame rate | 15 |

### Comparison of performance under different network conditions
- **Frame rate**
![](https://qcloudimg.tencent-cloud.cn/raw/90051b4833ccbaa2dd1fbbd96cea8f68.png)
>? For a description of the network parameters, see [Appendix: Network Parameters](#appendix1).
- **Stutter rate**
![](https://qcloudimg.tencent-cloud.cn/raw/52ab188e330da9552457d662a0e96f50.png)
>? For a description of the network parameters, see [Appendix: Network Parameters](#appendix1).

[](id:appendix1)
## Appendix: Network Parameters
| Parameter | Description |
|---------|---------|
| Frame rate | Frames rendered per second |
| Packet loss | A packet loss rate of 50% means that for every 10 data packets sent, five fail to arrive at their destination. |
| Latency | A latency of 200 ms indicates that data packets are delivered by the network only 200 ms after they are sent by the SDK. |
| Transfer speed cap | A transfer speed cap of 800 Kbps means that 800 KB of data can be sent per second at most. |
| Stutter rate | Stutter occurs if the interval between the rendering of two consecutive frames exceeds 200 ms. Stutter rate is the total stuttering time divided by the total playback time. |
