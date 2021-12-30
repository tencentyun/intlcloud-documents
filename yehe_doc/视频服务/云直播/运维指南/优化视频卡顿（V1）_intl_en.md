![](https://main.qcloudimg.com/raw/c38bbed25d2953aea75f76764522e25d.png)
There are three main reasons for playback stuttering.

- **Reason 1: low upstream frame rate**
Low upstream frame rate may be a result of poor performance of the host’s mobile phone or CPU-intensive applications at the backend. Normally, to ensure smooth playback, the upstream frame rate should be 15 FPS or higher. Frame rate lower than 10 FPS is deemed **too low**, which results in playback stuttering for **all viewers**. If the live streaming screen displays a static image, PowerPoint, or other images with little change, low frame rate will not cause stuttering.
- **Reason 2: upstream congestion**
The host's mobile phone keeps pushing audio and video data during live streaming. If the phone’s upstream bandwidth is too low, the data waiting to be pushed will accumulate, causing congestion in data transfer and thus resulting in playback stuttering for **all viewers**.

 Though **ISPs in Chinese mainland** offer broadband packages with the downstream bandwidth as fast as 10 Mbps, 20 Mbps or even 100 Mbps or 200 Mbps, the upstream bandwidth is slow. In many small cities, the upstream bandwidth is up to 512 Kbps, meaning a maximum of 64 KB data can be uploaded per second.
 **Wi-Fi** uses the carrier-sense multiple access and collision avoidance (CSMA/CA) strategy, as specified in IEEE 802.11. To put it simply, a Wi-Fi hotspot can communicate with only one phone at one time, and other phones must verify or query if communication is possible before initiating a connection to a hotspot. Therefore, the more people using a Wi-Fi hotspot, the slower the connection is. Furthermore, Wi-Fi signal decays greatly when passing through walls or obstacles. Most families seldom consider the Wi-Fi router position and the strength of Wi-Fi signal across rooms when designing and decorating their houses. Moreover, when hosts push video streams, they probably pay little attention to how many walls they are apart from their routers.
- **Reason 3: poor downstream connection**
Poor downstream connection means slow download speed or instable network for audience. A bitrate of 2 Mbps in live streaming means 2 Mb of data needs to be downloaded per second. Audience will experience stuttering if their network bandwidth is low, but users with sufficient bandwidth will not.

## Checking SDK Performance Metrics
The MLVB SDK of RT-Cube has a status feedback mechanism that reports status metrics of the SDK every 1-2 seconds. If you use the MLVB SDK to publish streams, you can register TXLivePushListener to get the metrics. The metrics reported are as follows:
![](https://main.qcloudimg.com/raw/533391ae5c188ed87b748f78d8168591.png)

| Metric                | Description                    |
| :------------------------  |  :------------------------ |
| NET_STATUS_CPU_USAGE |  CPU utilizations of the current process and the device |
| NET_STATUS_VIDEO_FPS | Current video frame rate, i.e., the number of frames produced by the video encoder per second |
| NET_STATUS_NET_SPEED | Current data transfer rate in Kbps |
| NET_STATUS_VIDEO_BITRATE | Output bitrate of the video encoder, i.e., the amount of video data produced by the encoder per second, in Kbps |
| NET_STATUS_AUDIO_BITRATE | Output bitrate of the audio encoder, i.e., the amount of audio data produced by the encoder per second, in Kbps |
| NET_STATUS_CACHE_SIZE | Accumulated audio/video data size. A value ≥ 10 indicates that there isn’t enough upstream bandwidth to consume the audio/video data generated.|
| NET_STATUS_CODEC_DROP_CNT | Number of packet drops globally. Once the accumulated data exceeds a certain threshold, the SDK starts dropping packets to prevent worsening data accumulation. A larger number of packets the SDK drops indicates a severer network problem.|
| NET_STATUS_SERVER_IP | IP address of the connected publishing server, which is typically the one with the fewest hops from the client. |

## Fixing Low Frame Rate
### 1. How to know whether the frame rate is too low
The upstream frame rate is indicated by the **VIDEO_FPS** status parameter returned by the MLVB SDK through TXLivePushListener. Normally, the frame rate should be 15 FPS or higher to ensure smooth playback. Viewers will experience notable stutter when the publish frame rate is lower than 10 FPS.

### 2. How to fix the problem
- **2.1 Tracking `CPU_USAGE`**
You can learn about the **CPU usage of the stream publishing SDK and the entire system** from the `CPU_USAGE` status parameter returned by the MLVB SDK through TXLivePushListener. System CPU utilization larger than 80% will affect video data capturing and encoding; if the CPU utilization reaches 100%, publishing by hosts will stutter, and smooth watch experience for viewers is impossible.

- **2.2 Identifying CPU consumers**
The publishing SDK is not the only CPU consumer in a live streaming application. Leaving on-screen comments, sending hearts, and text messaging all consume CPU. To evaluate the CPU usage of the push SDK only, you may use our [Basic Edition Demo](https://intl.cloud.tencent.com/document/product/1071/38147).

- **2.3 Choosing an appropriate resolution**
High resolution does not necessarily result in high video quality. To begin with, high resolution translates into improved video quality only when the bitrate is also high. Low bitrate and high resolution usually produce lower video quality than high bitrate and low resolution. In addition, viewers may be able to sense notable difference between a resolution of 1280 × 720 and 960 × 540 when watching videos full screen on PCs, but not on mobile phones, whose average screen size is only around 5 inches. High resolution increases the CPU utilization of the SDK significantly. Therefore, we recommend you use `setVideoQuality` in `TXLivePusher` of the MLVB SDK to set video quality to **HD**. You may not get the expected high video quality by setting the resolution too high.

- **2.4 Using hardware for acceleration if necessary**
Most smartphones use hardware encoders to reduce the CPU consumption of video encoding. When the CPU utilization of your app is too high, you can enable hardware encoding. When `setVideoQuality` in `TXLivePusher` is set to **HD**, software encoders are used by default (hardware encoding doesn't work well on some Android devices and results in blurry video). You can use `enableHWAcceleration` in `TXLivePushConfig` to enable hardware encoding.

## Fixing Upstream Congestion
Statistics show that upstream congestion for hosts is responsible for over 80% of playback stuttering in live streaming.

### 1. How to know if upstream congestion occurs
- **1.1: Relationship between `BITRATE` and `NET_SPEED`**
 `BITRATE` (`VIDEO_BITRATE` plus `AUDIO_BITRATE`) is the amount of audio/video data produced by the encoder per second for publishing, and `NET_SPEED` is the amount of data actually published per second. If `BITRATE` == `NET_SPEED` most of the time, the publishing quality is excellent. However, if `BITRATE` >= `NET_SPEED` for a long period of time, the publishing quality is unsatisfactory.
  
- **1.2: `CACHE_SIZE` and `DROP_CNT`**
When `BITRATE` >= `NET_SPEED`, the audio/video data produced by the encoder builds up on the host’s phone. `CACHE_SIZE` indicates the severity of data accumulation. Once it exceeds the alarm threshold, the SDK will start dropping data, which increases `DROP_CNT`. The figure below shows a typical example of upstream congestion. As you can see, `CACHE_SIZE` stays above the **alarm threshold** (red line) throughout the course, which indicates that the upstream network cannot meet the demand for data transfer, leading to serious upstream congestion.
![](https://main.qcloudimg.com/raw/c894db6a9745543a349683745c4ba491.png)


 >? You can find the above figures in **[CSS console](https://console.cloud.tencent.com/live/livestat)** > **Operation Analysis**.

### 2. How to fix the problem
- **2.1 Notifying hosts of poor network conditions**
In scenarios where video quality is important, you’re advised to inform the hosts of bad network conditions through UI notifications. For example, you can send: **Bad network conditions. You’re advised to move closer to your router and not to make Wi-Fi signal pass through walls.**
For more information on how to do this, please see **Mobile Live Video Broadcasting > Basic Features > Camera Push > Event Handling**. You are advised to remind hosts to check their network conditions if your application receives the [**PUSH_WARNING_NET_BUSY**](https://intl.cloud.tencent.com/document/product/1071/41678) event multiple times within a short period of time. Hosts are often unable to notice upstream congestion until reminded by viewers or an application message.

- **2.2 Setting appropriate values for encoding parameters**
You can set video quality using the `setVideoQuality` API in `TXLivePusher`. We recommend the encoding settings below (for live showroom). To learn more about ensuring video quality, see [Video Quality](https://intl.cloud.tencent.com/document/product/1071/41932).
<table>
<tr><th width="15%">Video Quality</th>
<th width="15%">Resolution</th>
<th width="5%">FPS</th>
<th width="20%">Bitrate</th>
<th width="45%">Use Case</th>
</tr><tr>
<td><b>SD</td>
<td>360 × 640</td>
<td>15</td>
<td>400-800 Kbps</td>
<td>Use this setting to save bandwidth cost. The image may lack clarity, but the bandwidth cost is 60% lower than that of high definition.</td>
</tr><tr>
<td><b>HD (recommended)</td>
<td>540 × 960</td>
<td>15</td>
<td>1200 Kbps</td>
<td>Use this setting to improve video quality. It guarantees clear video images on most mainstream mobile phones.</td>
</tr><tr>
<td><b>FHD</td>
<td>720 × 1280</td>
<td>15</td>
<td>1800 Kbps</td>
<td>Use this setting with caution. It is recommended only if viewers watch live streaming on big screens and hosts have excellent network connections, but not recommended for playback on small screens.<td>
</tr></table>


## Fixing Player Issues
![](https://main.qcloudimg.com/raw/1f221c3ecba79a706014154531a02bbd.png)

### 1. Stuttering and lag
As shown in the figure above, both downstream network fluctuations and insufficient downstream bandwidth can result in **unfed periods** (during which the app cannot get any audio/video data for playback) in the playback process. To avoid playback stuttering, the app needs to cache video data enough to cover the unfed periods. However, caching too much data causes a new problem: **high latency**, which is undesirable for interactive scenarios. The latency could **build up** over time if not fixed, meaning that it increases as the playback continues. The capability to fix latency is a key performance indicator for players. **Latency and playback smoothness are like the two ends of a scale**. To ensure low latency, you may have to compromise network stability, which causes playback stuttering, and to ensure smooth playback, you must deal with high latency. A typical example of the latter is the introduction of a 20-30 second delay in the playback of HLS (M3U8) streams to ensure smooth playback experience.

### 2. How to fix the problem
Through optimization across multiple versions of the MLVB SDK, we have developed an automatic adjustment technology, based on which we came up with three latency control schemes, allowing you to deliver superior playback experience without having to learn QoS control.

- **Auto mode**: use this mode if you are not sure about what the live streaming scenarios will be.
>?You can switch to this mode by setting `setAutoAdjustCache` to `true` in `TXLivePlayConfig`. In this mode, the player adjusts lag automatically based on network conditions to minimize the lag between hosts and viewers and thus ensure host-viewer interaction quality while delivering good playback experience. By default, the player adjusts lag in the range of 1-5s. You can use `setMinCacheTime` and `setMaxCacheTime` to modify the default range.

- **Speedy mode**: suitable for **live show** and other scenarios that require low lag.
>? You can switch to this mode by **setting both `SetMinCacheTime` and `setMaxCacheTime` to 1s**. The auto and speedy modes differ only in terms of the `MaxCacheTime` value, which is generally lower in the speedy mode and higher in the auto mode. This flexibility is made possible by the automatic control technology of the SDK, which can automatically adjust lag without causing stutter. `MaxCacheTime` is associated with the adjustment speed. The higher the `MaxCacheTime` value, the more conservative the adjustment is, and the less likely stutter will occur.

- **Smooth mode**: suitable for **live game streaming** and other scenarios that require high bitrate and high definition.
>? 
>- You can switch to this mode by setting `setAutoAdjustCache` of the player to `false`. In this mode, the player adopts a strategy similar to the buffering strategy of Adobe Flash Player for IE. When stutter occurs, the player switches to the loading mode, and when enough data is buffered; it returns to the playing mode, until the next network fluctuation. By default, 5 seconds of video data is buffered, which you can change via `setCacheTime`.
>- This seemingly simple mode reduces playback stuttering by moderately increasing lag, thus it is a reliable option for scenarios that do not require low lag.

