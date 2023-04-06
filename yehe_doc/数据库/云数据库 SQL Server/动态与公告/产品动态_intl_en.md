## March 2023
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Document</th></tr></thead>
<tbody>
<tr>
<td>Added cloud disk types for single-node instances</td>
<td>A TencentDB for SQL Server single-node (formerly Basic Edition) instance of cloud disk edition supports mounting Balanced and Enhanced SSD cloud disks of up to 32 TB in all regions, making it easier to flexibly sustain more business load scenarios.</td>
<td>2023-03-02</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/46490" target="_blank">Storage Type</a></td></tr>
<tr>
<td>Fully released the two-node architecture of cloud disk edition</td>
<td>TencentDB for SQL Server has fully released the new two-node architecture of cloud disk edition in Beijing, Shanghai, Guangzhou, Chengdu, Chongqing, Nanjing, Hong Kong (China), and Singapore regions. It has all the features of the two-node architecture of local disk edition, offers more flexible CPU/memory specifications, and supports mounting Balanced and Enhanced SSD cloud disks of up to 32 TB in all regions.</td>
<td>2023-03-02</td>
<td><a href="https://www.tencentcloud.com/document/product/238/53977" target="_blank">Instance Architecture</a></td></tr>
</tbody></table>

## February 2023
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Document</th></tr></thead>
<tbody>
<tr>
<td>Optimized backup restoration</td>
<td>TencentDB for SQL Server optimizes the backup restoration and supports task editing, database renaming, and multiple COS file formats </td>
<td>2023-02-14</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/39005" target="_blank">Cold Backup Migration</a></td></tr>
<tr>
<td>Account type and permission modification</td>
<td>TencentDB for SQL Server launched a new database account type and permission logic to better help you manage your accounts.</td>
<td>2023-02-09</td>
<td></td></tr>
<tr>
<td>Added monitoring metrics</td>
<td>The RO sync delay time is added for TencentDB for SQL Server to monitor the data sync delay time between the primary and the replica instance.</td>
<td>2023-02-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/46502" target="_blank">Monitoring Metrics</a></td></tr>
<tr>
<td>Try out two-node cloud disk architecture</td>
<td>TencentDB for SQL Server launched two-node cloud disk edition instance, which is fully compatible with all features of the two-node local disk instance. Its performance is comparable to that of a local SSD, allowing you to easily handle various business scenarios that require high performance, concurrency, and availability. It has more flexible CPU/memory specification ratios, supports general and enhanced SSD cloud disks, and can store up to 32 TB of data. <br>In addition, the formerly high-availability/cluster editions are renamed as two-node, and the formerly basic edition as single-node for tryout. To use it in advance, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application. </td>
<td>2023-02-09</td>
<td></td></tr>
</tbody></table>


## January 2023
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Document</th></tr></thead>
<tbody>
<tr>
<td>Supported cross-account data migration</td>
<td>TencentDB for SQL Server supports cross-account data migration between instances with DTS</td>
<td>2023-01-13</td>
<td><a href="https://www.tencentcloud.com/document/product/238/53570" target="_blank">Across-Account Migration with DTS</a></td></tr>
</tbody></table>

## December 2022
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Document</th></tr></thead>
<tbody>
<tr>
<td>Supported version upgrade for Basic Edition</td>
<td>Self-service version upgrade is supported for TencentDB for SQL Server Basic Edition instances.</td>
<td>2022-12-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/44354" target="_blank">Adjusting Instance Version</a></td></tr>
<tr>
<td>Supported cross-AZ migration for Basic Edition</td>
<td>Cross-AZ migration is supported for TencentDB for SQL Server Basic Edition instances. All attributes and configurations (including the private network address and the subnet) of the instances remain unchanged after migration.</td>
<td>2022-12-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/42695" target="_blank">Migrating Across AZs</a></td></tr>
<tr>
<td>Optimized the console and features</td>
<td>The TencentDB for SQL Server team has made the following optimizations on the product features and console display to further improve the user experience: <ul><li>The replica AZ field is added in the instance list in the console, which can display the primary and replica AZs and multi-AZ status of the instance. </li><li>The database list and account list support fuzzy search by database or account name.</li></ul></td>
<td>2022-12-12</td>
<td>-</td></tr>
</tbody></table>

