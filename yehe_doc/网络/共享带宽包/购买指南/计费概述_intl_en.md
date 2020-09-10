>BWP is currently in beta test. If you want to try it out, please [submit an application](https://intl.cloud.tencent.com/apply/p/86ulv50u1e8).

This document describes the billing mode and price of bandwidth packages. The two billing modes are Monthly Top 5 and Monthly 95th Percentile.

## Billing

- **Billing date**
  The first day of the calendar month immediately after the current billing cycle. For example, the BWP bill for usage in May (2019-05-01 00:00:00 to 2019-05-31 23:59:59) is generated on June 1st.
- **Settlement date**
  After the bill is generated, the charge is automatically deducted from your account balance to settle the bill. Therefore, ensure that your account balance is sufficient at the time of settlement to avoid going into arrears.
- **Billing scope**
  BWP charges by region. One BWP covers a single region.
- **Usage details**
  BWP provides minute-level usage details, which can be downloaded in the console.

## Billing by monthly-top-5

### Billing formula
**BWP fee** = BWP monthly peak x Number of valid days x Unit price/Number of days of the billed month.

- **Daily peak: **the highest BWP bandwidth value at the granularity of 10 seconds is collected every five minutes. At the end of the day, the collected values are sorted in descending order, and the fifth highest value is used as the daily peak.
As one sample point is generated every 5 minutes, 288 (60 min × 24/5 min) sample points are generated every day. The values of the 288 sample points are sorted in descending order, the fifth sample point is taken as the daily peak bandwidth.
- **Monthly peak**: When the billed month is over, the collected daily peaks are sorted in descending order, and the average value of the top 5 peaks is used as the monthly peak.
- **Valid days**: the number of days in which bandwidth is greater than 1 Kbps.
- **Days of the billed month**: the actual number of days during the month in which BWP is used.

>
>1. The daily peak is collected for inbound and outbound traffic respectively to calculate the monthly peak for inbound and outbound traffic.
>2. The monthly peak is collected for inbound and outbound traffic respectively, and the higher one is used as the monthly peak.

### Price
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

Monthly peak =（100 + 95 + 90 + 85 + 80) / 5 = 90 MB
BWP fee = 90 × 20 × 16.97 / 30 = 1,018.2 USD
The final fee for June is 1,018.2 USD, payable in early July.


## Billing by monthly-95th-percentile
>Monthly 95th percentile billing is currently only available to customers with monthly consumption greater than 15,000 USD. For details, please contact your sales rep or [submit a ticket](https://console.cloud.tencent.com/workorder/category).

### Billing formula
**BWP fee** = BWP monthly peak x Number of valid days x Unit price/Number of days of the billed month.
- **Monthly peak**: Every five minutes, the highest BWP bandwidth value per minute is collected. When the billed month is over, the collected values are sorted from high to low. After the top 5% values are eliminated, the highest value is used as the monthly peak.
For example, you use BWP for 14 days in June. As one sample point is generated every 5 minutes, 288 (60 min × 24/5 min) sample points are generated every day, and 4032 (14 days × 288 sample points/day) sample points are generated in 14 days. The bandwidth values of the 4032 sample points are sorted in descending order, the top 5% of the sample points (4032 sample points × 0.05 = 201.6 statistical points) are removed, and the bandwidth value of the 202nd sample point is taken as the monthly 95th percentile of peak bandwidth.
- **Valid days**: the number of days in which bandwidth is greater than 1 Kbps.
- **Days of the billed month**: the actual number of days during the month in which BWP is used.

>Monthly peak is collected for inbound and outbound traffics respectively and the higher one is used as the monthly peak of the current billed month.


### Price
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

>The monthly 95th percentile billing is in beta, and the prices are subject to change for some on the regions later.

### Billing example
Assume you use BWP in June, where there are 30 billable days. Of those days, there are 20 days with active usage. The monthly 95th percentile peak is 120 MB.
BWP fee = 120 × 20 × 16.97 / 30 = 1,357.6 USD
The final fee for June is 1,357.6 USD, payable in early July.
