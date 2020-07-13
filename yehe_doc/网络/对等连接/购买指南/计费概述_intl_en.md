## Billing Overview
Tencent Cloud peering connections are billed by bandwidth in the following pay-as-you-go modes.
- Billing by daily peak bandwidth: you will be charged by the peak inbound/outbound bandwidth on a day.
- Billing by monthly 95th percentile: you will be charged by the 95th percentile of the monthly peak bandwidth. (This billing mode is not yet available to all users. To use this mode, please [submit a ticket](https://intl.cloud.tencent.com/apply/p/clg22aj1t6n).)
>!
> - Bandwidth of 5 Gbps or less in the same region is free of charge, while cross-region bandwidth always incurs a cost. If you need more than 5 Gbps of bandwidth in the same region, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us.
> - The cost of a cross-region or cross-account peering connection is paid by the initiator of the peering connection (not the actual communication requester).

## Billing Modes

### Billing by daily peak bandwidth
You will be charged by the daily peak inbound/outbound bandwidth.
- **Billing cycle**: daily. The costs generated for the day are deducted between 8 and 10 AM on the next day.
- **Calculation formula**: Daily cost = Daily peak bandwidth × Tiered unit price of the bandwidth.
   - Daily peak bandwidth: maximum inbound or outbound bandwidth of the current day, which is acquired every 5 minutes.
   - Tiered unit price: unit price of the tier into which the daily peak bandwidth falls.
- **Tiered prices for billing by daily peak bandwidth**
 <table align=“center”>
 <tr>
 <th><center>Billable Items</center> </th>
 <th><center>Billing Tier (Mbps)</center> </th>
 <th><center>Prices of Interconnection Between Regions in Mainland China (USD/Mbps/day)</center> </th>
 </tr>
 <tr>
 <td rowspan=5><center>Cross-region peering connection</center> </td>
 <td><center>(0,20] </td>
 <td><center>3.19 </center></td>
 </tr>
 <tr>
 <td><center>(20,100]</center> </td>
 <td><center>1.98</center> </td>
 </tr>
 <tr>
 <td><center>(100,500]</center> </td>
 <td><center>1.48 </center></td>
 </tr>
 <tr>
 <td><center>(500,2000]</center> </td>
 <td><center>1.19</center> </td>
 </tr>
 <tr>
 <td><center>> 2000 </center></td>
 <td><center>0.82</center> </td>
 </tr>
 </table>

>
>- For prices of interconnection between regions outside Mainland China, consult our sales.
>- For the ease of clarity, the peering connection bill described as cross-region interconnection (Mainland China) means that both the initiator and acceptor are in the Mainland China region (not including Hong Kong, Macao, and Taiwan regions).

- **Example of billing by daily peak bandwidth**
Assume that you used a peering connection between Shanghai (initiator) and Guangzhou (acceptor), and consumed a peak outbound bandwidth of 20 Mbps and inbound bandwidth of 30 Mbps. So the daily peak bandwidth is 30 Mbps and the tiered unit price of the bandwidth is 1.98 USD/Mbps per day. The daily cost is: 30 × 1.98 = 59.4 USD, which will be paid by the initiator between 8 and 10 AM on the next day.

 <span id=yjf> </span>

### Billing by monthly 95th percentile
- Billing by monthly 95th percentile: you will be charged by 95th percentile of the monthly peak bandwidth. (This billing mode is not yet available to all users. To use this mode, please [submit a ticket](https://intl.cloud.tencent.com/apply/p/clg22aj1t6n).)
- **Billing cycle**: monthly. The costs generated for the month are deducted between 8 and 10 AM on the first day of the next month.
- **Calculation formula**: Monthly cost = 95th percentile of monthly peak bandwidth for cross-region peering connections × Proportion of valid days × Tiered unit price.
   - 95th percentile of monthly peak bandwidth: acquired every 5 minutes. The peak bandwidth between two regions within 5 minutes is taken as a sample point. All sample points of the current month are sorted in descending order, and the top 5% are removed. The highest value of the remaining sample points is used as the 95th percentile of the monthly peak bandwidth.
**Example**: you used a peering connection in June to build cross-region interconnection between Shanghai (initiator) and Guangzhou (acceptor) for 14 valid days. Because one sample point is generated every 5 minutes, 288 (60 min × 24/5 min) sample points are generated every day, and 4,032 (14 days × 288 sample points/day) sample points are generated in 14 days. The bandwidth values of the 4,032 sample points are sorted in descending order, the top 5% (4,032 sample points × 0.05 = 201.6 sample points) are removed, and the bandwidth value of the 202nd sample point is used as the 95th percentile of the monthly peak bandwidth.
   - Proportion of valid days: valid days in which at least one sample point has a bandwidth greater than 10 Kbps.
Proportion of valid days = number of valid days in the current month / number of days in the current month.
   - Tiered unit price: unit price of the tier into which the 95th percentile of the monthly peak bandwidth falls.
- **Tiered prices for billing by monthly 95th percentile**
 <table align=“center”>
 <tr>
 <th><center>Billable Items</center></th>
 <th><center>Billing Tier (Mbps)</center></th>
 <th><center>Prices of Interconnection Between Regions in Mainland China (USD/Mbps/day)</center></th>
 </tr>
 <tr>
 <td rowspan=9><center>Cross-region bandwidth<center></td >
 <td><center>(0,10] </center></td>
 <td><center>85</center> </td>
 </tr>
 <tr>
 <td><center>(10,20]</center> </td>
 <td><center>63</center> </td>
 </tr>
 <tr>
 <td><center>(20,50]</center> </td>
 <td><center>43</center> </td>
 </tr>
 <tr>
 <td><center>(50,100]</center> </td>
 <td><center>34</center> </td>
 </tr>
 <tr>
 <td><center>(100,200] </center></td>
 <td><center>25</center> </td>
 </tr>
 <tr>
 <td><center>(200,500] </center></td>
 <td><center>18</center> </td>
 </tr>
 <tr>
 <td><center>(500,1000]</center> </td>
 <td><center>14</center> </td>
 </tr>
 <tr>
 <td><center>(1000,2000] </center></td>
 <td><center>11</center> </td>
 </tr>
 <tr>
 <td><center>> 2000</center> </td>
 <td><center>10</center> </td>
 </tr>
 </table>

>For prices of interconnection between regions outside Mainland China, consult our sales.

- **Example of billing by monthly 95th percentile**
Assume that you used a peering connection between Shanghai (initiator) and Guangzhou (acceptor) in June and consumed a bandwidth higher than 10 Kbps for 14 valid days. The 95th percentile of the monthly peak bandwidth is 60 Mbps.
   - Proportion of valid days: 14/30.
   - Tiered unit price: 24 USD/Mbps per month, which is the unit price of the tier into which 60 Mbps falls.
  

Cost of June = 95th percentile of the monthly peak bandwidth × Proportion of valid days × Tiered unit price = 60 × (14/30) × 24 = 672 USD, which will be paid by the initiator between 8 and 10 AM on July 1.