## November 2022
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Document</th></tr></thead>
<tbody>
<tr>
<td>Supported archive backup</td>
<td>TencentDB for SQL Server automatic backup supports setting archive backup retention and non-archive backup retention. You can use this feature to back up data by scheduling two cycles, which reduces the costs compared with a single-cycle backup policy.</td>
<td>2022-11-22</td>
<td><a href="https://www.tencentcloud.com/document/product/238/51892" target="_blank">Setting Archive Backup Retention</a></td></tr>
</tbody></table>

## October 2022
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Document</th></tr></thead>
<tbody>
<tr>
<td>Added monitoring metrics.</td>
<td>New metrics are available for TencentDB for SQL Server 2014 and later, including internally locked/used memory.</td>
<td>2022-10-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/46502" target="_blank">Monitoring Metrics</a></td></tr>
</tbody></table>

## September 2022
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Document</th></tr></thead>
<tbody>
<tr>
<td>Optimized operations for security group binding</td>
<td>TencentDB for SQL Server security groups can be unbound from projects and support multi-selection and fuzzy search capabilities.</td>
<td>2022-09-16</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/35789" target="_blank">Configuring Security Group</a></td></tr>
</tbody></table>

## November 2022
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody>
<tr>
<td>Supported archive backup</td>
<td>TencentDB for SQL Server automatic backup supports setting archive backup retention and non-archive backup retention. You can use this feature to back up data by scheduling two cycles, which reduces the costs compared with a single-cycle backup policy.</td>
<td>2022-11-22</td>
<td><a href="https://www.tencentcloud.com/document/product/238/51892" target="_blank">Setting Archive Backup Retention</a></td></tr>
</tbody></table>

## October 2022
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody>
<tr>
<td>Added monitoring metrics.</td>
<td>New metrics are available for TencentDB for SQL Server 2014 and later, including internally locked/used memory.</td>
<td>2022-10-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/46502" target="_blank">Monitoring Metrics</a></td></tr>
</tbody></table>

## September 2022
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody>
<tr>
<td>Optimized operations for security group binding</td>
<td>TencentDB for SQL Server security groups can be unbound from projects and support multi-selection and fuzzy search capabilities.</td>
<td>2022-09-16</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/35789" target="_blank">Configuring Security Group</a></td></tr>
</tbody></table>

## August 2022
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody><tr>
<td>Supported modifying the system character set collation and time zone of instances</td>
<td>TencentDB for SQL Server allows you to set the system character set collation and time zone when purchasing an instance.</td>
<td>2022-08-25</td>
<td><ul><li><a href="https://www.tencentcloud.com/document/product/238/50258" target="_blank">Modifying Instance-Level Character Set Collation</a></li><li><a href="https://www.tencentcloud.com/document/product/238/50257" target="_blank">Modifying System Time Zone</a></li></ul></td></tr>
<tr>
<td>Launched the service in Hong Kong Zone 3</td>
<td>TencentDB for SQL Server is now available in Hong Kong Zone 3 in Dual-Server High Availability Edition and Cluster Edition.</td>
<td>2022-08-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/7520" target="_blank">Regions and AZs</a></td></tr>
</tbody></table>

## July 2022
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody><tr>
<td>Supported public network access</td>
<td>TencentDB for SQL Server supports public network access. After this feature is enabled, an instance can be accessed at its public network address.</td>
<td>2022-07-25</td>
<td><a href="https://www.tencentcloud.com/document/product/238/50230" target="_blank">Enabling/Disabling Public Network Address</a></td></tr>
<tbody><tr>
<td>Supported cross-region backup</td>
<td>TencentDB for SQL Server supports cross-region backup to ensure the high availability, security, and recoverability of data and implement various features, such as remote backup and restoration, remote disaster recovery, long-term data archive, and regulatory compliance. </td>
<td>2022-07-20</td>
<td><a href="https://www.tencentcloud.com/document/product/238/49138" target="_blank">Cross-Region Backup</a></td></tr>
</tbody></table>

