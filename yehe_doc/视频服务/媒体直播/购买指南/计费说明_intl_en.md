## Billing Overview

<table>
<thead>
<tr>
<th colspan=2>Billable Item</th>
<th>Description</th>
<th>Billing Mode</th>
</tr>
</thead>
<tbody><tr>
<td rowspan=3>Live transcoding</td>
<td>Standard transcoding</td>
<td><li>Incurred for using the standard transcoding feature during live streaming<li>Billed based on the transcoding duration and aspect ratio of output video</td>
<td>Daily pay-as-you-go</td>
</tr>
<tr>
<td>Top speed codec transcoding</td>
<td><li>Incurred for using the top speed codec transcoding feature during live streaming<li>Billed based on the transcoding duration and aspect ratio of output video</td>
<td>Daily pay-as-you-go</td>
</tr>
<tr>
<td>Audio transcoding</td>
<td><li>Incurred for using the audio transcoding feature during live streaming<li>Billed based on the transcoding duration</td>
<td>Daily pay-as-you-go</td>
</tr>
<tr>
<td colspan=2>Relaying</td>
<td>The relaying feature adopts a tiered pricing method and is billed based on traffic, whose cost varies from region to region.</td>
<td>Daily pay-as-you-go</td>
</tr>
</tbody></table>

## Live Transcoding

StreamLive offers the **standard transcoding**, **top speed codec transcoding**, and **audio transcoding** features, which are billed separately based on the transcoding duration and resolution (aspect ratio) of output video during live streaming.

