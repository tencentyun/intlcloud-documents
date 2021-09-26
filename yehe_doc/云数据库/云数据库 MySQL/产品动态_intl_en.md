## July 2021
<table>
<tr><th width=20%>Update</th><th width=50%>Description</th><th width=10%>Release Date</th><th width=20%>Documentation</th></tr>
<tbody>
<tr>
<td>QuickChange is supported</td>
<td>TencentDB for MySQL now supports QuickChange. If the physical machine where the instance is deployed has sufficient resources (aka local resources), you can adjust instance configuration in the QuickChange mode without migrating data. As less time is spent in the preparation stage, the overall adjustment process is faster.</td>
<td>2021-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/19707" target="_blank">Adjusting Database Instance Specification</a></td></tr>
</tbody></table>


## April 2021
<table>
<tr><th width=20%>Update</th><th width=50%>Description</th><th width=10%>Release Date</th><th width=20%>Document</th></tr>
<tbody>
<tr>
<td>Database proxy is supported</td>
<td>The database proxy provides a network proxy service between TencentDB and the application. It proxies all requests from the application to TencentDB.<br>The database proxy uses an access address independent from the original access address of a TencentDB instance. Requests using the proxy access address are relayed to source and replica database nodes by the proxy cluster. If read/write separation is enabled, read requests are relayed to read-only instances to reduce the load pressure of the source instance.</td>
<td>2021-04</td>
<td><a href="https://cloud.tencent.com/document/product/236/54652" target="_blank">Database Proxy</a></td></tr>
<tr>
<td>Binlogs take up the disk space</td>
<td>As the speed of writing to binlog affects database performance, TencentDB for MySQL now migrates the binlog files to high-performance SSDs (i.e., instance disk space) in order to improve database performance and stability.</td>
<td>2021-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/40209" target="_blank">Notice on Binlog Taking up the Disk Space</a></td></tr>
<tr>
<td>Local binlog retention period can be customized</td>
<td>You can now customize the retention period of local binlog files in the TencentDB for MySQL console.</td>
<td>2021-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/40186" target="_blank">Configuring Local Binlog Retention Policy</a></td></tr>
</tbody></table>

## March 2021
<table>
<tr><th width=20%>Update</th><th width=50%>Description</th><th width=10%>Release Date</th><th width=20%>Document</th></tr>
<tbody>
<tr>
<td>Instance architectures have been renamed</td>
<td>TencentDB for MySQL now supports three types of architectures including single-node (formerly Basic Edition), two-node (formerly High-Availability Edition), and three-node (formerly Finance Edition), and three resource isolation policies including basic, general, and dedicated policies. Renaming won't change any features of these architectures.</td>
<td>2021-03</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/236/38328" target="_blank">Database Architecture Overview</a><li><a href="https://intl.cloud.tencent.com/document/product/236/39794">Resource Isolation Policy</a></td></tr>
<tr>
<td>Read-only instances support exclusive private network addresses</td>
<td>You can now configure a custom and exclusive private network address (IP and port) for a read-only instance.</td>
<td>2021-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/7270" target="_blank">Creating Read-Only Instances</a></td></tr>
</tbody></table>

## November 2020
<table>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
<tbody>
<tr>
<td>Instances can be cloned</td>
<td>You can now restore a TencentDB for MySQL instance to any point in time within the log backup retention period or from a specific physical backup set by cloning.</td>
<td>2020-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/38864" target="_blank">Cloning Instances</a></td>
</tr>
</tbody></table>

## October 2020
<table>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
<tbody><tr>
<td>The purchase page is optimized</td>
<td>You can now specify alarm policies, parameter templates, and bind an instance with security groups of other projects on the purchase page.</td>
<td>2020-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/37785" target="_blank">Creating MySQL Instances</a></td>
</tr>
<tr>
<td>TDE is supported for MySQL v8.0</td>
<td>TencentDB for MySQL v8.0 now supports Transparent Data Encryption (TDE).</td>
<td>2020-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/38491" target="_blank">Enabling Transparent Data Encryption</a></td>
</tr>
</tbody></table>

## August 2020
<table>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
<tbody><tr>
<td>MySQL v8.0 is now supported</td>
<td>TencentDB for MySQL v8.0 is now supported. Combined with a complete set of management services and the TXSQL kernel, TencentDB for MySQL provides an enterprise-level database service that is more stable and quicker to deploy. It is applicable to a variety of use cases and helps you upgrade your business.</td>
<td>2020-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31896" target="_blank">Database Versions</a></td>
</tr>
</tbody></table>

