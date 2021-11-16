## September 2021
<table>
<tr><th width=20%>Update</th><th width=50%>Description</th><th width=10%>Release Date</th><th width=20%>Documentation</th></tr>
<tbody>
<tr>
<td>Supported heterogeneous migration between Percona, MariaDB, and MySQL</td>
<td>Heterogeneous migration between Percona, MariaDB, and MySQL is supported.</td>
<td>2021-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42644" target="_blank">Migration from MariaDB or Percona to MySQL</a></td></tr><tr>
<tr>
<td>Supported data subscription to TDSQL for MySQL</td>
<td>DTS supports subscription to TDSQL for MySQL.</td>
<td>2021-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42663" target="_blank">Databases Supported by Data Subscription</a></td></tr>
</tbody></table>


## August 2021
<table>
<tr><th width=20%>Update</th><th width=50%>Description</th><th width=10%>Release Date</th><th width=20%>Documentation</th></tr>
<tbody>
<tr>
<td>Supported custom routing policies</td>
<td>MySQL subscription supports customizing data fields for routing to Kafka partitions.</td>
<td>2021-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42664" target="_blank">Creating Data Subscription Task</a></td></tr><tr>
<td>Supported data sync to TDSQL-C</td>
<td>DTS supports data sync between TDSQL-C instances.</td>
<td>2021-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42621" target="_blank">Data Sync Between TDSQL-C Instances</a></td></tr>
</tbody></table>


## July 2021
<table>
<tr><th width=20%>Update</th><th width=50%>Description</th><th width=10%>Release Date</th><th width=20%>Documentation</th></tr>
<tbody>
<td>Supported the default alarm policy</td>
<td>Default configuration is supported for key event monitoring in data migration, data sync, and data subscription to promptly notify you of triggered events.</td>
<td>2021-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42611" target="_blank">Supported Events and Metrics</a></td></tr>
<tr>
<td>Supported data migration retry</td>
<td>If a data migration task is interrupted by an exception, it can be restarted after the exception is fixed.</td>
<td>2021-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42634" target="_blank">Retrying Task</a></td></tr>
<tr>
<td>Supported MySQL data sync to TDSQL for PostgreSQL</td>
<td>DTS supports data sync from MySQL to TDSQL for PostgreSQL.</td>
<td>2021-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42622" target="_blank">Data Sync from TencentDB for MySQL to TDSQL for PostgreSQL and TDSQL-A for PostgreSQL</a></td></tr>
<tr>
<td>Supported table mapping</td>
<td>Tables migrated to the target database can be renamed.</td>
<td>2021-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42629" target="_blank">Table Mapping</a></td></tr>
<tr>
<td>Supported migration progress details display</td>
<td>You can view the migration progress details on the migration progress tab, such as source tables, target tables, number of estimated rows, number of completed rows, and migration status.</td>
<td>2021-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42637" target="_blank">Viewing Task</a></td></tr>
<tr>
<td>Modified the view export feature</td>
<td><li>Before modification: when a view is exported, only the same definers as the target `user@host` can be migrated.<li>After modification: when a view is exported, DTS will check whether `user1` corresponding to `DEFINER` (`[DEFINER = user1]`) in the source database is the same as `user2` in the migration target, and if not, DTS will change the `SQL SECURITY` attribute of `user1` in the target database from `DEFINER` to `INVOKER` (`[INVOKER = user1]`), and set the `DEFINER` in the target database to `user2` of the migration target (`[DEFINER = migration target user2]`).</td>
<td>2021-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42561" target="_blank">View Check</a></td></tr>
</tbody></table>


## May 2021
<table>
<tr><th width=20%>Update</th><th width=50%>Description</th><th width=10%>Release Date</th><th width=20%>Documentation</th></tr>
<tbody>
<tr>
<td>Supported data sync metric monitoring</td>
<td>Metrics in data sync tasks can be monitored.</td>
<td>2021-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42579" target="_blank">Supported Events and Metrics</a></td></tr>
<tr>
<td>Supported MySQL data sync</td>
<td>DTS supports real-time data sync between MySQL databases. It is suitable for various business scenarios such as cloud-local active-active, multi-site active-active, multi-site active-active, and cross-border data sync, as well as real-time data warehousing, helping you build a secure, scalable, and highly available data architecture.</td>
<td>2021-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42624" target="_blank">Data Sync Between MySQL Databases</a></td></tr>
</tbody></table>



## April 2021
<table>
<tr><th width=20%>Update</th><th width=50%>Description</th><th width=10%>Release Date</th><th width=20%>Documentation</th></tr>
<tbody>
<tr>
<td>Supported cross-account migration</td>
<td>NewDTS supports across-account instance migration.</td>
<td>2021-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42646" target="_blank">Cross-account TencentDB Instance Migration</a></td></tr>
<tr>
<td>Supported MySQL 8.0 for data migration</td>
<td>NewDTS supports MySQL 8.0 and data migration from a lower MySQL version to 8.0.</td>
<td>2021-04</td><td>-</td></tr>
</tbody></table>

