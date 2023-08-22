>?
>- For detailed BWP pricing, please see [Billing ‍Overview](https://intl.cloud.tencent.com/document/product/684/15254).
>- Pay-as-you-go - Enhanced 95th percentile is only available to bill-by-IP accounts. You can check your account type as instructed in [Checking Account Type](https://www.tencentcloud.com/document/product/684/15246) and upgrade your account if necessary. 
>- When a bandwidth package is activated, the bandwidth fee of one billing cycle is frozen from your account based on your selected bandwidth capand the unit price. For detials, see [Frozen Funds](https://www.tencentcloud.com/zh/document/product/555/12039?lang=zh)‍.
>- The minimum bandwidth usage defaults to 20%. If your bandwidth cap is higher than 5G, the ratio may exceed 20%.

## Billing description
- **Billing date**
The bill is issued on Day 1-2 of every month. You can check the details in Cost Center.
- **Settlement date**
Fees are calculated on a monthly basis. The fee is automatically deducted from the account balance of the user.
- **Billing scope**
Bandwidth packages are region-specific, which means that one bandwidth pakcage only applies to a single region.

>? View the component usage details shown in the bills obtained from the billing center. Usage = Bandwidth package monthly peak x Number of valid days/Number of billable days in the month.

- **Bandwidth cap**
  - Instance-based bandwidth cap: 
  - Regional total bandwidth: For bandwidth limits of different line types, see [Use Limits](https://www.tencentcloud.com/document/product/684/15247).

## Fee calculation
**Bandwidth package fee** = **MAX (Monthly peak bandwidth x Valid days/Days of the billable month, Package duration/Days of the billable month) x Unit price**.
 - **Monthly peak bandwidth**: Collect the values of inbound and outbound bandwidth every 5 minutes. Take the higher one between these two as the bandwidth of the sampling point of time. 288 sample points are collected every day. The fifth highest value is taken as the daily peak bandwidth. The average of the five highest daily peaks is taken as the monthly peak bandwidth.
 - **Monthly minimum bandwidth**[](id:ybddk): Daily minimum bandwidth = Bandwidth cap of the package on that day × Minimum usage ratio (default to 20%). The average of daily minimum bandwidth values of package duration days is taken as the Monthly minimum bandwidth. The daily minimum bandwidth is recorded from the package creation day till the deletion day.
 - **Valid days:** Number of days with at least one bandwidth sample point greater than 1 Kbps.
 - **Package duration**: Number of calendar days from the creation day to the deletion day of the package. 
 - **Days of the billable month:** Number of calendar days of the billable month.

## Billing examples
Assume that you create a general BGP bandwidth package on June 10, and delete it on June 21. During this period, the bandwidth cap of the package is set to 500 Mbps, with the minimum bandwidth usage of 20%. The unit price is 16.97 USD/Mbps/month. 

Bandwidth peaks over 1 Kbps are recorded on 6 days. The bandwidth package is valid for 12 days. The monthly peak bandwidth is 80 Mbps. The bandwidth package fee of the month is calculated as below: 
- Monthly peak bandwidth = 80 Mbps
- Daily minimum bandwidth = 500 Mbps × 20% = 100 Mbps 
- Monthly minimum bandwidth = 100 Mbps

Bandwidth package fee = MAX (80 × 6/30, 100 × 12/30) × 16.97 = MAX (16, 40)× 16.97 = 678.8 USD.