## Overview

Transcoding fees and relaying fees are the two main types of fees for using StreamLive. In addition, for StreamLive features that rely on the capabilities of other Tencent Cloud products, fees for the corresponding product will be incurred as well.

Billable items:
<table>
<thead>
<tr>
<th colspan="2">Item</th>
<th>Description</th>
<th>Billing Mode</th>
</tr>
</thead>
<tbody><tr>
<td rowspan="3">Live transcoding</td>
<td>Standard transcoding</td>
<td><li>Incurred for using the standard transcoding feature.<li>Billed based on the transcoding duration (the price varies with the resolution of the output stream).</td>
<td>Daily pay-as-you-go</td>
</tr>
<tr>
<td>Top Speed Codec (TSC) transcoding</td>
<td><li>Incurred for using the TSC transcoding feature<li>Billed based on the transcoding duration (the price varies with the resolution of the output stream).</td>
<td>Daily pay-as-you-go</td>
</tr>
<tr>
<td>Audio transcoding</td>
<td><li>Incurred for using the audio transcoding feature.<li>Billed based on the transcoding duration.</td>
<td>Daily pay-as-you-go</td>
</tr>
<tr>
<td colspan="2">Relaying</td>
<td>Billed according to the traffic consumed (a tiered pricing model is used).</td>
<td>Daily pay-as-you-go</td>
</tr>
</tbody></table>

StreamLive features that depend on other Tencent Cloud products:

<table>
<thead>
<tr>
<th>Feature</th>
<th>Description</th>
<th>Billing Mode</th>
</tr>
</thead>
<td>Recording</td>
<td>The scheduled recording feature (whose event type is `Time Record`) relies on Cloud Object Storage (COS). Using it will incur COS storage fees.</td>
<td><a href="https://www.tencentcloud.com/document/product/436/16871">COS Billing Overview</a></td>
</tr>
<tr>
<td>Time shifting</td>
<td>The time shifting feature is implemented by Cloud Streaming Services (CSS). Using it will incur CSS time shifting fees.</td>
<td><a href="(https://www.tencentcloud.com/document/product/267/46847">Billing of CSS Time Shifting</a></td>
</tr>
<tr>
<td>Face blurring</td>
<td>The face blurring feature is implemented by Media Processing Service (MPS). Using it will incur MPS content recognition fees.</td>
<td><a href="((https://www.tencentcloud.com/document/product/1041/49204">MPS Billing Overview</a></td>
</tr>
</tbody></table>

## Live Transcoding

StreamLive offers three types of transcoding capabilities: **standard transcoding**, **TSC transcoding**, and **audio transcoding**. They are billed according to the transcoding duration. The price varies with the codec used and resolution of the output video.

