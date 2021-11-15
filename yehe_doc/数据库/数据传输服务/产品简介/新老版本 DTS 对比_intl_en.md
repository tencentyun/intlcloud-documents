## Overview
The legacy version of DTS implements incremental data sync through cloud native replication, which has a strong dependency on the kernel form of the source database and has many restrictions on the features; for example, it does not support advanced features such as table name mapping and many-to-one database sync.

The new version of DTS uses a new proprietary kernel and comprehensively improves the product features to provide more stable, available, flexible, and secure data transfer capabilities for better ease of use. Its capabilities are polished for data transfer, with advanced feature such as heterogeneous database migration and cross-account data migration. 

The new version of DTS will gradually replace the legacy version, which will be disused at the end of 2021. You need to upgrade to the new version as soon as possible if If you are using the legacy version. 

## Feature Comparison
### Data migration
The key features of the new and legacy versions of DTS are compared as follows:

| **Item**     | **Legacy Version**                       | **New Version**                     |
| -------------- | --------------------------------- | --------------------------------- |
| Database type     | <li>Heterogeneous databases cannot be migrated. <br><li>Alibaba Cloud source databases can be migrated. | <li>Heterogeneous databases can be migrated. <br><li>Alibaba Cloud and AWS source databases can be migrated. |
| Cross-account migration     | Not supported.          | Supported.                                             |
| Supported versions     | It does not support cross-version migration.         | It supports cross-version migration for most databases. For more information on the supported versions, see [Databases Supported for Data Migration](https://intl.cloud.tencent.com/document/product/571/42580). |
| Migration object       | It has more generic migration dimensions, supports migrating basic tables and views, and supports user information sync for certain database versions. | It focuses more on the data content itself during migration. It migrates basic tables and views but not user information and database parameters. In the future, it will support migrating other database objects such as triggers and functions. |
| Task progress visualization     | Not supported.      | Supported.                   |
| Monitoring and alarming       | <li>It does not support metric monitoring. <li>It does not support default alarm policy. | <li>It supports metric monitoring. <li>It supports default alarm policy, so that alarms will be automatically triggered for exceptions during migration. |
| Enhanced operation experience   | -                                     | <li>For tables with a primary key or non-null unique key, it supports migration without locks. <br><li>It supports table mapping. <br><li>It supports instance restart or upgrade during incremental migration. <br><li>It decouples the migration task from databases and releases locks during incremental migration. |
| High availability (HA) | It has strict restrictions for HA switch.  | <li>It supports HA switch of the source database if GTID is enabled. <li>It supports HA switch of the target database. </li> |
| Data verification       | The operator must have the super privileges of the source database account.  | The operator does not need to have the super privileges of the source database account (only for certain databases currently). |

### Data sync
The key features of the new and legacy versions of DTS are compared as follows:

| **Item**     | **Legacy Version**                       | **New Version**                     |
| -------------- | ---------------------------- | ------------------------------------- |
| Sync type       | It supports one-way and one-to-one sync modes.     | It supports two-way, ring, and many-to-one sync modes.                         |
| Supported versions     | It does not support cross-version sync.         | It supports cross-version sync. For more information on the supported versions, see [Databases Supported for Data Sync](https://intl.cloud.tencent.com/document/product/571/42579). |
| Sync object       | It has more generic sync dimensions, supports syncing basic tables and views, and supports user information sync for certain database versions. | It focuses more on the data content itself during sync. It syncs basic tables and views but not user information and database parameters. In the future, it will support syncing other database objects such as triggers and functions. |
| Content conflict       | It does not support content conflict check.                         | It provides table conflict check policies and supports renaming tables.                     |
| Primary key conflict       | It does not support primary key conflict policies.                          | It provides primary key conflict processing policies: <br><li>Report: if a primary key conflict of tables is found during data sync, it will report an error and pause the data sync task. <br/> <li>Ignore: if a primary key conflict is found during data sync, it will keep the primary key record in the target database. <br/> <li>Overwrite: if a primary key conflict is found during data sync, it will use the primary key record in the source database to overwrite that in the target database. |
| Task progress visualization     | Not supported.      | Supported.                   |
| Monitoring and alarming       | <li>It does not support metric monitoring. <li>It does not support default alarm policy. | <li>It supports metric monitoring. <li>It supports default alarm policy, so that alarms will be automatically triggered for exceptions during sync. |
| Enhanced operation experience   | -                                     | <li>It supports table mapping. <br> <li>It supports instance restart or upgrade during incremental sync. |
| High availability (HA) | It has strict restrictions for HA switch.  | <li>It supports HA switch of the source database if GTID is enabled. <br><li>It supports HA switch of the target database. </li> |

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

