## Overview
For businesses with frequent updates or flash sales, the hotspot update feature greatly optimizes the performance of the UPDATE operation on frequently updated rows. If automatic hotspot update detection is enabled, the system will automatically detect whether there is a single row of hotspot update, and if so, it will queue the large number of concurrent UPDATE operations and execute them in sequence, so as to reduce the risk of concurrency performance being compromised by many row locks.

## Supported Versions
- Kernel version: MySQL 5.7 20200630 and above.
- Kernel version: MySQL 8.0 20200830 and above.

## Use Cases
This feature is suitable for scenarios where the pressure of updating a single row or multiple rows with the primary key specified is very high, such as flash sales.

## Performance Data
For high-concurrency UPDATE operations on a single row with the primary key specified, the performance is improved by over 10 times.
![](https://qcloudimg.tencent-cloud.cn/raw/bcc3908c862a16b9d3c7fb5d51b25d60.png)

## Instructions
For more information, see [Hotspot Update Protection](https://intl.cloud.tencent.com/document/product/1035/36037).
