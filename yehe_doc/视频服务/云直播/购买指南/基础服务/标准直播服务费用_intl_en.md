## Notes

- Billing mode: daily pay-as-you-go
- Billing cycle: daily billing cycle. Traffic fees generated in one day will be deducted the next day. See your billing statement for the actual bill generation time and amount.
- **The default mode for new users of LVB is bill-by-traffic.**
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
- **Starting from 00:00 (UTC+08:00), January 4, 2022**, CSS will adjust the daily billing prices and pricing tiers of LVB’s basic services and bill usage outside the Chinese mainland by region instead of at a unified price. For details, see [Notice: CSS to Adjust Prices of Basic Services](https://intl.cloud.tencent.com/document/product/267/43055).

>!
> - By default, fees are billed by downstream usage. However, upstream usage will also be billed when the ratio of upstream usage to downstream usage is larger than 1:10, and the daily upstream peak bandwidth exceeds 100 Mbps.
> - **The same billing method, tiered pricing rules, and billing regions (in/outside the Chinese mainland)** are used for live push and LVB playback. **Live push has been billed since 00:00 (UTC+08:00), July 1, 2021.**
> - Billing example:
>  **Use daily bill-by-traffic as an example.** Assume that the total upstream and downstream traffic used in a day are 10 GB and 90 GB respectively, and the highest upstream bandwidth used is 101 Mbps. As the ratio of upstream usage to downstream usage is 10:90, which is larger than 1:10, and the peak upstream bandwidth usage is higher than 100 Mbps, the traffic fee would be:
>  Upstream traffic fees + Downstream traffic fees = 0.0417 (USD/GB/Day) × (10 (GB) + 90 (GB)) = 4.17 USD.


[](id:overseas_speed)

## Acceleration Outside Chinese Mainland

Traffic/Bandwidth usage outside the Chinese mainland is the downstream traffic/bandwidth used when users connect to Tencent Cloud’s acceleration origin servers outside the Chinese mainland. You can choose to be billed [by traffic](#overseas_flow) or [by bandwidth](#overseas_bandwidth). The former is used for new users by default.
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


#### Details
- Billable item: downstream traffic generated during LVB playback outside the Chinese mainland
- Billing rules: Fees are calculated by multiplying the total traffic generated in a day in a billing region by the unit price of the corresponding tier.

#### Billing example
- Assume that you use the LVB service on January 4, 2022 and generate 1 TB of downstream traffic in Hong Kong (China) and 6 TB of downstream traffic in Russia. On January 5, 2022, you will be charged:
0.0748 (USD/GB) × 1000 (GB) + 0.0634 (USD/GB) × 6000 (GB) = 445.2 USD.

- By default, fees are billed by downstream usage. However, upstream usage will also be billed when the ratio of upstream usage to downstream usage is larger than 1:10 and the daily upstream peak bandwidth exceeds 100 Mbps. Upstream usage is billed according to the same billing modes and tiered pricing rules as downstream usage.

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


#### Details
- Billable item: downstream bandwidth used during LVB playback outside the Chinese mainland
- Billing rules: Fees are calculated by multiplying the highest bandwidth used in a day in a billing region by the unit price of the corresponding tier.

#### Billing example

- Assume that you use the LVB service on January 4, 2022 for playback in Macao (China) and your bandwidth usage reaches 600 Mbps at the highest. On January 5, 2022, you will be charged:
0.1854 (USD/Mbps) × 600 (Mbps) = 111.24 USD.
- By default, fees are billed by downstream usage. However, upstream usage will also be billed when the ratio of upstream usage to downstream usage is larger than 1:10 and the daily upstream peak bandwidth exceeds 100 Mbps. Upstream usage is billed according to the same billing modes and tiered pricing rules as downstream usage.

[](id:domestic)

## Traffic/Bandwidth Usage in Chinese Mainland

The LVB service is billed by the downstream traffic/bandwidth used during live streaming. LVB provides two daily pay-as-you-go billing modes: [bill-by-traffic](#flow) and [bill-by-bandwidth](#bandwidth). You can choose whichever suits your needs.

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

#### Details

- Billable item: downstream traffic generated during LVB playback in the Chinese mainland
- Billing rules: Fees are calculated by multiplying the total traffic generated in a day by the unit price of the corresponding tier.
- Calculation formula:
  - Consumed traffic = Bitrate/8 × Total watch duration. 

>?Total watch duration = Daily average number of online viewers × Average watch duration per viewer. That is to say, the total watch duration is the same if 1 viewer watches for 60 minutes and 60 viewers watch for 1 minute each.

  - Traffic fees = Consumed traffic × Unit price of the corresponding tier

#### Billing example

- Assume that an LVB session lasts for 2 hours at a bitrate of 1 Mbps, which is the sum of the audio bitrate and the video bitrate. If you enable transcoding and specify a video bitrate, the sum of the audio bitrate and the specified video bitrate will be used for billing. If 100 viewers watch for 1 hour each and 50 viewers watch for 2 hours each, the consumed traffic will be:
  1 (Mbps)/8 × 7,200 (s) × 50 (Viewers) + 1 (Mbps)/8 × 3,600 (s) × 100 (Viewers) = 90,000 (MB) = 90 GB.
- Assume that you use the LVB service on January 4, 2022 and generate 90 GB of downstream traffic. On January 5, 2022, you will be charged:
  0.0423 (USD/GB) × 90 (GB) = 3.807 USD.
- By default, fees are billed by downstream usage. However, upstream usage will also be billed when the ratio of upstream usage to downstream usage is larger than 1:10 and the daily upstream peak bandwidth exceeds 100 Mbps. Upstream usage is billed according to the same billing modes and tiered pricing rules as downstream usage.
  <span id="bandwidth"></span>

### Bill-by-bandwidth

#### Pricing

We bill LVB bandwidth usage on a daily basis and adopt a tiered pricing approach. You are charged for your peak bandwidth usage in a day. See below for the pricing tiers:

| Bandwidth Tier | Price (USD/Mbps/Day) |
| -------------------- | ------------------ |
| 0-500 Mbps          | 0.1057             |
| 500 Mbps (inclusive) - 5 Gbps | 0.1024             |
| 5 Gbps (inclusive) - 20 Gbps  | 0.0992             |
| ≥ 20 Gbps             | 0.0943             |

#### Details

- Billable item: downstream bandwidth used during LVB playback in the Chinese mainland
- Billing rules: Fees are calculated by multiplying the highest bandwidth used in a day by the unit price of the corresponding tier.

#### Billing example

- Assume that an LVB session lasts for 1 hour at a bitrate of 500 Kbps, which is the sum of the audio bitrate and the video bitrate. If you enable transcoding and specify a video bitrate, the sum of the audio bitrate and the specified video bitrate will be used for billing. If the session is watched by 100 viewers, the consumed bandwidth will be:
  500 (Kbps) × 100 = 50,000 (Kbps) = 50 Mbps.
- Assume that you use the LVB service on January 4, 2022 and your bandwidth usage reaches 50 Mbps at the highest. On January 5, 2022, you will be charged:
  0.1057 (USD/Mbps/Day) × 50 (Mbps) = 5.285 USD.
- By default, fees are billed by downstream usage. However, upstream usage will also be billed when the ratio of upstream usage to downstream usage is larger than 1:10 and the daily upstream peak bandwidth exceeds 100 Mbps. Upstream usage is billed according to the same billing modes and tiered pricing rules as downstream usage.

>? If you have a large-scale live streaming business and its consumption of Tencent Cloud resources has exceeded or is expected to exceed 10,000 USD, then a daily billing mode may not meet your needs. Please [contact](https://intl.cloud.tencent.com/contact-us) the Tencent Cloud sales team or [submit a ticket](https://console.cloud.tencent.com/workorder/category) to determine the best billing option for you.

