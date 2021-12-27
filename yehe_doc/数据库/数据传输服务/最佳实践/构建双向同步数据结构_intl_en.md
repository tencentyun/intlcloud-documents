## Overview
DTS supports two-way data sync between two databases, which can be applied to multi-site active-active scenarios. In a two-way sync task, two one-way sync tasks are created to establish a two-way topology, and data can be written into both databases at the same time during sync.

As a two-way sync task consists of two one-way sync tasks to establish a two-way topology, restrictions on one-way sync and relevant operations must be followed. For more information, see the appropriate sync scenario in [Data Sync](https://intl.cloud.tencent.com/document/product/571/42579).

## Notes
- During full data sync, DTS consumes certain source database resources, which may increase the load and pressure of the source database. If your database configuration is low, we recommend you sync the data during off-peak hours.
- To avoid duplicate data, make sure that the tables to be synced have a primary key or non-null unique key. 
- You should plan the data in advance. The two source databases are responsible for updating (adding, deleting, and modifying) data with different primary keys so as to avoid problems such as primary key conflict and mutual overwriting of data with the same primary key. If there are duplicate primary keys in the two source databases for business reasons, select an appropriate conflict resolution method as instructed in [Recommended Configurations for Typical Use Cases](#tjpz) to make the sync behavior and data meet the expectations.

## Application Restrictions
- DDL statements can be executed in at most one direction during two-way sync, as the sync linkage should not form a ring (you can run DDL statements in either the forward or reverse direction).
- Currently, a two-way sync task can be created between two MySQL databases, two TDSQL-C for MySQL databases, or one MySQL database and one TDSQL-C for MySQL database.

## [Recommended Configurations for Typical Use Cases](id:tjpz)
A two-way sync task consists of two one-way sync tasks to establish a two-way topology. The creation steps for each one-way sync task are similar to those for a general one-way sync task. They differ only in the following sync option settings:
<dx-fold-block title="Sync Option Settings Difference">
<img src="https://qcloudimg.tencent-cloud.cn/raw/d87c28a91ef22a8f1f31e72049cc9654.png" style="zoom:80%;" />
</dx-fold-block>

<br>
The following configurations are recommended for typical use cases for your reference.
Example: a two-way sync task consisting of two one-way sync tasks (1 and 2) needs to be created between databases A and B: A > B (task 1) and B > A (task 2).
<table>
<tr><th width="16%">Scenario</th> <th width="14%">Time Requirements</th> <th width="12%">Sync Task</th><th width="14%">Initialization Type</th><th width="14%">If Target Already Exists</th><th width="16%">Conflict Resolution Method</th><th width="18%">SQL Type</th></tr>
<tr>
<td rowspan="2">Scenario 1: database A has database/table structures and data, and database B is empty</td><td rowspan="2">Task 2 can be created only after task 1 enters the "incremental sync" phase</td><td>Task 1: forward sync</td><td>Structure initialization/full data initialization</td><td>Precheck and report error</td><td rowspan="6">Select an option as needed.<li>Example: if a primary key conflict occurs, and you want the content of database A to prevail, you need to select **Overwrite** for task 1 and **Ignore** or **Report** for task 2.</li><li>The conflict resolution method takes effect only for the data with primary key conflict.</td><td rowspan="6"><li>Select DDL in at most one task.</li><li>For operation types other than DDL, keep them consistent between the two tasks.</li></td></tr>
<tr>
<td>Task 2: reverse sync</td><td>Do not select</td><td>Ignore and execute</td></tr>
<tr>
<td rowspan="2">Scenario 2: database A has database/table structures and data, and database B has only database/table structures but no data</td><td rowspan="2">None</td><td>Task 1: forward sync</td><td>Full data initialization</td><td>Ignore and execute</td></tr>
<tr>
<td>Task 2: reverse sync</td><td>Do not select</td><td>Ignore and execute</td></tr>
<tr>
<td rowspan="2">Scenario 3: both databases A and B have database/table structures and data</td><td rowspan="2">None</td><td>Task 1: forward sync</td><td>Full data initialization</td><td>Ignore and execute</td></tr>
<tr>
<td>Task 2: reverse sync</td><td>Full data initialization</td><td>Ignore and execute</td></tr>
</table>



## Directions
This document uses MySQL two-way sync (where database A has database/table structures and data, and database B has only database/table structures but no data) as an example. The two-way sync operations for other databases are similar.

### Creating sync task 1: forward sync (database A > database B)
1. Log in to the [data sync purchase page](https://buy.intl.cloud.tencent.com/dts), select appropriate configuration items, and click **Buy Now**.
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Billing Mode</td><td>Monthly subscription and pay-as-you-go billing modes are supported. Currently, the data sync feature is free of charge, and you will receive notifications by email and Message Center one month before the billing officially starts.</td></tr>
<tr>
<td>Source Database Type</td><td>Select MySQL (including TencentDB for MySQL and self-built MySQL).</td></tr>
<tr>
<td>Source Database Region</td><td>Select the source database A region.</td></tr>
<tr>
<td>Target Database Type</td><td>Select MySQL (including TencentDB for MySQL and self-built MySQL).</td></tr>
<tr>
<td>Target Database Region</td><td>Select the target database B region.</td></tr>
<tr>
<td>Sync Task Specification</td><td>Currently, only the Standard Edition is supported</td></tr>
</tbody></table>
2. After successful purchase, return to the [data sync list](https://console.cloud.tencent.com/dts/replication), and you can see the newly created data sync task. You need to configure it before you can use it.
3. In the data sync list, click **Configure** in the **Operation** column to enter the sync task configuration page.
4. On the sync task configuration page, configure the source and target databases and their accounts and passwords, test the connectivity, and click **Next**.
<table>
<thead><tr><th>Category</th><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td rowspan=2 >Task Configuration</td>
<td>Task Name</td>
<td>DTS will automatically generate a task name, which is customizable.</td></tr>
<tr>
<td>Running Mode</td><td>Immediate execution and scheduled execution are supported.</td></tr>
<tr>
<td rowspan=4 >Source Database Settings</td>
<td>Source Database Type</td>
<td>Select the TencentDB instance type selected during purchase, which cannot be changed once configured.</td></tr>
<tr>
<td>Source Database Region</td>
<td>Select the TencentDB instance A region selected during purchase, which cannot be changed once configured.</td></tr>
<tr>
<td>Service Provider</td>
<td>Others (including TencentDB for MySQL and self-built MySQL), AWS, and Alibaba Cloud are supported.</td></tr>
<tr>
<td>Access Type</td>
<td>If **Other Cloud Vendors** is selected as **Service Provider**, the access type can be public network; if **Others** is selected as **Service Provider**, you need to select an access type according to the database deployment conditions.<ul>
    <li>Public Network: self-built database connected through a public IP.</li>
    <li>Self-Build on CVM: self-built database on CVM.</li>
    <li>Direct Connect/VPN Access: self-built database connected through a Direct Connect/VPN gateway.</li>
    <li>VPC: self-built database connected through a VPC.</li>
    <li>Database: TencentDB database.</li>
    <li>CCN: self-built database connected through CCN.</li>
    </ul></td></tr>
<tr>
<td rowspan=3 >Target Database Settings</td>
<td>Target Database Type</td><td>Select the target database type, which cannot be changed once configured.</td></tr>
<tr>
<td>Target Database Region</td><td>Select the target database B region, which cannot be changed once configured.</td></tr>
<tr>
<td>Access Type</td><td>Select the access type of the target database B.</td></tr>
</tbody></table>
5. On the **Set sync options and objects** page, set the data initialization, data sync, and sync object options and click **Save and Go Next**.
<table>
<thead><tr><th>Category</th><th>Parameter</th><th>Description</th></tr></thead>
<tbody>
<tr>
<td rowspan=2>Data Initialization Option</td>
<td>Initialization Type</td>
    <td><ul><li>Structure initialization: table structures in the source database will be initialized into the target database before the sync task runs.</li><li>Full data initialization: data in the source database will be initialized into the target database before the sync task runs.</li></ul>In this document, select **Full data initialization**.</td></tr>
<tr>
<td>If Target Already Exists</td>
<td><ul><li>Precheck and report error: if a table with the same name exists in both the source and target databases, an error will be reported, and the task will stop.</li><li>Ignore and execute: full and incremental data will be directly added to tables in the target database.</li></ul>In this document, select **Ignore and execute**.</td></tr>
<tr>
<td rowspan=2>Data Sync Option</td>
<td>Conflict Resolution Method</td>
<td><ul><li>Report: if a primary key conflict is found during data sync, an error will be reported, and the data sync task will be paused.</li><li>Ignore: if a primary key conflict is found during data sync, the primary key record in the target database will be retained.<li>Overwrite: if a primary key conflict is found during data sync, the primary key record in the source database will overwrite that in the target database.</li></ul>Select an option as needed.</td></tr>
<tr>
<td>SQL Type</td><td>Supported operations: INSERT, UPDATE, DELETE, and DDL.<br>In two-way sync, you can select DDL in at most one task. In this document, select DDL in task 1 but not task 2.</td></tr>
<tr>
<td rowspan=2>Sync Object Option</td>
<td>Database and Table Objects of Source Database</td><td>Select the objects to be synced. You can select databases, tables, and views.</td></tr>
<tr>
<td>Selected Object</td><td>It displays the selected sync objects, and database/table mapping is supported.</td></tr>
</tbody></table>
6. On the task verification page, the system will check the DDL configuration first and then check the source and target database parameters. After all check items are passed, click **Start Task**.
>?
>- If the verification failed, fix the problem as instructed in [Fix for Verification Failure](https://intl.cloud.tencent.com/document/product/571/42552) and initiate the verification task again.
>- If an alarm is displayed in the verification result, it will not affect the task start, but we recommend you click **View Details** to get the suggestions for adjustment.
>
 - DDL check
 - Source and target database parameter check
7. Return to the data sync task list, and you can see that the task has entered the **Running** status.

### Creating sync task 2: reverse sync (database B > database A)
The operations of the two sync tasks are basically the same. The following only describes their differences:
1. Set the sync source and target databases.
Swap the settings of the source and target databases in task 1.
2. Set the sync options and objects.
 - Initialization Type: do not select.
 - If Target Already Exists: select **Ignore and execute**.
 - Conflict Resolution Method: select the same option as selected in task 1.
 - SQL Type: in two-way sync, you can select DDL in at most one task. In this document, select DDL in task 1 but not task 2.

### Stopping sync task
If you no longer need a sync task, you can select **More** > **Stop** in the **Operation** column to stop it.