## June 2022
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody><tr>
<td>Optimized the console and features</td>
<td>The TencentDB for SQL Server team makes the following optimizations in the product feature and console UI to further improve the user experience.<br><li>Manual backups in the specified time range can be batch deleted.<br><li>The backup name can contain up to 128 characters.<br><li>The visual display of the backup space trend chart is optimized in the console.<br><li>You can search for slow query files in the specified time range.<br><li>On the purchase page, VPC, subnet, and project lists support exact and fuzzy searches. <br><li>The display order of system monitoring metrics is adjusted in the console.<br><li>The logic to set the instance maintenance cycle is optimized. You need to select at least one maintenance cycle to guarantee the database Ops security.<br><li>A quick redirect link is added to the VPC console to quickly query the TencentDB for SQL Server instances bound to VPCs.</td>
<td>2022-06-22</td>
<td>-</td></tr>
<tbody><tr>
<td>Released the SSIS feature</td>
<td>TencentDB for SQL Server business intelligence server is released, which supports SQL Server Integration Services (SSIS). SSIS can be used to sustain complex business scenarios, such as merging data from heterogeneous data stores, cleansing and standardizing data, populating data warehouses and datasets, transforming data for complex business logic, supporting management features, and automating data loading. It helps meet your diversified needs in various use cases, including BI analysis, high-value data mining, and primary data management system setup.</td>
<td>2022-06-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/48060" target="_blank">Overview</a></td></tr>
</tbody></table>

## May 2022
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody>
<tr>
<td>Supported data migration over CCN</td>
<td>When you use DTS to migrate data to TencentDB for SQL Server, the source database can interconnect with the VPC over CCN.</td>
<td>2022-05-30</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/39006" target="_blank">Migrating Data with DTS</a></td></tr>
<tr>
<td>Supported Korean character sets</td>
<td>You can select a Korean character set during TencentDB for SQL Server instance creation.</td>
<td>2022-05-30</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/35780" target="_blank">Creating Database</a></td></tr>
<tr>
<td>Release new documents</td>
<td>Documents such as FAQs, Constraints and Limits, Usage Specifications and Suggestions are added to help you better use TencentDB for SQL Server.</td>
<td>2022-05-27</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/238/47719" target="_blank">FAQs</a>
<li><a href="https://intl.cloud.tencent.com/document/product/238/2021" target="_blank">Constraints and Limits</a>
<li><a href="https://intl.cloud.tencent.com/document/product/238/48122" target="_blank">Usage Specifications and Suggestions</a></td></tr>
</tbody></table>


## March 2022
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody><tr>
<td>Supported concurrently executing multiple tasks at the database level</td>
<td>TencentDB for SQL Server allows you to execute up to five concurrent tasks, including backup, restoration, account authorization, database deletion, and renaming, in different databases in the same instance under the same account.</td>
<td>2022-03-14</td>
<td>-</td></tr>
</tbody></table>

## February 2022
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody>
<tr>
<td>Released the commercial edition of the backup feature</td>
<td>The commercial edition of the backup feature of TencentDB for SQL Server is released, which supports customizing the automatic backup policy. Data backup supports custom retention period and cycle, and log backup supports view and download.<br>The backup statistics overview of all instances is added. You can quickly view the backup space statistics and trends of all instances in each region under your account, free tier usage, as well as the real-time backup space statistics of each instance.</td>
<td>2022-02-15</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/238/45852" target="_blank">Viewing Backup List</a>
<li><a href="https://intl.cloud.tencent.com/document/product/238/45850" target="_blank">Viewing Backup Space</a>
<li><a href="https://intl.cloud.tencent.com/document/product/238/45849" target="_blank">Backup Space Billing</a></td></tr>
<tr>
<td>Optimized the system monitoring feature</td>
<td>The system monitoring page in the TencentDB for SQL Server console is optimized to support full-screen data display, time comparison, monitoring granularity configuration, and data export.</td>
<td>2022-02-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/46503" target="_blank">Viewing Monitoring Chart</a></td></tr>
<tbody><tr>
</tbody></table>

## January 2022
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody>
<tr>
<td>Supported SSD cloud disks on Basic Edition</td>
<td>You can use SSD cloud disks on TencentDB for SQL Server Basic Edition with a specification of up to 24-core 96 GB MEM.</td>
<td>2022-01-20</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/32561" target="_blank">Performance Test Report</a></td></tr>
<tr>
<td>Supported setting instance remarks</td>
<td>TencentDB for SQL Server allows you to edit instance remarks in the console for easier instance identification and management.</td>
<td>2022-01-17</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/46507" target="_blank">Setting Instance Remarks</a></td></tr>
<tr>
<td>Supported switching from classic network to VPC</td>
<td>TencentDB for SQL Server allows you to switch from the classic network to VPC in the console for easier network management based on your business requirements.</td>
<td>2022-01-14</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/46498" target="_blank">Switching from Classic Network to VPC</a></td></tr>
<tr>
<td>Supported specifying IP for VPC</td>
<td>TencentDB for SQL Server allows you to change the instance network in the console. You can change from VPC A to VPC B in another AZ in the same region and specify the subnet IP.</td>
<td>2022-01-14</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/46497" target="_blank">Changing Network (from VPC to VPC)</a></td></tr>
</tbody></table>

