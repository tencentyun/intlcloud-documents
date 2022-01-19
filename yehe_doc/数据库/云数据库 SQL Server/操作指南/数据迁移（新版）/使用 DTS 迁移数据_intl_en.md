This document describes how to use the data migration feature of DTS to migrate data from SQL Server to TencentDB for SQL Server.

## Notes 
- During full data migration, DTS consumes certain source database resources, which may increase the load and pressure of the source database. If your database configuration is low, we recommend you migrate the data during off-peak hours.
- Full migration is implemented with tables locked, during which write operations will be blocked for seconds.

## Prerequisites
- You have created a [TencentDB for SQL Server](https://intl.cloud.tencent.com/document/product/238/31571) instance.
- The source and target databases must meet the requirements for the migration feature and version as instructed in [Databases Supported by Data Migration](https://intl.cloud.tencent.com/document/product/571/42647).
- You have completed all [preparations](https://intl.cloud.tencent.com/document/product/571/42652).
- If the source database is not a TencentDB for SQL Server or TencentDB for SQL Server Basic Edition instance (such as a public network/CVM-based self-built instance or instance on another cloud), an account with the `sysadmin` permission needs to be used for migration, and the `xp_cmdshell` stored procedure must be able to run. If the source data is a TencentDB for SQL Server High-Availability Edition or Cluster Edition instance, there is no permission restriction.
- The migration account must be `localsystem`.
- The service where the source database is located must open the file sharing port 445.
- The source database must be set to "full recovery mode", and we recommend you make a full backup before migration.
- The local disk space of the source database must be large enough, so that the remaining free space can fit the size of the database to be migrated. 

## Application Restrictions
- Only one migration task can be initiated at any time for the same source instance.
- Currently, cross-region migration is supported between the Chinese mainland and Hong Kong (China) but not between other regions.
- Only database-level migration is supported (i.e., all objects in the database must be migrated together), while single-table migration is not supported.
- Logins, job agents, triggers, and database links (link server) at the instance level cannot be migrated.

## Operation Restrictions
- Do not modify or delete user information (including username, password, and permissions) in the source and target databases and port numbers during migration; otherwise, the migration task will fail.
- Do not perform transaction log backup during incremental sync; otherwise, the transaction log will be truncated and become discontinuous.
- If you only perform full data migration, do not write new data into the source database during migration; otherwise, the data in the source and target databases will be inconsistent. In scenarios with data writes, to ensure the data consistency in real time, we recommend you select full + incremental data migration.
- For full + incremental data migration, after you click **Complete** and the task status becomes **Completed**, do not write new data to the source database. We recommend you stop writing for two minutes; otherwise, the data in the source and target databases may be inconsistent.

## Supported SQL Operations
| Operation Type | Supported SQL Operations                                              |
| -------- | ------------------------------------------------------------ |
| DML | INSERT, UPDATE, DELETE, and REPLACE |
| DDL | TABLE: CREATE TABLE, ALTER TABLE, DROP TABLE, TRUNCATE TABLE, and RENAEM TABLE <br>VIEW: CREATE VIEW, ALTER VIEW, and DROP VIEW<br>INDEX: CREATE INDEX and DROP INDEX <br>DATABASE: CREATE DATABASE, ALTER DATABASE, and DROP DATABASE |

## Environment Requirements
>?The system will automatically check the following environment requirements before starting a migration task and report an error if a requirement is not met. If you can identify the failed check item, fix it as instructed in [Requirements for Check Items](https://intl.cloud.tencent.com/document/product/571/42552); otherwise, wait for the system verification to complete and fix the problem according to the error message.

| **Type** | **Environment Requirements** |
| :------------- | :----------------------------------------------------------- |
| Source database requirements | <li>The service where the source database resides must open the file sharing port 445. <br><li>The source and target databases can be connected. <br/><li>The server where the source database resides must have enough outbound bandwidth; otherwise, the migration speed will be affected. |
| Target database requirements | <li>Only migration from Basic Edition to High Availability Edition (including Dual-Server High Availability Edition and Cluster Edition) is supported, and the version number of the target database must be above that of the source database.<br/><li>The target database cannot have the same name as the source database. <br/><li>The disk space of the target database must be at least 1.5 times the size of the source database. <br/><li>The target database cannot have access requests or active businesses; otherwise, migration will fail. </li> |

## Directions
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/migration), select **Data Migration** on the left sidebar, and click **Create Migration Task** to enter the **Create Migration Task** page.
2. On the **Create Migration Task** page, select the region of the target database and click **Free Trial**. Currently, the DTS data migration feature is free of charge.
3. On the **Set source and target databases** page, configure the task, source database, and target database settings. After the source and target databases pass the connectivity test, click **Create**.
>?If the connectivity test fails, troubleshoot and fix the problem as prompted and as instructed in [Troubleshooting Guide](https://intl.cloud.tencent.com/document/product/571/42552) and try again.
>
<table>
<thead><tr><th width="10%">Setting Type</th><th width="20%">Configuration Item</th><th width="70%">Description</th></tr></thead>
<tbody>
<tr>
<td rowspan=3>Task Configuration</td>
<td>Task Name</td>
<td>Set a meaningful name for easy task identification.</td></tr>
<tr>
<td>Running Mode</td>
<td><ul><li>Immediate execution: the task will be started immediately after the task verification is passed.</li><li>Scheduled execution: you need to configure a task execution time and the task will be started automatically then.</li></ul></td></tr>
<tr>
<td>Tag</td>
<td>The tag is used to manage resources by category from different dimensions. If the existing tag does not meet your requirements, manage tags in the console.</td></tr>
<tr>
<td rowspan=6>Source Database Settings</td>
<td>Source Database Type</td><td>Select your source database type. In this document, select **SQL Server**.</td></tr>
<td>Access Type</td><td>Select a type based on your scenario. In this document, **Database** is selected as an example. For the preparations for different access types, see <a href="https://cloud.tencent.com/document/product/571/59968">Overview</a>.
<ul><li>Public Network: the source database can be accessed through a public IP.</li>
<li>Self-Build on CVM: the source database is deployed in a <a href="https://cloud.tencent.com/document/product/213">CVM</a> instance.</li>
<li>Direct Connect: the source database can be interconnected with VPCs through <a href="https://cloud.tencent.com/document/product/216">Direct Connect</a>.</li>
<li>VPN Access: the source database can be interconnected with VPCs through <a href="https://cloud.tencent.com/document/product/554">VPN Connection</a>.</li>
<li>Database: the source database is a TencentDB database.</li>
</ul>For a third-party cloud database, you can select **Public Network** generally or select **VPC Access**, **Direct Connect**, or **CCN** based on your actual network conditions.</td></tr>
<tr>
<td>Region</td><td>Select the region of the source database.</td></tr>
<tr>
<td>Database Instance</td><td>Select the instance ID of the target database.</td></tr>
<tr>
<td>Account</td><td>Account of the source SQL Server database, which must have the required permissions.</td></tr>
<tr>
<td>Password</td><td>Password of the source SQL Server database.</td></tr>
<tr>
<td rowspan=6>Target Database Settings</td>
<td>Target Database Type</td><td>Select **SQL Server**.</td></tr>
<tr>
<td>Access Type</td><td>Select a type based on your scenario. In this document, select **Database**.</td></tr>
<tr>
<td>Region</td><td>Select the region of the target database.</td></tr>
<tr>
<td>Database Instance</td><td>Select the instance ID of the target database.</td></tr>
<tr>
<td>Account.</td><td>Account of the target database, which must have the required permissions.</td></tr>
<tr>
<td>Password</td><td>Password of the target database.</td></tr>
</tbody></table>
4. On the **Set migration options and select migration objects** page, configure the migration type and objects and click **Save**.
<img src="https://main.qcloudimg.com/raw/3a0d33529d07be6b6c2ed7d245a0cf52.png"  style="zoom:80%;">
<table>
<thead><tr><th>Configuration Item</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Migration Type</td>
<td>Select a type based on your scenario.<ul><li>Full migration:the entire database will be migrated.</li><li>Full + incremental migration: the entire database and subsequent incremental data will be migrated. If there are data writes during migration, and you want to smoothly migrate the data in a non-stop manner, select this option.</li></ul></td></tr>
<tr>
<td>Specified Object</td>
<td>Only database-level migration is supported; that is, all objects in the specified database must be migrated together. Select the database to be migrated in **Source Database Object** and move it to the **Selected Object** box.</td></tr>
</tbody></table>
5. On the task verification page, verify the task. After the verification is passed, click **Start Task**.
    If the verification failed, fix the problem as instructed in [Fix for Verification Failure](https://intl.cloud.tencent.com/document/product/571/42552) and initiate the verification task again.
 - Failed: it indicates that a check item failed and the task is blocked. You need to fix the problem and run the verification task again.
 - Alarm: it indicates that a check item doesn't completely meet the requirements, and the task can be continued, but the business will be affected. You need to assess whether to ignore the alarm or fix the problem and continue the task based on the alarm message.
![](https://qcloudimg.tencent-cloud.cn/raw/acb446cee2725f999c8ced3614e85f2d.png)
6. Return to the data migration task list, and you can see that the task has entered the **Preparing** status. After 1–2 minutes, the data migration task will be started.
   - Select **Full migration**: once completed, the task will be stopped automatically.
   - Select **Full + Incremental migration**: after full migration is completed, the migration task will automatically enter the incremental data sync stage, which will not stop automatically. You need to click **Complete** to manually stop the incremental data sync.
      - Manually complete incremental data sync and business switch at appropriate time.
      - Observe whether the migration task is in the incremental sync stage and is not in the lag status. If so, stop writing data to the source database for a few minutes.
      - Manually complete incremental sync when the data gap between the target and the source databases is 0 MB and the time lag between them is 0 second.
7. (Optional) If you want to view, delete, or perform other operations on a task, click the task and select the target operation in the **Operation** column. For more information, see [Task Management](https://intl.cloud.tencent.com/document/product/571/42637).
8. After the migration task status becomes **Task successful**, you can formally cut over the business. For more information, see [Cutover Description](https://intl.cloud.tencent.com/document/product/571/42612).