## July 2020
<table>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
<tbody><tr>
<td>Parameter templates can be applied to instances</td>
<td>TencentDB for MySQL supports modifying parameters of multiple instances at the same time through parameter templates. You can perform a parameter modification task during the custom time window, or cancel it.</td>
<td>2020-07</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/236/35793" target="_blank">Setting Instance Parameters</a><li><a href="https://intl.cloud.tencent.com/document/product/236/31906" target="_blank">Managing Parameter Templates</a></td>
</tr>
<tr>
<td>Transparent Data Encryption (TDE) is supported</td>
<td>TencentDB for MySQL supports the transparent data encryption (TDE) feature. Transparent encryption means that the data encryption and decryption are imperceptible to users. TDE supports real-time I/O encryption and decryption of data files. It encrypts data before the data is written to disk, and decrypts data when the data is read into memory from disk, which meets the compliance requirements of static data encryption.</td>
<td>2020-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/38491" target="_blank">Enabling Transparent Data Encryption</a></td>
</tr>
</tbody></table>

## June 2020
<table>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
<tbody><tr>
<td>Manual kernel minor version upgrade is supported</td>
<td>TencentDB for MySQL supports manual kernel minor version upgrade. The upgrade can add new features, improve the performance, and fix issues.</td>
<td>2020-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/36816" target="_blank">Upgrading Kernel Minor Version</a></td>
</tr>
</tbody></table>

## April 2020
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>One-source-two-replica High-Availability Edition is renamed as Finance Edition</td>
<td>The Finance Edition adopts a one-source-two-replica architecture (three nodes in total) and supports strong sync replication. It guarantees strong data consistency through real-time hot backup to provide finance-grade reliability and high availability.</td>
<td>2020-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/17136" target="_blank">Database Architecture</a></td>
</tr>
<tr>
<td>Repossession time for the old IP address can be customized</td>
<td>The repossession time of the old IP address can be customized between 0 and 168 hours when the network is switched. If the repossession time is set to 0 hours, the old IP address will be repossessed immediately after the network switch.</td>
<td>2020-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31915" target="_blank">Network Switch</a></td>
</tr>
</tbody></table>

## January 2020

<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>TencentDB for DBbrain is supported</td>
<td>TencentDB for DBbrain (DBbrain) is an intelligent database diagnosis and optimization product. It provides real-time database protection, locates causes of and offers solutions to database exceptions, and helps with exception prevention at the source.</td>
<td>2020-01</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/36027" target="_blank">TencentDB for DBbrain</a></td>
</tr>
<tr>
<td>Slow log and error log details can now be queried</td>
<td>TencentDB for MySQL instances (excluding the Basic Edition) now provide an operation log management feature. You can view the slow log details, error log details, rollback logs of an instance and download slow logs on the operation logs page in the console.</td>
<td>2020-01</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/34588" target="_blank">Operation Log</a></td>
</tr>
</tbody></table>

## December 2019

<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>MySQL backup is now a paid service</td>
<td>TencentDB for MySQL will start charging for the usage of instance backup space exceeding the free tier. Improvements will be made for data compression, backup stability and availability. You can shorten retention periods and lower backup frequencies to reduce your backup capacity costs.</td>
<td>2019-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/32344" target="_blank">Backup Space Billing</a></td>
</tr>
</tbody></table>

## November 2019
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Event alarming is now supported</td>
<td>By subscribing to events such as OOM, source-replica switch, read-only instance removal, and instance migration caused by server failure, you can now stay on top of your instance statuses.</td>
<td>2019-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/8457" target="_blank">Alarming Feature</a></td>
</tr>
</tbody></table>

## September 2019

<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Database backup page is available</td>
<td>We have released the TencentDB for MySQL database backup page. It is divided into two sections: overview and backup list. Backup trends and statistics can be viewed in the overview tab. Backup data details and log backups can be found in the backup list.</td>
<td>2019-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/33131" target="_blank">Viewing Backup Capacity</a></td>
</tr>
</tbody></table>

## May 2019

<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Automatic backups are fully upgraded to physical backup</td>
<td>TencentDB for MySQL now only supports physical automatic backups. Existing logical automatic backups will be switched to the physical type automatically. If you need logical backups, you can use the manual backup feature in the TencentDB for MySQL console or call APIs.</td>
<td>2019-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/32340" target="_blank">Backup Mode</a></td>
</tr>
<tr>
<td>Nanjing Zone 1 is now available</td>
<td>TencentDB for MySQL is now available in Nanjing Zone 1. With this new AZ, TencentDB for MySQL is now available in two regions in East China: Shanghai and Nanjing.</td>
<td>2019-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/8458" target="_blank">Regions and AZs</a></td>
</tr>
</tbody></table>

## March 2019