## December 2021
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody><tr>
<td>Supported self-service configuration adjustment</td>
<td>TencentDB for SQL Server supports self-service instance configuration adjustment in the console, including architecture/version upgrade and CPU/memory/disk scaling. It offers multiple adjustment modes, such as concurrent scaling and differentiated scaling, and displays reminders for the adjustment impact in different scenarios.</td>
<td>2021-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/44352" target="_blank">Overview</a></td></tr>
</tbody></table>

## November 2021
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody><tr>
<td>Launched the updated data migration feature (new)	</td>
<td>The updated data migration feature (new) is launched, and the old data migration feature has been disused and will be deactivated on March 1, 2022. The new feature has more data migration capabilities.</td>
<td>2021-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42638" target="_blank">Migration from SQL Server to TencentDB for SQL Server</a></td></tr>
<tr>
<td>Launched the service in Chongqing region</td>
<td>TencentDB for SQL Server is now available in Chongqing Zone 1.</td>
<td>2021-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/7520" target="_blank">Regions and AZs</a></td></tr>
</tbody></table>

## October 2021
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody><tr>
<td>Supported cross-AZ migration	</td>
<td>You can now migrate an instance to another AZ in the same region. All attributes and configurations (including the private network address and the subnet) of the instance remain unchanged after migration.</td>
<td>2021-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/42695" target="_blank">Migrating Across AZs</a></td></tr>
</tbody></table>

## September 2021
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody><tr>
<td>Updated the performance test report</td>
<td>TencentDB for SQL Server has been comprehensively upgraded with the new ultra-high specification of 90 cores, 720 GB MEM, and 4.5 million TPM. Both performance and cost performance have been improved by more than 30% once again, breaking Tencent Cloud's own performance record in the industry. Besides, the performance test report now covers the high availability edition and basic edition instances.</td>
<td>2021-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/32561">Performance Test Report</a></td></tr>
<tr>
<td>Supported unarchived backup files upload to COS</td>
<td>By default, backup files (i.e., .bak files) will be archived into a .tar file and then uploaded to COS. If you select "Unarchived files" here, the .bak file of each database in the instance will be directly uploaded to COS without being archived, which means that you can now download the backup file of a single database.</td>
<td>2021-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/35790">Creating and Viewing Backup Task</a></td></tr>
<tr>
<td>Supported backup on the replica node</td>
<td>You can now back up data at the replica node of a cluster edition 2017/2019 instance.</td>
<td>2021-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/35790">Creating and Viewing Backup Task</a></td></tr>
<tr>
<td>Launched the service in Bangkok region</td>
<td>TencentDB for SQL Server is now available in Bangkok Zones 1 and 2.</td>
<td>2021-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/7520">Regions and AZs</a></td></tr>
<tr>
<td>Launched the service in Singapore region</td>
<td>TencentDB for SQL Server is now available in Singapore Zone 2.</td>
<td>2021-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/7520">Regions and AZs</a></td></tr>
<tr>
<td>Launched the service in Jakarta region</td>
<td>TencentDB for SQL Server is now available in Jakarta Zone 2.</td>
<td>2021-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/7520">Regions and AZs</a></td></tr>
</tbody></table>

## August 2021
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody><tr>
<td>Launched the service in Beijing Zone 6	</td>
<td>	TencentDB for SQL Server is now available in Beijing Zone 6.</td>
<td>2021-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/7520" target="_blank">Regions and AZs</a></td></tr>
<tr>
<td>Launched the service in Guangzhou Zone 7</td>
<td>TencentDB for SQL Server is now available in Guangzhou Zone 7.</td>
<td>2021-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/7520" target="_blank">Regions and AZs</a></td></tr>
</tbody></table>