TSC uses intelligent, dynamic transcoding technologies and a high-precision bitrate control model to produce videos with higher definitions and lower bitrates. For details, see [TSC Transcoding](https://www.tencentcloud.com/document/product/267/39604#.E6.9E.81.E9.80.9F.E9.AB.98.E6.B8.85.E8.BD.AC.E7.A0.81).

Your transcoding fees vary according to the transcoding mode you use.

<table>
<thead>
<tr>
<th>Transcoding Mode</th>
<th colspan="2" style="text-align:center;">Fees</th>
</tr>
</thead>
<tbody><tr>
<td>Joint transcoding</td>
<td colspan="2" style="text-align:center;">Video transcoding fees</td>
</tr>
<tr>
<td>Separate transcoding</td>
<td style="text-align:center;">Video transcoding fees</td>
<td style="text-align:center;">Audio transcoding fees</td>
</tr>
<tr>
<td>Audio-only transcoding</td>
<td colspan="2" style="text-align:center;">Audio transcoding fees</td>
</tr>
</tbody></table>

### Must-knows

*   Billing mode: Pay-as-you-go.
*   Billing cycle: The transcoding feature is billed daily. The fees incurred each day (from 00:00 to 24:00 (UTC+8)) are deducted the following day at the time of billing.
*    **When input data is first received after you start a channel (the channel status is "RUNNING"), the system will start transcoding the data according to the transcoding templates bound to the channel's output. If an output is bound with two transcoding templates, transcoding fees will be calculated separately according to the codec used and the output resolution. Please note that after input data is first received, as long as the channel is still in "RUNNING" status, even if no data is received or generated for a certain period of time, transcoding fees will still be incurred. This is because the system inserts frames in between automatically. Only channels whose status is "IDLE" will not incur transcoding fees.**
*   Transcoding duration is rounded up to the nearest minute. The system calculates your transcoding cost by dividing your total transcoding minutes by 60 and then multiplying the result by the unit price of transcoding.
*   Joint transcoding only incurs video transcoding fees. Audio transcoding fees are charged only if you use audio-only transcoding.


### Standard transcoding

#### Pricing

<table>
<thead>
<tr>
<th>Codec</th>
<th>Resolution</th>
<th>Price (USD/hour)</th>
<th>Remarks (the long side is whichever dimension is longer)</th>
</tr>
</thead>
<tbody><tr>
<td rowspan="5"><strong>H.264 (AVC)</strong></td>
<td>480p</td>
<td>0.1818</td>
<td>Long side ≤ 640 px and short side ≤ 480 px</td>
</tr>
<tr>
<td>720p</td>
<td>0.3636</td>
<td>Long side ≤ 1280 px and short side ≤ 720 px</td>
</tr>
<tr>
<td>1080p</td>
<td>0.7272</td>
<td>Long side ≤ 1936 px and short side ≤ 1088 px</td>
</tr>
<tr>
<td>2K</td>
<td>1.4544</td>
<td>Long side ≤ 2560 px and short side ≤ 1440 px</td>
</tr>
<tr>
<td>4K</td>
<td>3.1288</td>
<td>Long side &gt; 2560 px or short side &gt; 1440 px</td>
</tr>
<tr>
<td rowspan="5"><strong>H.265 (HEVC)</strong></td>
<td>480p</td>
<td>0.9453</td>
<td>Long side ≤ 640 px and short side ≤ 480 px</td>
</tr>
<tr>
<td>720p</td>
<td>1.8907</td>
<td>Long side ≤ 1280 px and short side ≤ 720 px</td>
</tr>
<tr>
<td>1080p</td>
<td>3.7814</td>
<td>Long side ≤ 1936 px and short side ≤ 1088 px</td>
</tr>
<tr>
<td>2K</td>
<td>7.5628</td>
<td>Long side ≤ 2560 px and short side ≤ 1440 px</td>
</tr>
<tr>
<td>4K</td>
<td>15.1257</td>
<td>Long side &gt; 2560 px or short side &gt; 1440 px</td>
</tr>
</tbody></table>

>! For example, if the long side of an output video is 1280 px and the short side is 480 px, the price for 720p will apply. The long side is whichever dimension is longer.

#### Billing details

*   Billable item: Standard transcoding duration
*   Billing rules: Your standard transcoding durations in a natural day are multiplied by their respective unit prices (which depend on the codec used and resolution of the output video) to determine the fee.

#### Billing formula

Standard transcoding fee = Transcoding duration x Unit price (determined by the codec and output resolution)

#### Billing example

Assume that on January 1, 2021, you transcoded a one-hour live stream to 720p using the H.264 codec and watermarked a 30-min live stream (the output resolution is 480p). The following transcoding fee would be billed on January 2, 2021:

0.3636 (USD/hour) x 1 (hour) + 0.1818 (USD/hour) x 0.5 (hour) = 0.4545 USD

### TSC transcoding

#### Pricing

<table>
<thead>
<tr>
<th>Codec</th>
<th>Resolution</th>
<th>Price (USD/hour)</th>
</tr>
</thead>
<tbody><tr>
<td rowspan="5">H.264 (AVC)</td>
<td>480p</td>
<td>0.5999</td>
</tr>
<tr>
<td>720p</td>
<td>1.1999</td>
</tr>
<tr>
<td>1080p</td>
<td>2.3998</td>
</tr>
<tr>
<td>2K</td>
<td>4.7995</td>
</tr>
<tr>
<td>4K</td>
<td>10.3250</td>
</tr>
<tr>
<td rowspan="5">H.265 (HEVC)</td>
<td>480p</td>
<td>3.1195</td>
</tr>
<tr>
<td>720p</td>
<td>6.2393</td>
</tr>
<tr>
<td>1080p</td>
<td>12.4786</td>
</tr>
<tr>
<td>2K</td>
<td>24.9572</td>
</tr>
<tr>
<td>4K</td>
<td>49.9148</td>
</tr>
</tbody></table>

#### Billing details

*   Billable item: TSC transcoding duration
*   Billing rules: Your TSC transcoding durations in a natural day are multiplied by their respective unit prices (which depend on the resolution of the output video) to determine the fee.

#### Billing formula

TSC transcoding fee = Transcoding duration x Unit price (determined by the output resolution)

#### Billing example

Assume that on August 1, 2021, you used the TSC transcoding feature to transcode a one-hour live stream to 720p and a 30-min live stream to 480p. The following transcoding fee would be billed on August 2, 2021:

1.1999 (USD/hour) x 1 (hour) + 0.5999 (USD/hour) x 0.5 (hour) = 1.49985 USD

### Audio transcoding

StreamLive's audio transcoding feature allows you to transcode audio to multiple formats to meet different business needs. It's a useful and reliable feature that can spare you the trouble of adaption and reduce your labor and hardware costs.

#### Pricing

| Billable Item     | Billed By                               | Price             |
| ---- | --------- | ------------ |
| Audio transcoding | The audio transcoding duration. | 0.1218 USD/hour |

#### Billing details

*   Billable item: Audio transcoding duration
*   Billing rules: Your audio transcoding duration in a natural day is multiplied by the unit price to determine the fee.

#### Billing formula

Audio transcoding fee = Transcoding duration x Unit price

#### **Billing example**

Assume that you used the audio-only transcoding feature to transcode a five-hour live stream on February 1, 2021. The following audio transcoding fee would be billed on February 2, 2021:

0.1218 (USD/hour) x 5 (hours) = 0.609 USD

## Relaying

Relaying fees will be incurred if you use StreamLive to publish streams to a third party.

### Must-knows

*   Billing mode: Pay-as-you-go.
*   Billing cycle: The relaying feature is billed daily. The fees incurred each day (from 00:00 to 24:00 (UTC+8)) are deducted the following day at the time of billing.
*   If your output type is "HLS_STREAM_PACKAGE", "DASH_STREAM_PACKAGE", "HLS_ARCHIVE", or "DASH_ARCHIVE", relaying fees will not be charged.

### Pricing

<table>
<thead>
<tr>
<th>Region</th>
<th>Traffic Tier</th>
<th>Price (USD/GB)</th>
</tr>
</thead>
<tbody><tr>
<td rowspan="4">Hong Kong</td>
<td>0-300 GB</td>
<td>0.1176</td>
</tr>
<tr>
<td>300 GB - 1.5 TB</td>
<td>0.0833</td>
</tr>
<tr>
<td>1.5-5 TB</td>
<td>0.0804</td>
</tr>
<tr>
<td>≥ 5 TB</td>
<td>0.0784</td>
</tr>
<tr>
<td rowspan="4">Singapore</td>
<td>0-300 GB</td>
<td>0.1176</td>
</tr>
<tr>
<td>300 GB - 1.5 TB</td>
<td>0.0833</td>
</tr>
<tr>
<td>1.5-5 TB</td>
<td>0.0804</td>
</tr>
<tr>
<td>≥ 5 TB</td>
<td>0.0784</td>
</tr>
<tr>
<td rowspan="4">Santa Clara</td>
<td>0-300 GB</td>
<td>0.0882</td>
</tr>
<tr>
<td>300 GB - 1.5 TB</td>
<td>0.0833</td>
</tr>
<tr>
<td>1.5-5 TB</td>
<td>0.0686</td>
</tr>
<tr>
<td>≥ 5 TB</td>
<td>0.0490</td>
</tr>
<tr>
<td rowspan="4">Frankfurt</td>
<td>0-300 GB</td>
<td>0.0882</td>
</tr>
<tr>
<td>300 GB - 1.5 TB</td>
<td>0.0833</td>
</tr>
<tr>
<td>1.5-5 TB</td>
<td>0.0686</td>
</tr>
<tr>
<td>≥ 5 TB</td>
<td>0.0490</td>
</tr>
<tr>
<td rowspan="4">Mumbai</td>
<td>0-300 GB</td>
<td>0.1071</td>
</tr>
<tr>
<td>300 GB - 1.5 TB</td>
<td>0.0833</td>
</tr>
<tr>
<td>1.5-5 TB</td>
<td>0.0804</td>
</tr>
<tr>
<td>≥ 5 TB</td>
<td>0.0784</td>
</tr>
<tr>
<td rowspan="4">Bangkok</td>
<td>0-300 GB</td>
<td>0.1071</td>
</tr>
<tr>
<td>300 GB - 1.5 TB</td>
<td>0.0833</td>
</tr>
<tr>
<td>1.5-5 TB</td>
<td>0.0804</td>
</tr>
<tr>
<td>≥ 5 TB</td>
<td>0.0784</td>
</tr>
<tr>
<td rowspan="4">Tokyo</td>
<td>0-300 GB</td>
<td>0.1341</td>
</tr>
<tr>
<td>300 GB - 1.5 TB</td>
<td>0.1047</td>
</tr>
<tr>
<td>1.5-5 TB</td>
<td>0.1011</td>
</tr>
<tr>
<td>≥ 5 TB</td>
<td>0.0988</td>
</tr>
<tr>
<td rowspan="4">Seoul</td>
<td>0-300 GB</td>
<td>0.1260</td>
</tr>
<tr>
<td>300 GB - 1.5 TB</td>
<td>0.1220</td>
</tr>
<tr>
<td>1.5-5 TB</td>
<td>0.1200</td>
</tr>
<tr>
<td>≥ 5 TB</td>
<td>0.1170</td>
</tr>
<tr>
<td rowspan="4">São Paulo</td>
<td>0-300 GB</td>
<td>0.1470</td>
</tr>
<tr>
<td>300 GB - 1.5 TB</td>
<td>0.1352</td>
</tr>
<tr>
<td>1.5-5 TB</td>
<td>0.1235</td>
</tr>
<tr>
<td>≥ 5 TB</td>
<td>0.1117</td>
</tr>
</tbody></table>

### Billing details

*   Billable item: Relaying traffic.
*   Billing rules: A tiered pricing model is used. The relaying traffic consumed is multiplied by its unit price in each tier, and the results are added up to determine the fee.

### Billing formula

Relaying fee = Amount of traffic relayed x Unit price

### Billing example

Assume that on August 5, 2021, you used StreamLive in Hong Kong to relay a live stream to the local address "rtp\://129.226.27.xxx:57024". The traffic consumed was 1.8 TB. The following relaying fee would be incurred:

300 (GB) x 0.1176 (USD/GB) + 1200 (GB) x 0.0833 (USD/GB) + 300 (GB) x 0.0804 (USD/GB) = 159.36 USD
