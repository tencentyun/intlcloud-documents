## Operation Scenarios
An SQL statement query that takes more time than the specified value is referred to as a "slow query", and the corresponding statement is called a "slow query statement". The process where a database administrator (DBA) analyzes slow query statements and finds out the reasons why slow queries occur is known as "slow query analysis".

You can view the slow log details, error log details, rollback logs of an instance and download slow logs on the operation log page in the console. You can also view and download database logs on the command line interface (CLI) or through TencentDB APIs. For more information, please see [Querying Backup Log](https://intl.cloud.tencent.com/document/product/236/15842) and [Querying Binary Log](https://intl.cloud.tencent.com/document/product/236/15843).

>?TencentDB for MySQL (excluding the Basic Edition) instances support operation log management.
>

#### Notes on slow queries in MySQL
- long_query_time: slow query threshold parameter down to the microsecond level. The default value is 10s. When an SQL statement takes more time to execute, it will be recorded in a slow log. 
When the `long_query_time` parameter is adjusted, existing slow logs will not be affected. For example, if the slow log threshold parameter is 10s, slow logs will be reported for exceeding queries; after this value is modified to 1s, the previously reported logs will still be displayed.
- log_queries_not_using_indexes: whether to log unindexed queries. Default value: OFF.


## Directions
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance name or **Manage** in the "Operation" column to enter the instance management page.
2. Go to the **Operation Log** tab, where you can view the slow log details, error log details, and rollback logs of the instance and download slow logs.
<table>
<thead>
<tr>
<th>Feature</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Slow log details</td>
<td>Records SQL statements that took more than 10s to execute in the database in the last month</td>
</tr>
<tr>
<td>Slow log download</td>
<td>Provides slow logs to download</td>
</tr>
<tr>
<td>Error log details</td>
<td>Records logs of database execution errors</td>
</tr>
<tr>
<td>Rollback log</td>
<td>Records the status and progress of rollback tasks</td>
</tr>
</tbody></table>
<img src="https://main.qcloudimg.com/raw/460115a1a260cb7437561556c2f8cb9a.png"  style="margin:0;">
3. On the **Download slow log** tab, you can click **Download** in the "Operation" column to download slow logs.
4. In the pop-up dialog box, download the logs in one of the following ways:
>?Logs with a size of 0 KB cannot be downloaded.
>
Method 1. Click **Download** to download directly.
Method 2. Copy the download address, log in to a Linux CVM instance in the same VPC as the TencentDB instance, and use the `wget` command for download.
>?`wget` command format: wget -c 'log file download address' -O custom filename.log
>Below is an example:
```
wget -c 'http://szx.dl.cdb.tencentyun.com:303/cfdee?appid=1210&time=1591&sign=aIGM%3D' -O test.log
```
