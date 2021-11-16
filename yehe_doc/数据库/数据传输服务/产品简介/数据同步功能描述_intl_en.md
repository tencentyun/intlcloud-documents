## Feature Overview
The data sync feature refers to real-time data sync between two database sources. It is suitable for cloud-local active-active, multi-site active-active, and cross-border data sync as well as real-time data warehousing.   

Unlike data migration which is a one-time short-term task to migrate the entire database, data sync is a continuous task. After a task is created, the data will be continuously synced (almost in real time) to keep consistency between the source and target databases. 

## How to Implement
The following takes MySQL sync as an example to describe the data sync feature, where data is exported from the source database and imported into the target database, and key steps include structure initialization, full data initialization, and incremental data processing.

- Structure initialization
  Structure initialization is to create the same table structure information in the target database as that in the source database. When configuring a sync task, you can select whether to sync the table structure. If the target database already contains the same structural information, you simply need to sync the data; otherwise, you'll need to sync the information as well.
  
- Full data initialization
  After structure initialization is completed, DTS will initialize the existing data, i.e., exporting all existing data from the source database and import it into the target database.
  
- Incremental data processing 
  In incremental data processing, DTS gets the incremental data continuously through the source database's binlog and persistently stores such data in the intermediate storage after a series filtering and conversion operations. After importing the full data, it continuously replays the changed incremental data stored in the intermediate storage into the target database in order to ensure data consistency between the source and target databases. 

![](https://qcloudimg.tencent-cloud.cn/raw/f516a016acb92a1f466e4bc84e16be0b.png)

## Supported Topologies
The basic unit of the sync service is one-way sync. During configuration, you can choose to use data definition language (DDL) or data manipulation language (DML) for sync. By combining one-way sync tasks, you can customize various complex topologies.
In a complex topology, technical measures will be used for DML operations to avoid data loop. However, for DDL, the data sync service will check for loop during configuration to avoid forming DDL loop. 

Below are some common topologies, which you can customize by purchasing multiple sync instances:
- One-to-One one-way sync
<img src="https://qcloudimg.tencent-cloud.cn/raw/3863e49c63a95266e787852733421a9a.png" style="zoom:50%;" />
- Cascaded one-way sync
<img src="https://qcloudimg.tencent-cloud.cn/raw/cf4e594ea2f4152e8140200d1cdb805b.png" style="zoom:55%;" />
- One-to-Many one-way sync
<img src="https://qcloudimg.tencent-cloud.cn/raw/057a8df426d2da9dbdb0ec0c00b9bae4.png" style="zoom:50%;" />
- Many-to-One one-way sync
<img src="https://qcloudimg.tencent-cloud.cn/raw/3edfb237c1519f1f92ec285c9a5db702.png" style="zoom:55%;" />
- Two-Way sync
<img src="https://qcloudimg.tencent-cloud.cn/raw/2fc3834ed3bb8f1e0711b0ae6afba498.png" style="zoom:70%;" />
- Cascaded two-way sync<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/4fc9624a1965feb250e33f31789539ca.png" style="zoom:55%;" />


## Typical Use Cases
By using DTS, you can sync data between MySQL databases in multiple regions to implement multi-site active-active deployment. Database instances in each region can run in the cloud or your self-built IDC.
<img src="https://qcloudimg.tencent-cloud.cn/raw/f1e3638e92d99b6e51b61e0980e96a83.png" style="zoom:67%;" />

## Restrictions
You can implement two-way sync by combining one-way sync tasks, but the following restrictions exist:
- Your business should cooperate in terms of data consistency, i.e., ensuring that data with the same primary key is updated only on the same node.
- If a data sync conflict occurs, DTS will process the data strictly according to the selected conflict processing policy. You need to confirm whether the corresponding policy meets your business expectation during configuration.
- DML statements support two-way sync, but DDL statements support only one-way sync. To create two-way sync, ensure that DDL sync is disabled in one of the one-way instances.

## Supported Database Types
For more information on the source and target database types, versions, and sync types supported for data sync, see [Databases Supported for Data Sync](https://intl.cloud.tencent.com/document/product/571/42579).

## Supported Advanced Features

| **Feature**          | **Description**                        | **Documentation**                           |
| -------------------------- | -------------------------------------- | ----------------------------------------------- |
| Two-Way sync, ring sync, and many-to-one sync | -         | [Databases Supported for Data Sync](https://intl.cloud.tencent.com/document/product/571/42579) |
| Cross-version sync of most databases              | The target database version should be equal to or above the source database version; for example, data on v5.5.x can be synced to v5.5.x, v5.6.x, or above. The last digit in the version number is the minor version number, which is not restricted. | -                                   |
| Table conflict check                   | The duplicate table name check policy is provided.             | -                               |
| Primary key conflict check                   | The following three primary key conflict processing policies are supported: <br/><li>Report: if a primary key conflict of tables is found during data sync, it will report an error and pause the data sync task. <br> <li>Ignore: if a primary key conflict is found during data sync, it will keep the primary key record in the target database. <br/> <li>Overwrite: if a primary key conflict is found during data sync, it will use the primary key record in the source database to overwrite that in the target database. | -                                          |
| DML and DDL filtering | You can select the data types to be synced, such as INSERT, UPDATE, DELETE, and DDL statements. | - |
| Task progress visualization                 | Information such as sync steps and progress can be displayed.            | -                               |
| Metric monitoring and default alarm policy          | <li>Data sync metrics can be monitored. <li>Default configuration is supported for data sync event monitoring to automatically notify you of exceptional events. | [Supported Events and Metrics](https://intl.cloud.tencent.com/document/product/571/42611)                   |
| Database restart or upgrade          | During incremental data sync, the source and target databases can be restarted or upgraded.           | -               |
| HA switch         | <li>HA switch of the source database is supported if GTID is enabled. <li>HA switch of the target database is supported.</li> | -           |


