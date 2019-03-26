CCN is a pay-as-you-go service.

- Interconnection of cross-regional network instances incurs fees, so please set bandwidth limits timely.
- Interconnection of intra-regional network instances below 1 Gbps is currently free of charge.

## Billing Method
Cross-regional CCN interconnection charge is based on monthly used bandwidth and billed by the pay-as-you-go monthly 95th percentile.

**Cross-account Billing:**

- Cross-account billing is the same as same-account billing.

- All the interconnection charges incurred by the cross-account shall be paid by the instance account.

 
## Billing Formula
**Monthly CCN fee** is the sum of the interconnection fees of cross-regional CCN instances.

**Monthly cross-region fee** = the monthly 95th percentile bandwidth peak of the region \* valid day proportion \* tiered unit price

- The monthly 95th percentile bandwidth peak：

The average bandwidth value is taken every 5 minutes on each valid day, then the taken average bandwidth values are sorted in ascending order with the highest 5% of the values removed, and the next highest value is used as the monthly 95th percentile bandwidth peak.

**For example**, if you use CCN in June and there are 14 valid days when cross-region interconnection is realized between region A and B, then the number of statistical points per day is 288 (24 h * 60 min / 5 min), and the number of all statistical points in the 14 days are 4032 (14 days * 288/day). The bandwidth values of the 4032 statistical points are sorted in ascending order, and the highest 5% of points are removed (4032 * 0.05 = 201.6), so the bandwidth value of the 202nd point is the monthly 95th percentile bandwidth peak.


- Valid day proportion:

A valid day refers to a day when the bandwidth value of any 5-minute statistical point is greater than 10 Kbps.

Valid day proportion = the valid days in the month / the natural days in the month.

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
