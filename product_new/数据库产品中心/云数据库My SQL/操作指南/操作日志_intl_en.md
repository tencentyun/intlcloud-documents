## Operation Scenarios
An SQL statement query that takes more time than the specified value is referred to as a "slow query", and the corresponding statement is called a "slow query statement". The process where a database administrator (DBA) analyzes slow query statements and finds out the reasons why slow queries occur is known as "slow query analysis".

TencentDB for MySQL High-Availability Edition and Single-Node High-IO Edition instances provide an operation log management feature to help you quickly locate faults and issues. You can view the slow log details, error log details, rollback logs of an instance and download slow logs on the operation logs page in the console.
You can also view and download database logs on the command line interface (CLI) or through TencentDB APIs. For more information, please see [Querying Backup Logs](https://intl.cloud.tencent.com/document/product/236/15842) and [Querying Binary Logs](https://intl.cloud.tencent.com/document/product/236/15843).

#### Notes on Slow Queries in MySQL
- long_query_time: slow query threshold parameter down to the microsecond level. The default value is 10s. When an SQL statement takes more time to execute, it will be recorded in a slow log. 
When the `long_query_time` parameter is adjusted, existing slow logs will not be affected. For example, if the slow log threshold parameter is 10s, slow logs will be reported for exceeding queries; after this value is modified to 1s, the previously reported logs will still be displayed.
- log_queries_not_using_indexes: whether to log unindexed queries. Default value: OFF.


## Directions
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb).
2. In the instance list, click an instance name or **Manage** in the "Operation" column to enter the instance management page.
3. Go to the **Operation Logs** page, on which you can view the slow log details, error log details, and rollback logs of the instance and download slow logs.
<table>
<thead>
<tr>
<th>Feature</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Slow log details</td>
<td>Records SQL statements that took more than 10s to execute in the database in the past month</td>
</tr>
<tr>
<td>Slow log download</td>
<td>Provides the ability to download slow logs</td>
</tr>
<tr>
<td>Error log details</td>
<td>Records logs of database execution errors</td>
</tr>
<tr>
<td>Rollback logs</td>
<td>Records the status and progress of rollback tasks</td>
</tr>
</tbody></table>
<img src="https://main.qcloudimg.com/raw/321e4fe17bf8d06693593323c91447b3.png"  style="margin:0;">
4. On the **Slow Log Download** page, you can click **Download** in the "Operation" column to download slow logs.
5. In the pop-up dialog box, you can click **Local Download** to download directly. You can also choose to copy the download address, log in to a Linux CVM instance in the same VPC as the TencentDB instance, and use the `wget` command for download.
>- `wget` command format: wget -c 'log file download address' -O custom filename.log
>Below is an example:
```
wget -c 'http://szx.dl.cdb.tencentyun.com:303/cfdee?appid=1210&time=1591&sign=aIGM%3D' -O test.log
```
>- Logs with a size of 0 KB cannot be downloaded.

