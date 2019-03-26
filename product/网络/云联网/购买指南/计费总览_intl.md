CCN is a pay-as-you-go service.

- Cross-regional instance interconnection incurs fees, so promptly set your bandwidth limits.
- Instance interconnection within the same region less than 1 Gbps is currently free of charge.

## Billing Method
Cross-regional CCN interconnection billing adopts pay-as-you-go and monthly 95th percentile approach. Its billing is based on monthly actual bandwidth usage.

**Cross-account Billing:**

- Cross-account billing is the same as same-account billing.

- All the interconnection charges incurred by the cross-account shall be paid by the instance account.

 
## Billing Formula
**Monthly CCN fee** is the sum of the interconnection fees of cross-regional CCN instances.

**Monthly cross-region fee** = the monthly 95th percentile bandwidth peak of the region \* valid day ratio \* tiered unit price

- The monthly 95th percentile bandwidth peak：

The average bandwidth values are collected every 5 minutes and sorted in a descending order. After discarding the highest 5% of values, the next highest value is recorded as the monthly 95th percentile bandwidth peak.

**For example**, suppose you used CCN in June and there were 14 days of cross-regional interconnection between region A and B. Because there was one data point every 5 minutes, there were 288 data points in a day (60 min * 24 h / 5 min), and a total number of 4032 data points in 14 days  (14 days * 288). 4032 data points are then sorted in a descending order according to corresponding bandwidth values, and the highest 5% are discarded (4032 * 0.05 = 201.6). Then the 202th data point's bandwidth value is deemed as the monthly 95th percentile bandwidth peak.

- Valid day ratio:

A valid day refers to a day when the bandwidth value of any 5-minute statistical point is greater than 10 Kbps.

Valid day ratio = valid days in a month / natural days in a month.

- Tiered unit price:

A unit price in the tiered pricing scheme. 
 
## Pricing
 <table>

 <tr>

 <th>Billing Item </th>

 <th>Tier </th>

 <th>Mainland China </th>

 <th>Billing Unit </th>

 </tr>

 
 <tr>

 <td rowspan=3>Cross-regional Bandwidth </td>

 <td>0 - 100Mbps </td>

 <td>37 </td>

 <td rowspan=3>USD/Mbps/month </td>

 </tr>

 
 <tr>

 <td>100Mbps - 1000Mbps </td>

 <td>13 </td>

 </tr>

 
 <tr>

 <td>1000+Mbps </td>

 <td>9 </td>

 </tr>

 
 </table>

 
>?

>- Interconnection between CPM and public cloud of the same city below 1 Gbps is free of charge. For example: The interconnection between Beijing CPM VPC and Beijing Public VPC below 1 Gbps is free of charge.

>- For the price of the interconnection between Mainland China and outside Mainland China regions, please consult your Tencent Cloud representative.

 
## Billing Example
Suppose that your CCN instance is associated with network instances in three regions in June: Guangzhou, Beijing and Shanghai.

Example (Guangzhou-Beijing):

- The monthly 95th percentile bandwidth peak：

Billable bandwidth: 120 Mbps

- Valid day proportion (suppose there are 14 valid days):

Valid day ratio= 14 / 30

- Tiered unit price:

Tiered unit price: 13USD/Mbps/month 

 
The CCN fee incurred by the interconnection between Guangzhou and Beijing in June is: billable bandwidth (120 Mbps) * valid day ratio (14 / 30) * tiered unit price (13USD/Mbps/month) = USD728


Fees for other regions (Guangzhou-Shanghai, Beijing-Shanghai) are calculated in the same way .

The CCN fee incurred in June is **the sum of the inter-region interconnection fees**
[!](https://main.qcloudimg.com/raw/67fc221ad32ae2359e5159e3af219d98.png)
