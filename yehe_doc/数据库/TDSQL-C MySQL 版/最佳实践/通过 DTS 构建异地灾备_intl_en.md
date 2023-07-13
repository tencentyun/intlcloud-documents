TDSQL-C for MySQL allows you to use Data Transmission Service (DTS) to implement remote disaster recovery to ensure database availability and stability.
## Overview
If your TDSQL-C for MySQL cluster is deployed in a single region, your service is more likely to be interrupted by force majeure like power outages and network disconnection.

To prevent this problem, you can build a disaster recovery center in another region to improve service availability. DTS allows you to continually sync data and replicas between your business center and disaster recovery center. In case of a failure in your business region, you can switch to the disaster recovery region to process user requests.

With the remote disaster recovery architecture, if a disaster occurs in an IDC, the traffic in this IDC can be routed to other IDCs to implement quick cross-region failover and guarantee business continuity.

## Remote Disaster Recovery Directions
**Step 1. Purchase a cluster**
Go to the [TDSQL-C for MySQL purchase page](https://buy.cloud.tencent.com/cynosdb?regionId=8) and purchase two TDSQL-C for MySQL clusters in two different regions, with one deployed in your business center and the other in the disaster recovery center.
>?For data sync prerequisites and environment requirements, see [Sync from TDSQL-C for MySQL to TDSQL-C for MySQL](https://intl.cloud.tencent.com/document/product/571/47348).
>
**Step 2. Use DTS to implement remote disaster recovery**
1. Go to the [data sync purchase page](https://buy.cloud.tencent.com/replication), select appropriate configuration items, and click **Buy Now**.
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Billing Mode</td><td>Pay-as-you-go billing and monthly subscription are supported.</td></tr>
<tr>
<td>Source Instance Type</td><td>Select "TDSQL-C for MySQL", which cannot be changed after purchase.</td></tr>
<tr>
<td>Source Instance Region</td><td>Select the source instance region, which cannot be changed after purchase.</td></tr>
<tr>
<td>Target Instance Type</td><td>Select "TDSQL-C for MySQL", which cannot be changed after purchase.</td></tr>
<tr>
<td>Target Instance Region</td><td>Select the target instance region, which cannot be changed after purchase.</td></tr>
<tr>
<td>Specification</td><td>Select a specification based on your business needs. The higher the specification, the higher the performance. For more information, see <a href="https://www.tencentcloud.com/document/product/571/35322">Billing Overview</a>.</td></tr>
</tbody></table>
2. After successful purchase, return to the [data sync task list](https://console.cloud.tencent.com/dts/replication), and you can see the newly created data sync task. You need to configure it before using it.
3. In the data sync task list, click **Configure** in the **Operation** column to enter the sync task configuration page.
4. On the sync task configuration page, configure the source and target instances and their accounts and passwords, test the connectivity, and click **Next**.
<br>As there are many overlapped scenarios of source database deployment modes and access types, the sync steps for different scenarios are similar. Below is a configuration example for typical scenarios, to which you can refer for other scenarios.
<br>
Sync between TDSQL-C for MySQL instances is used as an example.
<table>
<thead><tr><th width="10%">Category</th><th width="15%">Parameter</th><th width="75%">Description</th></tr></thead>
<tbody><tr>
<td rowspan=2 >Task Settings</td>
<td>Task Name</td>
<td>DTS will automatically generate a task name, which is customizable.</td></tr>
<tr>
<td>Running Mode</td><td>Immediate execution and scheduled execution are supported.</td></tr>
<tr>
<td rowspan=7 >Source Instance Settings</td>
<td>Source Instance Type</td>
<td>Select the source instance type selected during purchase, which cannot be changed once configured.</td></tr>
<tr>
<td>Source Instance Region</td>
<td>Select the source instance region selected during purchase, which cannot be changed once configured.</td></tr>
<tr>
<td>Service Provider</td>
<td>For a self-built database (such as a CVM-based one) or TencentDB database, select **Others**. For a third-party cloud database, select the corresponding service provider.<br>In this scenario, select **Others**.</td></tr>
<tr>
<td>Access Type</td>
<td>Select a type based on your scenario. In this scenario, select **Database**. For the preparations for different access types, see <a href="https://intl.cloud.tencent.com/document/product/571/42652">Overview</a>.<ul>
<li>Public Network: The source database can be accessed through a public IP.</li>
<li>Self-Build on CVM: The source database is deployed on a <a href="https://www.tencentcloud.com/document/product/213">CVM</a> instance.</li>
<li>Direct Connect: The source database can be interconnected with VPCs through <a href="https://www.tencentcloud.com/document/product/216">Direct Connect</a>.</li>
<li>VPN Access: The source database can be interconnected with VPCs through <a href="https://www.tencentcloud.com/document/product/1037">VPN Connections</a>.</li>
<li>Database: The source database is a TencentDB database.</li>
<li>CCN: The source database can be interconnected with VPCs through <a href="https://www.tencentcloud.com/document/product/1003">CCN</a>.</li><li>VPC: The source and target databases are both deployed in Tencent Cloud <a href="https://www.tencentcloud.com/document/product/215">VPCs</a>. To use the VPC access type, <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> for application.</li></ul></td></tr>
<tr>
<td>Instance ID</td><td>Source instance ID. You can view the source instance information in the <a href="https://console.cloud.tencent.com/cynosdb/mysql/ap-guangzhou/cluster/cynosdbmysql-iimys9mv/detail">cluster list</a>.</td></tr>
<tr>
<td>Account</td><td>Account of the source instance, which must have the required permissions.</td></tr>
<tr>
<td>Password</td><td>Password of the source instance account.</td></tr>
<tr>
<td rowspan=6>Target Instance Settings</td>
<td>Target Instance Type</td><td>The target instance type selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Target Instance Region</td><td>The target instance region selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Access Type</td><td>Select a type based on your scenario. In this scenario, select **Database**.</td></tr>
<tr>
<td>Instance ID</td><td>Target instance ID.</td></tr>
<tr>
<td>Account</td><td>Account of the target instance, which must have the required permissions.</td></tr>
<tr>
<td>Password</td><td>Password of the target instance account.</td></tr>
</tbody></table>


5. On the **Set sync options and objects** page, set the data initialization, data sync, and sync object options and click **Save and Go Next**.
>?
>- If you only select **Full data initialization** for **Initialization Type**, the system will assume by default that you have created the table structures in the target database and will neither sync table structures nor check whether the source and target databases have tables with the same name. Therefore, if you select **Precheck and report error** for **If Target Already Exists**, the precheck and error reporting feature won't take effect.
>- If you want to rename a table (for example, rename table A "table B") during the sync, you must select the entire database (or entire instance) where table A resides rather than only table A as the **sync object**; otherwise, the system will report an error.
>
<table>
<thead><tr><th>Category</th><th>Parameter</th><th>Description</th></tr></thead>
<tbody>
<tr>
<td rowspan=2>Data Initialization Option</td>
<td>Initialization Type</td>
<td><ul><li>Structure initialization: Table structures in the source database will be initialized into the target database before the sync task runs.<li>Full data initialization: Data in the source database will be initialized into the target database before the sync task runs. If you only select <b>Full data initialization</b>, you need to create the table structure in the target database in advance. <br> Both options are selected by default, and you can deselect them as needed.</td></tr>
<tr>
<td>If Target Already Exists</td>
<td><ul><li>Precheck and report error: If a table with the same name exists in both the source and target databases, an error will be reported, and the task will stop.<li>Ignore and execute: Full and incremental data will be directly added to tables in the target instance.</td></tr>
<tr>
<td rowspan=2>Data Sync Option</td>
<td>Conflict Resolution Method</td>
<td><ul><li>Report: If a primary key conflict is found during data sync, an error will be reported, and the data sync task will be paused.<li>Ignore: If a primary key conflict is found during data sync, the primary key record in the target database will be retained.<li>Overwrite: If a primary key conflict is found during data sync, the primary key record in the source database will overwrite that in the target database.</td></tr>
<tr>
<td>SQL Type</td><td>Supported operations include INSERT, UPDATE, DELETE, and DDL. If you select **Custom DDL**, you can select different DDL statement sync policies as needed. For more information, see <a href="https://www.tencentcloud.com/document/product/571/47342">Setting SQL Filter Policy</a>.</td></tr>
<tr>
<td rowspan=3>Sync Object Option</td>
<td>Database and Table Objects of Source Instance</td><td>Select the objects to be synced. You can select basic databases, tables, views, procedures, and functions.<br>The sync of advanced objects is a one-time operation: only advanced objects already in the source database before the task start can be synced, while those added to the source database after the task start will not be synced to the target database. For more information, see <a href="https://www.tencentcloud.com/document/product/571/48487">Syncing Advanced Object</a>.</td></tr>
<tr>
<td>Selected Object</td><td><ul><li>Database/Table mapping (renaming) is supported. Hover over a database or table name, click the displayed **Edit** icon, and enter a new name in the pop-up window.</li><li>When advanced objects are selected for sync, we do not recommend that you rename databases/tables. If you do so, sync of the advanced objects may fail.</li></ul></td></tr>
<tr>
< td>Sync Online DDL Temp Table</td>
<td>If you use the "gh-ost" or "pt-osc" tool to perform online DDL operations on source database tables, DTS supports migrating the generated temp tables to the target database.<ul><li>If you select `gh-ost`, DTS will migrate the temp tables named `_Table name_ghc`, `_Table name_gho`, and `_Table name_del` to the target database.</li>
<li>If you select "pt-osc", DTS will migrate the temp tables named `_Table name_new` and `_Table name_old` to the target database.</li></ul>For more information, see <a href="https://intl.cloud.tencent.com/document/product/571/48486">Syncing Online DDL Temp Table</a>.</td></tr>
</tbody></table>
6. On the task verification page, complete the verification. After all check items are passed, click **Start Task**.
    If the verification fails, troubleshoot as instructed in [Check Item Overview](https://intl.cloud.tencent.com/document/product/571/42551) and initiate the verification again.
 - Failed: It indicates that a check item failed and the task is interrupted. You need to fix the problem and run the verification task again.
 - Alarm: It indicates that a check item doesn't completely meet the requirements. The task can be continued, but the business will be affected. You need to assess whether to ignore the alarm or fix the problem and continue the task based on the alarm message.
7. Return to the data sync task list, and you can see that the task has entered the **Running** status.
>?You can click **More** > **Stop** in the **Operation** column to stop a sync task. Before doing so, ensure that data sync has been completed.
>
8. (Optional) You can click a task name to enter the task details page and view the task initialization status and monitoring data.

