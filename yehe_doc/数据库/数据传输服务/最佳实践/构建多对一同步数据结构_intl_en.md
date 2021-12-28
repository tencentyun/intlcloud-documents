## Overview
Many-to-One sync is to sync the content in multiple source databases to one target database. If you use a single database, you may often need to shard the data due to high load or region issues, but storing the databases/tables of the same type in many databases makes data query inconvenient. The many-to-one sync feature can easily solve this problem.

As a many-to-one sync task consists of multiple one-way sync tasks to establish a many-to-one topology, restrictions on one-way sync and relevant operations must be followed. For more information, see the appropriate sync scenario in [Data Sync](https://intl.cloud.tencent.com/document/product/571/42579).

## Notes
- During full data sync, DTS consumes certain source database resources, which may increase the load and pressure of the source database. If your database configuration is low, we recommend you sync the data during off-peak hours.
- To avoid duplicate data, make sure that the tables to be synced have a primary key or non-null unique key. 
- You should plan the data in advance. Each source database is responsible for updating (adding, deleting, and modifying) data with different primary keys so as to avoid problems such as primary key conflict and mutual overwriting of data with the same primary key. If there are duplicate primary keys in multiple source databases for business reasons, select an appropriate conflict resolution method as instructed in [Recommended Configuration for Typical Use Case](#tjpz) to make the sync behavior and data meet the expectations.

## Application Restrictions
- DDL statements in the configurations of multiple sync tasks should not form a ring.
- Currently, a many-to-one sync task can be created between two MySQL databases, two TDSQL-C for MySQL databases, or one MySQL database and one TDSQL-C for MySQL database.

## DDL Configuration Principles
- DDL statements in the configurations of multiple sync tasks should not form a ring; otherwise, they will loop in the system, causing errors.
- The same table object in the target database cannot receive DDL sync from multiple source databases; otherwise, such DDL statements may conflict with each other in the target database, causing errors.
   - In many-to-one sync that combines multiple tables with the same name into one, you can select DDL in only one sync task.
   - In other types of many-to-one sync tasks (such as a task that combines multiple tables with different names into one database), you can select DDL in each task. In this case, select an appropriate DDL sync policy based on the actual conditions.
- During verification, the sync system will judge whether the sync task being created will cause a DDL loop or conflict based on all your other sync tasks and provide prompts for your reference. 

## [Recommended Configurations for Typical Use Cases](id:tjpz)
A many-to-one sync task consists of multiple one-way sync tasks to establish a many-to-one topology. The creation steps for each one-way sync task are similar to those for a general one-way sync task. They differ only in the following sync option settings:

The following configurations are recommended for typical use cases for your reference.

Example: a sync task among databases A, B, and C needs to be created, where databases A and B have tables with the same name that need to be synced to database C, task 1 is sync from A to C, and task 2 is sync from B to C. To sync data from more source databases to the target database, simply add sync tasks by referring to task 2.

<table>
<tr><th width="15%">Scenario</th> <th width="13%">Time Requirements</th> <th width="10%">Sync Task</th><th width="12%">Initialization Type</th><th width="13%">If Target Already Exists</th><th width="17%">Conflict Resolution Method</th><th width="15%">SQL Type</th></tr>
<tr>
<td rowspan="2">Scenario 1: databases A and B have database/table structures and data, and database C is empty</td><td rowspan="2">Task 2 can be started only after task 1 enters the "incremental sync" phase</td><td>Task 1</td><td>Structure initialization/full data initialization</td><td>Ignore and execute</td><td rowspan="6">Select an option as needed.<li>Example: if a primary key conflict occurs, and you want the content of database A to prevail, you need to select **Overwrite** for task 1 and **Ignore** or **Report** for task 2.</li><li>The conflict resolution method takes effect only for the data with primary key conflict.</li></td><td rowspan="6"><li>Select DDL in at most one task.</li><li>For operation types other than DDL, keep them consistent between the other multiple tasks.</li></td></tr>
<tr>
<td>Task 2</td><td>Full data initialization</td><td>Ignore and execute</td></tr>
<tr>
<td rowspan="2">Scenario 2: databases A and B have database/table structures and data, and database C has only database/table structures but no data</td><td rowspan="2">None</td><td>Task 1</td><td>Full data initialization</td><td>Ignore and execute</td></tr>
<tr>
<td>Task 2</td><td>Same as task 1</td><td>Same as task 1</td></tr>
<tr>
<td rowspan="2">Scenario 3: databases A, B, and C all have database/table structures and data</td><td rowspan="2">None</td><td>Task 1</td><td>Full data initialization</td><td>Ignore and execute</td></tr>
<tr>
<td>Task 2</td><td>Same as task 1</td><td>Same as task 1</td></tr>   
</table>

## Directions
The following uses MySQL two-to-one sync (databases A and B have database/table structures and data, and database C is empty) as an example. The many-to-one sync operations for other databases are similar.

### Creating sync task 1 (database A > database C)
1. Log in to the [data sync purchase page](https://buy.cloud.tencent.com/dts), select appropriate configuration items, and click **Buy Now**.
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
<td>Target Database Region</td><td>Select the target database C region.</td></tr>
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
<td>Target Database Region</td><td>Select the target database C region, which cannot be changed once configured.</td></tr>
<tr>
<td>Access Type</td><td>Select the access type of the target database C.</td></tr>
</tbody></table>
5. On the **Set sync options and objects** page, set the data initialization, data sync, and sync object options and click **Save and Go Next**.
<table>
<thead><tr><th>Category</th><th>Parameter</th><th>Description</th></tr></thead>
<tbody>
<tr>
<td rowspan=2>Data Initialization Option</td>
<td>Initialization Type</td>
    <td><ul><li>Structure initialization: table structures in the source database will be initialized into the target database before the sync task runs.</li><li>Full data initialization: data in the source database will be initialized into the target database before the sync task runs.</li></ul>In this document, select **Structure initialization/Full data initialization**.</td></tr>
<tr>
<td>If Target Already Exists</td>
<td><ul><li>Precheck and report error: if a table with the same name exists in both the source and target databases, an error will be reported, and the task will stop.</li><li>Ignore and execute: full and incremental data will be directly added to tables in the target database.</li></ul>In this document, select **Ignore and execute**.</td></tr>
<tr>
<td rowspan=2>Data Sync Option</td>
<td>Conflict Resolution Method</td>
<td><ul><li>Report: if a primary key conflict is found during data sync, an error will be reported, and the data sync task will be paused.</li><li>Ignore: if a primary key conflict is found during data sync, the primary key record in the target database will be retained.<li>Overwrite: if a primary key conflict is found during data sync, the primary key record in the source database will overwrite that in the target database.</li></ul>Select an option as needed.</td></tr>
<tr>
<td>SQL Type</td><td>Supported operations: INSERT, UPDATE, DELETE, and DDL.<br>In many-to-one sync, you can select DDL in at most one task. In this document, select DDL in task 1 but not other tasks.</td></tr>
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

### Creating sync task 2 (database B > database C)
Configure sync task 2 after the previous sync task enters the **incremental sync** phase.
The operations of tasks 1 and 2 are basically the same. The following only describes their differences:

1. Set the sync source and target databases.
Enter the information of databases A and B in the source and target database settings respectively.
2. Set the sync options and objects.
  - Initialization Type: select **Full data initialization** only but not **Structure Initialization**.
  - If Target Already Exists: select **Ignore and execute**.
  - Conflict Resolution Method: select an option as needed.
  - SQL Type: do not select DDL. In many-to-one sync, you can select DDL in at most one task. In this document, select DDL in task 1 but not other tasks.

### Stopping sync task
If you no longer need a sync task, you can select **More** > **Stop** in the **Operation** column to stop it.