<div class="doc-table-wrap"><table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Switching between VPCs is now supported</td>
<td>Switching between VPCs is now supported. A single TencentDB instance can now be switched from VPC A to VPC B.</td>
<td>2019-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31915" target="_blank">Network Switch</a></td>
</tr>
</tbody></table></div>

## February 2019

<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>One-click connectivity check is now supported</td>
<td>A one-click connectivity check is now provided in the console to help you quickly locate internal and external connectivity problems and offer corresponding solutions.</td>
<td>2019-02</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31927" target="_blank">One-Click Connectivity Checker</a></td>
</tr>
</tbody></table>

## June 2018

<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Basic Edition instances are now purchasable</td>
<td>TencentDB for MySQL Basic Edition adopts a single-node deployment method with computation-storage separation. If a computing node fails, the system can switch to a healthy one for quick recovery. Premium cloud disks are used as the underlying storage media of the Basic Edition, which feature high quality, cost-effectiveness, stability, and performance, making them suitable for 90% of I/O scenarios.</td>
<td>2018-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/17136" target="_blank">Database Architecture</a></td>
</tr>
<tr>
<td>Network switching is now supported</td>
<td>Switching between the classic network and VPC and between subnets in the same VPC is now supported.</td>
<td>2018-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31915" target="_blank">Network Switch</a></td>
</tr>
<tr>
<td>Self-service connectivity check is now supported</td>
<td>You can now quickly check the connectivity status of your databases.</td>
<td>2018-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31927" target="_blank">One-Click Connectivity Checker</a></td>
</tr>
<tr>
<td>Downgrading and refunding are now supported</td>
<td>You can now downgrade your database configuration and be refunded accordingly.</td>
<td>2018-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/32345" target="_blank">Instance Adjustment Fee</a></td>
</tr>
<tr>
<td>MySQL 5.7 data migration is now supported</td>
<td>DTS now supports migrating MySQL 5.7.</td>
<td>2018-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/34103" target="_blank">Online Import of MySQL Data</a></td>
</tr>
<tr>
<td>Product is renamed</td>
<td>CDB for MySQL is renamed as TencentDB for MySQL.</td>
<td>2018-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236" target="_blank">TencentDB for MySQL</a></td>
</tr>
</tbody></table>

## August 2017

<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Read-only instances support elastic specifications</td>
<td>A read-only instance can now adopt a different specification from that of its source instance.</td>
<td>2017-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/7270" target="_blank">Read-Only Instances</a></td>
</tr>
<tr>
<td>Monitoring at a 1-minute granularity is now supported</td>
<td>Monitoring can now be performed at a 1-minute granularity.</td>
<td>2017-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/8455" target="_blank">Monitoring Feature</a></td>
</tr>
<tr>
<td>Physical backup is now supported</td>
<td>Data can now be stored through physical backups.</td>
<td>2017-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/32340" target="_blank">Backup Mode</a></td>
</tr>
<tr>
<td>Manual backup is now supported</td>
<td>You can now customize the backup time and retention period (up to 732 days)</td>
<td>2017-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/32340" target="_blank">Backup Mode</a></td>
</tr>
<tr>
<td>Security group is now supported</td>
<td>A security group is a stateful virtual firewall capable of filtering. As an important means for network security isolation provided by Tencent Cloud, it can be used to set network access controls for one or more TencentDB instances.</td>
<td>2017-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/14470" target="_blank">TencentDB Security Group</a></td>
</tr>
<tr>
<td>Data subscription is now supported</td>
<td>DTS can now help you get incrementally updated data in TencentDB in real time, so that you can consume incremental data based on your business needs.</td>
<td>2017-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/8774" target="_blank">Data Subscription</a></td>
</tr>
<tr>
<td>Data migration between TencentDB instances is now supported</td>
<td>DTS is now compatible with more types of network environments.</td>
<td>2017-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/34103" target="_blank">Online Import of MySQL Data</a></td>
</tr>
</tbody></table>

## June 2017

<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>MySQL 5.7 is now supported</td>
<td>MySQL 5.7 (Percona server) is now supported as well as MySQL 5.6 kernel. Native capabilities such as horizontal scaling and read/write separation are also supported. </td>
<td>2017-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31896" target="_blank">Database Version</a></td>
</tr>
</tbody></table>

## March 2016

<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Read-only instance feature is available</td>
<td>TencentDB for MySQL allows you to create one or more read-only instances, which are suitable for read/write separation and one-source-multiple-replica application scenarios and capable of greatly enhancing the read load capacity of your database.</td>
<td>2016-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/7270" target="_blank">Read-Only Instances</a></td>
</tr>
<tr>
<td>Pay-as-You-Go instances are now supported</td>
<td>Database services can now be billed by the hour.</td>
<td>2016-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/18335" target="_blank">Billing Overview</a></td>
</tr>
</tbody></table>
