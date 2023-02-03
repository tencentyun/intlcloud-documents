
## October 2022
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=20%>Documentation</th></tr></thead>
<tbody>
<tr>
<td>Supported adding account permission</td>
<td>You can grant the RELOAD permission for the account for NewDTS data migration.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/237/7054" target="_blank">Managing Account</a></td></tr>
<tr>
<td>Supported downgrade for disaster recovery read-only instances </td>
<td>You can downgrade the disaster recovery read-only instances in the console.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/237/46722" target="_blank">Disaster Recovery Read-Only Instance</a></td></tr>
<tr>
<td>Optimized the display of available regions</td>
<td>You can view the region where resources are sold out when selecting a region, and select a random AZ in the console.</td>
<td>-</td></tr>
</tbody></table>

## September 2022
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=20%>Documentation</th></tr></thead>
<tbody>
<tr>
<td>Backup time optimization</td>
<td>The backup can be retained for 365 days and performed at your selected time.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/237/8487" target="_blank">Backup Mode</a></td></tr>
<tr>
<td>Backup search optimization</td>
<td>You can filter the cold backup list, binlog list, slow query, and error log by time.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/237/8486" target="_blank">Downloading Backup Files</a></td></tr>
<tr>
<td>Newly supported version for data encryption</td>
<td>TencentDB for MySQL 8.0 supports Transparent Data Encryption (TDE).</td>
<td><a href="https://www.tencentcloud.com/document/product/237/51134" target="_blank">Transparent Data Encryption (TDE)</a></td></tr>
<tr>
<td>Supported creating database in CDC</td>
<td>You can create MariaDB instances in CDC and manage them in the console.</td>
<td></td></tr>
</tbody></table>

## July 2022
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=20%>Documentation</th></tr></thead>
<tbody>
<tr>
<td>Public network security group</td>
<td>For instances with public network address enabled in Guangzhou, Chengdu, Shanghai, Beijing, Nanjing, security groups support public network access.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/237/35446" target="_blank">Security Group Configuration</a></td></tr>
<tr>
<td>Supported InnoDB page size setting when purchasing an instance</td>
<td>InnoDB page size is set to 16 KB by default, and it cannot be modified once the instance is created. Select a page size with caution.</td>
<td>-</td></tr>
<tr>
<td>Supported setting max connections for creating an account</td>
<td>The number of concurrent connections under this account is subjected to the maximum connections of the instance and can be set when creating an account for TencentDB for MariaDB 5.6 and 8.0.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/237/7054" target="_blank">Managing Account</a></td></tr>
<tr>
<td>Supported setting replica connection mode for read-only account</td>
<td>When setting the connection mode for read-only account, you can decide whether to switch to another replica if the primary-replica delay exceeds the delay parameter.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/237/7054" target="_blank">Managing Account</a></td></tr>
</tbody></table>

## January 2022
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=20%>Documentation</th></tr></thead>
<tbody>
<tr>
<td>Supported rollback to pay-as-you-go instances</td>
<td>The database rollback feature is updated, so data will be rolled back to pay-as-you-go instances instead of temp instances. After rollback to a pay-as-you-go instance, you can flexibly configure the retention time of the rollback instance based on your business needs. Rollback instances have the same functionality, security, and reliability as general instances.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/237/8719" target="_blank">Rolling back Databases</a></td></tr>
<tr>
<td>Supported modifying the parameters for disaster recovery read-only instances</td>
<td>You can modify the parameters for disaster recovery read-only instances in the console.</td>
<td>-</td></tr>
<tr>
</tbody></table>


## December 2021
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=20%>Documentation</th></tr></thead>
<tbody>
<tr>
<td>Supported AZ migration</td>
<td>The AZ migration feature is launched. It can implement nearby access and resource expansion for your business and better utilize resources in different AZs in the same region.</td>
<td>-</td></tr>
<tr>
<td>Supported custom old IP retention period	</td>
<td>When switching IP manually, you can customize the old IP retention period. In this way, IP resources can be released quickly or retained for a long time to allow for business migration.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/237/40160" target="_blank">Changing Networks</a></td></tr>
<tr>
<td>Supported modifying the read-only policy</td>
<td>You can modify the policy of a read-only account to satisfy different read-only access and delay requirements.</td>	
<td><a href="https://intl.cloud.tencent.com/document/product/237/35409" target="_blank">Read/Write Separation</a></td></tr>
</tbody></table>


## March 2021
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=20%>Documentation</th></tr></thead>
<tbody>
<tr>
<td>Cloud Monitor optimization</td>
<td>TencentDB for MongoDB now works with the latest version of Cloud Monitor, supporting dashboards, more monitoring metrics, and default alarms. The metric names are modified to better follow the naming conventions; and you can now use Cloud Monitor APIs to fetch TencentDB for MongoDB monitoring data.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/248/40014" target="_blank">TencentDB for MariaDB Monitoring Metrics</a></td></tr>
<tr>
<td>One-primary-multi-replica instances are supported</td>
<td>You can now create an instance with one primary node and up to five replica nodes, so as to provide higher data availability.</td>
<td>-</td></tr>
<tr>
<td>Supported modifying VPC configurations</td>
<td>You can now modify the access address of an instance via network translation.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/237/40160" target="_blank">Changing Networks</a></td></tr>
</tbody></table>

## October 2020
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=20%>Documentation</th></tr></thead>
<tbody>
<tr>
<td>Supported disaster recovery read-only instances</td>
<td>You can quickly create disaster recovery read-only instances in the console for data deployment and disaster recovery capability across regions and AZs </td>
<td><a href="https://intl.cloud.tencent.com/document/product/237/46722" target="_blank">Disaster Recovery Read-Only Instance</a></td></tr>
<tr>
<td>Supported instance architecture diagram.</td>
<td>You can view instance region, nodes, shards, and primary-replica relationship, or create a disaster recovery read-only instance sync in the instance architecture diagram in the console.</td>
<td>-</td></tr>
</tbody></table>

## August 2020
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=20%>Documentation</th></tr></thead>
<tbody>
<tr>
<td>Supported MySQL 8.0</td>
<td>You can now purchase TencentDB for MariaDB instances running the MySQL 8.0 kernel. Such instances support multi-thread async replication (MAR, namely strong sync), thread pools (enabled by default), and async deletion of big tables.</td>
<td>-</td></tr>
<tr>
<td>Supported tags</td>
<td>You can manage TencentDB for MariaDB instances by tag.</td>
<td>-</td></tr>
<tr>
<td>Supported DMC</td>
<td>You can now manage TencentDB for MariaDB instances in DMC.</td>
<td>-</td></tr>
<tr>
<td>Other features</td>
<td><li>You can now download the latest binlog, split and analyze it.<li>Related user interactions in the console are optimized.</td>
<td>-</td></tr>
</tbody></table>

## June 2015
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=20%>Documentation</th></tr></thead>
<tbody><tr>
<td>TencentDB for MariaDB is officially launched</td>
<td>TencentDB for MariaDB is a highly secure enterprise-grade cloud database dedicated to the online transaction processing (OLTP) scenario. It has always been used in Tencent's billing business. It is compatible with MySQL syntax and has various advanced features such as thread pool, audit, and remote disaster recovery while delivering easy scalability, simplicity, and high cost efficiency of TencentDB.
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/237/1054" target="_blank">Overview</a></td></tr>
</tbody></table>
