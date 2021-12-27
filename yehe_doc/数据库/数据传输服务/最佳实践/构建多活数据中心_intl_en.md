## Overview
The multi-site active-active IDC architecture refers to multiple IDCs that are deployed in different regions and provide service concurrently. Data can be synced among them in real time. If a disaster occurs in an IDC, its traffic can be routed to other IDCs to implement quick cross-region failover and guarantee business continuity.

The multi-site active-active IDC architecture is implemented by creating multiple two-way sync tasks, each of which consists of two one-way sync tasks. Therefore, restrictions on one-way sync and relevant operations must be followed. For more information, see the appropriate sync scenario in [Data Sync](https://intl.cloud.tencent.com/document/product/571/42579).

## Notes
- During full data sync, DTS consumes certain source database resources, which may increase the load and pressure of the source database. If your database configuration is low, we recommend you sync the data during off-peak hours.
- To avoid duplicate data, make sure that the tables to be synced have a primary key or non-null unique key.
- You should plan the data in advance. Each IDC is responsible for updating (adding, deleting, and modifying) data with different primary keys so as to avoid problems such as primary key conflict and mutual overwriting of data with the same primary key. If there are duplicate primary keys in multiple source databases for business reasons, select an appropriate conflict resolution method to make the sync behavior and data meet the expectations.

## Application Restrictions
- DDL statements in the configurations of multiple sync tasks should not form a ring.
- Currently, a two-way sync task can be created between two MySQL databases, two TDSQL-C for MySQL databases, or one MySQL database and one TDSQL-C for MySQL database.

## DDL Configuration Principles
This document uses a specific scenario to describe how to configure DDL statements for easier understanding. For example, in a multi-site active-active-active IDC architecture, three two-way sync tasks are created among databases A (Beijing region), B (Shanghai region), and C (Guangzhou region): A <-> B, B <-> C, and C <-> A.
<img src="https://qcloudimg.tencent-cloud.cn/raw/bddef945c4316f902bfe5da564c827c7.png" style="zoom:40%;" />

- DDL statements in the configurations of multiple sync tasks should not form a ring; otherwise, they will loop in the system, causing errors.
  For example, among the three sync tasks (1, 3, and 5) marked by blue lines in the following figure, you can select DDL in up to two of them, and if you select three, a ring will be formed.

- The same table object cannot receive DDL sync from multiple IDCs; otherwise, such DDL statements may conflict with each other in the target database, causing errors.
  For example, databases A and C have tables with the same name to be synced to database B. Then, you can select DDL in only one task between tasks 1 and 4.
  
- During verification, the sync system will judge whether the sync task being created will cause a DDL loop or conflict based on all your other sync tasks and provide prompts for your reference.

## Recommended Configurations for Typical Use Cases
The multi-site active-active IDC architecture is implemented by creating multiple two-way sync tasks, each of which consists of two one-way sync tasks. Therefore, the operation steps for each sync task in such architecture are basically the same as those for a general one-way sync task. They differ only in the following configurations:
<dx-fold-block title="Sync Option Settings Difference">
<img src="https://qcloudimg.tencent-cloud.cn/raw/448645a136cbac9f8d499493cefd0a57.png" style="zoom:80%;" />
</dx-fold-block>


<br>This document recommends the following configuration for a typical multi-site active-active IDC architecture for your reference.

For example, in a multi-site active-active-active IDC architecture, three two-way sync tasks are created among databases A (Beijing region), B (Shanghai region), and C (Guangzhou region): A <-> B (tasks 1 and 2), B <-> C (tasks 3 and 4), and C <-> A (tasks 5 and 6).

<table>
<tr><th width="16%">Scenario</th> <th width="17%">Time Requirements</th> <th width="9%">Sync Task</th><th width="14%">Initialization Type</th><th width="14%">If Target Already Exists</th><th width="16%">Conflict Resolution Method</th><th width="18%">SQL Type</th></tr>
<tr>
<td rowspan="6">Scenario 1: database A has database/table structures and data, and databases B and C are empty</td><td rowspan="2">Task 2 can be created only after task 1 enters the "incremental sync" phase</td><td>Task 1</td><td>Structure initialization/full data initialization</td><td>Precheck and report error</td><td rowspan="7">Select an option as needed. The conflict resolution method takes effect only for the data with primary key conflict.</td><td rowspan="7">Select DDL statements according to the configuration principles. For other operation types, we recommend you keep them consistent among all sync tasks.</td></tr>
<tr>
<td>Task 2</td><td>Do not select</td><td>Ignore and execute</td></tr>
<tr>
<td rowspan="2">Task 4 can be created only after task 3 enters the "incremental sync" phase</td><td>Task 3</td><td>Structure initialization/full data initialization</td><td>Precheck and report error</td></tr>
<tr>
<td>Task 4</td><td>Do not select</td><td>Ignore and execute</td></tr>
<tr>
<td rowspan="2">Task 6 can be created only after task 5 enters the "incremental sync" phase</td><td>Task 5</td><td>Structure initialization/full data initialization</td><td>Precheck and report error</td></tr>
<tr>
<td>Task 6</td><td>Do not select</td><td>Ignore and execute</td></tr>
 <tr>
<td>Scenario 2: databases A, B, and C all have database/table structures and data</td><td>None</td><td>Tasks 1–6</td><td>Full data initialization</td><td>Ignore and execute</td></tr>
</table>

## Directions
Creating a multi-site active-active IDC architecture is to create multiple two-way sync tasks. For detailed directions, see [Creating Two-Way Sync Data Structure](https://intl.cloud.tencent.com/document/product/571/42605).
