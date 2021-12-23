This document describes how to use the data migration feature of DTS to migrate data from PostgreSQL to TencentDB for PostgreSQL.

## Notes 
- During full data migration, DTS consumes certain source database resources, which may increase the load and pressure of the source database. If your database configuration is low, we recommend you migrate the data during off-peak hours.
- When migrating an instance on the public network, make sure that the source database service is accessible over the public network and keep the public network connection stable. If the network fluctuates or fails, migration will fail, in which case you need to initiate the migration task again.
- If the source PostgreSQL database is not TencentDB for PostgreSQL, it must have the replication permission; otherwise, the precheck will fail.

## Prerequisites
- You have created a [TencentDB for PostgreSQL](https://intl.cloud.tencent.com/document/product/409/40724) instance.
- The source and target databases must meet the requirements for the migration feature and version as instructed in [Databases Supported by Data Migration](https://cloud.tencent.com/document/product/571/58686).
- You have completed all [preparations](https://cloud.tencent.com/document/product/571/59968).
- The source database must have the following permissions:
  - If the source PostgreSQL database is not TencentDB for PostgreSQL, it must have the replication permission.  
  - If the source database is TencentDB for PostgreSQL, the source database user must be the initial user selected when the TencentDB instance is created.  
  - If some tables or objects have no permissions, you can use a high-privileged user to run the following sample statements to grant them permissions:  
```
grant select on table `table name` to `username`;
grant select on SEQUENCE `sequence name` to `username`;
grant connect on database `database name` to `username`;
grant select on large object `large object name` oid to `username`;
GRANT USAGE ON SCHEMA `schema name` to `username`;
```
- The target database user must be the initial user selected when the TencentDB instance is created. 
   - If the target database contains the database to be migrated and the database owner is not the current migration user, run the following statement to grant the database permissions to the migration user:
```
alter database `database name` owner to `migration user`;
```
   - If the target migration account is not a user with the `pg_tencentdb_superuser` role, the system will prompt "Failed to verify the target database permissions and unable to get the schema list" during verification. In this case, run the following statement to grant the initial user's permissions to the migration user:
```
grant pg_tencentdb_superuser to migration user;
```

## Application Restrictions
- Correlated data objects must be migrated together; otherwise, migration will fail. Common correlations include table reference by views, view reference by views, view/table reference by stored procedures/functions/triggers, and tables correlated through primary/foreign keys.
- To ensure migration efficiency, cross-region migration of CVM-based self-built instances is not supported. If you need cross-region migration, use the public network access type.
- If the entire instance is migrated, there cannot be users and roles in the target database with the same name as those in the source database.

## Operation Restrictions
- Do not modify or delete user information (including username, password, and permissions) in the source and target databases and port numbers during migration.
- Do not perform DDL or large object operations during structural, full, and incremental migration; otherwise, the migrated data will be inconsistent.
- If you only perform full data migration, only data before the migration start time will be migrated. If you write new data into the source database during migration, there will be data inconsistency between the source and target databases. In scenarios with data writes, to ensure the data consistency in real time, we recommend you select full + incremental data migration.

## Environment Requirements
>?The system will automatically check the following environment requirements before starting a migration task and report an error if a requirement is not met. If you can identify the failed check item, fix it as instructed in [Requirements for Check Items](https://cloud.tencent.com/document/product/571/58685); otherwise, wait for the system verification to complete and fix the problem according to the error message.

<table>
<tr><th width="20%">Type</th><th width="80%">Environment Requirement</th></tr>
<tr>
<td>Requirements for source database</td>
<td><ul>
<li>The source and target databases can be connected.</li>
<li>The server where the source database resides must have enough outbound bandwidth; otherwise, the migration speed will be affected.</li>
<li>Requirements for the database parameters:
<ul>
<li>The `wal_level` parameter in the source database must be set to `logical` during incremental migration.</li>
<li>The value of `max_replication_slots` in the source database must be greater than the number of databases to be migrated during incremental migration.</li>
<li>The value of `max_wal_senders` in the source database must be greater than the number of databases to be migrated during incremental migration.</li></ul>
</ul></td>
<tr> 
<td>Requirements for the target database</td>
<td>
<li>In full migration, the target database version must be greater than or equal to the source database version; in incremental migration, migration between versions above v10.x is supported.</li>
<li>The available size of the target database space must be at least 1.2 times that of the databases/tables to be migrated in the source database. (Incremental data migration will execute UPDATE and DELETE operations, causing some tables in the database to generate data fragments. Therefore, after migration is completed, the size of the tables in the target database may be larger than that in the source database. This is mainly because the `autovcauum` trigger conditions of the source and target databases are different.)</li>
<li>The target database cannot have migration objects such as usernames and tables with the same name as those in the source database.</li>
<li>The value of `max_worker_processes` of the target database during incremental migration must be greater than that of `max_logical_replication_workers`. </li>
</tr>
</table>

## Directions
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/migration), select **Data Migration** on the left sidebar, and click **Create Migration Task** to enter the **Create Migration Task** page.
2. On the **Create Migration Task** page, select the region of the target database and click **Free Trial**. Currently, the DTS data migration feature is free of charge.
>?Select the region with caution as it cannot be changed once the migration task is created.
3. On the **Set source and target databases** page, configure the task, source database, and target database settings. After the source and target databases pass the connectivity test, click **Create**.
>?If the connectivity test fails, troubleshoot and fix the problem as prompted and as instructed in [Troubleshooting Guide](https://intl.cloud.tencent.com/document/product/571/42552) and try again.
>
<table>
<thead><tr><th width="10%">Setting Type</th><th width="15%">Configuration Item</th><th width="75%">Description</th></tr></thead>
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
<td>Tags are used to manage resources by category in different dimensions. If the existing tags do not meet your requirements, go to the console to create more.</td></tr>
<tr>
<td rowspan=6>Source Database Settings</td>
<td>Source Database Type</td><td>Select your source database type. In this document, select **PostgreSQL**.</td></tr>
<tr>
<td>Access Type</td><td>Select a type based on your scenario. In this document, select **Database**.<br>To ensure migration efficiency, cross-region migration of CVM-based self-built instances is not supported. If you need cross-region migration, use the public network access type.
<ul><li>Public Network: the source database can be accessed through a public IP.</li>
<li>Self-Build on CVM: the source database is deployed in a <a href="https://intl.cloud.tencent.com/document/product/213">CVM</a> instance.</li>
<li>Direct Connect: the source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/216">Direct Connect</a>.</li>
<li>VPN Access: the source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/1037">VPN Connection</a>.</li>
<li>Database: the source database is a TencentDB database.</li>
<li>CCN: the source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/1003">CCN</a>.</li></ul>For the preparations for different access types, see <a href="https://intl.cloud.tencent.com/document/product/571/42652">Overview</a>.</td></tr>
<tr>
<td>Region</td><td>Select the region of the source PostgreSQL database.</td></tr>
<tr>
<td>Database Instance</td><td>Select the instance ID of the target database.</td></tr>
<tr>
<td>Account</td><td>Account of the source PostgreSQL database, which must have the required permissions.</td></tr>
<tr>
<td>Password</td><td>Password of the source PostgreSQL database.</td></tr>
<tr>
<td rowspan=6>Target Database Settings</td>
<td>Target Database Type</td><td>Select **PostgreSQL**.</td></tr>
<tr>
<td>Access Type</td><td>Select a type based on your scenario. In this document, select **Database**.</td></tr>
<tr>
<td>Region</td><td>Select the same region as in the source database settings.</td></tr>
<tr>
<td>Database Instance</td><td>Select the instance ID of the target database.</td></tr>
<tr>
<td>Account.</td><td>Account of the target database, which must have the required permissions.</td></tr>
<tr>
<td>Password</td><td>Password of the target database.</td></tr>
</tbody></table>
4. On the **Set migration options and select migration objects** page, configure the migration type and objects and click **Save**.
<table>
<thead><tr><th>Configuration Item</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Migration Type</td>
<td>Select a type based on your scenario.<ul><li>Structural migration: structured data such as databases and tables in the database will be migrated.</li><li>Full migration:the entire database will be migrated.</li><li>Full + incremental migration: the entire database and subsequent incremental data will be migrated. If there are data writes during migration, and you want to smoothly migrate the data in a non-stop manner, select this option.</li></ul></td></tr>
<tr>
<td>Migration Object</td>
<td><ul><li>Entire instance: migrate the entire database instance, including the metadata definitions of roles and users but excluding system databases such as system objects in PostgreSQL.</li>
<li>Specified objects: migrate specified objects.</li></ul> </td></tr>
<tr>
<td>Specify object</td>
<td>Select the objects to be migrated in **Source Database Object** and move them to the **Selected Object** box.</td></tr>
</tbody></table>
5. On the task verification page, verify the task. After the verification is passed, click **Start Task**.
    If the verification failed, fix the problem as instructed in [Fix for Verification Failure](https://intl.cloud.tencent.com/document/product/571/42552) and initiate the verification task again.
  - Failed: it indicates that a check item failed and the task is blocked. You need to fix the problem and run the verification task again.
  - Alarm: it indicates that a check item doesn't completely meet the requirements, and the task can be continued, but the business will be affected. You need to assess whether to ignore the alarm or fix the problem and continue the task based on the alarm message.
6. Return to the data migration task list, and you can see that the task has entered the **Preparing** status. After 1–2 minutes, the data migration task will be started.
   - Select **Structural migration** or **Full migration**: once completed, the task will be stopped automatically.
   - Select **Full + Incremental migration**: after full migration is completed, the migration task will automatically enter the incremental data sync stage, which will not stop automatically. You need to click **Complete** to manually stop the incremental data sync. Then, the task will enter the **Completed** status. At this point, do not make any changes to the source and target databases. The backend will automatically align some objects with the source.
      - Select an appropriate time to manually complete the incremental data sync and perform business switch.
      - You can see that the migration task is in the incremental sync stage, and there is no latency. Stop writing the source database for several minutes.
      - When the source-target database data gap is 0 MB, and the source-target database time lag is 0s, manually complete the incremental sync.
7. (Optional) If you want to view, delete, or perform other operations on a task, click the task and select the target operation in the **Operation** column. For more information, see [Task Management](https://intl.cloud.tencent.com/document/product/571/42637).
8. After the migration task status becomes **Task successful**, you can formally cut over the business. For more information, see [Cutover Description](https://intl.cloud.tencent.com/document/product/571/42612).
