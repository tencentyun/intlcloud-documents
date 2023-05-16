This document describes the billing and pricing of connection, dedicated tunnel and direct connect gateway.

## Billing Details
**Tencent Cloud Direct Connect is billed on the basis of connection, dedicated tunnel, and direct connect gateway.**

>?
>- The bandwidth units are 1000-based, which means 1 Tbps is equal to 1,000 Gbps and 1 Gbps is equal to 1,000 Mbps.
>- The traffic units are 1024-based, which means 1 TB is equal to 1,024 GB and 1 GB is equal to 1,024 MB.
>
The figure below specifies the fees:
![](https://main.qcloudimg.com/raw/810dbbd6163c5f19a2d98eac91e0556b.png)

### Connections
A connection is the connection between your local IDC and the Tencent Cloud Direct Connect access point. You need to pay both Tencent Cloud billable items and non-Tencent Cloud billable items.
- **Tencent Cloud billable items**
  - You need to pay the monthly resource occupation fee for a dedicated access port.
  - You do not need to pay the resource occupation fee for a shared access port by partners.
- **Non-Tencent Cloud billable items**
  - Leased-line fee: you should pay your ISP for the leased line between your local IDC and the Tencent Cloud Direct Connect access point.
  - In-house wiring (IHW) rental fee: Direct Connect access points are generally deployed in neutral IDCs. Therefore, fiber-to-the-building (FTTB) or IHW rental fee may incur. For more information, consult your property operator or wiring provider.

### Dedicated tunnels
A dedicated tunnel is the Tencent Cloud private network connection between the Direct Connect access point and the Tencent Cloud direct connect gateway.
- If the Direct Connect access point and direct connect gateway are deployed in the same region, a free tier of 10 Gbps will be provided. If you require a higher bandwidth, contact your Tencent Cloud sales rep.
- If the Direct Connect access point and direct connect gateway are deployed in different regions, cross-region communication over the private network will be charged for dedicated tunnels, and no free tier will be provided.
>?
>- Tencent Cloud has discontinued the Direct Connect - Cross-Region Dedicated Tunnel Service from December 31, 2022. For more information, see [Migration of Direct Connect Cross-Region Tunnel Service to CCN](https://www.tencentcloud.com/document/product/216/50215). If you need cross-region tunnels, use Cloud Connect Network (CCN).
>- If you are an existing user of the Direct Connect - Cross-Region Dedicated Tunnel Service, migrate your cross-region dedicated tunnels to CCN as instructed in [Migrating Cross-Region Dedicated Tunnel to CCN](https://www.tencentcloud.com/document/product/216/47706).
>
- For a shared dedicated tunnel created using a partner's connection, the resource occupation fee for shared dedicated tunnel will be charged based on the specifications. For more information, see [Shared dedicated tunnel fee](#gxxvlan).

### Direct connect gateways
A direct connect gateway is your gateway object in Tencent Cloud, and the traffic fee will be billed.
- Inbound traffic fee: traffic from your local IDC to a Tencent Cloud IDC over Direct Connect is free of charge.
- Outbound traffic fee: traffic from a Tencent Cloud IDC to your local IDC over Direct Connect is charged based on actual traffic usage. For detailed pricing, see [Direct connect gateway traffic fee](#zxwgllf).

## Pricing Description
Direct Connect is billed as follows.
![](https://main.qcloudimg.com/raw/4c62cd77dd8aef1097bba22958055f47.png)

### Dedicated access port fee
- **Resource occupation fee for dedicated access port**: monthly pay-as-you-go. The fee incurred in the current month will be charged from your account between 8 and 10 AM on the first day of the next month.
- **Billing time**: the billing starts on the day when the connection goes to **Running** status, and stops when the connection is deleted on the Direct Connect console. The connection used less than one month will be billed on the basis of valid days.
- **Billing formula**: Total fee = (Number of valid days in the month/Number of calendar days in the month) × Monthly price for the port.
<table>
<tr><th>Billable Item</th><th>Specification</th><th>Price (USD/month)</th></tr>
<tr><td rowspan=3>Resource occupation fee (Mainland China)</td><td>1 GbE or below </td><td>92</td></tr>
<tr><td>10 GbE<td>769 </td></tr>
<tr><td>100 GbE</td><td>5385 </td></tr>
<tr><td rowspan=3>Resource occupation fee (outside the Chinese mainland)</td><td>1GE or below</td><td>231 </td></tr>
<tr><td>10 GbE<td>1692</td></tr>
<tr><td>100 GbE</td><td>12308</td></tr>
</table>



[](id:zxwgllf)
### Direct connect gateway traffic fee
- **Billing description**: the direct connect gateway will be charged starting from December 1, 2020. The inbound traffic is free of charge, while the outbound traffic billing will be accurate to MB at the price as shown below. The outbound traffic less than 1 MB will not be charged.
-**Billing object**: the total outbound traffic of all direct connect gateways under a Tencent Cloud account.
- **Billing mode**: monthly pay-as-you-go. The fee incurred in the current month will be charged from your account between 8 and 10 AM on the first day of the next month.
- **Billing formula**: Total fee = Total outbound traffic of all direct connect gateways × Unit price.
>! A new region-based pricing plan will be introduced on June 1, 2023 for the outbound traffic of direct connect gateways. For more information, see [Discontinuing the Free Tier of Outbound Traffic and Introducing a New Pricing Plan](https://www.tencentcloud.com/document/product/216/51076).
>
<table>
<tr>
<th rowspan="2" width="18%">Billable Item</th>
<th rowspan="2" width="52%" colspan="2">Total Outbound Traffic</th>
<th style="text-align:center;" colspan="2">Price (USD/GB)</th>
</tr>
<tr>
<th>Starting from June 1, 2023</th>
<th>Before June 1, 2023</th>
</tr>
<tr>
<td>Inbound traffic</td>
<td colspan="2">-</td>
<td>Free of charge</td>
<td>Free of charge</td>
</tr>
<tr>
<td rowspan="6">Outbound traffic</td>
<td colspan="2">Chinese mainland</td>
<td>0.015</td>
<td rowspan="6">0.015</td>
</tr>
<tr>
<td rowspan="2">Asia</td>
<td>Taiwan (China), Hong Kong (China), Tokyo, Singapore, Seoul, Bangkok</td>
<td>0.037 </td>
</tr>
<tr>
<td>Mumbai</td>
<td>0.041</td>
</tr>
<tr>
<td>Jakarta</td>
<td>0.074 </td>
</tr>
<tr>
<td rowspan="44">Europe and America</td>
<td>Frankfurt, Virginia, Silicon Valley, Toronto
</td>
<td>0.018</td>
</tr>
<tr>
<td>São Paulo</td>
<td>0.037</td>
</tr>
</table>




### Cross-region dedicated tunnel bandwidth resource fee
>?
>- Tencent Cloud has discontinued the Direct Connect - Cross-Region Dedicated Tunnel Service from December 31, 2022. For more information, see [Migration of Direct Connect Cross-Region Tunnel Service to CCN](https://www.tencentcloud.com/document/product/216/50215). If you need cross-region tunnels, use CCN.
>- If you are an existing user of the Direct Connect - Cross-Region Dedicated Tunnel Service, migrate your cross-region dedicated tunnels to CCN as instructed in [Migrating Cross-Region Dedicated Tunnel to CCN](https://www.tencentcloud.com/document/product/216/47706).
>

#### Monthly 95th percentile billing
Monthly dedicated tunnel fee = number of valid days in the month / number of calendar days in the month * 95th percentile of the monthly peak bandwidth * tiered unit price.
- **5-minute bandwidth value**
 The system collects the higher value of the inbound and outbound bandwidth on the devices every minute, and calculates the average in the last five minutes once every five minutes. The average is recorded as the 5-minute bandwidth value.
- **Valid day**
 A valid day is a day in which at least one 5-minute bandwidth value is greater than 3 Kbps.
- **Proportion of valid days**
Proportion of valid days = number of valid days in the month / number of calendar days in the month
- **95th percentile of the monthly peak bandwidth**
 In a calendar month, the 5-minute bandwidth values on all valid days are sorted in ascending order, and the top 5% are removed. The highest value of the remaining sample points is used as the 95th percentile of the monthly peak bandwidth.
- **Tiered unit price**
 Non-accumulative tiered pricing.

#### Tiered unit prices for 95th percentile of the monthly peak bandwidth
In Chinese mainland, the **pay-as-you-go** billing mode applies at the price as shown below.
<table>
<tr>
<th>Specification (Mbps)</th>
<th>Monthly Price (USD/Mbps)</th>
</tr>
<tr>
<td> [0, 10)</td>
<td>85</td>
</tr>
<tr>
<td>[10, 20)</td>
<td>63</td>
</tr>
<tr>
<td>[20, 50)</td>
<td>45</td>
</tr>
<tr>
<td>[50, 100)</td>
<td>34</td>
</tr>
<tr>
<td>[100, 200)</td>
<td>25</td>
</tr>
<tr>
<td>[200, 500)</td>
<td>18</td>
</tr>
<tr>
<td>[500, 1000)</td>
<td>14</td>
</tr>
<tr>
<td>[1000, 2000)</td>
<td>11</td>
</tr>
<tr>
<td>[2000, 1000000)</td>
<td>10</td>
</tr>
</table>


>?
>- For more information on tiered pricing, contact your Tencent Cloud rep.
>- Communication over the Beijing-Tianjin and Guangzhou-Shenzhen dedicated tunnels is free of charge before December 31, 2021.
>

#### Billing example
A user uses a Guangzhou-Beijing dedicated tunnel for 14 valid days in January. The number of sample points per day is 288, which is the result of Total duration/Statistical period (24 × 60/5). Therefore, the total number of sample points for the 14 valid days is 4,032 (14 × 288). The bandwidth values of the 4,032 sample points are sorted in ascending order, and the top 5% sample points are removed. The average bandwidth value of the 3,830 sample points (4,032 × 0.95 = 3,830.4) is taken as the billable bandwidth of the month and recorded as Max95. Assume that the value of Max95 is 15 Mbps, for which the corresponding tiered unit price is 63 USD/Mbps. The total fee is calculated as follows: 14/31 × 15 × 63 = 426.77 USD. The fee will be deducted between 8 and 10 AM on February 1.

### Shared dedicated tunnel fee[](id:gxxvlan)
- **Resource occupation fee for shared dedicated tunnel**: The fee is billed in pay-as-you-go mode monthly. The fee incurred in the current month will be deducted from your account between 8 and 10 AM on the first day of the next month.
- **Billing time**: The billing starts on the day when the shared dedicated tunnel enters the **Connected** state, and stops when the tunnel is deleted in the Direct Connect console. The tunnel used less than one month will be billed on the basis of valid days.
- **Billing formula**: Total fee = (Number of valid days in the month/Number of calendar days in the month) × Monthly price for the shared dedicated tunnel.
<table>
<tr>
<th>Tunnel specification</th>
<th>Occupation fee within Chinese mainland (USD/month)</th>
<th>Occupation fee outside Chinese mainland (USD/month)</th>
</tr>
<tr>
<td>50 Mbps</td>
<td>23</td>
<td>23</td>
</tr>
<tr>
<td>100 Mbps</td>
<td>31</td>
<td>46</td>
</tr>
<tr>
<td>200 Mbps</td>
<td>38</td>
<td>57</td>
</tr>
<tr>
<td>300 Mbps</td>
<td>46</td>
<td>92</td>
</tr>
<tr>
<td>400 Mbps</td>
<td>54</td>
<td>120</td>
</tr>
<tr>
<td>500 Mbps</td>
<td>62</td>
<td>146</td>
</tr>
<tr>
<td>1 Gbps</td>
<td>92</td>
<td>231</td>
</tr>
<tr>
<td>2 Gbps</td>
<td>169</td>
<td>523</td>
</tr>
<tr>
<td>5 Gbps</td>
<td>400</td>
<td>1,169</td>
</tr>
<tr>
<td>8 Gbps</td>
<td>631</td>
<td>1,508</td>
</tr>
<tr>
<td>10 Gbps</td>
<td>769</td>
<td>1,692</td>
</tr>
<tr>
<td>40 Gbps</td>
<td>2,769</td>
<td>5,846</td>
</tr>
<tr>
<td>100 Gbps</td>
<td>5,385</td>
<td>12,308</td>
</tr>
</table>
