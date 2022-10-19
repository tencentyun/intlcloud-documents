## Feature overview
The data sync feature refers to real-time data sync between two database sources. It is suitable for cloud-local active-active, multi-site active-active, and cross-border data sync as well as real-time data warehousing.   

Data migration is a one-time short-term task to migrate the entire database and requires a cutover operation after migration for business connection to the new database. In contrast, data sync is a continuous task. After a task is created, the data will be continuously synced (almost in real time) to keep consistency between the source and target databases. 

DTS supports the sync of self-built, TencentDB, and third-party cloud databases to TencentDB.

- Cloud-local sync: DTS can sync an IDC-based self-built database to a TencentDB instance and vice versa.
- Cross-cloud sync: DTS can sync a third-party cloud database to TencentDB instance.
- Cross-TencentDB instance sync: DTS can sync TencentDB instances in various scenarios, such as multi-site active-active, cross-border, and cross-Tencent Cloud account sync.

## How it works
The following takes MySQL sync as an example to describe the data sync feature, where data is exported from the source instance and imported into the target instance, and key steps include structure initialization, full data initialization, and incremental data processing.

- Structure initialization
  Structure initialization is to create the same table structure information in the target instance as that in the source instance. When configuring a sync task, you can select whether to sync the table structure. If the target database already contains the same structural information, you simply need to sync the data; otherwise, you'll need to sync the information as well.
  
- Full data initialization
  After structure initialization is completed, DTS will initialize the existing data, i.e., exporting all existing data from the source instance and import it into the target instance.
  
- Incremental data processing 
  In incremental data processing, DTS gets the incremental data continuously through the source instance's binlog and persistently stores such data in the intermediate storage after a series filtering and conversion operations. After importing the full data, it continuously replays the changed incremental data stored in the intermediate storage into the target database in order to ensure data consistency between the source and target databases. 

