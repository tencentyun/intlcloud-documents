## CSS

[](id:live_que1)
### What are the billable items of CSS? What fees do I need to pay?
Billable items include basic services and value-added services. Extended service fees will also be charged if you use CSS features that rely on the capabilities of other Tencent Cloud products.

- **Basic service fees** are billed based on the downstream traffic/bandwidth consumed for connecting with cache origin servers. Traffic/bandwidth is consumed whenever your live streams are played.
>? CSS provides two billing modes: bill-by-traffic and bill-by-bandwidth. For the billing details, see [Basic Services](https://intl.cloud.tencent.com/document/product/267/2818). To change your billing mode, see [Changing Billing Modes](https://intl.cloud.tencent.com/document/product/267/30411).
- **Value-added service fees** are incurred if you use the transcoding, recording, screencapture, or porn detection feature. The features are disabled by default. For details, see “Value-Added Service Fees” in [Pricing Overview](https://intl.cloud.tencent.com/document/product/267/2819#value-added-service-fees).
- **Extended service fees** are incurred if you use CSS features that rely on the capabilities of other Tencent Cloud products. The fees are charged according to the billing rules of the corresponding products. For details, see “Extended Service Fees” in [Pricing Overview](https://intl.cloud.tencent.com/document/product/267/2819#extended-service-fees).

[](id:live_que2)
### How can I know whether my account has overdue payments?
Log in to the [CSS console](https://console.cloud.tencent.com/live) and click **Billing Center** in the top right corner to view your balance. Your account has overdue payments if the available balance is negative. To continue using CSS and other services, please make the payment in a timely manner.

[](id:live_que3)
### Will I be charged for pushing streams?
- By default, fees are billed based on downstream usage. However, upstream usage will also be billed if the ratio of downstream traffic to upstream traffic is smaller than 10:1 and the highest upstream bandwidth used in a day exceeds 100 Mbps.
- The billing modes, list prices, and tiered pricing rules for upstream usage are the same as those for downstream usage. Downstream usage has been billed since 00:00 (UTC+08:00), July 1, 2021.


[](id:live_que4)
### When are value-added service fees incurred?
If you enable features that are bound to push domains, such as recording, screencapture, porn detection, and watermarking, fees are incurred when streams are pushed. If you enable features bound to playback domains, fees are incurred when streams are played. This means if you create a transcoding template and bind it to a playback domain name, as long as you do not use the domain for playback, no transcoding fees will be charged. Using the watermarking or stream mix feature may incur standard transcoding fees, which are based on the resolution of output streams.

[](id:live_que5)

### Are there two expenses for porn detection?
Because CSS analyzes screenshots of live streams to detect pornographic content, using the porn detection feature will incur two expenses: **screencapture** and **porn detection**. Porn detection fees are based on the number of screenshots analyzed.
- CSS offers a free tier of 1,000 screenshots per month for the screencapture feature.
- CSS offers a free tier of 1,000 screenshots per month for porn detection.
  

For details, see [Live Screencapture](https://intl.cloud.tencent.com/document/product/267/39606) and [Intelligent Porn Detection](https://intl.cloud.tencent.com/document/product/267/39607).

[](id:live_que8)


### Can I allow only paid users to access my content?
Currently, CSS does not support controlling access to your content depending on whether a user is a paid user. However, if you record your videos and save them to VOD, you can encrypt the videos to control playback permissions.

## Transcoding

[](id:tran_que1)
### How is live transcoding billed? How can I estimate the transcoding fees?
Live transcoding fees depend on codec, resolution, and transcoding duration. Stream mix and watermarking are implemented by the transcoding module, so using the two features may also incur transcoding fees. For details, see [Live Transcoding](https://intl.cloud.tencent.com/document/product/267/39604).
Transcoding fees will only be charged once if the same live stream is watched by multiple viewers at the same bitrate.

**Example:** On January 1, 2022, you transcoded stream A to H.264_720P (one hour) and added watermarks to stream B (30 minutes; resolution of the output stream: 480p).
On January 2, 2021, your transcoding fees would be 0.0057 (USD/min) x 60 (min) + 0.0028 (USD/min) x 30 (min) = 0.426 USD.

[](id:tran_que2)
### I didn’t use the live transcoding feature, so why were transcoding fees incurred?
Live transcoding services include live real-time transcoding, stream mix, and watermarking. Using stream mix or watermarking will also incur transcoding fees.

[](id:tran_que3)
### Does stream mix always incur transcoding fees?
Yes. Because transcoding resources are consumed during stream mix regardless of whether the output stream is played, the transcoding fees for stream mix are based on the stream mix duration. This is different from the billing of live transcoding, which is based on playback duration.



## Live Recording
[](id:record_que1)
### How is live recording billed?
Live recording is billed by the peak number of concurrent recording channels in the current month. A single live stream recorded in one file format is counted as one recording channel. If you record in two formats (MP4 and HLS), they will be counted as two recording channels.

[](id:record_que2)
### How is the peak number of concurrent recording channels calculated?
One stream (stream ID) recorded in one format is counted as one recording channel. The number of concurrent recording channels is collected every five minutes, and the highest number each month is used for billing.
**Example:**

<style>#ye{background:#ffe699;}#gr{background:#c6e0b4;}#br{background:#bdd7ee}</style>
<table id="rroad">
<tr><th rowspan=2 width="10%" style="text-align:center;">Stream ID</th>
<th rowspan=2 width="10%" style="text-align:center;">Recording<br>Format</th>
<th colspan=7 width="50%" style="text-align:center;">Current Month</th>
</tr><tr>
<td style="text-align:center;">Day 1</td><td style="text-align:center;">Day 2</td><td style="text-align:center;">Day 3</td>
<td style="text-align:center;">…</td>
<td style="text-align:center;">Day 28</td><td style="text-align:center;">Day 29</td><td style="text-align:center;">Day 30</td>
</tr><tr>
<td rowspan=4 style="text-align:center;">A</td>
<td style="text-align:center;">HLS</td><td></td><td></td><td></td>
<td rowspan=13 style="text-align:center;">No recording tasks</td>
<td id="ye"></td><td id="ye"></td>
<td></td>
</tr><tr>
<td style="text-align:center;">MP4</td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td>
</tr><tr>
<td style="text-align:center;">FLV</td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td></td>
</tr><tr>
<td style="text-align:center;">AAC</td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td>
</tr><tr>
<td rowspan=4 style="text-align:center;">B</td>
<td style="text-align:center;">HLS</td><td></td><td id="gr"></td><td id="gr"></td><td id="gr"></td><td></td><td></td>
</tr><tr>
<td style="text-align:center;">MP4</td><td id="gr"></td><td id="gr"></td><td></td><td id="gr"></td><td id="gr"></td><td></td>
</tr><tr>
<td style="text-align:center;">FLV</td><td></td><td id="gr"></td><td></td><td id="gr"></td><td></td><td id="gr"></td>
</tr><tr>
<td style="text-align:center;">AAC</td><td></td><td id="gr"></td><td></td><td id="gr"></td><td></td><td></td>
</tr><tr>
<td rowspan=4 style="text-align:center;">C</td>
<td style="text-align:center;">HLS</td><td id="br"></td><td></td><td id="br"></td><td id="br"></td><td></td><td></td>
</tr><tr>
<td style="text-align:center;">MP4</td><td></td><td></td><td id="br"></td><td id="br"></td><td id="br"></td><td id="br"></td>
</tr><tr>
<td style="text-align:center;">FLV</td><td></td><td></td><td></td><td id="br"></td><td></td><td></td>
</tr><tr>
<td style="text-align:center;">AAC</td><td></td><td></td><td></td><td></td><td></td><td id="br"></td>
</tr><tr>
<td colspan=2 style="text-align:center;">Recording Channels</td>
<td style="text-align:center;">5</td><td style="text-align:center;">7</td><td style="text-align:center;">6</td><td style="text-align:center;">11</td><td style="text-align:center;">6</td><td style="text-align:center;">5</td>
</tr><tr>
<td colspan=2 style="text-align:center;">Peak Number of Recording Channels</td><td colspan=7 style="text-align:center;">11</td>
</tr>
</table>

>? 
>- Yellow: Recording tasks for stream **A**.
>- Green: Recording tasks for stream **B**.
>- Blue: Recording tasks for stream **C**.




[](id:record_que3)
### Why was I charged 10.5882 USD after using live recording? 
When two live streams are recorded simultaneously or one live stream is recorded into two formats, there will be two concurrent recording channels. Live recording is billed based on the peak number of concurrent recording channels each month at 5.2941 USD per channel. Therefore, if you started two concurrent recording channels at most in a month, your recording fee for the month would be 10.5882 USD. For more information, see [Live Recording](https://intl.cloud.tencent.com/document/product/267/39605).
To view your peak number of concurrent recording channels in a previous month, go to **Bill Details** > [Bill by Instance](https://console.cloud.tencent.com/expense/bill/summary) and click **Bill Details** in the **Operation** column.

