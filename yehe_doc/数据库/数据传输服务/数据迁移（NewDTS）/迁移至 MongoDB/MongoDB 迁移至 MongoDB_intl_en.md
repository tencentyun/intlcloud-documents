 This document describes how to use the data migration feature of DTS to migrate data from MongoDB to TencentDB for MongoDB. 

MongoDB supports heterogeneous migration between replica set and sharded cluster, i.e., four source-target architecture scenarios: replica set-to-replica set, replica set-to-sharded cluster, sharded cluster-to-replica set, and sharded cluster-to-sharded cluster.

## Notes
- When DTS performs full data migration, it will occupy certain source instance resources, which may increase the load of the source instance and the database pressure. If your database has low configurations, we recommend that you migrate data during off-peak hours.
- To migrate instances over the public network, make sure that the source instance is accessible from the public network.

## Prerequisites
- You have created a [TencentDB for MongoDB](https://intl.cloud.tencent.com/document/product/240/3551) instance.
- The source and target databases must meet the requirements for the migration feature and version as instructed in [Databases Supported by Data Migration](https://intl.cloud.tencent.com/document/product/571/42647).
- You have completed all [preparations](https://intl.cloud.tencent.com/document/product/571/42652).
- You need to create a read-only account in the source instance for the migration; otherwise, the precheck will fail.
```
use admin
db.createUser({
    user: "username",
    pwd: "password",
    roles:
        [
            {role: "readAnyDatabase", db: "admin"},
            {role: "read", db: "local"}
        ]
})
```

## Restrictions
- To ensure migration efficiency, cross-region migration is not supported for CVM-based MongoDB instances.
- Incremental migration is not supported for self-built single-node instances as they have no oplogs.

## Operation Restrictions
- During migration, do not perform the following operations; otherwise, the migration task will fail: 
  - Do not modify or delete user information (including username, password, and permissions) in the source and target databases and port numbers.
  - Do not clear oplogs in the source database.
  - Do not delete the target database `TencetDTSData` during data migration.
  - Manipulate data in the target database with caution during data migration; otherwise, data inconsistency may occur.
  - As DTS will filter out the DDL operations of the sharded cluster, do not perform DDL operations other than transactions on the source database during shard migration; otherwise, data inconsistency may occur.
- If you only perform full data migration, do not write new data into the source instance during migration; otherwise, the data in the source and target databases will be inconsistent. In scenarios with data writes, to ensure the data consistency in real time, we recommend you select full + incremental data migration.

## Supported SQL Operations
> ?Only replica set migration supports DDL operations, while shard migration will filter out DDL operations (except transactions).

| **Operation Type** | **Supported SQL Operation** |
| ------------ | ------------------------------------------------------------ |
| DML          | INSERT, UPDATE, and DELETE                                       |
| DDL          | INDEX: createIndexes, createIndex, dropIndex, and dropIndexes<br>COLLECTION: createCollection, drop, collMod, renameCollection, and convertToCapped<br>DATABASE: dropDatabase and copyDatabase |

## Environment Requirements

| **Type** | **Environment Requirements** |
| -------------- | ------------------------------------------------------------ |
| Source database requirements | <li>The server where the source database resides must have enough outbound bandwidth; otherwise, the migration speed will be affected.<li>The user account provided by the source database must have permission to read the database. <li>The source database cannot have a database named `TencetDTSData`. <li>If the source database is in cluster mode, the balancer must be disabled before incremental sync. <li>Oplogs must be obtained from the source database during full + incremental migration. |
| Target database requirements | <li>The space of the target database must be at least 1.3 times the size of the tables to be migrated in the source database. <li>The user account provided by the target database must have the root privilege. <li>The target database cannot have a database named `TencetDTSData`. <li>The target database cannot have tables with the same name as those in the source database. <br><li>If the source database is a shard, you must enter the correct `mongos`, `config server`, and `mongod` node information. <li>The target database cannot have active businesses; otherwise, a warning will be reported. <li>The shardkey information of the source and target databases must be the same; otherwise, a warning will be reported.</li> |

## Directions
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts), select **Data Migration** on the left sidebar, and click **Create Migration Task** to enter the **Create Migration Task** page.
2. On the **Create Migration Task** page, select the types, regions, and specifications of the source and target instances and click **Buy Now**.
<table>
<thead><tr><th>Configuration Item</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Source Instance Type</td>
<td>Select the source database type, which cannot be changed after purchase. In this scenario, select <b>MongoDB</b>.</td></tr>
<tr>
<td>Source Instance Region</td>
<td>Select the source database region. If the source database is a self-built one, select a region nearest to it.</td></tr>
<tr>
<td>Target Instance Type</td>
<td>Select the target database type, which cannot be changed after purchase. In this scenario, select <b>MongoDB</b>.</td></tr>
<tr>
<td>Target Instance Region</td>
<td>Select the target database region.</td></tr>
<tr>
<td>Specification</td>
<td>Select the specification of the migration linkage according to your business conditions.</td></tr>
</tbody></table>

3. On the **Set source and target databases** page, configure the task, source database, and target database settings.  
>?Create a read-only account in the source instance for migration; otherwise, the precheck will fail.
>
**As there are many cross-scenarios of source database deployment modes and access types, the migration steps for different scenarios are similar. The following only provides configuration examples for typical scenarios. For other scenarios, configure by referring to the examples.**
**Example 1**: Migrate a local self-built MongoDB instance (sharded cluster) to a TencentDB instance over Direct Connect.
![](https://qcloudimg.tencent-cloud.cn/raw/c867347ff1dff2dc8643a13013c0f47f.png)
<table>
<thead><tr><th width="10%">Setting Type</th><th width="15%">Configuration Item</th><th width="75%">Description</th></tr></thead>
<tbody>
<tr>
<td rowspan=2>Task Configuration</td>
<td>Task Name</td>
<td>Set a meaningful name for easy task identification.</td></tr>
<tr>
<td>Running Mode</td>
<td><ul><li>Immediate execution: The task will be started immediately after the task verification is passed.</li><li>Scheduled execution: You need to configure a task execution time and the task will be started automatically then.</li></ul></td></tr>
<tr>
<td rowspan=13>Source Database Settings</td>
<td>Source Database Type</td><td>The source database type selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Region</td><td>The source database region selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Access Type</td><td>Select a type based on your scenario. This scenario takes <b>Direct Connect</b> as an example. For the preparations for different access types, see <a href="https://intl.cloud.tencent.com/document/product/571/42652">Overview</a>.
<ul><li>Public Network: The source database can be accessed through a public IP.</li>
<li>Self-Build on CVM: The source database is deployed in a <a href="https://intl.cloud.tencent.com/document/product/213">CVM</a> instance.</li>
<li>Direct Connect: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/216">Direct Connect</a>.</li>
<li>VPN Access: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/1037">VPN Connections</a>.</li>
<li>Database: The source database is a TencentDB instance.</li>
<li>CCN: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/1003">CCN</a>.</li><li>VPC: Both the source and target databases are deployed in Tencent Cloud and have <a hrref="https://intl.cloud.tencent.com/document/product/215">VPCs</a>.</li></ul></td></tr>
<tr>
<td>Architecture</td><td>Select the architecture of the source database. This scenario takes <b>Cluster Migration</b> as an example.</td></tr>
<tr>
<td>VPC-based Direct Connect Gateway</td><td>Only VPC-based direct connect gateway is supported. Confirm the network type associated with the gateway.</tr>
<tr>
<td>VPC</td><td>Select the VPC and subnet of the VPC-based Direct Connect gateway.</td></tr>
<tr>
<td>Node - mongod</td><td>Enter the IP and port of the mongod node and separate multiple nodes by line breaks, such as `186.3.55.77:6379`.</td></tr>
<tr>
<td>Node - mongos</td><td>Enter the IP and port of the mongos node.</td></tr>
<tr>
<td>Node - config server</td><td>Enter the IP and port of the config server node.</td></tr>
<tr>
<td>Authentication Required</td><td>Select whether to check the security of username and password in the source database.</td></tr>
<tr>
<td>Authentication Database</td><td>Name of the database to be authenticated, i.e., name of the database of the account executing the migration task, such as `admin`.</td></tr>
<tr>
<td>Authentication Mechanism</td><td>Currently, SCRAM-SHA-1 is supported.</td></tr>
<tr>
<td>Account & Password Selection</td><td>If the three nodes of mongod, mongos, and config server in the source database have the same account and password, select <b>Same account & password</b>; otherwise, select <b>Different accounts & passwords</b> and enter their respective accounts and passwords.</td></tr>
<tr>
<td rowspan=6>Target Database Settings</td>
<td>Target Database Type</td><td>The target database type selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Region</td><td>The target database region selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Access Type</td><td>In this scenario, select <b>Database</b>.</td></tr>
<tr>
<td>Database Instance</td><td>Select the instance ID of the target database.</td></tr>
<tr>
<td>Account</td><td>Account of the target database, which must have the required permissions.</td></tr>
<tr>
<td>Password</td><td>Password of the target database.</td></tr>
</tbody></table>
<b>Example 2</b>: Migrate between two TencentDB instances.
<img src="https://qcloudimg.tencent-cloud.cn/raw/7b7d3b493950ac63761a7389e42b8fac.png" >

<table>
<thead><tr><th width="10%">Setting Type</th><th width="15%">Configuration Item</th><th width="75%">Description</th></tr></thead>
<tbody>
<tr>
<td rowspan=3>Task Configuration</td>
<td>Task Name</td>
<td>Set a meaningful name for easy task identification.</td></tr>
<tr>
<td>Running Mode</td>
<td><ul><li>Immediate execution: The task will be started immediately after the task verification is passed.</li><li>Scheduled execution: You need to configure a task execution time and the task will be started automatically then.</li></ul></td></tr>
<tr>
<td>Tag</td>
<td>Tags are used to manage resources by category in different dimensions. If the existing tags do not meet your requirements, go to the console to create more.</td></tr>
<tr>
<td rowspan=7>Source Database Settings</td>
<td>Source Database Type</td><td>The source database type selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Region</td><td>The source database region selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Access Type</td><td>If the source database is a TencentDB instance, select <b>Database</b>. For the preparations for different access types, see <a href="https://intl.cloud.tencent.com/document/product/571/42652">Overview</a>.
<ul><li>Public Network: The source database can be accessed through a public IP.</li>
<li>Self-Build on CVM: The source database is deployed in a <a href="https://intl.cloud.tencent.com/document/product/213">CVM</a> instance.</li>
<li>Direct Connect: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/216">Direct Connect</a>.</li>
<li>VPN Access: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/1037">VPN Connections</a>.</li>
<li>Database: The source database is a TencentDB instance.</li>
<li>CCN: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/1003">CCN</a>.</li><li>VPC: Both the source and target databases are deployed in Tencent Cloud and have <a hrref="https://intl.cloud.tencent.com/document/product/215">VPCs</a>.</li></ul></td></tr>
<tr>
<td>Cross-/Intra-Account</td><td>This parameter needs to be configured when <b>TencentDB</b> is selected as the access type. <ul><li>Intra-account: The source and target database instances belong to the same Tencent Cloud root account. </li><li>Cross-account: The source and target database instances belong to different Tencent Cloud root accounts.</li></ul></td></tr>
<tr>
<td>Database Instance</td><td>Select the instance ID of the source database.</td></tr>
<tr>
<td>Account</td><td>Account of the source MongoDB database, which must have the required permissions.</td></tr>
<tr>
<td>Password</td><td>Password of the source MongoDB database.</td></tr>
<tr>
<td rowspan=6>Target Database Settings</td>
<td>Target Database Type</td><td>The target database type selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Region</td><td>The target database region selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Access Type</td><td>In this scenario, select <b>Database</b>.</td></tr>
<tr>
<td>Database Instance</td><td>Select the instance ID of the target database.</td></tr>
<tr>
<td>Account</td><td>Account of the target database, which must have the required permissions.</td></tr>
<tr>
<td>Password</td><td>Password of the target database.</td></tr>
</tbody></table>
<b>Example 3</b>: Migrate an ApsaraDB for MongoDB instance (sharded cluster) to a TencentDB instance.
<table>
<thead><tr><th width="10%">Setting Type</th><th width="15%">Configuration Item</th><th width="75%">Description</th></tr></thead>
<tbody>
<tr>
<td rowspan=2>Task Configuration</td>
<td>Task Name</td>
<td>Set a meaningful name for easy task identification.</td></tr>
<tr>
<td>Running Mode</td>
<td><ul><li>Immediate execution: The task will be started immediately after the task verification is passed.</li><li>Scheduled execution: You need to configure a task execution time and the task will be started automatically then.</li></ul></td></tr>
<tr>
<td rowspan=11>Source Database Settings</td>
<td>Source Database Type</td><td>The source database type selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Region</td><td>The source database region selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Access Type</td><td>For a third-party cloud database, you can select <b>Public Network</b> generally or select <b>VPN Access</b>, <b>Direct Connect</b>, or <b>CCN</b> based on your actual network conditions. This scenario takes <b>Public Network</b> as an example. For the preparations for different access types, see <a href="https://intl.cloud.tencent.com/document/product/571/42652">Overview</a>.
<ul><li>Public Network: The source database can be accessed through a public IP.</li>
<li>Self-Build on CVM: The source database is deployed in a <a href="https://intl.cloud.tencent.com/document/product/213">CVM</a> instance.</li>
<li>Direct Connect: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/216">Direct Connect</a>.</li>
<li>VPN Access: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/1037">VPN Connections</a>.</li>
<li>Database: The source database is a TencentDB instance.</li>
<li>CCN: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/1003">CCN</a>.</li><li>VPC: Both the source and target databases are deployed in Tencent Cloud and have <a hrref="https://intl.cloud.tencent.com/document/product/215">VPCs</a>.</li></ul></td></tr>
<tr>
<td>Architecture</td><td>Select the architecture of the source database. This scenario takes <b>Cluster Migration</b> as an example.</td></tr>
<tr>
<td>Node - mongod</td><td>Enter the IP and port of the mongod node and separate multiple nodes by line breaks, such as `186.3.55.77:6379`.</td></tr>
<tr>
<td>Node - mongos</td><td>Enter the IP and port of the mongos node.</td></tr>
<tr>
<td>Node - config server</td><td>Enter the IP and port of the config server node.</td></tr>
<tr>
<td>Authentication Required</td><td>Select whether to check the security of username and password in the source database.</td></tr>
<tr>
<td>Authentication Database</td><td>Name of the database to be authenticated, i.e., name of the database of the account executing the migration task, such as `admin`.</td></tr>
<tr>
<td>Authentication Mechanism</td><td>Currently, SCRAM-SHA-1 is supported.</td></tr>
<tr>
<td>Account & Password Selection</td><td>If the three nodes of mongod, mongos, and config server in the source database have the same account and password, select <b>Same account & password</b>; otherwise, select <b>Different accounts & passwords</b> and enter their respective accounts and passwords.</td></tr>
<tr>
<td rowspan=6>Target Database Settings</td>
<td>Target Database Type</td><td>The target database type selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Region</td><td>The target database region selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Access Type</td><td>In this scenario, select <b>Database</b>.</td></tr>
<tr>
<td>Database Instance</td><td>Select the instance ID of the target database.</td></tr>
<tr>
<td>Account</td><td>Account of the target database, which must have the required permissions.</td></tr>
<tr>
<td>Password</td><td>Password of the target database.</td></tr>
</tbody></table>

4. Test the connectivity between the source and target instances.
If the connectivity test fails, fix the problem as instructed in [Failed Connectivity Test](https://intl.cloud.tencent.com/document/product/571/47306).
5. On the **Set migration options and select migration objects** page, set the migration options and migration objects (you can select specified databases and tables).
<table>
<thead><tr><th>Configuration Item</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Migration Type</td>
<td>Select a type based on your scenario. <ul><li>Full migration: The entire database will be migrated. The migrated data will only be existing content of the source database when the task is initiated but not include the incremental data written to the source database after the task is initiated. </li><li>Full + Incremental migration: The migrated data will include the existing content of the source database when the task is initiated as well as the incremental data written to the source database after the task is initiated. If there are data writes to the source database during migration, and you want to smoothly migrate the data in a non-stop manner, select this option.</li></ul></td></tr>
<tr>
<td>Migration Object</td>
<td><ul><li>Entire instance: Migrate the entire database instance, including the metadata definitions of roles and users but excluding system databases such as system objects in PostgreSQL.</li>
<li>Specified objects: Migrate specified objects.</li></ul> </td></tr>
<tr>
<td>Specified objects</td>
<td>Select the objects to be migrated in <b>Source Database Object</b> and move them to the <b>Selected Object</b> box.</td></tr>
</tbody></table>

6. On the **Verify task** page, complete the precheck and click **Start Task**.
If the verification fails, fix the problem as instructed in [Fix for Verification Failure](https://intl.cloud.tencent.com/document/product/571/42552) and initiate the verification task again.
 - Failed: It indicates that a check item fails and the task is blocked. You need to fix the problem and run the verification task again.
 - Alarm: It indicates that a check item doesn't completely meet the requirements, and the task can be continued, but the business will be affected. You need to assess whether to ignore the alarm or fix the problem and continue the task based on the alarm message.
7. Return to the migration task list. After the incremental sync is 100% complete, click **Complete** in the **Operation** column to complete the migration task.
 - Select **Structural migration** or **Full migration**: Once completed, the task will be stopped automatically.
 - Select **Full + Incremental migration**: After full migration is completed, the migration task will automatically enter the incremental data sync stage, which will not stop automatically. You need to click **Complete** to manually stop the incremental data sync.
   - Manually complete incremental data sync and business switchover at appropriate time.
    - Observe whether the migration task is in the incremental sync stage and is not in the lag status. If so, stop writing data to the source database for a few minutes.
    - Manually complete incremental sync when the data gap between the target and the source databases is 0 MB and the time lag between them is 0 seconds.
8. (Optional) If you want to view, delete, or perform other operations on a task, click the task and select the target operation in the **Operation** column. For more information, see [Task Management](https://intl.cloud.tencent.com/document/product/571/42637).
9. After the migration task status becomes **Task successful**, you can formally cut over the business. For more information, see [Cutover Description](https://intl.cloud.tencent.com/document/product/571/42612).

