## Overview
- Billing mode: **Daily pay-as-you-go**
- Billing cycle: Daily billing cycle. Traffic fees generated each day are deducted the following day. For the actual fee deduction and bill generation time, see your billing statement.
- **Billing regions outside the Chinese mainland**:
  - Asia Pacific 1: Hong Kong (China), Singapore, Macao (China), Vietnam, Thailand, Nepal, Cambodia, Pakistan
  - Asia Pacific 2: Taiwan (China), Japan, Malaysia, Indonesia, South Korea
  - Asia Pacific 3: Philippines, India, Australia
  - North America: United States, Canada, Mexico
  - Europe: Netherlands, Germany, Russia, United Kingdom, Ireland, Italy, Spain, France
  - Middle East: United Arab Emirates, Türkiye, Qatar, Saudi Arabia, Bahrain, Iraq
  - Africa: South Africa
  - South America: Brazil, Colombia, Argentina
- The conversion factor for units of traffic/bandwidth is 1,000. For example, 1 TB = 1,000 GB.
- A CSS service day is 00:00-23:59 (UTC+08:00).
- Because LEB uses channels with ultra-low latency, its traffic/bandwidth fees are slightly higher than those of LVB.
- LEB does not support live streams with B-frames. If a pushed stream contains B-frames, the system will remove them through transcoding, which will incur transcoding fees.
- Playback using a browser only supports the standard WebRTC protocol and does not support AAC. If a stream pushed contains audio in AAC format, the system will transcode the audio into Opus format, which will incur audio transcoding fees.
- **At 00:00 (UTC+08:00), January 4, 2022**, CSS adjusted the daily billing prices and pricing tiers of LEB’s basic services and started billing usage outside the Chinese mainland by region instead of at a unified price. For details, see [Notice: CSS to Adjust Prices of Basic Services](https://intl.cloud.tencent.com/document/product/267/43055).

>! 
>- By default, fees are billed based on downstream usage. However, upstream usage will also be billed if the ratio of downstream traffic to upstream traffic is smaller than 10:1 and the highest upstream bandwidth used in a day exceeds 100 Mbps.
>- The billing method, tiered pricing rules, and billing regions (inside/outside the Chinese mainland) for upstream traffic **are the same as** those for [LVB playback traffic](https://intl.cloud.tencent.com/document/product/267/2818). **Upstream traffic has been billed since 00:00 (UTC+08:00), July 1, 2021**.
>- Take the Asia Pacific 1 billing region for example. Assume that the total downstream and upstream traffic used in a day are 9 GB and 1 GB respectively, and the highest upstream bandwidth used is 101 Mbps. Because the ratio of downstream traffic to upstream traffic is 9:1, which is smaller than 10:1, and the peak upstream bandwidth usage is higher than 100 Mbps, the traffic fee would be:
Upstream traffic fees + Downstream traffic fees = 0.1496 (USD/GB/Day) x (9 (GB) + 1 (GB)) = 1.496 USD.



[](id:overseas)
## Acceleration Outside the Chinese Mainland

Traffic/Bandwidth usage outside the Chinese mainland is the downstream traffic/bandwidth used when users connect to Tencent Cloud’s acceleration origin servers outside the Chinese mainland. You can choose to be billed [by traffic](#overseas_flow) or [by bandwidth](#overseas_bandwidth). The former is used for new users by default.

>! LEB bill-by-traffic/bandwidth rules for regions outside the Chinese mainland took effect on April 20, 2021. Since April 21, 2021, all bills have been generated according to the new billing rules.

[](id:overseas_flow)
### Bill-by-traffic

#### Pricing
LEB traffic outside the Chinese mainland is billed by region on a daily basis, and is based on tiered pricing. See below for the pricing tiers:

<table>
<thead>
<tr>
<th rowspan=2>Traffic Tier</th>
<th colspan=8 style="text-align:center;">Price (USD/GB/Day)</th>
</tr>
<tr>
<th>Asia Pacific 1</th>
<th>Asia Pacific 2</th>
<th>Asia Pacific 3</th>
<th>North America</th>
<th>Europe</th>
<th>Middle East</th>
<th>Africa</th>
<th>South America</th>
</tr>
</thead>
<tbody>
<tr>
<td>0-2 TB</td>
<td>0.1496</td>
<td>0.2472</td>
<td>0.2276</td>
<td>0.1431</td>
<td>0.1431</td>
<td>0.3902</td>
<td>0.3902</td>
<td>0.3350</td>
</th>
<tr>
<td>2 TB (inclusive) - 50 TB</td>
<td>0.1398</td>
<td>0.2276</td>
<td>0.2081</td>
<td>0.1268</td>
<td>0.1268</td>
<td>0.3577</td>
<td>0.3577</td>
<td>0.3187</td>
</tr>
<tr>
<td>50 TB (inclusive) - 100 TB</td>
<td>0.1171</td>
<td>0.2114</td>
<td>0.1821</td>
<td>0.1008</td>
<td>0.1008</td>
<td>0.3350</td>
<td>0.3350</td>
<td>0.2927</td>
</tr>
<tr>
<td>100 TB (inclusive) - 1 PB</td>
<td>0.1008</td>
<td>0.1821</td>
<td>0.1626</td>
<td>0.0650</td>
<td>0.0650</td>
<td>0.3089</td>
<td>0.3089</td>
<td>0.2764</td>
</tr>
<tr>
<td>≥ 1 PB</td>
<td>0.0911</td>
<td>0.1691</td>
<td>0.1431</td>
<td>0.0520</td>
<td>0.0520</td>
<td>0.2764</td>
<td>0.2764</td>
<td>0.2602</td>
</tr>
</tbody></table>

#### Billing details
- Billable item: Downstream traffic consumed during LEB playback outside the Chinese mainland
- Billing rules: Fees are calculated by multiplying the total traffic consumed in a day in a billing region by the unit price of the corresponding tier.

#### Billing example
- Assume that the bitrate of a live streaming session was 500 Kbps (This is the sum of the audio bitrate and video bitrate. If you transcode the stream to a specific video bitrate, the sum of this video bitrate and the audio bitrate will be used for billing), and there were 100 concurrent viewers at the peak, the traffic consumed would be 500/8 x 3,600 x 100 = 22,500,000 KB = 22.5 GB.
- Assume that you used the LEB service on January 4, 2022 and consumed 22.5 GB of downstream traffic. On January 5, 2022, you would be charged:
  0.1496 (USD/GB) x 22.5 (GB) = 3.366 USD.
- By default, fees are billed based on downstream usage. However, upstream usage will also be billed if the ratio of downstream traffic to upstream traffic is smaller than 10:1 and the peak upstream bandwidth used in a day exceeds 100 Mbps. The billing mode, list prices, and tiered pricing rules for upstream usage are the same as those for LVB playback.

[](id:overseas_bandwidth)

### Bill-by-bandwidth
#### Pricing
We bill bandwidth usage outside the Chinese mainland by region on a daily basis and adopt a tiered pricing approach. You are charged for your peak bandwidth usage in a day. See below for the pricing tiers:

<table>
<thead>
<tr>
<th rowspan=2>Bandwidth Tier</th>
<th colspan=8 style="text-align:center;">Price (USD/Mbps/Day)</th>
</tr>
<tr>
<th>Asia Pacific 1</th>
<th>Asia Pacific 2</th>
<th>Asia Pacific 3</th>
<th>North America</th>
<th>Europe</th>
<th>Middle East</th>
<th>Africa</th>
<th>South America</th>
</tr>
</thead>
<tbody>
<tr>
<td>0-500 Mbps</td>
<td>0.4098</td>
<td>1.2033</td>
<td>1.2455</td>
<td>0.3967</td>
<td>0.3967</td>
<td>1.8667</td>
<td>1.8667</td>
<td>1.6911</td>
</tr>
<tr>
<td>500 Mbps (inclusive) - 5 Gbps</td>
<td>0.3707</td>
<td>1.0829</td>
<td>1.2098</td>
<td>0.3610</td>
<td>0.3610</td>
<td>1.8407</td>
<td>1.8407</td>
<td>1.6553</td>
</tr>
<tr>
<td>5 Gbps (inclusive) - 20 Gbps</td>
<td>0.3415</td>
<td>0.9659</td>
<td>1.1122</td>
<td>0.3363</td>
<td>0.3363</td>
<td>1.8016</td>
<td>1.8016</td>
<td>1.6130</td>
</tr>
<tr>
<td>≥ 20 Gbps</td>
<td>0.3252</td>
<td>0.8455</td>
<td>1.0081</td>
<td>0.3187</td>
<td>0.3187</td>
<td>1.7821</td>
<td>1.7821</td>
<td>1.5935</td>
</tr>
</tbody></table>

#### Billing details

- Billable item: Downstream bandwidth used during LEB playback outside the Chinese mainland
- Billing rules: Fees are calculated by multiplying the highest bandwidth used in a day in a billing region by the unit price of the corresponding tier.

#### Billing example
- Assume that the bitrate of a live streaming session was 500 Kbps (This is the sum of the audio bitrate and video bitrate. If you transcode the stream to a specific video bitrate, the sum of this video bitrate and the audio bitrate will be used for billing), and there were 100 concurrent viewers at the peak, the highest bandwidth used would be:
500 (Kbps) x 100 = 50,000 (Kbps) = 50 Mbps.
- Assume that you used the LEB service on January 4, 2022 for playback in Macao (China) and your bandwidth usage reached 50 Mbps at the highest. On January 5, 2022, you would be charged:
   0.4098 (USD/Mbps/Day) x 50 (Mbps) = 20.49 USD.
- By default, fees are billed based on downstream usage. However, upstream usage will also be billed if the ratio of downstream traffic to upstream traffic is smaller than 10:1 and the peak upstream bandwidth used in a day exceeds 100 Mbps. The billing mode, list prices, and tiered pricing rules for upstream usage are the same as those for LVB playback.

[](id:domestic)

## Traffic/Bandwidth Usage in the Chinese Mainland

LEB is a basic service of CSS and is billed based on the downstream traffic/bandwidth consumed during live streaming.
LEB provides two daily pay-as-you-go billing modes: [bill-by-traffic](#flow) and [bill-by-bandwidth](#bandwidth). You can choose whichever suits your needs. **The default mode for new users of LEB is bill-by-traffic.**

[](id:flow)

### Bill-by-traffic

#### Pricing

We bill LEB traffic on a daily basis and adopt a tiered pricing approach. See below for the pricing tiers:

| Traffic Tier | Price (USD/GB/Day) |
| ----------------- | ---------------- |
| 0-2 TB           | 0.0846           |
| 2 TB (inclusive) - 10 TB   | 0.0813           |
| 10 TB (inclusive) - 50 TB   | 0.0780                                  |
| 50 TB (inclusive) - 100 TB | 0.0715           |
| 100 TB (inclusive) - 1 PB | 0.0618           |
| ≥ 1 PB             | 0.0520           |

#### Billing details

- Billable item: Downstream traffic consumed during LEB playback in the Chinese mainland
- Billing rules: Fees are calculated by multiplying the total traffic consumed in a day by the unit price of the corresponding tier.

#### Billing example

- Assume that the bitrate of a live streaming session was 500 Kbps (This is the sum of the audio bitrate and video bitrate. If you transcode the stream to a specific video bitrate, the sum of this video bitrate and the audio bitrate will be used for billing), and there were 100 concurrent viewers at the peak, the traffic consumed would be 500/8 x 3,600 x 100 = 22,500,000 KB = 22.5 GB.
- Assume that you used the LEB service on January 4, 2022 and consumed 22.5 GB of downstream traffic. On January 5, 2022, you would be charged:
  0.0846 (USD/GB) x 22.5 (GB) = 1.9035 USD.
- By default, fees are billed based on downstream usage. However, upstream usage will also be billed if the ratio of downstream traffic to upstream traffic is smaller than 10:1 and the peak upstream bandwidth used in a day exceeds 100 Mbps. The billing mode, list prices, and tiered pricing rules for upstream usage are the same as those for LVB playback.

[](id:bandwidth)

### Bill-by-bandwidth

#### Pricing

We bill LEB bandwidth usage on a daily basis and adopt a tiered pricing approach. The fee is charged based on your peak bandwidth usage in a day. See below for the pricing tiers:

| Bandwidth Tier | Price (USD/Mbps/Day) |
| -------------------- | ------------------ |
| 0 - 500 Mbps          | 0.2114             |
| 500 Mbps (inclusive) - 5 Gbps | 0.2049             |
| 5 Gbps (inclusive) - 20 Gbps  | 0.1984             |
| ≥ 20 Gbps             | 0.1886             |

#### Billing details

- Billable item: Downstream bandwidth used during LEB playback in the Chinese mainland
- Billing rules: Fees are calculated by multiplying the highest bandwidth used in a day by the unit price of the corresponding tier.

#### Billing example

- Assume that the bitrate of a live streaming session was 500 Kbps (This is the sum of the audio bitrate and video bitrate. If you transcode the stream to a specific video bitrate, the sum of this video bitrate and the audio bitrate will be used for billing), and there were 100 concurrent viewers at the peak, the highest bandwidth used would be:
   500 Kbps x 100 = 50,000 Kbps = 50 Mbps.
- Assume that you used the LEB service on January 4, 2022 and your bandwidth usage reached 50 Mbps at the highest. On January 5, 2022, you would be charged:
   0.2114 (USD/Mbps/Day) x 50 (Mbps) = 10.57 USD.
- By default, fees are billed based on downstream usage. However, upstream usage will also be billed if the ratio of downstream traffic to upstream traffic is smaller than 10:1 and the peak upstream bandwidth used in a day exceeds 100 Mbps. The billing mode, list prices, and tiered pricing rules for upstream usage are the same as those for LVB playback.

>? If you have a large-scale live streaming business, then a daily billing mode may not meet your needs. Please [contact](https://intl.cloud.tencent.com/contact-us) the Tencent Cloud sales team or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for other billing options.