The top speed codec transcoding feature leverages intelligent and dynamic transcoding technologies and a high-precision bitrate control model to produce high-definition video at lower bitrate. For details, please see [Top Speed Codec Transcoding](https://intl.cloud.tencent.com/document/product/267/39604#.E6.9E.81.E9.80.9F.E9.AB.98.E6.B8.85.E8.BD.AC.E7.A0.81).

The transcoding fees incurred vary depending on the transcoding method, as detailed below.

<table>
<thead>
<tr>
<th>Transcoding Method</th>
<th colspan=2 style="text-align:center">Fee</th>
</tr>
</thead>
<tbody><tr>
<td>Joint transcoding</td>
<td colspan=2 style="text-align:center">Video transcoding fee</td>
</tr>
<tr>
<td>Separate transcoding</td>
<td style="text-align:center">Video transcoding fee</td>
<td style="text-align:center">Audio transcoding fee</td>
</tr>
<tr>
<td>Audio-only transcoding</td>
<td colspan=2 style="text-align:center">Audio transcoding fee</td>
</tr>
</tbody></table>
### Notes

- Billing mode: pay-as-you-go
- Billing cycle: Transcoding is billed daily and the fees incurred in a day from 00:00 to 24:00 (UTC+8) are charged the next day when bills are generated. For the specific fees incurred and billing time, see the bills.
- Transcoding duration less than 1 minute will be billed as 1 minute.
- You won’t be charged the transcoding fee if you haven’t used the transcoding feature.
- Joint transcoding is billed as video transcoding, so you are not charged the audio transcoding fee for using this method. The audio transcoding fee will be incurred only if you use audio-only transcoding.
- **StreamLive also provides monthly billing mode to customers with large monthly demands. You can contact your sales rep to change your billing mode.**

### Standard transcoding

#### Pricing

<table>
<thead>
<tr>
<th>Codec</th>
<th>Resolution</th>
<th>Price (USD/hour)</th>
<th>Remarks (long side refers to the longer side between the width and height of output video)</th>
</tr>
</thead>
<tbody><tr>
<td rowspan=5><strong>H.264 (AVC)</strong></td>
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
<td rowspan=5><strong>H.265 (HEVC)</strong></td>
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
> ! For example, if the long side of an output video is 1280 px and short side 480 px, its resolution will be counted as 720p.

#### Billing

- Billable item: standard transcoding duration
- Billing rules: The fee is calculated by multiplying your transcoding durations in a natural day by their corresponding unit prices (determined by the codec used and the resolution of output video).

#### Fee calculation formula

Standard transcoding fee = Transcoding duration x Codec- and resolution-specific unit price

#### Billing example

Assume that, on January 1, 2021, you transcoded a 1-hour segment of live stream A to 720p video using the H.264 codec and watermarked a 30 min-segment of live stream B, outputting 480p video. The transcoding fee charged on January 2, 2021 would be:

Daily transcoding fee = 0.3636 (USD/hour) x 1 (hour) + 0.1818 (USD/hour) x 0.5 (hour) = 0.4545 USD

### Top speed codec transcoding

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
<td rowspan=5>H.264 (AVC)</td>
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
<td rowspan=5>H.265 (HEVC)</td>
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


#### Billing

- Billable item: top speed codec transcoding duration
- Billing rules: The fee is calculated by multiplying your top speed codec transcoding durations in a natural day by their corresponding unit prices (determined by the resolution of output video).

#### Fee calculation formula

Top speed codec transcoding fee = Transcoding duration x Resolution-specific unit price

#### Billing example

Assume that, on August 1, 2021, you used the top speed codec transcoding feature to transcode a 1-hour segment of live stream A to 720p video and a 30-min segment of live stream B to 480p video. The transcoding fee charged on August 2, 2021 would be:

Daily top speed codec transcoding fee = 1.1999 (USD/hour) x 1 (hour) + 0.5999 (USD/hour) x 0.5 (hour) = 1.49985 USD

### Audio transcoding

StreamLive’s audio transcoding feature allows you to transcode audio to multiple formats based on your business needs at high quality, enabling effective and reliable audio output and helping you reduce adaptation, labor, and hardware costs.

#### Pricing

| Billable Item   | Billing Mode           | Price            |
| -------- | ------------------ | ---------------- |
| Audio transcoding | By audio transcoding duration | 0.1218 USD/hour |

#### Billing

- Billable item: audio transcoding duration
- Billing rules: The fee is calculated by multiplying your audio transcoding duration in a natural day by the unit price.

#### Fee calculation formula

Audio transcoding fee = Transcoding duration x Unit price

#### **Billing example**

Assume that you used the audio-only transcoding feature to transcode audio of 5 hours on February 1, 2021. The audio transcoding fee charged on February 2, 2021 would be:

Daily audio transcoding fee = 0.1218 (USD/hour) x 5 (hours) = 0.609 USD

## Relaying

StreamLive’s relaying feature allows you to relay live streams to third-party addresses and is charged based on the amount of traffic relayed.

### Notes

- Billing mode: pay-as-you-go
- Billing cycle: Relaying is billed daily and the fees incurred in a day from 00:00 to 24:00 (UTC+8) are charged the next day when bills are generated. For the specific fees incurred and billing time, see the bills.
- You are not charged the relaying fee if you relay to StreamPackage, as it’s not a third-party service.

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
<td rowspan=4>Hong Kong</td>
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
<td rowspan=4>Santa Clara</td>
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
<td rowspan=4>Frankfurt</td>
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
<td rowspan=4>Mumbai</td>
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
<td rowspan=4>Bangkok</td>
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
<td rowspan=4>Tokyo</td>
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
<td rowspan=4>Seoul</td>
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
<td rowspan=4>Saint Paul</td>
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
### Billing

- Billable item: amount of traffic relayed to third parties
- Billing rules: The fee is calculated by multiplying the amount of traffic relayed to third parties by the unit price of traffic for each traffic tier. Traffic relayed to StreamPackage is not charged.

### Fee calculation formula

Relaying fee = Amount of traffic relayed x Unit price

### Billing example

Assume that, on August 5, 2021, you used StreamLive’s relaying service in Hong Kong and relayed live streams of 1.8 TB to the local address rtp://129.226.27.xxx:57024. The relaying fee incurred would be:

300 (GB) x 0.1176 (USD/GB) + 1200 (GB) x 0.0833 (USD/GB) + 300 (GB) x 0.0804 (USD/GB) = 159.36 USD