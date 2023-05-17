## Overview

- Billing mode: Daily pay-as-you-go
- Billing cycle: Daily billing cycle. Traffic fees generated each day are deducted the following day. For the actual fee deduction and bill generation time, see your billing statement.
- **The default mode for new users of LVB is bill-by-traffic.**
- We offer **prepaid traffic packages**. A traffic package deducts LVB downstream traffic in the Chinese mainland at a ratio of 1:1. Different deduction ratios are applied to **LVB downstream traffic outside the Chinese mainland, LEB downstream traffic in the Chinese mainland, LEB downstream traffic outside the Chinese mainland, and upstream traffic inside and outside the Chinese mainland**. For details, see [Prepaid Packages](https://www.tencentcloud.com/document/product/267/52220).
- Billing regions outside the Chinese mainland:
  - Asia Pacific 1: Hong Kong (China), Singapore, Macao (China), Vietnam, Thailand, Nepal, Cambodia, Pakistan, Laos
  - Asia Pacific 2: Taiwan (China), Japan, Malaysia, Indonesia, South Korea
  - Asia Pacific 3: Philippines, India, Australia
  - North America: United States, Canada, Mexico
  - Europe: Netherlands, Germany, Russia, United Kingdom, Ireland, Italy, Spain, France
  - Middle East: United Arab Emirates, Türkiye, Qatar, Saudi Arabia, Bahrain, Iraq, Oman
  - Africa: South Africa, Egypt
  - South America: Brazil, Colombia, Argentina, Chile
- The conversion factor for units of traffic/bandwidth is 1,000. For example, 1 TB = 1,000 GB.
- A CSS service day is 00:00-23:59 (UTC+08:00).
- **At 00:00 (UTC+08:00), January 4, 2022**, CSS adjusted the daily billing prices and pricing tiers of LVB’s basic services and started billing usage outside the Chinese mainland by region instead of at a unified price. For details, see [Notice: CSS to Adjust Prices of Basic Services](https://www.tencentcloud.com/document/product/267/43055).

>!
>- By default, fees are billed based on downstream usage. However, upstream usage will also be billed if the ratio of downstream traffic to upstream traffic is smaller than 10:1 and the highest upstream bandwidth used in a day exceeds 100 Mbps.
>- The billing method, tiered pricing rules, and billing regions for upstream traffic inside/outside the Chinese mainland are **the same as** those for LVB downstream traffic. **Upstream traffic became a billable item starting at 00:00 (UTC+08:00), July 1, 2021.**
>- For example: <br/>Suppose you consumed 9 GB of downstream traffic and 1 GB of upstream traffic in **Asia Pacific 1** one day, and the peak bandwidth on that day was 101 Mbps. Because the ratio of downstream traffic to upstream traffic is 9:1, which is smaller than 10:1, and the peak upstream bandwidth usage is higher than 100 Mbps, the following traffic fee would be billed:<br/>
Upstream traffic fees + Downstream traffic fees = 0.0748 (USD/GB) x (9 GB + 1 GB) = 0.748 USD.


[](id:overseas_speed)
## Acceleration Outside the Chinese Mainland

Traffic/Bandwidth usage outside the Chinese mainland is the downstream traffic/bandwidth used when users connect to Tencent Cloud’s acceleration servers outside the Chinese mainland. You can choose to be billed [by traffic](#overseas_flow) or [by bandwidth](#overseas_bandwidth). By default, new users are billed by traffic.
[](id:overseas_flow)

### Bill-by-traffic

#### Pricing

We bill traffic outside the Chinese mainland by region on a daily basis and adopt a tiered pricing approach. See below for the pricing tiers:

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
<td>0.0748</td>
<td>0.1236</td>
<td>0.1138</td>
<td>0.0715</td>
<td>0.0715</td>
<td>0.1951</td>
<td>0.1951</td>
<td>0.1675</td>
</th>
<tr>
<td>2 TB (inclusive) - 50 TB</td>
<td>0.0699</td>
<td>0.1138</td>
<td>0.1041</td>
<td>0.0634</td>
<td>0.0634</td>
<td>0.1789</td>
<td>0.1789</td>
<td>0.1593</td>
</tr>
<tr>
<td>50 TB (inclusive) - 100 TB</td>
<td>0.0585</td>
<td>0.1057</td>
<td>0.0911</td>
<td>0.0504</td>
<td>0.0504</td>
<td>0.1675</td>
<td>0.1675</td>
<td>0.1463</td>
</tr>
<tr>
<td>100 TB (inclusive) - 1 PB</td>
<td>0.0504</td>
<td>0.0911</td>
<td>0.0813</td>
<td>0.0325</td>
<td>0.0325</td>
<td>0.1545</td>
<td>0.1545</td>
<td>0.1382</td>
</tr>
<tr>
<td>≥ 1 PB</td>
<td>0.0455</td>
<td>0.0846</td>
<td>0.0715</td>
<td>0.0260</td>
<td>0.0260</td>
<td>0.1382</td>
<td>0.1382</td>
<td>0.1301</td>
</tr>
</tbody></table>

#### Billing details
- Billable item: Downstream traffic generated during LVB playback outside the Chinese mainland
- Billing rules: Fees are calculated by multiplying the total traffic consumed in a day in a billing region by the unit price of the corresponding tier.

#### Billing example
- Assume that you used the LVB service on January 4, 2022 and consumed 1 TB of downstream traffic in Hong Kong (China) and 6 TB of downstream traffic in Russia. On January 5, 2022, the following traffic fee would be billed:
0.0748 (USD/GB) x 1000 (GB) + 0.0634 (USD/GB) x 6000 (GB) = 445.2 USD.
- By default, fees are billed based on downstream usage. However, upstream usage will also be billed if the ratio of downstream traffic to upstream traffic is smaller than 10:1 and the peak upstream bandwidth used in a day exceeds 100 Mbps. The billing mode, list prices, and tiered pricing rules for upstream usage are the same as those for downstream usage.

[](id:overseas_bandwidth)
### Bill-by-bandwidth
#### Pricing
We bill bandwidth usage outside the Chinese mainland by region on a daily basis and adopt a tiered pricing approach. The fee is based on your peak bandwidth usage in a day. See below for the pricing tiers:

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
<td>0.2049</td>
<td>0.6016</td>
<td>0.6228</td>
<td>0.1984</td>
<td>0.1984</td>
<td>0.9333</td>
<td>0.9333</td>
<td>0.8455</td>
</tr>
<tr>
<td>500 Mbps (inclusive) - 5 Gbps</td>
<td>0.1854</td>
<td>0.5415</td>
<td>0.6049</td>
<td>0.1805</td>
<td>0.1805</td>
<td>0.9203</td>
<td>0.9203</td>
<td>0.8276</td>
</tr>
<tr>
<td>5 Gbps (inclusive) - 20 Gbps</td>
<td>0.1707</td>
<td>0.4829</td>
<td>0.5561</td>
<td>0.1681</td>
<td>0.1681</td>
<td>0.9008</td>
<td>0.9008</td>
<td>0.8065</td>
</tr>
<tr>
<td>≥ 20 Gbps</td>
<td>0.1626</td>
<td>0.4228</td>
<td>0.5041</td>
<td>0.1593</td>
<td>0.1593</td>
<td>0.8911</td>
<td>0.8911</td>
<td>0.7967</td>
</tr>
</tbody></table>

#### Billing details
- Billable item: Downstream bandwidth used during LVB playback outside the Chinese mainland
- Billing rules: Fees are calculated by multiplying the highest bandwidth used in a day in a billing region by the unit price of the corresponding tier.

#### Billing example
- Assume that you used the LVB service on January 4, 2022 for playback in Macao (China) and your bandwidth usage reached 600 Mbps at the highest. On January 5, 2022, the following bandwidth fee would be billed:
0.1854 (USD/Mbps) x 600 (Mbps) = 111.24 USD.
- By default, fees are billed based on downstream usage. However, upstream usage will also be billed if the ratio of downstream traffic to upstream traffic is smaller than 10:1 and the peak upstream bandwidth used in a day exceeds 100 Mbps. The billing mode, list prices, and tiered pricing rules for upstream usage are the same as those for downstream usage.

[](id:domestic)

## Traffic/Bandwidth Usage in the Chinese Mainland

LVB is a basic service of CSS and is billed based on the downstream traffic/bandwidth consumed during live streaming. LVB provides two daily pay-as-you-go billing modes: [bill-by-traffic](#flow) and [bill-by-bandwidth](#bandwidth). You can choose whichever suits your needs.

[](id:flow)

### Bill-by-traffic

#### Pricing

We bill LVB traffic on a daily basis and adopt a tiered pricing approach. See below for the pricing tiers:

| Traffic Tier | Price (USD/GB/Day) |
| ----------------- | ---------------- |
| 0-2 TB           | 0.0423           |
| 2 TB (inclusive) - 10 TB   | 0.0407           |
| 10 TB (inclusive) - 50 TB   | 0.0390                                  |
| 50 TB (inclusive) - 100 TB | 0.0358           |
| 100 TB (inclusive) - 1 PB | 0.0309                                                |
| ≥ 1 PB             | 0.0260           |

#### Billing details

- Billable item: Downstream traffic consumed during LVB playback in the Chinese mainland
- Billing rules: Fees are calculated by multiplying the total traffic consumed in a day by the unit price of the corresponding tier.
- Calculation formula:
  - Consumed traffic = Bitrate/8 x Total playback duration. 

>? Total playback duration = Daily number of online viewers x Average playback duration per viewer. That is to say, the total playback duration is the same if 1 viewer watches for 60 minutes and 60 viewers watch for 1 minute each.

  - Traffic fees = Consumed traffic x Unit price of the corresponding tier

#### Billing example

- Assume that a live streaming session lasted for 2 hours and the bitrate was 1 Mbps (This is the sum of the audio bitrate and video bitrate. If you transcode the stream to a specific video bitrate, the sum of this video bitrate and the audio bitrate will be used for billing). If 100 viewers watched the live stream for 1 hour each and 50 viewers watched it for 2 hours each, the consumed traffic would be:
  1 (Mbps)/8 x 7,200 (s) x 50 (Viewers) + 1 (Mbps)/8 x 3,600 (s) x 100 (Viewers) = 90,000 (MB) = 90 GB.
- Assume that you used the LVB service on January 4, 2022 and consumed 90 GB of downstream traffic. On January 5, 2022, the following traffic fee would be billed:
  0.0423 (USD/GB) x 90 (GB) = 3.807 USD.
- By default, fees are billed based on downstream usage. However, upstream usage will also be billed if the ratio of downstream traffic to upstream traffic is smaller than 10:1 and the peak upstream bandwidth used in a day exceeds 100 Mbps. The billing mode, list prices, and tiered pricing rules for upstream usage are the same as those for downstream usage.
  <span id="bandwidth"></span>

### Bill-by-bandwidth

#### Pricing

We bill LVB bandwidth usage on a daily basis and adopt a tiered pricing approach. The fee is based on your peak bandwidth usage in a day. See below for the pricing tiers:

| Bandwidth Tier | Price (USD/Mbps/Day) |
| -------------------- | ------------------ |
| 0-500 Mbps          | 0.1057             |
| 500 Mbps (inclusive) - 5 Gbps | 0.1024             |
| 5 Gbps (inclusive) - 20 Gbps  | 0.0992             |
| ≥ 20 Gbps             | 0.0943             |

#### Billing details

- Billable item: Downstream bandwidth used during LVB playback in the Chinese mainland
- Billing rules: Fees are calculated by multiplying the highest bandwidth used in a day by the unit price of the corresponding tier.

#### Billing example

- Assume that the bitrate of a live streaming session was 500 Kbps (This is the sum of the audio bitrate and video bitrate. If you transcode the stream to a specific video bitrate, the sum of this video bitrate and the audio bitrate will be used for billing), and there were 100 concurrent viewers at the peak, the highest bandwidth used would be:
  500 (Kbps) x 100 = 50,000 (Kbps) = 50 Mbps.
- Assume that you used the LVB service on January 4, 2022 and your bandwidth usage reached 50 Mbps at the highest. On January 5, 2022, the following bandwidth fee would be billed:
  0.1057 (USD/Mbps/Day) x 50 (Mbps) = 5.285 USD.
- By default, fees are billed based on downstream usage. However, upstream usage will also be billed if the ratio of downstream traffic to upstream traffic is smaller than 10:1 and the peak upstream bandwidth used in a day exceeds 100 Mbps. The billing mode, list prices, and tiered pricing rules for upstream usage are the same as those for downstream usage.

>? If you have a large-scale live streaming business and your spending on Tencent Cloud resources has exceeded or is expected to exceed 10,000 USD, then a daily billing mode may not meet your needs. Please [contact](https://www.tencentcloud.com/contact-us) the Tencent Cloud sales team or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for other billing options.

