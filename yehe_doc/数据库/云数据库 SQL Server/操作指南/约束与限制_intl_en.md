TencentDB for SQL Server only offers instances with attached licenses. When an instance is created, it is licensed with the appropriate Microsoft SQL Server edition. You cannot bring your own license.

In order to ensure the stability and security of instances, TencentDB for SQL Server has certain restrictions on usage as detailed below.

TencentDB for SQL Server is available in two editions: single-node edition (formerly Basic Edition) and two-node edition (formerly High Availability/Cluster Edition), each with its own set of features. For more information, see [Features and Differences](https://www.tencentcloud.com/document/product/238/46495).
>?If you have other questions about usage restrictions, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

<table>
<thead><tr><th>Feature</th><th>Two-Node Edition</th><th>Single-Node Edition</th></tr></thead>
<tbody>
<tr><td>Database version</td><td>2008 R2 Enterprise<br>2012 Standard/Enterprise<br>2014 Standard/Enterprise<br>2016 Standard/Enterprise<br>2017 Standard/enterprise<br>2019 Standard/enterprise</td><td>2008 R2 Enterprise<br>2012 Enterprise<br>2014 Enterprise<br>2016 Enterprise<br>2017 Enterprise<br>2019 Enterprise</td></tr>
<tr><td>Maximum number of databases (subject to the number of instance CPU cores as described in <a href="https://intl.cloud.tencent.com/document/product/238/2021" target="_blank">Constraints and Limits > Database quantity</a>)</td><td>2008 R2: 70<br>2012/2014/2016: 300<br>2017: 340<br>2019: 340</td><td>400</td></tr>
<tr><td>Maximum number of database accounts</td><td>Unlimited</td><td>Unlimited</td></tr>
<tr><td>Database creation</td><td>Supported</td><td>Supported</td></tr>
<tr><td>User/Login account creation and deletion</td><td>Supported</td><td>Supported</td></tr>
<tr><td>SA account creation</td><td>Not supported</td><td>Supported</td></tr>
<tr><td>Database authorization</td><td>Supported</td><td>Supported</td></tr>
<tr><td>Database-level DDL trigger</td><td>Supported</td><td>Supported</td></tr>
<tr><td>Thread killing permission</td><td>Supported</td><td>Supported</td></tr>
<tr><td>SQL profiler</td><td>Supported</td><td>Supported</td></tr>
<tr><td>Publish/Subscribe</td><td>Supported</td><td>Not supported</td></tr>
<tr><td>Optimization advisor</td><td>Not supported</td><td>Supported</td></tr>
<tr><td>Linked server</td><td colspan = "2"><li>Supported only in Tencent Cloud private network<br><li>Not supported between other clouds/self-built environments and Tencent Cloud</td></tr>
<tr><td>Distributed transaction</td><td colspan = "2"><li>Supported only in Tencent Cloud private network<br><li>Not supported between other clouds/self-built environments and Tencent Cloud</td></tr>
<tr><td>Change data capture (CDC)</td><td>Supported</td><td>Supported</td></tr>
<tr><td>Change tracking (CT)</td><td>Supported</td><td>Supported</td></tr>
<tr><td>Windows domain account login</td><td>Not supported</td><td>Not supported</td></tr>
<tr><td>Email</td><td>Not supported</td><td>Not supported</td></tr>
<tr><td>SQL Server Integration Services (SSIS)</td><td>Supported</td><td>Supported</td></tr>
<tr><td>SQL Server Analysis Services (SSAS)</td><td>Not supported</td><td>Not supported</td></tr>
<tr><td>SQL Server Reporting Services (SSRS)</td><td>Not supported</td><td>Not supported</td></tr>
<tr><td>R language service</td><td>Not supported</td><td>Not supported</td></tr>
<tr><td>Common Language Runtime (CLR) integration</td><td>Not supported</td><td>Not supported</td></tr>
<tr><td>Async messaging</td><td>Not supported</td><td>Not supported</td></tr>
<tr><td>Policy management</td><td>Not supported</td><td>Not supported</td></tr>
</tbody></table>	

## Database quantity[](id:SJKSL)
>!
>- For a two-node (formerly High Availability/Cluster Edition) instance, if you set `max worker threads` to the default value 0, you can create no more than 100 databases. To create more databases, you must set this parameter to 20,000 as instructed in [Setting Instance Parameters](https://www.tencentcloud.com/document/product/238/41609).
>- If the instance only has one CPU core, we recommend that you keep the database quantity limit at 70 to guarantee instance stability.
>
SQL Server 2008 R2 Enterprise instances don't support lifting the database quantity limit, which is 70. The limit in other SQL Server instances is subject to the number of instance CPU cores as calculated below:
- **Two-node (formerly High Availability Edition)**
2012 Standard/Enterprise
2014 Standard/Enterprise
2016 Standard/Enterprise
Maximum number of databases:
![](https://qcloudimg.tencent-cloud.cn/raw/f982294bd7bebcf5fdb68e9da01e40d1.jpg)
Extract the square root of the CPU core quantity, round it to one decimal place, multiply the result by 40, and add the product to 80 to get the value X. The smaller value between X and 300 is the maximum number of databases. For example, you can create up to 160 databases in a 4-core 16 GB MEM SQL Server 2014 Enterprise instance.
- **Two-node (formerly Cluster Edition)**
2017 Enterprise
2019 Enterprise
Maximum number of databases:
![](https://qcloudimg.tencent-cloud.cn/raw/6f2eb0ade4f54c3d46da8224a55748e2.jpg)
Extract the square root of the CPU core quantity, round it to one decimal place, multiply the result by 40, and add the product to 120 to get the value Y. The smaller value between Y and 340 is the maximum number of databases. For example, you can create up to 200 databases in a 4-core 16 GB MEM SQL Server 2017 Enterprise instance.
- **Single-node (formerly Basic Edition)**
2008 R2 Enterprise
2012 Enterprise
2014 Enterprise
2016 Enterprise
2017 Enterprise
2019 Enterprise
Maximum number of databases:
![](https://qcloudimg.tencent-cloud.cn/raw/d412fc0b2c1fc12f08046dfc5c3aa546.jpg)
Extract the square root of the CPU core quantity, round it down to the nearest integer, and multiply the result by 100 to get the value N. The smaller value between N and 400 is the maximum number of databases. For example, you can create up to 200 databases in a 4-core 16 GB MEM SQL Server 2017 Enterprise instance.

**Table of instance CPU core quantity and corresponding database quantity limit**
<dx-tabs>
::: Database quantity limit for two-node edition (formerly High Availability/Cluster Edition)
| CPU cores | Two-node 2008 R2/2012/2014/2016 Enterprise | Two-node 2017/2019 Enterprise |
|---------|---------|---------|
| 1 | 70 | 70 |
| 2 | 136 | 176 |
| 4 | 160 | 200 |
| 8 | 193 | 233 |
| 12 | 218 | 258 |
| 16 | 240 | 280 |
| 24 | 275 | 315 |
| 32 | 300 | 340 |
| 48 | 300 | 340 |
| 64 | 300 | 340 |
| 96 | 300 | 340 |

:::
::: Database quantity limit for single-node edition (formerly Basic Edition)
| CPU cores | Single-node edition (formerly Basic Edition) |
|---------|---------|
| 2 | 100 |
| 4 | 200 |
| 8 | 200 |
| 16 | 400 |
| 24 | 400 |
:::
</dx-tabs>

