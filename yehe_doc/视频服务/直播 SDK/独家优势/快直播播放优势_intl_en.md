Live Event Broadcasting (LEB) is an extension to LVB in ultra low-latency playback scenarios, which enables viewers to enjoy an ultimate live viewing experience with a millisecond-level latency. Compared with traditional CDN-based live streaming, where the playback latency is 3–5 seconds, LEB is more suitable for scenarios with high requirements for latency, such as online education, sports streaming, and online quizzes.

## Main Strengths

<table>
<thead>
<tr>
<th width=20%>Strength</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Playback with millisecond latency</td>
<td>LEB uses the UDP protocol to reduce the live streaming latency between nodes to milliseconds in high-concurrency scenarios, solving the problem of 3–5 second latency in traditional live streaming. It delivers high performance in terms of core metrics such as instant live streaming and lag rate to deliver an ultra low-latency live streaming experience.</td>
</tr>
<tr>
<td>Diverse features and smooth migration</td>
<td>LEB integrates a wide range of features including stream publishing, transcoding, recording, screenshots, porn detection, and playback. It allows smooth migration from standard live streaming services.</td>
</tr>
<tr>
<td>Abundant cache nodes and a high bandwidth capacity</td>
<td>LEB can deliver streams through more than 2,000 acceleration nodes in 25 countries/regions, which can sustain a bandwidth of over 100 Tbps.</td>
</tr>
<tr>
<td>Ease of use</td>
<td>LEB uses a standard protocol for easy integration. You can use it for playback on Chrome and Safari without installing any plugins.</td>
</tr>
<tr>
<td>High immunity to poor network conditions</td>
<td>LEB guarantees high quality video streaming under different poor network conditions such as high packet loss rate and high latency, so as to offer a more stable live streaming experience.</td>
</tr>
<tr>
<td>Low-latency live streaming on web</td>
<td>Currently, CDN-based live streaming supports only the HLS format on web. However, the latency of playback in this format is as high as several seconds. By contrast, LEB also supports web playback but with a latency of only hundreds of milliseconds.</td>
<tr>
<td>Seamless switch between multiple bitrates</td>
<td>LEB can seamlessly switch between streams transcoded at different bitrates with no interruption or jump, guaranteeing a smooth transition and better viewing experience.</td>
</tr>
<tr>
<td>Adaptive bitrate streaming</td>
<td>LEB switches between different bitstreams adaptively based on the network bandwidth to guarantee a smooth playback experience under changing network conditions.</td>
</tr>
</tr>
</tbody></table>


## Use Cases
<table>
<thead><tr><th width=10%>Scenario</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Sports events</td>
<td>LEB offers ultra-low-latency streaming for sports events. It brings sports content to audience at low latency, allowing the audience to see the action happening in real time.</td>
</tr>
<tr>
<td>E-commerce streaming</td>
<td>Some e-commerce streaming scenarios, for example, online auctions and sales promotions, require extremely low latency. LEB's ability to stream at ultra-low latency ensures that hosts and audience members get real-time feedback from each other, improving the online shopping experience.</td>
</tr>
<tr>
<td>Online classes</td>
<td>LEB’s ultra-low latency allows teachers and students to interact with each other naturally, the same way as they do in offline classes.</td>
</tr>
<tr>
<td>Online quizzes</td>
<td>Due to latency issues, some online quizzes have to insert extra frames at the audience end to ensure that the host and audience are in sync with each other. However, LEB’s ultra-low-latency streaming capability ensures that the two sides are in sync, which makes it easier to stream a live quiz with a smoother experience.</td>
</tr>
<tr>
<td>Showrooms</td>
<td>LEB significantly improves the experience of latency-sensitive interactions such as gift giving in live showrooms.</td>
</tr>
</tbody></table>

## Performance Under Normal and Poor Network Conditions

### Test method

The host uses RTMP for stream push over a lossless network, viewers play back FLV and LEB streams under different poor network conditions respectively, and metrics such as frame rate and lag rate are tested.

### Stream push parameter configuration

| Parameter | Value   |
| :------- | :--------- |
| Resolution   | 720x1080 |
| Bitrate     | 1,800 Kbps  |
| Frame rate     | 15         |

### Comparison of performance under different network conditions

- Video frame rate
![](https://qcloudimg.tencent-cloud.cn/raw/02de46c16b80294d682a57d3c97684ad.png)
- Video lag rate
![](https://qcloudimg.tencent-cloud.cn/raw/0d092087cae58b7331af314c1032f81d.png)
- Audio lag rate
![](https://qcloudimg.tencent-cloud.cn/raw/03dbdb30ca32ce9a21d91668a5f73997.png)

### Parameter description
| Metric       | Description                                                         |
| --------- | ---------------------------------------------------------- |
| Video lag rate | If video rendering lags for over 500 milliseconds, it will be considered a lag. The lag rate is the total lag divided by the total playback duration. |
| Audio lag rate | If audio playback lags for over 200 milliseconds, it will be considered a lag. The lag rate is the total lag divided by the total playback duration. |
| Video frame rate   | The number of video frames played back per second.                                           |
