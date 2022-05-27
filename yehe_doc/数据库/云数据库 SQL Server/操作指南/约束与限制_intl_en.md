TencentDB for SQL Server only offers instances with attached licenses. When an instance is created, it is licensed with the appropriate Microsoft SQL Server edition. You cannot bring your own license.

In order to ensure the stability and security of instances, TencentDB for SQL Server has certain restrictions on usage as detailed below.

TencentDB for SQL Server is available in three editions: Basic, Dual-Server High Availability, and Cluster, each with its own set of features. For more information, see [Features and Differences](https://intl.cloud.tencent.com/document/product/238/46495).
>?If you have other questions about usage restrictions, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

<table>
<thead><tr><th>Feature</th><th>Cluster Edition</th><th>Dual-Server High Availability Edition</th><th>Basic Edition</th></tr></thead>
<tbody>
<tr><td>Database version</td><td>2017 Enterprise<br>2019 Enterprise</td><td>2008 R2 Enterprise<br>2012 Standard/Enterprise<br>2014 Standard/Enterprise<br>2016 Standard/Enterprise<br>2017 Standard/Enterprise<br>2019 Standard/Enterprise</td><td>2008 R2 Enterprise<br>2012 Enterprise<br>2014 Enterprise<br>2016 Enterprise<br>2017 Enterprise<br>2019 Enterprise</td></tr>
<tr><td>Maximum number of databases</td><td>2017: 70<br>2019: 70</td><td>2008 R2, 2012, 2016, 2017: 70<br>2019: 70<br>2014: 70</td><td>Unlimited</td></tr>
<tr><td>Maximum number of database accounts</td><td>Unlimited</td><td>Unlimited</td><td>Unlimited</td></tr>
<tr><td>Database creation</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr><td>User/Login account creation and deletion</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr><td>SA account creation</td><td>Not supported</td><td>Not supported</td><td>Supported</td></tr>
<tr><td>Database authorization</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr><td>Database-level DDL trigger</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr><td>Thread killing permission</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr><td>SQL profiler</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr><td>Pub/Sub</td><td>Supported</td><td>Supported</td><td>Not supported</td></tr>
<tr><td>Optimization advisor</td><td>Not supported</td><td>Not supported</td><td>Supported</td></tr>
<tr><td>Linked server</td><td colspan = "3"><li>Supported only in Tencent Cloud private network<br><li>Not supported between other clouds/self-built environments and Tencent Cloud</td></tr>
<tr><td>Distributed transaction</td><td colspan = "3"><li>Supported only in Tencent Cloud private network<br><li>Not supported between other clouds/self-built environments and Tencent Cloud</td></tr>
<tr><td>Change data capture (CDC)</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr><td>Change tracking (CT)</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr><td>Windows domain account login</td><td>Not supported</td><td>Not supported</td><td>Not supported</td></tr>
<tr><td>Mailing</td><td>Not supported</td><td>Not supported</td><td>Not supported</td></tr>
<tr><td>SQL Server Integration Services (SSIS)</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr><td>SQL Server Analysis Services (SSAS)</td><td>Not supported</td><td>Not supported</td><td>Not supported</td></tr>
<tr><td>SQL Server Reporting Services (SSRS)</td><td>Not supported</td><td>Not supported</td><td>Not supported</td></tr>
<tr><td>R language service</td><td>Not supported</td><td>Not supported</td><td>Not supported</td></tr>
<tr><td>Common Language Runtime (CLR) integration</td><td>Not supported</td><td>Not supported</td><td>Not supported</td></tr>
<tr><td>Async messaging</td><td>Not supported</td><td>Not supported</td><td>Not supported</td></tr>
<tr><td>Policy management</td><td>Not supported</td><td>Not supported</td><td>Not supported</td></tr>
</tbody>
</table>	
