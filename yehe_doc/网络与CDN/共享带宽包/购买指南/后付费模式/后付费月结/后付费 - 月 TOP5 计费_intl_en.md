This document describes the monthly top 5 billing mode of BWP. 
>?For detailed BWP pricing, see [Billing Overview](https://www.tencentcloud.com/document/product/684/15254).
>

## Billing Details
- **Billing date**
The bill is issued on Day 1-2 of every month. You can check the details in Cost Center.
- **Settlement date**
Fees are calculated on a monthly basis. The fee is automatically deducted from the account balancer of the user.
- **Billing scope**
BWP is region-specific, which means that one BWP only applies to a single region.
>?View the component usage details shown in the bills obtained from the billing center. Usage = BWP monthly peak x Number of valid days/Number of billable days in the month.
>
- **Peak bandwidth**
   - Instance peak bandwidth: The peak bandwidth of an instance billed on bandwidth packages is 2 Gbps. Note that this is the max possible bandwidth, but not the committed bandwidth. In case of resource contention, the peak bandwidth may not reach this value.
   - Regional total bandwidth: For bandwidth limits of different line types, see [Use Limits](https://intl.cloud.tencent.com/document/product/684/15247).

[](id:mtop5)
## Billing Formula
**BWP fee** = BWP monthly peak x Unit price x Number of valid days/Number of billable days in the month.
- **Daily peak**: the maximum outbound bandwidth and inbound bandwidth will be respectively collected every five minutes, and the higher value is taken as a sample point. All the 288 sample points on the day are sorted in descending order, and the fifth-highest value is used as the daily peak bandwidth.
- **Monthly peak**: on the settlement date, the daily peaks of the valid days in the last month are sorted in descending order, and the average value of the top 5 peaks is used as the monthly peak.
- **Valid day:** a day in which at least one bandwidth value is greater than 1 Kbps.
- **Billable days in the month**: the actual number of days during the month in which BWP is used.

## Billing Example
Assume you use a BGP bandwidth package in June at a unit price of 16.97 USD/Mbps/month, where there are 30 billable days. Of those days, there are 20 days with active usage, and the top 5 peak bandwidths are 100 MB, 95 MB, 90 MB, 85 MB and 80 MB.
- Monthly peak = (100 + 95 + 90 + 85 + 80) / 5 = 90 MB
- BWP fee = 90 × 16.97 × 20 / 30 = 1,018.2 USD


