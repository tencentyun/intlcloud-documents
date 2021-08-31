The actual BWP charges depend on the monthly peak. You can check the billable monthly peak of any bandwidth package on the Bandwidth Package console.

## Calculation Rule

**Monthly top 5 billing**
- **Daily peak**: the maximum bandwidth value (outbound or inbound bandwidth) is collected every 10 seconds, and the peak bandwidth within 5 minutes is taken as a sample point. All the 288 sample points on the day are sorted in descending order, and the fifth highest value is used as the daily peak bandwidth.
- **Monthly top 5 bandwidth**: the daily peaks of the valid days in the current month are sorted in descending order, and the average of the top 5 values is used as the monthly peak bandwidth, i.e. billable bandwidth. The monthly peak bandwidth is updated at 00:00:00 every day. For example, suppose you view the monthly billable bandwidth on January 20, 2021, the value is calculated on the daily peaks from January 1 to January 19, 2021.

**Monthly 95th percentile**
- **95th percentile of the monthly peak bandwidth**: the maximum bandwidth value (outbound or inbound bandwidth) of the bandwidth package is collected every 10 seconds, and the peak bandwidth within 5 minutes is taken as a sample point. All sample points of the current month are sorted in descending order, and the top 5% are removed. The highest value of the remaining sample points is used as the 95th percentile of the monthly peak bandwidth, i.e. billable bandwidth. The monthly peak bandwidth is updated at 00:00:00 every day. For example, suppose you view the monthly billable bandwidth on January 20, 2021, the value is calculated on the daily peaks from January 1, 2021 00:00:00 to January 19, 2021 23:59:59.


## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and click **Bandwidth Package** on the left sidebar.
2. At the top left of the **Bandwidth Package** page, choose the region you want to check the bandwidth.
3. Click the ID/Name of the target instance in the list.
4. View the current billable bandwidth (after peak clipping) on the instance details page.

## Documentation
- [Billing Overview](https://intl.cloud.tencent.com/document/product/684/15255)
