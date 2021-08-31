Cloud Connect Network (CCN) is billed according to the interconnection bandwidth and supports the billing mode of pay-as-you-go by monthly 95th percentile and three service levels ([platinum, gold, and silver](https://intl.cloud.tencent.com/document/product/1003/30217)).
You can choose the cost-effective billing plan that best suits your application requirements. For example, we recommend choosing pay-as-you-go by monthly 95th percentile - gold for real-time audio/video and game acceleration. 


## Billing
The following table describes the billing mode.
<table>
<thead>
<tr>
<th align="left" width="13%">Billing Plan</th>
<th align="left" width="15%">Payment Method</th>
<th align="left" width="29%">Billing Unit</th>
<th align="left" width="43%">Use Case</th>
</tr>
</thead>
<tbody>
<tr>
<td align="left">Pay-as-you-go by monthly 95th percentile</td>
<td align="left">Pay after use</td>
<td align="left">USD/month. Fees are charged based on the 95th percentile of the monthly peak bandwidth and the proportion of valid days.</td>
<td align="left">Suitable for business that requires low bandwidth or business volume grows significantly. (it is currently in beta. To try it out, please <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">submit a ticket</a>.)</td>
</tr>
</tbody></table>

The three CCN service levels are as follows:

| Service Level | Service Availability       | Price Ratio        | Use Case  |
| :------- | :---------- | :----------------- | :----------------- |
| Platinum   | 99.99%                   | 1.5                      | Suitable for business that requires extremely high communication quality, such as payment.                           |
| Gold | 99.95%                     | 1                            | Suitable for business that requires moderately high communication quality, such as game acceleration.                                  |
| Silver |  99.50% | 0.75 | Suitable for business that is cost-sensitive but less sensitive to communication quality, such as data backup.  |

>?
>- You can test the network quality using the 10 Kbps of free bandwidth between regions.
>- Bandwidth of 5 Gbps or less in the same region (same account or cross account) is free of charge. There is no free quota for cross-region bandwidth. If you need more than 5 Gbps of bandwidth in the same region, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us.
>- Cross-account and cross-region costs are paid by the account to which CCN instances belong.
>- This price ratio is for reference only. Please refer to the actual prices.

## Pay-As-You-Go by Monthly 95th Percentile
Pay after use. Fees are charged based on the 95th percentile of the monthly peak bandwidth and the proportion of valid days. Monthly pay-as-you-go billing is suitable for business with large bandwidth fluctuations.
For example, if you have 10 Mbps of bandwidth between Beijing and Shanghai regions but also a bandwidth burst of 30 Mbps. We recommend using pay-as-you-go by monthly 95th percentile because you may only need to pay for 10 Mbps of bandwidth after the top 5% is removed.
### Billing cycle
**Monthly pay-as-you-go**: fees are generated each month. You will be charged for the current month between 8 and 10 AM on the first day of the next month.

### Billing formula
**Total monthly cost of CCN** = Sum of the interconnection costs of all regions

**Monthly interconnection cost between two regions** = 95th percentile of the monthly peak bandwidth of the interconnection between regions A and B × Proportion of valid days × Tiered unit price.

- **95th percentile of the monthly peak bandwidth:** acquired every 5 minutes. The peak bandwidth between two regions within 5 minutes is taken as a sample point. All sample points of the current month are sorted in descending order, and the top 5% are removed. The highest value of the remaining sample points is used as the 95th percentile of the monthly peak bandwidth.
Suppose you used CCN in June to build cross-region connection between regions A and B for 14 valid days. Because one sample point is generated every 5 minutes, 288 (60 min × 24/5 min) sample points are generated every day, and 4,032 (14 days × 288 sample points/day) sample points are generated in 14 days. The bandwidth values of the 4,032 sample points are sorted in descending order, the top 5% (4,032 sample points × 0.05 = 201.6 sample points) are removed, and the bandwidth value of the 202nd sample point is used as the 95th percentile of the monthly peak bandwidth.
- **Proportion of valid days:** proportion of valid days = Number of valid days in the current month / Number of days in the current month. A valid day refers to when at least one sample point has a bandwidth greater than 10 Kbps on that day.
- **Tiered unit price:** unit price of the tier into which the 95th percentile of the monthly peak bandwidth falls.

### Pricing
<table>
<thead>
<tr>
<th>Service Level</th>
<th>Local Region</th>
<th>Peer Region</th>
<th>Tier 1 Price<br>(0 Mbps - 100 Mbps]<br>(USD/Mbps/month)</th>
<th>Tier 2 Price<br>(100 Mbps - 1,000 Mbps]<br>(USD/Mbps/month)</th>
<th>Tier 3 Price<br>(>1,000 Mbps)<br>(USD/Mbps/month)</th>
</tr>
</thead>
<tbody><tr>
<td>Platinum</td>
<td rowspan="3">The Chinese mainland<br>(excluding Hong Kong, Macao, and Taiwan)</td>
<td rowspan="3">The Chinese mainland<br>(excluding Hong Kong, Macao, and Taiwan)</td>
<td>55</td>
<td>21</td>
<td>13</td>
</tr>
<tr>
<td>Gold</td>
<td>37</td>
<td>13</td>
<td>9</td>
</tr>
<tr>
<td>Silver</td>
<td>28</td>
<td>10</td>
<td>7</td>
</tr>
</tbody></table>

>?
>- Please consult your sales rep for prices between regions outside the Chinese mainland and other regions.
>- Pay-as-you-go CCN instances are billed by actual usage. To avoid paying for extra bandwidth, we recommend configuring bandwidth cap between regions.

### Billing example
Suppose your CCN (service level: gold) was associated with network instances in Guangzhou, Beijing, and Shanghai regions in June 2019. The bandwidth usage is as follows:
- Interconnection cost between Guangzhou and Beijing regions = 95th percentile of the monthly peak bandwidth value (120 Mbps) × Proportion of valid days (14/30) × Tiered unit price (13 USD/Mbps/month) = 728 USD.
- Interconnection cost between Beijing and Shanghai regions can be calculated using the above formula.
The final CCN cost generated in June is the sum of the interconnection costs of all regions.
![](https://main.qcloudimg.com/raw/fed0ca551f967f9169427022010df878.png)
Prices published here are for reference only. Refer to your bills for final prices.