![](https://qcloudimg.tencent-cloud.cn/raw/f516a016acb92a1f466e4bc84e16be0b.png)

## Data conflict resolution

During a DTS sync task, the data in the source and target databases may have conflicts. DTS can check for duplicate table name and primary key conflicts.

**Duplicate table name conflict**

If the source and target databases have tables with the same name, the task can report an error (**Precheck and report error**) or append the data in the source database to the table with the same name in the target database (**Ignore and execute**).

**Primary key conflict**

DTS can check for primary key conflicts and provides the following conflict resolution methods. For specific implementation examples, see [Selecting Data Sync Conflict Resolution Policy](https://intl.cloud.tencent.com/document/product/571/49935).

- Report: During a sync task, if an INSERT statement in the source database has a primary key conflict with the data in the target database, the task will report an error and pause. You need to handle the conflict manually first before proceeding.
- Ignore: During a sync task, if an INSERT statement in the source database has a primary key conflict with the data in the target database, the data inserted into the source database will be ignored, and the data in the target database will prevail.
- Overwrite: During a sync task, if an INSERT or UPDATE statement has a primary key conflict with the data in the target database, the data in the target database will be overwritten by the inserted or updated data in the source database.

## Supported topologies

The basic unit of the sync service is one-way sync. During configuration, you can choose to use data definition language (DDL) or data manipulation language (DML) for sync. By combining one-way sync tasks, you can customize various complex topologies.
In a complex topology, technical measures will be used for DML operations to avoid data loop. However, for DDL, the data sync service will check for loop during configuration to avoid forming DDL loop. 

Below are some common topologies, which you can customize by purchasing multiple sync instances. For detailed directions on how to create a complex topology, see [Creating Two-Way Sync Data Structure](https://intl.cloud.tencent.com/document/product/571/42605), [Creating Many-to-One Sync Data Structure](https://intl.cloud.tencent.com/document/product/571/42604), or [Creating Multi-Site Active-Active IDC Architecture](https://intl.cloud.tencent.com/document/product/571/42603).
- One-to-One one-way sync
<img src="https://qcloudimg.tencent-cloud.cn/raw/3863e49c63a95266e787852733421a9a.png" style="zoom:50%;" />
- Cascaded one-way sync
<img src="https://qcloudimg.tencent-cloud.cn/raw/cf4e594ea2f4152e8140200d1cdb805b.png" style="zoom:55%;" />
- One-to-Many one-way sync
<img src="https://qcloudimg.tencent-cloud.cn/raw/057a8df426d2da9dbdb0ec0c00b9bae4.png" style="zoom:50%;" />
- Many-to-One one-way sync
<img src="https://qcloudimg.tencent-cloud.cn/raw/3edfb237c1519f1f92ec285c9a5db702.png" style="zoom:55%;" />
- Two-Way sync
<img src="https://qcloudimg.tencent-cloud.cn/raw/2fc3834ed3bb8f1e0711b0ae6afba498.png" style="zoom:55%;" />
- Cascaded two-way sync<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/4fc9624a1965feb250e33f31789539ca.png" style="zoom:55%;" />


## Typical use cases
By using DTS, you can sync data between MySQL databases in multiple regions to implement multi-site active-active deployment. Database instances in each region can run in the cloud or your self-built IDC.
<img src="https://qcloudimg.tencent-cloud.cn/raw/f1e3638e92d99b6e51b61e0980e96a83.png" style="zoom:67%;" />

## Restrictions
You can implement two-way sync by combining one-way sync tasks, but the following restrictions exist:
- Your business should cooperate in terms of data consistency and cannot update the data record with the same primary key on two nodes; otherwise, a primary key conflict or mutual overwrite may occur. For example, you can choose to update the data records with primary keys `1`, `3`, and `5` on node A and data records with primary keys `2`, `4`, and `6` on node B.
- If a data sync conflict occurs, DTS will process the data strictly according to the selected conflict resolution policy. You need to confirm whether the corresponding policy meets your business expectation during configuration.
- DML statements support two-way sync, but DDL statements support only one-way sync. To create two-way sync, ensure that DDL sync is disabled in one of the one-way instances.

## Supported database types
For more information on the source and target database types, versions, and sync types supported by data sync, see [Databases Supported by Data Sync](https://intl.cloud.tencent.com/document/product/571/42579).

## Supported advanced features

| **Feature**          | **Description**                        | **Documentation**                           |
| -------------------------- | -------------------------------------- | ----------------------------------------------- |
| Two-way sync, ring sync, and many-to-one sync | Complex sync topologies such as two-way sync, ring sync, and many-to-one sync are supported. | [Databases Supported by Data Sync](https://intl.cloud.tencent.com/document/product/571/42579) |
| Cross-account sync | Data sync between instances under different Tencent Cloud accounts is supported. | [Databases Supported by Data Sync](https://intl.cloud.tencent.com/document/product/571/42579) |
| Cross-version sync of most databases              | The target database version should be equal to or later than the source database version; for example, data on v5.5.x can be synced to v5.5.x, v5.6.x, or later. The last digit in the version number is the minor version number, which is not restricted. | -                                   |
| Table conflict check                   | The duplicate table name check policy is provided.             | -                               |
| Primary key conflict check                   | The following three primary key conflict resolution policies are supported: <br/><li>Report: If a primary key conflict of tables is found during data sync, it will report an error and pause the data sync task. <br> <li>Ignore: If a primary key conflict is found during data sync, it will keep the primary key record in the target database. <br/> <li>Overwrite: If a primary key conflict is found during data sync, it will use the primary key record in the source database to overwrite that in the target database. | [Selecting Data Sync Conflict Resolution Policy](https://intl.cloud.tencent.com/document/product/571/49935) |
| DML and DDL filtering | <li>You can select the data types to be synced, such as `INSERT`, `UPDATE`, and `DELETE` statements.<li>You can select the specific DDL operation, such as `CREATE TABLE`, `CREATE VIEW`, and `DROP INDEX`. | [Setting SQL Filter Policy](https://intl.cloud.tencent.com/document/product/571/47342) |
| WHERE conditional filter | You can customize a filter for a single table. | [Setting SQL Filter Policy](https://intl.cloud.tencent.com/document/product/571/47342) |
| Sync of views and advanced objects | Views, procedures, functions, triggers, and events can be synced. | - |
| Task progress visualization                 | Information such as sync steps and progress can be displayed.            | -                               |
| Metric monitoring and default alarm policy          | <li>Data sync metrics can be monitored. <li>Default configuration is supported for data sync event monitoring to automatically notify you of abnormal events. | [Supported Events and Metrics](https://intl.cloud.tencent.com/document/product/571/42611)                   |
| Instance restart or upgrade          | During incremental data sync, the source and target instances can be restarted or upgraded.           | -               |
| HA switch         | <li>HA switch of the source instance is supported if GTID is enabled. <li>HA switch of the target database is supported.</li> | -           |


