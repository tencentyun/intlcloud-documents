This document describes how to use the data migration feature of DTS to migrate data from PostgreSQL to TencentDB for PostgreSQL.

The steps of data migration from TDSQL-C for PostgreSQL to TencentDB for PostgreSQL are basically the same as those in this scenario.

## Notes 
- When DTS performs full data migration, it will occupy certain source instance resources, which may increase the load of the source instance and the database pressure. If your database has low configurations, we recommend that you migrate data during off-peak hours.
- When you migrate an instance over the public network, make sure that the source database service is accessible over the public network and keep the public network connection stable. If the network fluctuates or fails, migration will fail, and you need to restart the migration task.
- If the source PostgreSQL database is not TencentDB for PostgreSQL, it must have the replication permission; otherwise, the precheck will fail.
- During migration, the migration rate can be affected by factors such as the read performance of the source, the network bandwidth between the source and the target instances, and the specification of the target instance. Migration concurrency is determined by number of CPU cores of target instance, for instance, if the target instance has 2 cores, concurrency will be 2.

## Prerequisites
- You have created a TencentDB for PostgreSQL instance as instructed in [Creating TencentDB for PostgreSQL Instance](https://intl.cloud.tencent.com/document/product/409/40724).
- The source and target databases must meet the requirements for the migration feature and version as instructed in [Databases Supported by Data Migration](https://intl.cloud.tencent.com/document/product/571/42647).
- You have completed all the preparations as instructed in [Overview](https://intl.cloud.tencent.com/document/product/571/42652).
- Permissions required for the source database:
  - If the source PostgreSQL database is not TencentDB for PostgreSQL, it must have the replication permission.  
  - If the source database is TencentDB for PostgreSQL, the source database account must be the initial user selected when the TencentDB instance is created.  
  - If some tables or objects have no permissions, you can use a high-privileged user to run the following sample statements to grant them permissions:  
```
grant select on table `table name` to `username`;
grant select on SEQUENCE `sequence name` to `username`;
grant connect on database `database name` to `username`;
grant select on large object `large object name` oid to `username`;
GRANT USAGE ON SCHEMA `schema name` to `username`;
```
- The target database account must be the initial user selected when the TencentDB instance is created.   
 - If the target database instance contains the database to be migrated and the database owner is not the current migration user, run the following statement to grant the database permissions to the migration user:
```
alter database `database name` owner to `migration user`;
```
  - If the migration user (the account executing the migration task) is not a user with the `pg_tencentdb_superuser` role, the system will prompt "Failed to verify the target instance permissions and unable to get the schema list" during verification. In this case, run the following statement to grant the initial user's permissions to the migration user:
```
grant pg_tencentdb_superuser to migration user;
```

## Use limits
- Correlated data objects must be migrated together; otherwise, migration will fail. Common correlations include table referenced by views, view referenced by views, view/table referenced by procedures/functions/triggers, and tables correlated through primary/foreign keys.
- To ensure migration efficiency, the data of CVM-based self-built instances cannot be migrated across regions over the private network. If you need to migrate data across regions, you can do so over the public network .
- To migrate the entire instance, there cannot be users and roles in the target database with the same name as those in the source database.
- If you select **Full + Incremental migration**, tables in the source database must have a primary key; otherwise, data inconsistency will occur in the source and target database. We recommend you select **Full migration** for tables without the primary key.

## Operation limits
- Do not modify or delete user information (including username, password, and permissions) in the source and target databases and port numbers during migration.
- Do not perform DDL or large object operations during structural, full, and incremental migration; otherwise, the migrated data will be inconsistent.
- If you only perform full data migration, only data before the migration start time will be migrated. If you write new data into the source instance during migration, there will be data inconsistency between the source and target databases. In scenarios with data writes, to ensure the data consistency in real time, we recommend you select full + incremental data migration.

## Environment requirements
> ?The system will automatically check the following environment requirements before starting a migration task and report an error if a requirement is not met. If you can identify the failed check item, fix it as instructed in [Check Item Overview](https://intl.cloud.tencent.com/document/product/571/42551); otherwise, wait for the system verification to complete and fix the problem according to the error message.

<table>
<tr><th width="20%">Type</th><th width="80%">Environment Requirement</th></tr>
<tr>
<td>Requirements for source database</td>
<td><ul>
<li>The source and target databases can be connected.</li>
<li>The server where the source database resides must have enough outbound bandwidth; otherwise, the migration speed will be affected.</li>
<li>Requirements for the instance parameters:
<ul>
<li>The `wal_level` parameter in the source database must be set to `logical` during incremental migration.</li>
<li>The value of `max_replication_slots` in the source database must be greater than the number of databases to be migrated during incremental migration.</li>
<li>The value of `max_wal_senders` in the source database must be greater than the number of databases to be migrated during incremental migration.</li></ul>
</ul></td>
<tr> 
<td>Requirements for the target database</td>
<td>
<li>In full migration, the target database version must be greater than or equal to the source database version; in incremental migration, migration between versions later than v10.x is supported.</li>
<li>The available size of the target database space must be at least 1.2 times that of the instances to be migrated in the source database. Incremental data migration will execute UPDATE and DELETE operations, causing some tables in the database to generate data fragments. Therefore, after migration is completed, the size of the tables in the target database may be larger than that in the source database. This is mainly because that the `autovcauum` trigger conditions of the source and target databases are different.</li>
<li>The target database cannot have migration objects such as usernames and tables with the same name as those in the source database.</li>
<li>The value of `max_worker_processes` of the target database during incremental migration must be greater than that of `max_logical_replication_workers`. </li>
</tr>
</table>

## Directions
1 (Optional) When PostgreSQL 9.4, 9.5, and 9.6 are used as the source database for "full + incremental migration", you can install the tencent_decoding extension as instructed below. For other scenarios, skip this step.
 1. Download extension based on architecture of server where source database resides.  
    - Only "x86_64" and "aarch64" system architectures are supported.
    - The version of the extension version need to be the same as that of PostgreSQL.
    - Requirements for the Glibc version: x86_64 system should be v2.17 - 323 or later; aarch64 system should be v2.17 - 260 or later. 
       - View Glibc version on Linux system
```
RHEL/CentOS: rpm -q glibc
```
       - View Glibc version on other operation systems (Debian/Ubuntu/SUSE)
```
ldd --version | grep -i libc
```
Download address: [x86_64 9.4](https://postgresql-1258344699.cos.ap-shanghai.myqcloud.com/tencent_decoding/9.4/tencent_decoding.so), [x86_64 9.5](https://postgresql-1258344699.cos.ap-shanghai.myqcloud.com/tencent_decoding/9.5/tencent_decoding.so), [x86_64 9.6](https://postgresql-1258344699.cos.ap-shanghai.myqcloud.com/tencent_decoding/9.6/tencent_decoding.so), [aarch64 9.4](https://postgresql-1258344699.cos.ap-shanghai.myqcloud.com/tencent_decoding_aarch64/9.4/tencent_decoding.so), [aarch64 9.5](https://postgresql-1258344699.cos.ap-shanghai.myqcloud.com/tencent_decoding_aarch64/9.5/tencent_decoding.so), [aarch64 9.6](https://postgresql-1258344699.cos.ap-shanghai.myqcloud.com/tencent_decoding_aarch64/9.6/tencent_decoding.so)    
 2. Place the downloaded tencent_decoding.so file in the lib folder of the Postgres process directory without restarting the instance. 
2. Log in to the [DTS console](https://console.cloud.tencent.com/dts/migration), select **Data Migration** on the left sidebar, click **Create Migration Task**, and enter the **Create Migration Task** page.
3. On the **Create Migration Task** page, select the types, regions, and specifications of the source and target instances and click **Buy Now**.
<table>
<thead><tr><th>Configuration Item</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Source Instance Type</td>
<td>Select the source database type, which cannot be changed after purchase. In this scenario, select <b>PostgreSQL</b>.</td></tr>
<tr>
<td>Source Instance Region</td>
<td>Select the source database region. If the source database is a self-built one, select a region nearest to it.</td></tr>
<tr>
<td>Target Instance Type</td>
<td>Select the target database type, which cannot be changed after purchase. In this scenario, select <b>PostgreSQL</b>.</td></tr>
<tr>
<td>Target Instance Region</td>
<td>Select the target database region.</td></tr>
<tr>
<td>Specification</td>
<td>Select the specification of the migration link based on your business needs.</td></tr>
</tbody></table>

4. Complete task configuration, source database settings, and target database settings on the **Set source and target databases** page. After the connectivity test for the source and target databases is passed, click **Create**.
>?If the connectivity test fails, troubleshoot as prompted or as instructed in [Database Connection Check](https://intl.cloud.tencent.com/document/product/571/42552) and try again.
>
<table>
<thead><tr><th width="10%">Setting Type</th><th width="15%">Configuration Item</th><th width="75%">Description</th></tr></thead>
<tbody>
<tr>
<td rowspan=3>Task Configuration</td>
<td>Task Name</td>
<td>Set a task name that is easy to identify.</td></tr>
<tr>
<td>Running Mode</td>
<td><ul><li>Immediate execution: The task will be started immediately after the task verification is passed.</li><li>Scheduled execution: You need to configure a task execution time and the task will be started automatically then.</li></ul></td></tr>
<tr>
<td>Tag</td>
<td>Tags are used to manage resources by category in different dimensions. If the existing tags do not meet your requirements, go to the console to create more.</td></tr>
<tr>
<td rowspan=6>Source Database Settings</td>
<td>Source Database Type</td><td>The source database type selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Region</td><td>The source database region selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Access Type</td><td>Select a type based on your scenario. In this scenario, <b>TencentDB</b> is selected as an example. For the preparations for different access types, see <a href="https://intl.cloud.tencent.com/document/product/571/42652">Overview</a>. <br>To ensure migration efficiency, the data of CVM-based self-built instances cannot be migrated across regions over the private network. If you need to migrate data across regions, you can do so over the public network.
<ul><li>Public Network: The source database can be accessed through a public IP.</li>
<li>Self-Build on CVM: The source database is deployed in a <a href="https://intl.cloud.tencent.com/document/product/213">CVM</a> instance.</li>
<li>Direct Connect: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/216">Direct Connect</a>.</li>
<li>VPN Access: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/1037">VPN Connections</a>.</li>
<li>Database: The source database is a TencentDB instance.</li>
<li>CCN: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/1003">CCN</a>.</li>
<tr>
<td>Database Instance</td><td>Select the instance ID of source PostgreSQL database .</td></tr>
<tr>
<td>Account</td><td>Account of the source PostgreSQL database, which must have the required permissions.</td></tr>
<tr>
<td>Password</td><td>Password of the source PostgreSQL database account.</td></tr>
<tr>
<td rowspan=6>Target Database Settings</td>
<td>Target Database Type</td><td>The target database type selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Region</td><td>The target database region selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Access Type</td><td>Select a type based on your scenario. In this scenario, select <b>Database</b>.</td></tr>
<tr>
<td>Database Instance</td><td>Select the instance ID of the target database.</td></tr>
<tr>
<td>Account</td><td>Account of the target database, which must have the required permissions.</td></tr>
<tr>
<td>Password</td><td>Password of the target database account.</td></tr>
</tbody></table>
5. On the **Set migration options and select migration objects** page, set the migration type and objects, and click **Save**.
<table>
<thead><tr><th>Configuration Item</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Migration Type</td>
<td>Select a type based on your scenario. <ul><li> Structural migration: Structured data of databases and tables will be migrated. </li><li>Full migration: The entire database will be migrated. The migrated data will include only the existing data from the source database when the task is started, not incremental data written to the source database after the task is started. </li><li>Full + Incremental migration: The migrated data will include the existing data from the source database when the task is started as well as the incremental data written to the source database after the task is started. If there are data writes to the source database during migration, and you want to smoothly migrate the data in a non-stop manner, select this type.</li></ul></td></tr>
<tr>
<td>Migration Object</td>
<td><ul><li>Entire instance: Migrate the entire database instance, including the metadata definitions of roles and users but excluding system databases such as system objects in PostgreSQL.</li>
<li>Specified objects: Migrate specified objects.</li></ul> </td></tr>
<tr>
<td>Specified objects</td>
<td>Select the objects to be migrated in <b>Source Database Object</b> and move them to the <b>Selected Object</b> box.</td></tr>
</tbody></table>

6. Verify the migration task on the **Verify task** page. After the task is verified, click **Start**.
    If the verification fails, fix the problem as instructed in [Check Item Overview](https://intl.cloud.tencent.com/document/product/571/42551) and initiate the verification again.
  - Failed: It indicates that a check item fails and the task is blocked. You need to fix the problem and run the verification task again.
  - Alarm: It indicates that a check item doesn't completely meet the requirements, and the task can be continued, but the business will be affected. You need to assess whether to ignore the alarm or fix the problem and continue the task based on the alarm message.
7. Return to the data migration task list, and the task will be in the **Preparing** status. After running for 1-2 minutes, the data migration task will be started.
   - Select **Structural migration** or **Full migration**: Once completed, the task will be stopped automatically.
   - Select **Full + Incremental migration**: After full migration is completed, the migration task will automatically enter the incremental data sync stage, which will not stop automatically. You need to click **Complete** to manually stop the incremental data sync. Then, the task will enter the **Completed** status. At this point, do not make any changes to the source and target databases. The backend will automatically align some objects with the source.
      - Manually complete incremental data sync and business switchover at appropriate time.
      - Check whether the migration task is in the incremental sync stage without any lag. If so, stop writing data to the source database for a few minutes.
      - Manually complete incremental sync when the data gap between the target and the source databases is 0 MB and the time lag between them is 0 seconds.
8. (Optional) If you want to view, delete, or perform other operations on a task, click the task and select the target operation in the **Operation** column. For more information, see [Viewing Task](https://intl.cloud.tencent.com/document/product/571/42637).
9. After the migration task status becomes **Task successful**, you can formally cut over the business. For more information, see [Cutover Description](https://intl.cloud.tencent.com/document/product/571/42612).

