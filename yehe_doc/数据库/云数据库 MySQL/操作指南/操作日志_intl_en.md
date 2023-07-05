## Overview
A SQL statement query that takes more time than the specified value is referred to as a "slow query", and the corresponding statement is called a "slow query statement". The process where a database administrator (DBA) analyzes slow query statements and finds out the reasons why slow queries occur is known as "slow query analysis".

In the **Operation Log** tab, you can view the slow logs details, error logs details, and rollback logs of the instance and download slow logs. You can also view and download database logs on the command line interface (CLI) or through TencentDB APIs. For more information, see [DescribeSlowLogs](https://intl.cloud.tencent.com/document/product/236/15845) and [DescribeBinlogs](https://intl.cloud.tencent.com/document/product/236/15843).

>?Currently, slow log download and rollback features are not supported for TencentDB for MySQL single-node instances of the cloud disk edition.
>

#### Notes on MySQL slow queries
- long_query_time: Slow query threshold parameter that is accurate to the microsecond level. The default value is 10 seconds. When a SQL statement takes more time than the threshold to execute, it will be recorded in a slow log. 
When the `long_query_time` parameter is adjusted, existing slow logs will not be affected. For example, if the slow log threshold parameter is 10s, slow logs will be reported for exceeding queries; after this value is modified to 1s, the previously reported logs will still be displayed.
- log_queries_not_using_indexes: Whether to log unindexed queries. The default value is OFF.

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance management page.
2. On the **Operation Log** tab, you can view the slow logs details, error logs details, and rollback logs of the instance and download slow logs.
<table>
<thead><tr><th>Feature</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Slow log details</td><td>Records SQL statements that took more than 10 seconds to execute in the database for the past month</td></tr>
<tr>
<td>Slow log download</td><td>Downloads slow logs</td></tr>
<tr>
<td>Error log details</td><td>Records the detailed information of each startup and shutdown as well as all the serious warnings and errors during operation</td></tr>
<tr>
<td>Rollback logs</td><td>Records the status and progress of rollback tasks</td></tr>
</tbody></table>
3. On the **Download Slow Log** tab, click **Download** in the **Operation** column to download slow logs.
4. We recommend that you copy the download address in the pop-up window, log in to a (Linux) CVM instance in the same VPC as the TencentDB instance, and run the `wget` command to download over the private network at a higher speed. For more information, see [Customizing Linux CVM Configurations](https://www.tencentcloud.com/document/product/213/10517#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.99.BB.E5.BD.95.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8).
>?
>- Logs with a size of 0 KB cannot be downloaded.
>- You can also click **Download** to download it directly. However, this may take a longer time.
>- `wget` command format: wget -c 'log file download address' -O custom filename.log
>
Below is a sample:
```
wget -c 'http://szx.dl.cdb.tencentyun.com:303/cfdee?appid=1210&time=1591&sign=aIGM%3D' -O test.log
```

