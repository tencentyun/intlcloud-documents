## December 2021
<table>
<tr><th width=20%>Update</th><th width=50%>Description</th><th width=10%>Release Date</th><th width=20%>Documentation</th></tr>
<tbody>
<tr>
<td>Supported PostgreSQL 13</td>
<td>TencentDB for PostgreSQL supports PostgreSQL 13 to provide more stable and faster enterprise-grade database services that are easier to deploy in more industries and help upgrade your business.</td>
<td>2021-12</td><td>-</td></tr>
<td>Supported multi-network settings for instances</td>
<td>TencentDB for PostgreSQL supports multiple sets of network configurations, so the same instance can be accessed through different VIPs, and the networks can be modified and switched. This supports multi-plane network features.</td>
<td>2021-12</td><td><a href="https://intl.cloud.tencent.com/document/product/409/44359" target="_blank">Network Management</a></td></tr>
<td>Added extensions</td>
<td>New extensions such as `pg_roaringbitmap` and `postgres_fdw` (for cross-database access) are added.</td>
<td>2021-12</td><td><a href="https://intl.cloud.tencent.com/document/product/409/7567" target="_blank">Supported Plugins/Extensions</a></td></tr>
<td>Supported kernel version management</td>
<td>TencentDB for PostgreSQL supports multiple kernel versions, with stronger stability and shorter access latency. You can query them and submit tickets to upgrade them.</td>
<td>2021-12</td><td><a href="https://intl.cloud.tencent.com/document/product/409/44364" target="_blank">Kernel Version Management</a></td></tr>
</tbody></table>

## October 2021
<table>
<tr><th width=20%>Update</th><th width=50%>Description</th><th width=10%>Release Date</th><th width=20%>Documentation</th></tr>
<tbody>
<tr>
<td>Instances can be downgraded</td>
<td>You can now downgrade the compute and disk specifications of an instance in the console.</td>
<td>2021-10</td><td><a href="https://intl.cloud.tencent.com/document/product/409/41596" target="_blank">Modifying Instance Configuration</a></td></tr>
<tr>
<td>PostgreSQL 9.4, 9.5, and 9.6 support incremental migration</td>
<td>You can now install a migration plug-in to incrementally migrate PostgreSQL 9.4, 9.5, and 9.6 databases to reduce business cut-over costs.</td>
<td>2021-10</td><td><a href="https://intl.cloud.tencent.com/document/product/571/42640" target="_blank">Migration from PostgreSQL to TencentDB for PostgreSQL</a></td></tr>
</tbody></table>

## September 2021
<table>
<tr><th width=20%>Update</th><th width=50%>Description</th><th width=10%>Release Date</th><th width=20%>Documentation</th></tr>
<tbody>
<tr>
<td>Parameter management is supported</td>
<td>You can now set and modify common instance parameters in the console.</td>
<td>2021-09</td><td><a href="https://intl.cloud.tencent.com/document/product/409/43239" target="_blank">Setting Instance Parameters</a></td></tr>
</tbody></table>

## August 2021
<table>
<tr><th width=20%>Update</th><th width=50%>Description</th><th width=10%>Release Date</th><th width=20%>Documentation</th></tr>
<tbody>
<tr>
<td>Disk capacity and instance specification have been optimized</td>
<td>The mapping between disk capacity and instance specification has been optimized. Instances of low specification can now support a larger disk capacity.</td>
<td>2021-08</td><td><a href="https://intl.cloud.tencent.com/document/product/409/7562" target="_blank">Instance Types</a></td></tr>
<tr>
<td>Slow query analysis has been optimized</td>
<td>Slow query analysis has been upgraded. You can now view and compare the monitoring data of the slow query metric and another metric in the same chart, and view real-time slow query statements in the slow SQL list.</td>
<td>2021-08</td><td><a href="https://intl.cloud.tencent.com/document/product/409/39978" target="_blank">Slow Query Analysis</a></td></tr>
</tbody></table>


## July 2021
<table>
<tr><th width=20%>Update</th><th width=50%>Description</th><th width=10%>Release Date</th><th width=20%>Document</th></tr>
<tbody>
<tr>
<td>Scheduled configuration adjustment is supported</td>
<td>When upgrading an instance, you can specify the final switch time of the instance so as to avoid uncontrollable switch time after the instance configuration is adjusted.</td>
<td>2021-07</td><td><a href="https://intl.cloud.tencent.com/document/product/409/41596" target="_blank">Modifying Instance Configuration</a></td></tr>
<tr>
<td>Legacy versions are deactivated	</td>
<td><li>v9.3.5 and v9.5.4 are no longer available.<li>Instances cannot be created on these two versions subsequently, but existing instances are still maintained normally.</td>
<td>2021-07</td><td>-</td></tr>
</tbody></table>

## May 2021
<table>
<tr><th width=20%>Update</th><th width=50%>Description</th><th width=10%>Release Date</th><th width=20%>Document</th></tr>
<tbody>
<tr>
<td>The user experience is optimized</td>
<td><li>The shipping and initialization processes are merged, so newly created instances don't need to be initialized by default.<li>The complexity of the initial user password of databases is increased to meet various compliance requirements.</td>
<td>2021-05</td><td>-</td></tr>
<tr>
<td>Monitoring is upgraded</td>
<td><li>Alarm policies can be set for all metrics.<li>5-second monitoring is supported for all metrics.<li>The accuracy of data collection by certain metrics is optimized.</td>
<td>2021-05</td><td><a href="https://intl.cloud.tencent.com/document/product/409/7564" target="_blank">Monitoring Feature</a></td></tr>
<tr>
<td>Secondary authentication is supported now</td>
<td>Secondary authentication can be performed during password change.</td>
<td>2021-05</td><td>-</td></tr>
</tbody></table>

