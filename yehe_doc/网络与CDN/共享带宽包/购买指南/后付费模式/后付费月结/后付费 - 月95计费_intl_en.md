>?Starting from April 1, 2023, monthly-subscribed 95th percentile billing mode is no longer available for new BWP users.
>

## Billing Details
- **Billing date**
The bill is issued on Day 1-2 of every month. You can check the details in Cost Center.
- **Settlement date**
Fees are calculated on a monthly basis. The fee is automatically deducted from the account balance of the user.
- **Billing scope**
BWP is region-specific, which means that one BWP only applies to a single region.
>?View the component usage details shown in the bills obtained from the billing center. Usage = BWP monthly peak x Number of valid days/Number of billable days in the month.
>
- **Peak bandwidth**
 - Instance peak bandwidth: The peak bandwidth of an instance billed on bandwidth packages is 2 Gbps. The peak bandwidth is only regarded as the maximum possible bandwidth, and not as the committed bandwidth. In case of resource contention, the peak bandwidth may not reach this value.
 - Regional total bandwidth: For bandwidth limits of different line types, see [Use Limits](https://intl.cloud.tencent.com/document/product/684/15247).

## Billing Formula
**BWP fee** = BWP monthly peak x Unit price x Number of valid days/Number of billable days in the month.
- **Monthly peak:** the maximum outbound bandwidth and inbound bandwidth will be respectively collected every five minutes, and the higher value is taken as a sample point. All sample points of the current month are sorted in descending order, and the top 5% are removed. The highest value of the remaining sample points is used as the monthly peak bandwidth.
Suppose you use BWP for 14 valid days in June. As one sample point is generated every 5 minutes, 288 sample points are generated every day, and 4,032 sample points are generated in 14 days. The bandwidth values of these sample points are sorted in descending order, the top 5% of the sample points (4,032 sample points × 0.05 = 201.6 sample points) are removed. The bandwidth value of the 202nd sample point is taken as the 95th percentile of monthly peak bandwidth.
- **Valid day:** a day in which at least one bandwidth value is greater than 1 Kbps.
- **Billable days in the month**: the actual number of days during the month in which BWP is used.

## Billing Example
Assume you use a BGP bandwidth package in June at a unit price of 16.97 USD/Mbps/month, where there are 30 billable days. Of those days, there are 20 days with bandwidth usage. The 95th percentile of monthly peak is 120 MB.
BWP fee = 120 × 16.97 × 20 / 30 = 1,357.6 USD