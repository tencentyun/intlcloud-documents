CSS provides [standard transcoding](#n_trans), [Top Speed Codec (TSC) transcoding](#s_trans), and [audio transcoding](#a_trans) services, which are billed by the codec, live stream image resolution (size), and transcoding duration. Enabling **watermarking** or **stream mixing** may also incur transcoding fees, which are billed by the resolution of the output live streams.

## Notes

- Billing mode: Pay-as-you-go.
- Billing cycle: Daily billing cycle. The fees for a day will be deducted at 10 AM the next day. For users on the monthly billing cycle, this month's transcoding bill will be generated between the 1st and 5th day of the next month.
- Transcoding is disabled by default and can be enabled and configured via the [CSS console](https://intl.cloud.tencent.com/document/product/267/31071) or through [TencentCloud APIs](https://intl.cloud.tencent.com/document/product/267/30790).
- The transcoding duration will be rounded up to the nearest 1 minute for billing.
- If the transcoding service is not used, no fees will be incurred.



<span id="n_trans1"></span>

## Standard Transcoding

### Pricing

<table>
<tr>
<th >Codec</th>
<th >Recommended Bitrate (Kbps)</th>
<th >Resolution</th>
<th >Price (USD/min)</th>
<th >Notes (the longer side of the width and height is defined as the long side of the live stream image)</th>
</tr>
<tr>
<td rowspan="5"><b>H.264</td>
<td >500</td>
<td>480p</td>
<td>0.0028</td>
<td>The long side of the image is ≤ 640, and the short side of the image is ≤ 480</td>
</tr>
<tr>
<td >1000</td>
<td>720p</td>
<td>0.0057</td>
<td>The long side of the image is ≤ 1280, and the short side of the image is ≤ 720</td>
</tr>
<tr>
<td rowspan="2">2000</td>
<td>1080p</td>
<td>0.0111</td>
<td>The long side of the image is ≤ 1936, and the short side of the image is ≤ 1088</td>
</tr>
<tr>
<td>2K</td>
<td>0.024</td>
<td>The long side of the image is ≤ 2560, and the short side of the image is ≤ 1440</td>
</tr>
<tr>
<td >4000</td>
<td>4K</td>
<td>0.0491</td>
<td>The long side of the image is > 2560, and the short side of the image is > 1440</td>
</tr>
<tr>
<td rowspan="5"><b>H.265</td>
<td >500</td>
<td>480p</td>
<td>0.0141</td>
<td>The long side of the image is ≤ 640, and the short side of the image is ≤ 480</td>
</tr>
<tr>
<td >1000</td>
<td>720p</td>
<td>0.0275</td>
<td>The long side of the image is ≤ 1280, and the short side of the image is ≤ 720</td>
</tr>
<tr>
<td rowspan="2">2000</td>
<td>1080p</td>
<td>0.0549</td>
<td>The long side of the image is ≤ 1936, and the short side of the image is ≤ 1088</td>
</tr>
<tr>
<td>2K</td>
<td>0.1183</td>
<td>The long side of the image is ≤ 2560, and the short side of the image is ≤ 1440</td>
</tr>
<tr>
<td >4000</td>
<td>4K</td>
<td>0.2366</td>
<td>The long side of the image is > 2560, or the short side of the image is > 1440</td>
</tr>
</table>

>!For example, if the long side of the image is 1280 and the short side of the image is 480, then the video resolution will be counted as 720p. The side of the image with a greater value is taken to be the long side of the image.


### Billing overview

- Billable item: The duration of live transcoding (or the duration of stream mixing or the watermarked live stream if the stream mixing or watermarking feature is enabled).
- Billing rules:
  - The fees are calculated by multiplying the transcoding duration by the codec and resolution on a day and the corresponding unit price.
  - Live transcoding is triggered by stream pulling, and playback will incur standard transcoding fees. Live watermarking is triggered by pushing and live stream mixing is triggered by signaling. Using live watermarking and stream mixing will generate standard transcoding fees, even if the stream is not played back.

### Billing formula

Standard transcoding fees = Transcoding duration x Price of the corresponding codec and resolution. 

### Billing example

If you used the live transcoding and watermarking service on January 1, 2021 where live stream A was transcoded to `H.264_720P` for 1 hour and live stream B was watermarked at 480p for 30 minutes, then the live transcoding fees you would need to pay on January 2, 2021 would be as follows:
Daily live transcoding fees = 0.0057 (USD/min) × 60 (min) + 0.0028 (USD/min) × 30 (min) = 0.426 USD.
		
<span id="s_trans"></span>

## TSC Transcoding

### Pricing

<table>
<tr>
<th>Codec</th>
<th>Resolution</th>
<th>Price (USD/min)</th>
</tr><tr>
<td rowspan="5"><b>H.264</td>
<td>480p</td>
<td>0.0116</td>
</tr><tr>
<td>720p</td>
<td>0.0222</td>
</tr><tr>
<td>1080p</td>
<td>0.0443</td>
</tr><tr>
<td>2K</td>
<td>0.0886</td>
</tr><tr>
<td>4K</td>
<td>0.1772</td>
</tr><tr>
<td rowspan="5"><b>H.265</td>
<td>480p</td>
<td>0.0349</td>
</tr><tr>
<td>720p</td>
<td>0.0665</td>
</tr><tr>
<td>1080p</td>
<td>0.1329</td>
</tr><tr>
<td>2K</td>
<td>0.2659</td>
</tr><tr>
<td>4K</td>
<td>0.5317</td>
</tr>
</table>

### Billing overview

- Billing rules: Fees are calculated by multiplying the TSC transcoding duration on a day and the corresponding unit price.


### Billing formula

TSC transcoding fees = Transcoding duration x Price of the corresponding codec and resolution. 

### Billing example

If you used the TSC transcoding service on January 1, 2021, where live stream A was transcoded to a TSC output at 720p for 1 hour and live stream B was transcoded to a TSC output at 480p for 30 minutes, then the TSC transcoding fees you would need to pay on January 2, 2021 would be as follows:
Daily TSC transcoding fees = 0.0222 (USD/min) × 60 (min) + 0.0116 (USD/min) × 30 (min) = 1.68 USD.

>? If you have a large-scale live streaming business, then a daily billing mode may not meet your needs. Please contact Tencent Cloud sales or [submit a ticket](https://console.cloud.tencent.com/workorder/category) to determine the best billing mode for you.

<span id="a_trans"></span>	

## Audio Transcoding

CSS offers an audio transcoding service. The service offers high-quality audio transcoding features that can transcode audio and video content to multiple formats, helping you reduce your adaptation, labor, and hardware costs, provide more effective and reliable outputs for the audiovisual industry, and optimally adapt to your specific business.

### Pricing

| Billable Item   | Billing Mode           | Price            |
| -------- | ------------------ | ------------- |
| Audio transcoding | Billed by the audio transcoding duration | 0.00099 USD/min |

### Billing overview

- Billable item: The audio transcoding duration.
- Billing rules: Fees are calculated by multiplying the audio transcoding duration on a day and the corresponding unit price.

### Billing formula

Audio transcoding fees = Unit price × Transcoding duration.

### Billing example

If you used the audio transcoding service for 5 hours on February 1, 2021, then the live audio transcoding fees you would need to pay on February 2, 2021 would be as follows:
Daily audio transcoding fees = 0.00099 (USD/min) x 300 (min) = 0.297 USD.

> !
> - **New billing rules for the audio transcoding feature took effect on February 1, 2021. All bills since February 2, 2021 have been generated according to the new billing rules.**
> - [Web push](https://intl.cloud.tencent.com/document/product/267/35968) uses the WebRTC protocol and the Opus audio codec. If LVB is used for playing back web push in the RTMP, FLV, or HLS formats, then transcoding will be initiated automatically to transcode audio into the AAC format, which will incur audio transcoding fees.
