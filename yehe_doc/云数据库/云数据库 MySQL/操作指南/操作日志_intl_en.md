## Overview
An SQL statement query that takes more time than the specified value is referred to as a "slow query", and the corresponding statement is called a "slow query statement". The process where a database administrator (DBA) analyzes slow query statements and finds out the reasons why slow queries occur is known as "slow query analysis".

You can view the slow logs details, error logs details, and rollback logs of an instance, and download slow logs on the operation log page in the console. You can also view and download database logs through the command line interface (CLI) or TencentDB APIs. For more information, please see [DescribeSlowLogs](https://intl.cloud.tencent.com/document/product/236/15845) and [DescribeBinlogs](https://intl.cloud.tencent.com/document/product/236/15843).

>?TencentDB for MySQL instances (excluding basic single-node instances) support operation log management.
>

#### Notes on slow queries in MySQL
- long_query_time: slow query threshold parameter that is accurate to the microsecond level. The default value is 10 seconds. When an SQL statement takes more time than the threshold to execute, it will be recorded in a slow log. 
When the `long_query_time` parameter is adjusted, existing slow logs will not be affected. For example, if the slow log threshold parameter is 10 seconds, the slow log records exceeding 10 seconds are reported. After this value is modified to 1 second, the previously reported logs will still be kept.
- log_queries_not_using_indexes: whether to log unindexed queries. The default value is OFF.


## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
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
<img src="https://main.qcloudimg.com/raw/c229d0fe6a4869998d3472b0a35efa28.png"  style="margin:0;">
3. To download the slow log, on the **Download Slow Log** tab, click **Download** in the **Operation** column.
4. Copy the download address in the pop-up dialog box, [log in to the Linux CVM in the same VPC as the TencentDB instance](https://intl.cloud.tencent.com/document/product/213/10517), and run `wget` to download the file over the high-speed private network.
>?
>- Logs with a size of 0 KB cannot be downloaded.
>- You can also click **Download** to download it directly. However, this may take longer.
>- `wget` command format: wget -c 'log file download address' -O custom filename.log
>
Example:
```
wget -c 'http://szx.dl.cdb.tencentyun.com:303/cfdee?appid=1210&time=1591&sign=aIGM%3D' -O test.log
```
