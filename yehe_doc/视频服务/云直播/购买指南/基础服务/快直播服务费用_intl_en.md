## Notes

- Billing mode: **daily pay-as-you-go**
- Billing cycle: daily billing cycle. Traffic fees generated in one day will be deducted the next day. See your billing statement for the actual bill generation time and amount.
- Billing regions outside the Chinese mainland:
  - Asia Pacific 1: Hong Kong (China), Singapore, Macao (China), Vietnam, Thailand, Nepal, Cambodia
  - Asia Pacific 2: Taiwan (China), Japan, Malaysia, Indonesia, South Korea
  - Asia Pacific 3: Philippines, India, Australia
  - North America: United States, Canada, Mexico
  - Europe: Netherlands, Germany, Russia, United Kingdom, Ireland, Italy, Spain, France
  - Middle East: United Arab Emirates, Turkey, Qatar, Saudi Arabia, Bahrain
  - Africa: South Africa
  - South America: Brazil, Colombia
- The conversion factor for units of traffic/bandwidth is 1,000. For example, 1 TB = 1,000 GB.
- A CSS service day is 00:00-23:59 (UTC+08:00).
- As LEB uses channels with ultra-low latency, its traffic/bandwidth fees are a bit higher than those of LVB.
- LEB does not support playing back live streams with B-frames. If the pushed stream contains B-frames, the system will remove them by transcoding, which will incur transcoding fees.
- Pull by web browser only supports the standard WebRTC protocol and does not support the AAC audio codec. To push streams with audios in AAC format, the audios will be transcoded into Opus format, which will incur audio transcoding fees.
- **Starting from 00:00 (UTC+08:00), January 4, 2022**, CSS will adjust the daily billing prices and pricing tiers of LEB’s basic services and bill usage outside the Chinese mainland by region instead of at a unified price. For details, see [Notice: CSS to Adjust Prices of Basic Services](https://intl.cloud.tencent.com/document/product/267/43055).

>! 
>- By default, fees are billed by downstream usage. However, upstream usage will also be billed when the ratio of upstream usage to downstream usage is larger than 1:10, and the daily upstream peak bandwidth exceeds 100 Mbps.
>- **The same billing method, tiered pricing rules, and billing regions (in/outside the Chinese mainland)** are used for live push and [LVB playback](https://intl.cloud.tencent.com/document/product/267/2818). **Live push has been billed since 00:00 (UTC+08:00), July 1, 2021**.
>- Billing example:
Use daily bill-by-traffic as an example. Assume that the total upstream and downstream traffic used in a day are 10 GB and 90 GB respectively, and the highest upstream bandwidth used is 101 Mbps. As the ratio of upstream usage to downstream usage is 10:90, which is larger than 1:10, and the peak upstream bandwidth usage is higher than 100 Mbps, the traffic fee would be:
Upstream traffic fees + Downstream traffic fees = 0.0417 (USD/GB/Day) × (10 (GB) + 90 (GB)) = 4.17 USD.



[](id:overseas)
## Acceleration Outside Chinese Mainland

Traffic/Bandwidth usage outside the Chinese mainland is the downstream traffic/bandwidth used when users connect to Tencent Cloud’s acceleration origin servers outside the Chinese mainland. You can choose to be billed [by traffic](#overseas_flow) or [by bandwidth](#overseas_bandwidth). The former is used for new users by default.

>! LEB bill-by-traffic/bandwidth rules for regions outside the Chinese mainland took effect on April 20, 2021. Since April 21, 2021, all bills have been generated according to the new billing rules.

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


#### Details
- Billable item: downstream traffic generated during LEB playback outside the Chinese mainland
- Billing rules: Fees are calculated by multiplying the total traffic generated in a day in a billing region by the unit price of the corresponding tier.

#### Billing example
- Assume that an LEB session lasts for 1 hour at a bitrate of 500 Kbps, which is the sum of the audio bitrate and the video bitrate. If you enable transcoding and specify a video bitrate, the sum of the audio bitrate and the specified video bitrate will be used for billing. If the session is watched by 100 viewers, the consumed bandwidth will be: 500/8 × 3600 × 100 = 22,500,000 KB = 22.5 GB.
- Assume that you use the LEB service on January 4, 2022 and generate 22.5 GB of downstream traffic. On January 5, 2022, you will be charged:
  0.1496 (USD/GB) × 22.5 (GB) = 3.366 USD.
- By default, fees are billed by downstream usage. However, upstream usage will also be billed when the ratio of upstream usage to downstream usage is larger than 1:10, and the daily upstream peak bandwidth exceeds 100 Mbps. Upstream usage is billed according to the same billing modes and tiered pricing rules as LVB downstream usage.

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


#### Details
- Billable item: downstream bandwidth used during LEB playback outside the Chinese mainland
- Billing rules: Fees are calculated by multiplying the highest bandwidth used in a day in a billing region by the unit price of the corresponding tier.

#### Billing example
- Assume that an LEB session lasts for 1 hour at a bitrate of 500 Kbps, which is the sum of the audio bitrate and the video bitrate. If you enable transcoding and specify a video bitrate, the sum of the audio bitrate and the specified video bitrate will be used for billing. If the session is watched by 100 viewers, the consumed bandwidth will be:
   500 Kbps × 100 = 50,000 Kbps = 50 Mbps.
- Assume that you use the LEB service on January 4, 2022 for playback in Macao (China) and your bandwidth usage reaches 50 Mbps at the highest. On January 5, 2022, you will be charged:
   0.4098 (USD/Mbps/Day) × 50 (Mbps) = 20.49 USD.
-  By default, fees are billed by downstream usage. However, upstream usage will also be billed when the ratio of upstream usage to downstream usage is larger than 1:10, and the daily upstream peak bandwidth exceeds 100 Mbps. Upstream usage is billed according to the same billing modes and tiered pricing rules as LVB downstream usage.

[](id:domestic)

## Traffic/Bandwidth Usage in Chinese Mainland

The LEB service is billed by the downstream traffic/bandwidth used during live streaming.
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

#### Details

- Billable item: downstream traffic generated during LEB playback in the Chinese mainland
- Billing rules: Fees are calculated by multiplying the total traffic generated in a day by the unit price of the corresponding tier.

#### Billing example

- Assume that an LEB session lasts for 1 hour at a bitrate of 500 Kbps, which is the sum of the audio bitrate and the video bitrate. If you enable transcoding and specify a video bitrate, the sum of the audio bitrate and the specified video bitrate will be used for billing. If the session is watched by 100 viewers, the consumed bandwidth will be: 500/8 × 3600 × 100 = 22,500,000 KB = 22.5 GB.
- Assume that you use the LEB service on January 4, 2022 and generate 22.5 GB of downstream traffic. On January 5, 2022, you will be charged:
  0.0846 (USD/GB) × 22.5 (GB) = 1.9035 USD.
- By default, fees are billed by downstream usage. However, upstream usage will also be billed when the ratio of upstream usage to downstream usage is larger than 1:10, and the daily upstream peak bandwidth exceeds 100 Mbps. Upstream usage is billed according to the same billing modes and tiered pricing rules as LVB downstream usage.

[](id:bandwidth)

### Bill-by-bandwidth

#### Pricing

We bill LEB bandwidth usage on a daily basis and adopt a tiered pricing approach. You are charged for your peak bandwidth usage in a day. See below for the pricing tiers:

| Bandwidth Tier | Price (USD/Mbps/Day) |
| -------------------- | ------------------ |
| 0 - 500 Mbps          | 0.2114             |
| 500 Mbps (inclusive) - 5 Gbps | 0.2049             |
| 5 Gbps (inclusive) - 20 Gbps  | 0.1984             |
| ≥ 20 Gbps             | 0.1886             |

#### Details

- Billable item: downstream bandwidth used during LEB playback in the Chinese mainland
- Billing rules: Fees are calculated by multiplying the highest bandwidth used in a day by the unit price of the corresponding tier.

#### Billing example

- Assume that an LEB session lasts for 1 hour at a bitrate of 500 Kbps, which is the sum of the audio bitrate and the video bitrate. If you enable transcoding and specify a video bitrate, the sum of the audio bitrate and the specified video bitrate will be used for billing. If the session is watched by 100 viewers, the consumed bandwidth will be:
   500 Kbps × 100 = 50,000 Kbps = 50 Mbps.
- Assume that you use the LEB service on January 4, 2022 and your bandwidth usage reaches 50 Mbps at the highest. On January 5, 2022, you will be charged:
   0.2114 (USD/Mbps/Day) × 50 (Mbps) = 10.57 USD.
-  By default, fees are billed by downstream usage. However, upstream usage will also be billed when the ratio of upstream usage to downstream usage is larger than 1:10, and the daily upstream peak bandwidth exceeds 100 Mbps. Upstream usage is billed according to the same billing modes and tiered pricing rules as LVB downstream usage.

>? If you have a large-scale live streaming business, then a daily billing mode may not meet your needs. Please [contact](https://intl.cloud.tencent.com/contact-us) the Tencent Cloud sales team or [submit a ticket](https://console.cloud.tencent.com/workorder/category) to determine the best billing option for you.