## July 2021
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody><tr>
<td>Supported configuring change data capture (CDC)</td>
<td>You can configure CDC in the console on your own. CDC records the information of all changes in a table and the median values of changed data entries, which help you better track table changes.</td>
<td>2021-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/41608" target="_blank">Setting Change Data Capture (CDC)</a></td></tr>
<tr>
<td>Supported configuring change tracking (CT)</td>
<td>You can configure CT in the console on your own. CT records modifications of table rows and allows you to directly get the latest data from the track table.</td>
<td>2021-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/41607" target="_blank">Setting Change Tracking (CT)</a></td></tr>
<tr>
<td>Supported configuring database shrinking</td>
<td>You can directly shrink database in the console to avoid space waste.</td>
<td>2021-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/41606" target="_blank">Shrinking Database</a></td></tr>
<tr>
<td>Supported configuring parameters in the console</td>
<td>You can view and directly modify parameters in the console and view parameter modification logs, which make parameter modification easier.</td>
<td>2021-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/41609" target="_blank">Setting Instance Parameters</a></td></tr>
<tr>
<td>Launched 11 new system and instance monitoring metrics</td>
<td>Four memory and lock performance counter monitoring metrics and seven physical machine system monitoring metrics are added for enterprise-grade users to comprehensively monitor database performance.</td>
<td>2021-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/7524" target="_blank">Monitoring</a></td></tr>
</tbody></table>

## June 2021
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody><tr>
<td>Launched high-specification instances</td>
<td>Dual-Server High Availability Edition, Cluster Edition, and read-only instances are now available in 64-core 512 GB MEM and 90-core 720 GB MEM specifications, meeting the needs of enterprise users.</td>
<td>2021-06</td>
<td>-</td></tr>
<tr>
<td>Launched the service in Tokyo Zone 2</td>
<td>TencentDB for SQL Server is now available in Tokyo Zone 2.</td>
<td>2021-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/7520" target="_blank">Regions and AZs</a></td></tr>
</tbody></table>

## May 2021
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody><tr>
<td>Launched TencentDB for SQL Server 2019</td>
<td>TencentDB for SQL Server 2019 is officially launched and supports Basic, High Availability, and Cluster Edition instances, which have great improvements in performance, ease of use, high availability, and security.</td>
<td>2021-05</td>
<td>-</td></tr>
<tr>
<td>Launched the service in Beijing Zone 7</td>
<td>TencentDB for SQL Server is now available in Beijing Zone 7.</td>
<td>2021-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/7520" target="_blank">Regions and AZs</a></td></tr>
</tbody></table>

## December 2020
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody><tr>
<td>Supported self-service version and architecture upgrade</td>
<td>You can upgrade the version and architecture and scale instances in the console in a self-service manner to easily adjust instances based on your business needs.</td>
<td>2020-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/44352" target="_blank">Overview</a></td></tr>
</tbody></table>

## November 2020
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody><tr>
<td>Supported the use of tags</td>
<td>TencentDB for SQL Server supports using tags. You can use tags to mark different resource usages, users, and business scenarios under your account.</td>
<td>2020-11</td>
<td>-</td></tr>
<tr>
<td>Launched the service in Chengdu region</td>
<td>TencentDB for SQL Server is now available in Chengdu region.</td>
<td>2020-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/7520" target="_blank">Regions and AZs</a></td></tr>
</tbody></table>

## October 2020
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody><tr>
<td>Supported migration with DTS and optimized cold backup migration</td>
<td>DTS supports data migration from self-built SQL Server databases in IDCs, clouds, and other cloud vendors to TencentDB for SQL Server as well as data migration between TencentDB for SQL Server instances.<br>Cold backup migration restores data from .bak files, which is applicable to data migration from SQL Server databases in other cloud vendors and self-built SQL Server databases to TencentDB for SQL Server. Multiple migration methods deliver an easier and more user-friendly data migration experience.</td>
<td>2020-10</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/238/39005" target="_blank">Cold Backup Migration</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/39006" target="_blank">Migrating Data with DTS</a></li></td></tr>
</tbody></table>

## July 2020
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody><tr>
<td>Launched TencentDB for SQL Server Basic (Standalone) Edition</td>
<td>TencentDB for SQL Server Basic Edition is launched, which supports cloud `sysadmin` permissions. It provides a complete set of genuinely licensed database solutions with high availability, security, and performance and light Ops.</td>
<td>2020-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/3254" target="_blank">Architecture</a></td></tr>
</tbody></table>

