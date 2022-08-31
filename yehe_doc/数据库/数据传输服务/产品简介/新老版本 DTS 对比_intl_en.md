## Overview
The legacy version of DTS implements incremental data sync through cloud native replication, which has a strong dependency on the kernel form of the source database and has many restrictions on the features; for example, it does not support advanced features such as table name mapping and many-to-one database sync.

The new version of DTS uses a new proprietary kernel and comprehensively improves the product features to provide more stable, available, flexible, and secure data transfer capabilities for better ease of use. Its capabilities are polished for data transfer, with advanced feature such as heterogeneous database migration and cross-account data migration. 


## Feature Comparison
### Data migration
The key features of the new and legacy versions of DTS are compared as follows:

| **Item**     | **Legacy Version**                       | **New Version**                     |
| -------------- | --------------------------------- | --------------------------------- |
| Database type     | <li>Heterogeneous databases cannot be migrated. <br><li>Alibaba Cloud source databases can be migrated. | <li>Heterogeneous databases can be migrated. <br><li>Alibaba Cloud and AWS source databases can be migrated. |
| Cross-account migration     | Not supported.          | Supported.                                             |
| Supported data types | <li>It supports the migration of basic tables, views, functions, triggers, and stored procedures.<li>It supports the migration of user account information. | <li>It only supports the migration of basic tables and views, while the feature of migrating functions, triggers, and stored procedures is under development.<li>It supports the migration of user account information. |
| Supported versions     | It does not support cross-version migration.         | It supports cross-version migration for most databases. For more information on the supported versions, see [Databases Supported by Data Migration](https://intl.cloud.tencent.com/document/product/571/42647). |
| Task progress visualization     | Not supported.      | Supported.                   |
| Monitoring and alarming       | <li>It does not support metric monitoring. <li>It does not support default alarm policy. | <li>It supports metric monitoring. <li>It supports default alarm policy, so that alarms will be automatically triggered for exceptions during migration. |
| Enhanced operation experience   | -                                     | <li>It supports migration without lock to add locks only to tables without primary keys. <br><li>It supports table mapping. <br><li>It supports instance restart or upgrade during incremental migration. <br><li>It decouples the migration task from databases and releases locks during incremental migration. |
| High availability (HA) | It has strict restrictions for HA switch.  | <li>It supports HA switch of the source instance if GTID is enabled. <li>It supports HA switch of the target instance. </li> |
| Data verification       | The operator must have the super privileges of the source instance account.  | The operator does not need to have the super privileges of the source instance account (only for certain databases currently). |

### Data sync
The key features of the new and legacy versions of DTS are compared as follows:

| **Item**     | **Legacy Version**                       | **New Version**                     |
| -------------- | ---------------------------- | ------------------------------------- |
| Sync type       | It supports one-way and one-to-one sync modes.     | It supports two-way, ring, and many-to-one sync modes.                         |
| Cross-account sync | It does not support cross-account sync. | It supports cross-account sync. |
| Supported versions     | It does not support cross-version sync.         | It supports cross-version sync. For more information on the supported versions, see [Databases Supported for Data Sync](https://intl.cloud.tencent.com/document/product/571/42579). |
| Content conflict       | It does not support content conflict check.                         | It provides table conflict check policies and supports renaming tables.                     |
| Primary key conflict       | It does not support primary key conflict policies.                          | It provides primary key conflict processing policies: <br><li>Report: If a primary key conflict of tables is found during data sync, it will report an error and pause the data sync task. <br/> <li>Ignore: If a primary key conflict is found during data sync, it will keep the primary key record in the target database. <br/> <li>Overwrite: If a primary key conflict is found during data sync, it will use the primary key record in the source database to overwrite that in the target database. |
| Task progress visualization     | Not supported.      | Supported.                   |
| Monitoring and alarming       | <li>It does not support metric monitoring. <li>It does not support default alarm policy. | <li>It supports metric monitoring. <li>It supports default alarm policy, so that alarms will be automatically triggered for exceptions during sync. |
| Enhanced operation experience   | -                                     | <li>It supports table mapping. <br> <li>It supports instance restart or upgrade during incremental sync. |
| High availability (HA) | It has strict restrictions for HA switch.  | <li>It supports HA switch of the source instance if GTID is enabled. <br><li>It supports HA switch of the target instance. </li> |

### Data subscription
The key features of the new and legacy versions of DTS are compared as follows:

| **Item**     | **Legacy Version**                       | **New Version**                     |
| ---------------- | --------------------------------- | -------------------------------------------------- |
| Database type       | TencentDB for MySQL only. | TencentDB for MySQL, TencentDB for MariaDB, and TDSQL for MySQL. |
| Subscribed data storage method | The data is stored on physical machines in master/slave mode.    |  The data is stored in the Kafka middleware, and partitioned storage of data in a single topic is supported (with partitioning strategy available), improving the consumption efficiency. |
| Supported protocol       | Proprietary protocol with SDK for Java only.       | Kafka protocol with Kafka client SDKs for multiple programming languages.           |
| Monitoring and alarming       | <li>It supports metric monitoring. <li>It does not support default alarm policy. | <li>It supports more metric monitoring. <li>It supports default alarm policy, so that alarms will be automatically triggered for exceptions during subscription. |
| Data channel         | It allows creating only one data channel for a single instance.  | It allows creating multiple data channels for a single instance, which can be consumed concurrently through a consumer group.   |
| Consumption method         | It supports only serial processing.                  | It supports partitioned storage of data in a single topic for concurrent consumption of data in multiple partitions, improving the consumption efficiency. |

