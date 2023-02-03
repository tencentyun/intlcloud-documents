## Live Streaming
[](id:live_que1)
### What are the billable items of CSS? What fees do I need to pay?
Billable items of CSS include basic services and value-added services. You may also incur extended service fees if you use CSS features that rely on the capabilities of other Tencent Cloud products.

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
If you bind recording, screencapture, porn detection, or watermarking templates to push domains, fees are incurred when streams are pushed. If you bind the templates to playback domains, fees are incurred when streams are played. This means if you create a transcoding template and bind it to a playback domain name, as long as you do not use the domain for playback, no transcoding fees will be charged. Using the watermarking or stream mix feature may incur standard transcoding fees, which are based on the resolution of output streams.

[](id:live_que7)
### Are there two expenses for porn detection?
Because CSS analyzes screenshots of live streams to detect pornographic content, using the porn detection feature will incur two expenses: **screencapture** and **porn detection**. Porn detection fees are based on the number of screenshots analyzed.
- CSS offers a free tier of 1,000 screenshots per month for the screencapture feature.
- CSS offers a free tier of 1,000 screenshots per month for porn detection.

For details, see [Live Screencapture](https://intl.cloud.tencent.com/document/product/267/39606) and [Intelligent Porn Detection](https://intl.cloud.tencent.com/document/product/267/39607).

[](id:live_que9)
### Can I track my usage of CSS packages in real time?
You can view your package usage in the [CSS console](https://console.cloud.tencent.com/live/resources/package?type=traffic), but real-time usage statistics are not supported currently.
Your usage each day is not reflected in the data until billing is processed by the system the following day (the exact time may vary).

[](id:live_que10)
### Can I allow only paid users to access my content?
CSS cannot identify paid users currently. If you record your live streams and save them to VOD, you can allow only paid users to access your content by encrypting the videos.

 

[](id:live_que12)
### Why is the traffic usage data shown in the console different from the log data?

The downstream traffic recorded in logs is application layer data. The actual traffic consumed is 5-15% more than application layer data.

- TCP/IP headers: Each TCP/IP HTTP request packet can be up to 1,500 bytes, including 40-byte TCP and IP headers. The traffic consumed by headers (about 3% of the total) is not counted into application layer data.
- TCP retransmission: About 3-10% of packets are lost during transmission. The packets will be sent again by the server. Such traffic (about 3-7% of the total) is not counted by the application layer either.

As an industry standard, billable traffic is application-layer traffic plus the additional traffic described above. Tencent Cloud calculates the additional traffic as 10% of the total, so the traffic usage shown in the console is 110% of that recorded in logs.

## Prepaid Packages

[](id:pack_que2)
### I purchased traffic packages. Why were fees still deducted from my account balance?

Traffic packages can only deduct your traffic usage in the daily bill-by-traffic mode.
- If you are on daily bill-by-bandwidth mode, your traffic packages cannot be used for deduction. You can change your billing mode in the console. For details, see [Changing Billing Modes](https://intl.cloud.tencent.com/document/product/267/30411).
- If you are on daily bill-by-traffic mode and fees are still deducted from your account balance, check if you have used [value-added services](https://intl.cloud.tencent.com/document/product/267/2819) such as live transcoding, live recording, screencapture, and porn detection. Value-added services are billed based on usage. Your usage each day is billed the following day. You can also buy packages for value-added services. CSS offers three types of packages: traffic package, standard transcoding package, and Top Speed Codec (TSC) transcoding package. To learn more, see [Prepaid Packages](https://www.tencentcloud.com/document/product/267/52220).
- Fees are also incurred after you use up your packages. You can view the deduction details in [Bill Details](https://console.cloud.tencent.com/expense/bill/summary). For detailed directions, see [Viewing Bills](https://intl.cloud.tencent.com/document/product/267/36278).


[](id:pack_que3)
### I only bought traffic packages. Will CSS suspend services for my account after I use up the packages?
No. Traffic packages are paid in advance, and usage is deducted from purchased packages.

- If your billing mode for LVB is daily bill-by-traffic, downstream LVB traffic will be deducted from your traffic packages first, and the additional usage will be billed daily at tiered pay-as-you-go rates.
- After you use up your packages, make sure there is sufficient balance in your account to pay your daily pay-as-you-go charges. If you have overdue payments, please top up within 24 hours. Otherwise, services will be suspended for your account. We recommend you check your [account balance](https://console.cloud.tencent.com/expense/overview) regularly.

>? Traffic packages cannot be used for deduction if you are on monthly bill-by-traffic mode or monthly/daily bill-by-bandwidth mode.

## Transcoding

[](id:tran_que1)
### How is live transcoding billed? How can I estimate the cost?
Live transcoding fees depend on the transcoding codec, resolution, and duration. Because stream mixing and watermarking are implemented by the transcoding module, using these two features will also incur transcoding fees. For details, see [Live Transcoding](https://intl.cloud.tencent.com/document/product/267/39604).
Transcoding fees will only be charged once if the same live stream is watched by multiple viewers at the same bitrate.

**Example:** Suppose on January 1, 2021, you transcoded stream A to H.264_720P (one hour) and added watermarks to stream B (30 minutes; output resolution: 480p).
On January 2, 2021, your transcoding fees would be 0.0057 (USD/min) x 60 (min) + 0.0028 (USD/min) x 30 (min) = 0.426 USD.

[](id:tran_que2)
### I didn’t use the live transcoding feature. Why were transcoding fees incurred?
Transcoding services include live transcoding, stream mixing, and watermarking. Using the stream mixing or watermarking feature will also incur transcoding fees.

[](id:tran_que3)
### Does stream mixing always incur transcoding fees?
Yes. Because transcoding resources are consumed during stream mixing regardless of whether the output stream is played, stream mixing is billed based on the output duration. This is different from the billing of live transcoding, which is based on playback duration.

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
When two live streams are recorded simultaneously or one live stream is recorded into two formats, there will be two concurrent recording channels. Live recording is billed based on the peak number of concurrent recording channels each month at 5.2941 USD per channel. Therefore, if you had two concurrent recording channels at most in a month, your recording fee for the month would be 10.5882 USD. For more information, see [Live Recording](https://intl.cloud.tencent.com/document/product/267/39605).
To view your peak number of concurrent recording channels in a previous month, go to **Bill Details** > [Bill by Instance](https://console.cloud.tencent.com/expense/bill/summary) and click **Bill Details** in the **Operation** column.