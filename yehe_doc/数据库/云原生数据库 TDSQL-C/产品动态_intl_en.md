## November 2021
<table>
<tr><th width=20%>Update</th><th width=50%>Description</th><th width=10%>Release Date</th><th width=20%>Documentation</th></tr>
<td>Supported multi-AZ deployment</td>
<td>The engine of TDSQL-C for MySQL allows deploying a cluster across AZs. A multi-AZ cluster has superior disaster recovery capabilities than a single-AZ cluster and can protect your database against database instance failures, AZ outages, and even IDC-level failures.</td>
<td>2021-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1098/44327" target="_blank">Overview</a></td></tr>
</table>

## October 2021
<table>
<tr><th width=20%>Update</th><th width=50%>Description</th><th width=10%>Release Date</th><th width=20%>Documentation</th></tr>
<tr>
<td>Supported data subscription</td>
<td>DTS supports the migration of various relational databases including TDSQL-C for MySQL as well as NoSQL databases. You can use data subscription to meet your requirements for commercial data mining and async business decoupling.</td>
<td>2021-10</td>
<td><a href="https://cloud.tencent.com/document/product/571/52412" target="_blank">Data Subscription</a></td></tr>
<td>Supported automatic fragmented space reclaim</td>
<td>TDSQL-C for MySQL can automatically reclaim fragmented space after data deletion, which reduces the storage costs.</td>
<td>2021-10</td>
<td>-</td></tr>
</table>

## September 2021
<table>
<tr><th width=20%>Update</th><th width=50%>Description</th><th width=10%>Release Date</th><th width=20%>Documentation</th></tr>
<tr>
<td>Supported MySQL 8.0</td>
<td>The engine kernel of TDSQL-C for MySQL now supports MySQL 8.0. Combined with a complete set of management services and proprietary kernel features, it provides more stable and faster cloud native database services that are easier to deploy in more industries and help upgrade your business. (Currently, this version doesn't support adding read-only instances.)</td>
<td>2021-09</td>
<td>-</td></tr>
<tr>
<td>Supported instant DDL</td>
<td>TDSQL-C for MySQL supports the instant DDL feature to quickly modify columns in big tables while avoiding data replication. This feature can implement changes in seconds without replicating data or using disk capacity or I/O during peak hours.</td>
<td>2021-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1098/44589" target="_blank">Instant DDL Overview</a></td></tr>
</table>

## June 2021
<table>
<tr><th width=20%>Update</th><th width=50%>Description</th><th width=10%>Release Date</th><th width=20%>Documentation</th></tr>
<tr>
<td>Supported monthly subscription for storage billing</td>
<td>The monthly subscription (prepaid) billing mode is supported for storage. If you have a monthly-subscribed compute node in non-serverless mode, you can select monthly subscription for storage.</td>
<td>2021-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1098/40620" target="_blank">Billing Overview</a></td></tr>
<tr>
<td>Upgraded the computing power specification of the serverless mode</td>
<td>In serverless billing mode, the elastic computing power can be configured to up to 16 cores.</td>
<td>2021-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1098/40618" target="_blank">Serverless Service</a></td></tr>
</table>

## May 2021
<table>
<tr><th width=20%>Update</th><th width=50%>Description</th><th width=10%>Release Date</th><th width=20%>Documentation</th></tr>
<tr>
<td>Supported database audit in TDSQL-C</td>
<td>TDSQL-C for MySQL 5.7 supports database audit to log the fine-grained audit results of database operations and manage operation compliance. This feature helps you get a whole picture of all database SQL operations. It also provides detailed backtracking data of database operations and enables convenient accountability for database security incidents.</td>
<td>2021-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1102/41312" target="_blank">Enabling TDSQL-C Audit</a></td></tr>
</table>

## March 2021
<table>
<tr><th width=20%>Update</th><th width=50%>Description</th><th width=10%>Release Date</th><th width=20%>Documentation</th></tr>
<tbody>
<tr>
<td>Supported database and table-level rollback</td>
<td>TDSQL-C can roll back databases/tables to the original cluster and roll back an entire cluster (clone) to a new cluster. You can choose different rollback methods according to your business needs.</td>
<td>2021-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1098/40634" target="_blank">Rolling back Data</a></td></tr>
</tbody></table>

## December 2020
<table>
<tr><th width=20%>Update</th><th width=50%>Description</th><th width=10%>Release Date</th><th width=20%>Documentation</th></tr>
<tbody>
<tr>
<td>Supported the change from pay-as-you-go to serverless billing</td>
<td>The billing mode of TDSQL-C can be changed from pay-as-you-go to serverless. TDSQL-C implements the change by converting the cluster type on the backend. The bills and details will change as a result of the conversion, but the payment mode will remain postpaid.</td>
<td>2020-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1098/40624" target="_blank">Change from Pay-as-You-Go to Serverless Billing</a></td></tr>
<tr>
<td>Supported the change from pay-as-you-go to monthly subscription billing</td>
<td>The billing mode of TDSQL-C can be changed from pay-as-you-go to monthly subscription. TDSQL-C implements this change by generating renewal orders, so you need to make the corresponding payment promptly to ensure that the billing mode change is successful.</td>
<td>2020-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1098/40961" target="_blank">Change from Pay-as-You-Go to Monthly Subscription</a></td></tr>
<tr>
<td>Renamed TencentDB for CynosDB</td>
<td>TencentDB for CynosDB was renamed TDSQL-C on December 24, 2020. </td>
<td>2020-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1098/40615" target="_blank">Product Overview</a></td></tr>
<tr>
<td>Launched the serverless service</td>
<td>TencentDB for CynosDB Serverless Edition adopts the serverless architecture for cloud native database services. It is billed based on the actual computing and storage resource usage, so you only need for pay for what you use while enjoying the cloud native technologies of Tencent Cloud.</td>
<td>2020-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1098/40618" target="_blank">Serverless Service</a></td></tr>
</tbody></table>

## July 2020
<table>
<tr><th width=20%>Update</th><th width=50%>Description</th><th width=10%>Release Date</th><th width=20%>Documentation</th></tr>
<tbody>
<tr>
<td>Added the read-only instance feature</td>
<td>TencentDB for CynosDB allows you to create one or more read-only instances in a cluster, which are suitable for read/write separation and one-write-multiple-read application scenarios and capable of greatly enhancing the read load capacity of your database cluster.</td>
<td>2020-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1098/40631" target="_blank">Creating Read-Only Instance</a></td></tr>
<tr>
<td>Supported data migration with DTS</td>
<td>TencentDB for CynosDB supports migrating data from MySQL 5.7 to CynosDB for MySQL through DTS.</td>
<td>2020-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1098/40637" target="_blank">Migrating with DTS</a></td></tr>
</tbody></table>