## March 2020
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody><tr>
<td>Supported admin accounts</td>
<td>TencentDB for SQL Server supports admin permissions. An admin has read/write permissions for all databases on the instance and thread management permissions and can automatically discover new databases and get their read/write permissions.</td>
<td>2020-03</td>
<td>-</td></tr>
</tbody></table>

## January 2020
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody><tr>
<td>Supported Always On clusters</td>
<td>TencentDB for SQL Server 2017 Enterprise Edition instances supports adding read-only instances. The underlying Always On architecture implements the control of cluster capabilities, such as automated data replication, traffic load balancing of read-only instances, and primary/replica switch of primary instances.</td>
<td>2020-01</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/3254" target="_blank">Architecture</a></td></tr>
</tbody></table>

## December 2019
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody><tr>
<td>Supported setting device maintenance time</td>
<td>TencentDB for SQL Server supports setting the maintenance time. To ensure the stability of your TencentDB instance, the backend system performs maintenance operations on the instance during the maintenance time at irregular intervals.</td>
<td>2019-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/35785" target="_blank">Setting Instance Maintenance Information</a></td></tr>
</tbody></table>

## October 2019
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody><tr>
<td>Supported configuring security groups</td>
<td>A <a href="https://www.tencentcloud.com/document/product/213/12452">security group</a> is a stateful virtual firewall capable of filtering. As an important means for network security isolation, it can be used to set network access controls for one or more TencentDB instances.</td>
<td>2019-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/35789" target="_blank">Configuring Security Group</a></td></tr>
<tr>
<td>Supported recycle bin</td>
<td>After a pay-as-you-go instance expires or is manually terminated, it can be automatically put in the recycle bin for retention.</td>
<td>2019-10</td>
<td>-</td></tr>
</tbody></table>

## September 2019
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody><tr>
<td>Supported creating databases with multiple character sets available in the console</td>
<td>TencentDB for SQL Server supports multiple SQL Server character sets provided by Microsoft in the console for your choice when creating databases.</td>
<td>2019-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/35780" target="_blank">Creating Database</a></td></tr>
</tbody></table>

## July 2019
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody><tr>
<td>Launched the service in Seoul region</td>
<td>TencentDB for SQL Server is now available in Seoul region.</td>
<td>2019-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/7520" target="_blank">Regions and AZs</a></td></tr>
</tbody></table>

## June 2019
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody><tr>
<td>Supported pay-as-you-go billing mode</td>
<td>TencentDB for SQL Server supports the pay-as-you-go billing mode. You can select a billing mode based on your business needs.</td>
<td>2019-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/35798" target="_blank">Billing Overview</a></td></tr>
</tbody></table>

## May 2019
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody><tr>
<td>Supported instance configuration upgrade</td>
<td>The database instance specification can be upgraded, and the capacity can be expanded.</td>
<td>2019-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/44352" target="_blank">Overview</a></td></tr>
</tbody></table>

## September 2017
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody><tr>
<td>Launched SQL Server 2016</td>
<td>TencentDB for SQL Server is now available on SQL Server 2016.</td>
<td>2017-09</td><td>-</td>
</tr>
</tbody></table>

## December 2016
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody><tr>
<td>Supported read-only mode for replica servers</td>
<td>TencentDB for SQL Server supports read-only mode for replica servers. You can select memory and disks as needed to tailor the database specification for your actual business. The read-only mode is implemented through snapshots, facilitating online data analysis. It doesn't increase the costs, affect the primary database performance, or compromise high availability.</td>
<td>2016-12</td><td>-</td>
</tr>
</tbody></table>

## May 2016
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody><tr>
<td>Supported SQL Server 2012 Enterprise Edition</td>
<td>TencentDB for SQL Server is now available on SQL Server 2012 Enterprise Edition, which is compatible with all features of SQL Server 2008.</td>
<td>2016-05</td><td>-</td>
</tr>
</tbody></table>

## December 2015
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=15%>Release Date</th><th width=15%>Documentation</th></tr></thead>
<tbody><tr>
<td>Launched TencentDB for SQL Server officially</td>
<td>TencentDB for SQL Server is officially launched and provides various features such as instance management, instance details, system monitoring, database management, account management, and backup.</td>
<td>2015-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/2016" target="_blank">Product Overview</a></td></tr>
</tbody></table>
