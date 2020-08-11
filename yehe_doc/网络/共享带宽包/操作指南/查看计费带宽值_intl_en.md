The actual BWP charges depend on the monthly peak. You can check the billable monthly peak of any bandwidth package on the Bandwidth Package Console.

## Calculation Rule

- **Monthly top 5 billing**
	1. **Daily peak**: the maximum bandwidth value is collected every 10 seconds, and the peak bandwidth within 5 minutes is taken as a sample point. Because one sample point is generated every 5 minutes, 288 (60 min × 24/5 min) sample points are generated every day. All the sample points on the day are sorted in descending order, and the fifth highest value is used as the daily peak bandwidth.
	2. **Monthly top 5 bandwidth**: the daily peaks of the valid days in the current month are sorted in descending order, and the average of the top 5 values is used as the monthly peak bandwidth, i.e. billable bandwidth. The monthly peak bandwidth is updated at 00:00:00 every day. For example, suppose you view the monthly billable bandwidth on July 20, 2020, the value is calculated on the daily peaks from July 1 to July 19, 2020.

- **Monthly 95th percentile**
	95th percentile of the monthly peak bandwidth: the maximum bandwidth value of the bandwidth package is collected every 10 seconds, and the peak bandwidth within 5 minutes is taken as a sample point. All sample points of the current month are sorted in descending order, and the top 5% are removed. The highest value of the remaining sample points is used as the 95th percentile of the monthly peak bandwidth, i.e. billable bandwidth. The monthly peak bandwidth is updated at 00:00:00 every day. For example, suppose you view the monthly 95th percentile on July 20, 2020, the value is calculated on the daily peaks from July 1 2020 00:00:00 to July 19, 2020 23:59:59.

## Directions
1. Log in to the [VPC Console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and click **Bandwidth Package** in the left sidebar.
2. At the top left of the **Bandwidth Package** page, choose the region you want to check the bandwidth.
3. Click the ID/Name of the target instance in the list.
4. View the current billable bandwidth (after peak clipping) on the instance details page.
