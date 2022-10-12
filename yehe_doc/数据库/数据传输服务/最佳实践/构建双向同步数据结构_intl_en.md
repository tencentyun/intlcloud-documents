## Overview
DTS supports two-way data sync between two databases, which can be applied to multi-site active-active scenarios. In a two-way sync task, two one-way sync tasks are created to establish a two-way topology, and data can be written into both database instances at the same time during sync.

Two-way data sync must follow restrictions on one-way sync and relevant operations. For more information, see the appropriate sync scenario in [Databases Supported by Data Sync](https://intl.cloud.tencent.com/document/product/571/42579).

## Notes
- During full data sync, DTS consumes certain source instance resources, which may increase the load and pressure of the source database. If your database configuration is low, we recommend you sync the data during off-peak hours.
- To avoid duplicate data, make sure that the tables to be synced have a primary key or non-null unique key. 
- You should plan the data in advance. The two source databases are responsible for updating (adding, deleting, and modifying) data with different primary keys so as to avoid problems such as primary key conflict and mutual overwriting of data with the same primary key (for example, data records with primary keys `1`, `3`, and `5` are updated in database A, while data records with primary keys `2`, `4`, and `6` are updated in database B). If there are duplicate primary keys in the two source databases for business reasons, select an appropriate conflict resolution policy as instructed in [Recommended Configurations for Typical Use Cases](#tjpz) to make the sync behavior and data meet the expectations.
- Prepare the target database and [grant the account executing the sync task the permissions of the source and target databases](https://intl.cloud.tencent.com/document/product/571/47344#.3Ca-id.3D.22qttj.22.3E.E5.89.8D.E6.8F.90.E6.9D.A1.E4.BB.B6.3C.2Fa.3E).

## Use Limits
- DDL statements can be executed in at most one direction during two-way sync, as the sync linkage should not form a ring (you can run DDL statements in either the forward or reverse direction).
- All sync links between MySQL, TDSQL-C for MySQL, MariaDB, Percona, and TDSQL for MySQL support two-way sync except when a TDSQL for MySQL instance with the MariaDB kernel is used as the source or target database.

## [Recommended Configurations for Typical Use Cases](id:tjpz)
A two-way sync task consists of two one-way sync tasks to establish a two-way topology. The creation steps for each one-way sync task are similar to those for a general one-way sync task. They differ only in the following sync option settings:
<dx-fold-block title="Sync Option Settings Difference">
</dx-fold-block>

<br>
The following configurations are recommended for typical use cases for your reference.

<table>
<tr><th width="16%">Scenario</th> <th width="14%">Time Requirements</th> <th width="12%">Sync Task</th><th width="14%">Initialization Type</th><th width="14%">If Target Already Exists</th><th width="16%">Conflict Resolution Method</th><th width="18%">SQL Type</th></tr>
<tr>
<td rowspan="2">Scenario 1: Instance A has database/table structures and data, and instance B is empty</td><td rowspan="2">Task 2 can be created only after task 1 enters the "incremental sync" phase</td><td>Task 1: Forward sync (A < B)</td><td>Structure initialization/full data initialization</td><td>Precheck and report error</td><td rowspan="6">Select an option as needed.<li>Example: If a primary key conflict occurs, and you want the content of database A to prevail, you need to select **Overwrite** for task 1 and **Ignore** or **Report** for task 2.</li><li>The conflict resolution method takes effect only for the data with primary key conflict.</td><td rowspan="6"><li>Select DDL in at most one task.</li><li>For operation types other than DDL, keep them consistent between the two tasks.</li></td></tr>
<tr>
<td>Task 2: Reverse sync (B > A)</td><td>Do not select</td><td>Ignore and execute</td></tr>
<tr>
<td rowspan="2">Scenario 2: Instance A has database/table structures and data, and instance B has only database/table structures but no data</td><td rowspan="2">None</td><td>Task 1: Forward sync (A > B)</td><td>Full data initialization</td><td>Ignore and execute</td></tr>
<tr>
<td>Task 2: Reverse sync (B > A)</td><td>Do not select</td><td>Ignore and execute</td></tr>
<tr>
<td rowspan="2">Scenario 3: Both instances A and B have database/table structures and data</td><td rowspan="2">None</td><td>Task 1: Forward sync (A > B)</td><td>Full data initialization</td><td>Ignore and execute</td></tr>
<tr>
<td>Task 2: Reverse sync (B > A)</td><td>Full data initialization</td><td>Ignore and execute</td></tr>
</table>

## Directions
This document takes creating two-way sync between self-built MySQL database A in Shanghai region and TencentDB for MySQL database B in Beijing region as an example. Initially, A has database/table structures and data, while B is empty. When a primary key conflict occurs, data updates in A shall prevail. For A > B sync, the primary key conflict resolution policy is **Overwrite**, and DDL and DML statements are synced. For B > A sync, the policy is **Ignore**, and only DML statements are synced.

<img src="https://qcloudimg.tencent-cloud.cn/raw/7bae9e8811984139f9341009c9ed8644.jpg" style="zoom:90%;" />

### Creating a sync task 1: Reverse sync (A > B)
1. Log in to the [data sync purchase page](https://buy.intl.cloud.tencent.com/replication), select appropriate configuration items, and click **Buy Now**.
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Billing Mode</td><td>Pay-as-you-go billing is supported.</td></tr>
<tr>
<td>Source Instance Type</td><td>Select MySQL, which cannot be changed once configured.</td></tr>
<tr>
<td>Source Instance Region</td><td>Select the source instance A region, which cannot be changed once configured.</td></tr>
<tr>
<td>Target Instance Type</td><td>Select MySQL, which cannot be changed once configured.</td></tr>
<tr>
<td>Target Instance Region</td><td>Select the target instance B region, which cannot be changed once configured.</td></tr>
<tr>
<td>Specification</td><td>Select a specification based on your business needs. The higher the specification, the higher the performance. For more information, see <a href="https://intl.cloud.tencent.com/document/product/571/35322">Billing Overview</a>.</td></tr>
</tbody></table>
2. After successful purchase, return to the [data sync list](https://console.cloud.tencent.com/dts/replication), and you can see the newly created data sync task. You need to configure it before you can use it.
3. In the data sync list, click **Configure** in the **Operation** column to enter the sync task configuration page.  
4. On the sync task configuration page, configure the source and target instances and their accounts and passwords, test the connectivity, and click **Next**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/219d46d2c686d20b0b8610f0fd7b40fd.png" style="zoom:67%;" />
<table>
<thead><tr><th>Category</th><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td rowspan=2 >Task Configuration</td>
<td>Task Name</td>
<td>DTS will automatically generate a task name, which is customizable.</td></tr>
<tr>
<td>Running Mode</td><td>Immediate execution and scheduled execution are supported.</td></tr>
<tr>
<td rowspan=4 >Source Instance Settings</td>
<td>Source Instance Type</td>
<td>The database A type selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Source Instance Region</td>
<td>The database A region selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Service Provider</td>
<td>Select **Others**.</td></tr>
<tr>
<td>Access Type</td>
<td>For a third-party cloud database, you can select **Public Network** generally or select **VPN Access**, **Direct Connect**, or **CCN** based on your actual network conditions. <br>In this scenario, **Public Network** is selected as an example. For the preparations for different access types, see <a href="https://intl.cloud.tencent.com/document/product/571/42652">Overview</a>.</td></tr>
<tr>
<td rowspan=6 >Target Instance Settings</td>
<td>Target Instance Type</td><td>The target database B type selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Target Instance Region</td><td>The target database B region selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Access Type</td><td>In this scenario, select **Database**.</td></tr>
<tr>
<td>Instance ID</td><td>Instance ID of database B.</td></tr>
<tr>
<td>Account</td><td>Account of database B, which must have the required permissions.</td></tr>
<tr>
<td>Password</td><td>Password of database B.</td></tr>
</tbody></table>
5. On the **Set sync options and objects** page, set the data initialization, data sync, and sync object options and click **Save and Go Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/37a77d740fef9cd9899b272b20fd2e5f.png)
<table>
<thead><tr><th>Category</th><th>Parameter</th><th>Description</th></tr></thead>
<tbody>
<tr>
<td rowspan=2>Data Initialization Option</td>
<td>Initialization Type</td>
<td>In this scenario, select **Structure initialization/Full data initialization**.<ul><li>Structure initialization: Table structures in the source instance will be initialized into the target instance before the sync task runs.<li>Full data initialization: Data in the source instance will be initialized into the target database before the sync task runs.</td></tr>
<tr>
<td>If Target Already Exists</td>
<td>In this scenario, select **Precheck and report error**.<ul><li>Precheck and report error: If a table with the same name exists in both the source and target databases, an error will be reported, and the task will stop.<li>Ignore and execute: Full and incremental data will be directly added to tables in the target instance.</td></tr>
<tr>
<td rowspan=2>Data Sync Option</td>
<td>Conflict Resolution Method</td>
<td>Select a conflict resolution policy based on the business conditions. In this scenario, select **Overwrite**.<ul><li>Report: If a primary key conflict is found during data sync, an error will be reported, and the data sync task will be paused.<li>Ignore: If a primary key conflict is found during data sync, the primary key record in the target database will be retained.<li>Overwrite: If a primary key conflict is found during data sync, the primary key record in the source database will overwrite that in the target database.</td></tr>
<tr>
<td>SQL Type</td><td>Supported operations include INSERT, UPDATE, DELETE, and DDL. If you select **Custom DDL**, you can select different DDL statement sync policies as needed. For more information, see <a href="https://cloud.tencent.com/document/product/571/63955">Setting SQL Filter Policy</a>.<br>In two-way sync, you can select **DDL** in at most one task. In this scenario, select **DDL** in task 1 but not task 2.</td></tr>
<tr>
<td rowspan=2>Sync Object Option</td>
<td>Database and Table Objects of Source Instance</td><td>Select the objects to be synced.</td></tr>
<tr>
<td>Selected Object</td><td>Database/Table mapping (renaming) is supported. Hover over a database or table name, click the displayed **Edit** icon, and enter a new name in the pop-up window.</td></tr>
</tbody></table>
6. In an A > B forward sync task, DTS will check the source and target database parameters. After all check items are passed, click **Start Task**. In a B > A reverse sync task, DTS will also check the DDL configuration.
>?
>- If the verification failed, fix the problem as instructed in [Database Connection Check](https://intl.cloud.tencent.com/document/product/571/42552) and initiate the verification task again.
>- If an alarm is displayed in the verification result, it will not affect the task start, but we recommend you click **View Details** to get the suggestions for adjustment.
>
 - DDL check
 - Source and target database parameter check
![](https://qcloudimg.tencent-cloud.cn/raw/53f1da04b85ce4bed37f4bf0a6e74f2f.png)
7. Return to the data sync task list, and you can see that the task has entered the **Running** status.

### Creating a sync task 2: Reverse sync (B > A)
The operations of forward and reverse sync tasks are basically the same. The following only describes their differences:
1. Confirm the status of task 1. When task 1 enters the "incremental sync" phase, start configuring task 2.
This task configuration timing is required only when database B is empty. In other scenarios, there is no need to wait.
2. Set source and target databases.
    Swap the data in source and target databases in task 1.
    <img src="https://qcloudimg.tencent-cloud.cn/raw/0c78d0aa4ef8154ba6c13a23c6ee024b.png" style="zoom:67%;" />
3. Set sync options and objects.
 - Initialization Type: Do not select.
 - If Target Already Exists: Select **Ignore and execute**.
 - Primary Key Conflict Resolution: Select an option based on your business conditions. In this scenario, select **Ignore**.
 - SQL Type: In two-way sync, you can select DDL in at most one task. In this scenario, select DDL in task 1 but not task 2.
 ![](https://qcloudimg.tencent-cloud.cn/raw/1ff732473295edcae799fb0d65eefb50.png)
4. On the **Verify task** page, check the DDL configuration.

### Stopping a sync task
If you no longer need a sync task, you can select **More** > **Stop** in the **Operation** column to stop it.