## April 2021
<table>
<tr><th width=20%>Update</th><th width=50%>Description</th><th width=10%>Release Date</th><th width=20%>Document</th></tr>
<tbody>
<tr>
<td>Security enhancement</td>
<td><li>You can now use security groups to control instance access.<li>Security groups control both public and private network access of instances in Beijing, Guangzhou, Shanghai, and Chengdu, but only the private network access of instances in other regions.<li>The security group of an RO group can be different from those of the read-only instances in the RO group.</td>
<td>2021-04</td><td><a href="https://intl.cloud.tencent.com/document/product/409/40112" target="_blank">Managing Security Groups</a></td></tr>
<tr>
<td>Instance management</td>
<td><li>You can purchase read-only instances in the monthly subscription billing mode for monthly subscribed primary instances.<li>You can return monthly subscribed instances.</td>
<td>2021-04</td><td><a href="https://intl.cloud.tencent.com/document/product/409/40008" target="_blank">Instance Management</a></td></tr>
<tr>
<td>Instance recycle bin</td>
<td><li>Terminated instances will be moved to the recycle bin; therefore, if any instances are terminated by mistake, they can be restored from the recycle bin.<li>Instances in the recycle bin can be restored.<li>Instances in the recycle bin can be eliminated.</td>
<td>2021-04</td><td><a href="https://intl.cloud.tencent.com/document/product/409/40114" target="_blank">Instance Management</a></td</tr>
</tbody></table>

## January 2021
<table>
<tr><th width=20%>Update</th><th width=50%>Description</th><th width=10%>Release Date</th><th width=20%>Document</th></tr>
<tbody><tr>
<td>PostgreSQL v12.4 is now available</td>
<td>TencentDB for PostgreSQL now supports PostgreSQL v12.4.</td>
<td>2021-01</td>
<td><a href="https://intl.cloud.tencent.com/document/product/409/4989" target="_blank">Overview</a></td></tr>
</tbody></table>

## December 2020
<table>
<tr><th width=20%>Update</th><th width=50%>Description</th><th width=10%>Release Date</th><th width=20%>Document</th></tr>
<tbody><tr>
<td>Read-only instances are now supported</td>
<td>TencentDB for PostgreSQL allows you to create one or more read-only instances, which are suitable for read/write separation and one-primary-multi-standby application scenarios and capable of greatly enhancing the read load capacity of your database.</td>
<td>2020-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/409/39545" target="_blank">Creating Read-Only Instances</a></td></tr>
</tbody></table>

## September 2020
<table>
<tr><th width=20%>Update</th><th width=50%>Description</th><th width=10%>Release Date</th><th width=20%>Document</th></tr>
<tbody><tr>
<td>PostgreSQL v11.8 is now available</td>
<td>Combined with optimized kernel and a complete set of management services, TencentDB for PostgreSQL v11.8 provides a more stable enterprise-level database service that is easier to deploy in more areas, helping you upgrade your business.</td>
<td>2020-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/409/40953" target="_blank">Purchase Methods</a></td></tr>
<tr>
<td>Optimized monitoring metrics</td>
<td>TencentDB for PostgreSQL v11.8 optimized more than 10 monitoring metrics to better locate database issues. You can now view the history of databases status at a granularity of 5 seconds.</td>
<td>2020-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/409/7564" target="_blank">Monitoring Feature</a></td></tr>
<tr>
<td>Upgraded plugins</td>
<td>TencentDB for PostgreSQL v11.8 supports more plugins/extension such as wal2json and pg_bigm now.</td>
<td>2020-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/409/7567" target="_blank">Supported Plugins/Extensions</a></td></tr>
</tbody></table>

## August 2020
<table>
<tr><th width=20%>Update</th><th width=50%>Description</th><th width=10%>Release Date</th><th width=20%>Document</th></tr>
<tbody><tr>
<td>Instance tags are now supported</td>
<td>You can now add and edit a tag for a TencentDB for PostgreSQL instance. You can also authenticate resources according to their tags.</td>
<td>2020-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/409/38839" target="_blank">Overview</a></td></tr>
<tr>
<td>Serverless instances can be viewed in the console</td>
<td>You can view and manage serverless instances in the TencentDB for PostgreSQL console.</td>
<td>2020-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/409/41579" target="_blank">Overview</a></td></tr>
</tbody></table>

## July 2020
<table>
<tr><th width=20%>Update</th><th width=50%>Description</th><th width=10%>Release Date</th><th width=20%>Document</th></tr>
<tbody><tr>
<td>Access management is now supported</td>
<td>TencentDB for PostgreSQL now supports resource-level access management. You can set sub-users to control the permissions of instances on a detailed level.</td>
<td>2020-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/409/38834" target="_blank">Access Management</a></td></tr>
</tbody></table>

## April 2020
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=10%>Release Date</th><th width=20%>Document</th></tr></thead>
<tbody><tr>
<td>Pay-as-You-Go billing is now supported</td>
<td>You can now purchase pay-as-you-go TencentDB for PostgreSQL instances.</td>
<td>2020-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/409/4993" target="_blank">Pricing</a></td></tr>
</tbody></table>

## March 2020
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=10%>Release Date</th><th width=20%>Document</th></tr></thead>
<tbody><tr>
<td>Serverless instance support</td>
<td>PostgreSQL for Serverless (ServerlessDB) is a PostgreSQL-based database product that enables on-demand allocation of resources. It can automatically allocate resources according to the actual number of requests.</td>
<td>2020-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/409/41579" target="_blank">Serverless</a></td></tr>
</tbody></table>
