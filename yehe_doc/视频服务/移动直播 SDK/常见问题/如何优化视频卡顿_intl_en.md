![](https://main.qcloudimg.com/raw/5a6c7985d98037d627789ab75ec257a7.png)
There are three main reasons for playback lag.

- **Reason 1: Low push frame rate
Low push frame rate may be a result of poor performance of the host’s mobile phone or the running of CPU-consuming apps on the host’s phone. Normally, to ensure smooth playback, push frame rate must be 15 FPS or higher. Frame rate of lower than 10 FPS is deemed **too low**, which will cause **all viewers** to experience lag when watching the live broadcast. The exception is when the host’s video image changes little, for example, when the host is showing a static image or PowerPoint, in which case low frame rate will not cause lag.
**Reason 2: upstream congestion**
During a live broadcast, the host's mobile phone keeps generating audio and video data. If the phone’s upstream bandwidth is too low, the data waiting to be pushed will accumulate, causing congestion in data transfer and resulting in poor watching experience for **all viewers**.

  
  
**Reason 3: poor downstream networking**
Poor downstream networking means slow download speed or network instability on the part of viewers. Suppose the bitrate of a live broadcast stream is 2 Mbps. It means 2 Mb of data needs to be downloaded per second. Therefore, a viewer whose network bandwidth is low experiences lag when watching a live broadcast, but other viewers with sufficient bandwidth are not affected.

## Checking SDK Status Metrics
Tencent Cloud’s MLVB SDK has a status feedback mechanism that reports status metrics of the SDK every 1-2 seconds. If you use the MLVB SDK to push streams, you can register TXLivePushListener to get the metrics. The metrics reported are as follows:
![](https://main.qcloudimg.com/raw/75c18f2a2f822c5e19e52de9484663b0.png)

|  Items                   |  Description                    |
| :------------------------  |  :------------------------ |
| NET_STATUS_CPU_USAGE | CPU usage of the current process and the device |
| NET_STATUS_VIDEO_FPS | Current video frame rate, i.e., the number of frames produced by the video encoder per second |
| NET_STATUS_NET_SPEED | Current data transmission speed (Kbps) |
| NET_STATUS_VIDEO_BITRATE | Output bitrate of the video encoder, i.e., the amount of video data produced by the encoder per second (Kbps) |
| NET_STATUS_AUDIO_BITRATE | Output bitrate of the audio encoder, i.e., the amount of audio data produced by the encoder per second (Kbps) |
| NET_STATUS_CACHE_SIZE | Accumulated audio/video data size. A value ≥ 10 indicates that there isn’t enough upstream bandwidth to handle the audio/video data generated.|
| NET_STATUS_CODEC_DROP_CNT | Number of packet drops globally. To prevent data accumulation from becoming increasingly worse, the SDK starts dropping packets once the accumulated data exceeds a certain threshold. The higher number of packets the SDK drops, the severer the network problem is.|
| NET_STATUS_SERVER_IP | IP address of the server connected for push, which is typically the one with the fewest hops from the client. |

## Fixing Low Frame Rate
### 1. How to know when the frame rate is too low
You can learn about the video frame rate of the current push from the **VIDEO_FPS** status parameter returned by the MLVB SDK through TXLivePushListener. Normally, the frame rate must be 15 FPS or higher to ensure smooth playback. Viewers usually experience notable lag when the push frame rate is lower than 10 FPS.

### 2. How to fix the problem
**2.1 Tracking `CPU_USAGE`**
You can learn about the **CPU usage of the stream pushing SDK and the entire system** from the **CPU_USAGE** status parameter returned by the MLVB SDK through TXLivePushListener. If the system CPU usage exceeds 80%, the capturing and encoding of video data will be affected; if the CPU usage reaches 100%, it is difficult to even ensure smooth pushing by hosts, let alone superior watching experience for viewers.

**2.2 Identifying the biggest CPU consumers**
The stream pushing SDK is not the only CPU consumer in a live streaming app. Leaving on-screen comments, sending hearts, and text messaging all consume CPU. To monitor and evaluate the CPU usage of the stream pushing SDK only, you may use our [Basic Edition Demo](https://intl.cloud.tencent.com/document/product/1071/38147).

**2.3 Choosing a reasonable resolution**
High resolution does not necessarily result in high video quality. To begin with, high resolution translates into improved video quality only when the bitrate is high too. Low bitrate and high resolution usually produce lower video quality than high bitrate and low resolution. In addition, viewers may be able to sense notable differences between a resolution of 1280 x 720 pixels and 960 x 540 pixels when watching videos full screen on PCs, but not on mobile phones, whose average screen size is only around 5 inches. High resolution increases the CPU usage of the SDK significantly. Therefore, you are advised to set [setVideoQuality](https://intl.cloud.tencent.com/document/product/1071/38158) in TXLivePusher of the MLVB SDK to **High Definition**. You may not get the high video quality expected by setting the resolution too high.

- **2.4 Using hardware for acceleration if necessary**
Most smartphones today use hardware encoders to reduce the CPU consumption of video encoding. When the CPU usage of your app is too high, you can enable hardware encoding to lower the usage. When `setVideoQuality` of TXLivePusher is set to **High Definition**, software encoders are used by default (hardware encoding doesn't work well on some Android devices and results in blurry video). You can use `enableHWAcceleration` of TXLivePushConfig to enable hardware encoding.

## Fixing Upstream Congestion
Statistics show that upstream congestion at the host end is responsible for over 80% of playback lag in cloud live streaming.

### 1. How to know when there is upstream congestion
- **1.1: Relationship between `BITRATE` and `NET_SPEED`**
 `BITRATE` (`VIDEO_BITRATE` and `AUDIO_BITRATE`) is the amount of audio/video data produced by the encoder per second for push, and `NET_SPEED` is the amount of data actually pushed per second. If `BITRATE` == `NET_SPEED` most of the time, the push quality is excellent. However, if `BITRATE` >= `NET_SPEED` for a long period of time, the push quality is unsatisfactory.
  
- **1.2: `CACHE_SIZE` and `DROP_CNT`**
When `BITRATE` >= `NET_SPEED`, the audio/video data produced by the encoder builds up on the host’s phone. `CACHE_SIZE` indicates the severity of the accumulation of data. Once it exceeds the warning threshold, the SDK will start dropping data, which increases `DROP_CNT`. The figures below are a typical example of upstream congestion. As you can see, `CACHE_SIZE` stays above the **warning threshold** (red line) throughout the course, which indicates that the upstream network fails to meet the demand for data transmission, leading to serious upstream congestion.
![](https://main.qcloudimg.com/raw/c894db6a9745543a349683745c4ba491.png)
![](https://main.qcloudimg.com/raw/dd0b0c36629b11db2c6c1cd497e01a9e.jpg)

 >? You can find the above figures in [**LVB console**](https://console.cloud.tencent.com/live/livestat) > **Statistics** > **Operation Analysis**.

### 2. How to fix the problem
- **2.1 Informing hosts of poor network conditions**
In scenarios where video quality is highly valued, it is advisable to inform the hosts of bad network conditions through UI notifications. For example, you may send this notification to hosts: **Bad network conditions. Please move closer to your router or make sure that your Wi-Fi signal does not have to pass through walls.**
For more information on how to do this, please see **Documentation > Mobile Live Video Broadcasting > Basic Features > Camera Push > Event Handling**. You are advised to remind hosts to check their network conditions if your app receives the **PUSH_WARNING_NET_BUSY** event multiple times within a short period of time. This is because hosts are often unable to notice the problem of upstream congestion until reminded by the app or viewers.

- **2.2 Setting appropriate values for encoding parameters**
We recommend the following encoding settings through the `setVideoQuality` API in TXLivePusher.
<table>
<tr><th width="15%">Setting</th>
<th width="15%">Resolution</th>
<th width="5%">FPS</th>
<th width="20%">Bitrate</th>
<th width="45%">Use Case</th>
</tr><tr>
<td><b>Standard definition</td>
<td>360 x 640</td>
<td>15</td>
<td>400-800 Kbps</td>
<td>Use this setting for cost-sensitive scenarios. It may result in videos that lack clarity, but its bandwidth cost is 60% lower than that of high definition.</td>
</tr><tr>
<td><b>High definition (recommended)</td>
<td>540 x 960</td>
<td>15</td>
<td>1200 Kbps</td>
<td>Use this setting for scenarios with high requirements on video quality. It guarantees clear video images on most mainstream mobile phones on the market.</td>
</tr><tr>
<td><b>Ultra high definition</td>
<td>720 x 1280</td>
<td>15</td>
<td>1800 Kbps</td>
<td>Use this setting with caution. It is recommended only if viewers watch live broadcasts on big screens and hosts have excellent network connections, but not if viewers watch mostly on small screens.<td>
</tr></table>


## Fixing Player-End Issues
![](https://main.qcloudimg.com/raw/57d974de3d3069eb869a2c8d4fb219ad.png)

### 1. Lag and latency
As you can see from the figure above, both downstream network fluctuations and insufficient downstream bandwidth can result in **unfed periods** (during which the app cannot get any audio/video data for playback) in the playback process. To avoid playback lag, the app needs to buffer video data enough to cover the unfed periods. However, buffering too much data causes a new problem: **high latency**, which is undesirable for scenarios that stress host-viewer interaction. The latency could **build up** over time if not fixed, meaning that it increases as the playback continues. The ability to fix latency is a key performance indicator for players. **Latency and playback smoothness are like the two ends of a scale**. To ensure low latency, you may have to compromise network stability, which causes notable playback lag, and to ensure smooth playback, you must deal with high latency. A typical example is the introduction of a 20-30 second delay in the playback of HLS (m3u8) URLs to ensure watching experience.

### 2. How to fix the problem
Through optimization across multiple versions of the MLVB SDK, we have developed an automatic adjustment technology, based on which we came up with three [latency control schemes](https://intl.cloud.tencent.com/document/product/1071/38160), allowing you to deliver superior playback experience even without much knowledge about bandwidth control or processing.

-**Auto mode**: use this mode if you are not sure about what scenarios you will deal with.
>?You can switch to this mode by setting `setAutoAdjustCache` to `true` in TXLivePlayConfig. In this mode, the player adjusts latency automatically based on network conditions to minimize the latency between hosts and viewers and consequently ensure host-viewer interaction quality while delivering decent playback experience. By default, the player adjusts latency in the range of 1-5 seconds. You can use `setMinCacheTime` and `setMaxCacheTime` to modify the default range.

-**Speedy mode**: suitable for **live show streaming** and other scenarios that require low latency.
>? You can switch to this mode by **setting both `SetMinCacheTime` and `setMaxCacheTime` to one second**. The auto and speedy mode differ only in terms of the `MaxCacheTime` value, which is generally lower in the speedy mode and higher in the auto mode. This flexibility is made possible by the automatic control technology of the SDK, which can automatically adjust latency without causing lag. `MaxCacheTime` is associated with the adjustment speed. The higher the `MaxCacheTime` value, the more conservative the adjustment is, and the less likely lag will occur.

- **Smooth mode**: suitable for **live game streaming** and other high-bitrate and high-definition scenarios.
>? 
>- You can switch to this mode by setting `setAutoAdjustCache` of the player to `false`. In this mode, the player adopts a strategy similar to the buffering strategy of Adobe Flash Player for IE. When lag occurs, the player switches to the loading mode, and when enough data is buffered; it returns to the playing mode, until the next network fluctuation. By default, 5 seconds of video data is buffered, which you can change via `setCacheTime`.
>- This seemingly simple mode, which reduces playback lag by moderately increasing latency, is the more reliable option for scenarios that are not demanding on low latency.
