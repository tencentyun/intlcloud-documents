This document describes the two pay-as-you-go billing modes of bandwidth packages: monthly top 5 and monthly 95th percentile.
>?For detailed BWP pricing, please see [Product Pricing](https://intl.cloud.tencent.com/document/product/684/15254).

## Billing
- **Billing date**
  The first day of the calendar month immediately after the current billing cycle. For example, the BWP bill for usage in January (between 2021-01-01 00:00:00 and 2021-01-31 23:59:59) is generated on February 1st.
- **Settlement date**
  BWP is billed by month. The fees will be automatically deducted from the account balance after the bill is generated.
- **Billing scope**
  BWP is region-specific, which means that one BWP only applies to a single region.
- **Peak bandwidth**
 - Single instance: the peak bandwidth of an instance billed on bandwidth packages is 2 Gbps. The peak bandwidth is only regarded as the maximum bandwidth for reference, and not as the committed bandwidth. When bandwidth resources are contested, the peak bandwidth may be limited.
 - Single region: the sum of peak bandwidths of all the running instances billed on bandwidth packages cannot exceed 50 Gbps in one region. If your application requires a guaranteed or higher bandwidth, contact your sales rep or [submit a ticket](https://console.cloud.tencent.com/workorder/category). In this case, you need to pay the guaranteed bandwidth fee on a pro rata basis.

## Monthly Top 5 Billing[](id:mtop5)

### Billing formula
**BWP fee** = BWP monthly peak x Unit price x Number of valid days/Number of billable days in the month.
- **Daily peak**: the maximum outbound bandwidth and inbound bandwidth will be respectively collected every five minutes, and the higher value is taken as a sample point. All the 288 sample points on the day are sorted in descending order, and the fifth-highest value is used as the daily peak bandwidth.
- **Monthly peak**: on the settlement date, the daily peaks of the valid days in the last month are sorted in descending order, and the average value of the top 5 peaks is used as the monthly peak.
- **Valid day:** a day in which at least one bandwidth value is greater than 1 Kbps.
- **Billable days in the month**: the actual number of days during the month in which BWP is used.

### Billing sample
Assume you use a BGP bandwidth package in June at a unit price of 16.97 USD/Mbps/month, where there are 30 billable days. Of those days, there are 20 days with active usage, and the top 5 peak bandwidths are 100 MB, 95 MB, 90 MB, 85 MB and 80 MB.
- Monthly peak = (100 + 95 + 90 + 85 + 80) / 5 = 90 MB
- BWP fee = 90 × 16.97 × 20 / 30 = 1,018.2 USD

## Monthly 95th Percentile[](id:m95)
>?Monthly 95th percentile billing is available only to customers with monthly consumption greater than 15,000 USD. For more information, contact your sales rep or [submit a ticket](https://console.cloud.tencent.com/workorder/category). The monthly 95th percentile prices are subject to change in some regions.

### Billing formula
**BWP fee** = BWP monthly peak x Unit price x Number of valid days/Number of billable days in the month.
- **Monthly peak:** the maximum outbound bandwidth and inbound bandwidth will be respectively collected every five minutes, and the higher value is taken as a sample point. All sample points of the current month are sorted in descending order, and the top 5% are removed. The highest value of the remaining sample points is used as the monthly peak bandwidth.
Suppose you use BWP for 14 valid days in June. As one sample point is generated every 5 minutes, 288 sample points are generated every day, and 4,032 sample points are generated in 14 days. The bandwidth values of these sample points are sorted in descending order, the top 5% of the sample points (4,032 sample points × 0.05 = 201.6 sample points) are removed. The bandwidth value of the 202nd sample point is taken as the 95th percentile of monthly peak bandwidth.
- **Valid day:** a day in which at least one bandwidth value is greater than 1 Kbps.
- **Billable days in the month**: the actual number of days during the month in which BWP is used.

### Billing sample
Assume you use a BGP bandwidth package in June at a unit price of 16.97 USD/Mbps/month, where there are 30 billable days. Of those days, there are 20 days with bandwidth usage. The 95th percentile of monthly peak is 120 MB.
BWP fee = 120 × 16.97 × 20 / 30 = 1,357.6 USD

## Reference
[Product Pricing](https://intl.cloud.tencent.com/document/product/684/15254)
