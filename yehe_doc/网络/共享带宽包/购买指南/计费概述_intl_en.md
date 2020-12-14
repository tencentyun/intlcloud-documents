>? BWP is currently in beta. If you want to try it out, please [submit a ticket](https://intl.cloud.tencent.com/apply/p/86ulv50u1e8).

This document describes the billing mode and price of bandwidth packages. Two billing modes are available: monthly top 5 and monthly 95th percentile.

## Billing

- **Billing date**
  The first day of the calendar month immediately after the current billing cycle. For example, the BWP bill for usage in May (between 2019-05-01 00:00:00 and 2019-05-31 23:59:59) is generated on June 1st.
- **Settlement date**
  After the bill is generated, the fees will be automatically deducted from your account balance for settlement. Therefore, make sure that your account balance is sufficient to avoid the service suspension.
- **Billing scope**
  BWP is region-specific, which means that one BWP only applies to a single region.
- **Usage details**
  BWP provides minute-level usage details, which can be downloaded in the console.

## Monthly Top 5

### Billing formula
**BWP fee** = BWP monthly peak x Number of valid days x Unit price/Billable days in the month.

- **Daily peak:** the maximum bandwidth value of the bandwidth package is collected every 10 seconds, and the peak bandwidth within 5 minutes is taken as a sample point. All the sample points on the day are sorted in descending order, and the fifth highest value is used as the daily peak bandwidth.
Because one sample point is generated every 5 minutes, 288 (60 min × 24/5 min) sample points are generated every day. All the sample points on the day are sorted in descending order, and the fifth highest value is used as the daily peak bandwidth.
- **Monthly peak:** the daily peaks of the valid days in the current month are sorted in descending order, and the average of the top 5 values is used as the monthly peak bandwidth.
- **Valid day:** a day in which at least one bandwidth value is greater than 1 Kbps.
- **Billable days in the month:** the actual number of days during the month in which BWP is used.

> !
> 1. The daily peak is collected for inbound and outbound traffic respectively to calculate the monthly peak for inbound and outbound traffic.
>2. The monthly peak may be either the inbound or outbound traffic, whichever is higher.

### Pricing
<table>
<thead>
<tr>
<th align="left" width="80%">Region</th>
<th align="left" width="20%">Unit Price</th>
</tr>
</thead>
<tbody><tr>
<td align="left">All regions</td>
<td align="left">16.97 USD/Mbps/month</td>
</tr>
</tbody></table>

### Billing example
Assume you use BWP in June, where there are 30 billable days. Of those days, there are 20 days with active usage. These 20 days are sorted in descending order in accordance to the daily peak usage and the top 5 are 100 MB, 95 MB, 90 MB, 85 MB and 80 MB.

Monthly peak = (100 + 95 + 90 + 85 + 80) / 5 = 90 MB
BWP fee = 90 × 20 × 16.97 / 30 = 1,018.2 USD
The final fee for June is 1,018.2 USD, payable in early July.      

## Monthly 95th Percentile
>Monthly 95th percentile billing is available only to customers with monthly consumption greater than 15,000 USD. For more information, contact your sales rep or [submit a ticket](https://console.cloud.tencent.com/workorder/category).

### Billing formula
**BWP fee** = BWP monthly peak x Number of valid days x Unit price/Billable days in the month.
- **Monthly peak:** the maximum bandwidth value of the bandwidth package is collected every 10 seconds, and the peak bandwidth within 5 minutes is taken as a sample point. All sample points of the current month are sorted in descending order, and the top 5% are removed. The highest value of the remaining sample points is used as the monthly peak bandwidth.
For example, you use BWP for 14 valid days in June. Because one sample point is generated every 5 minutes, 288 (60 min × 24/5 min) sample points are generated every day, and 4,032 (14 days × 288 sample points/day) sample points are generated in 14 days. The bandwidth values of the 4,032 sample points are sorted in descending order, the top 5% (4032 sample points × 0.05 = 201.6 sample points) are removed, and the bandwidth value of the 202nd sample point is used as monthly 95th percentile peak.
- **Valid day:** a day in which at least one bandwidth value is greater than 1 Kbps.
- **Billable days in the month:** the actual number of days during the month in which BWP is used.

>!The monthly peak may be either the inbound or outbound traffic, whichever is higher.

### Pricing
<table>
<thead>
<tr>
<th align="left" width="80%">Region</th>
<th align="left" width="20%">Unit Price</th>
</tr>
</thead>
<tbody><tr>
<td align="left">All regions</td>
<td align="left">16.97 USD/Mbps/month</td>
</tr>
</tbody></table>

>The monthly 95th percentile billing is in beta, and the prices are subject to change for some regions later.

### Billing example
Assume you use BWP in June, where there are 30 billable days. Of those days, there are 20 days with active usage. The monthly 95th percentile peak is 120 MB.
BWP fee = 120 × 20 × 16.97 / 30 = 1,357.6 USD
The final fee for June is 1,357.6 USD, payable in early July.

