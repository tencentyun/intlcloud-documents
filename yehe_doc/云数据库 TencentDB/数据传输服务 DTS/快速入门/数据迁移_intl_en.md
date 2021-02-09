DTS can be used to migrate MySQL, Redis, MongoDB, PostgreSQL, MariaDB, and CynosDB databases.

### MySQL data migration
Continuous data replication is available from self-built MySQL databases to TencentDB. You can perform online hot migration of your data in a non-stop manner. MySQL databases with public IP/port, connected to Tencent Cloud via Direct Connect in local IDCs, or created on CVM instances can be migrated.

Currently, DTS does not support migration for TencentDB for MySQL Basic Edition. In addition, TencentDB instances associated with disaster recovery instances do not support DTS for the time being. If you need to migrate them, please [submit a ticket](https://console.cloud.tencent.com/workorder/category). You are recommended to limit the time of incremental migration to no more than 15 days. Meanwhile, be sure to click "Complete Migration" after the primary-secondary synchronization.

For more information, please see [MySQL Data Migration](https://intl.cloud.tencent.com/document/product/571/34103).

### Redis data migration
For more information, please see [Redis Data Migration](https://intl.cloud.tencent.com/document/product/571/33381).

#### Notes on migration
- To ensure migration efficiency, cross-region migration is not supported for self-built instances on CVM.
- To migrate instances over a public network, make sure that the source instance is accessible from the public network.
- Only instances that are running normally can be migrated, while instances with no password initialized or with ongoing tasks cannot be migrated.
- The target instance must be empty with no data. During the migration process, the instance will be locked and writes will not be allowed.
- After the successfully migrated data is verified by your business, the connection to the source instance can be closed and then switched to the target instance.

### PostgreSQL data migration
Continuous data replication is available from self-built PostgreSQL databases to TencentDB. You can perform online hot migration of your data in a non-stop manner. PostgreSQL databases with public IP/port, connected to Tencent Cloud via Direct Connect in local IDCs, or created on CVM instances can be migrated. Currently, data migration is only supported for PostgreSQL databases on version 9.3.x or 9.5.x. Incremental sync is not supported for v9.3.x and can be used in v9.5.x only through an online sync plugin.

For more information, please see [PostgreSQL Data Migration](https://intl.cloud.tencent.com/document/product/571/34105).


### MongoDB data migration
For more information, please see [MongoDB Data Migration](https://intl.cloud.tencent.com/document/product/571/13724).

#### Notes on migration
- To ensure migration efficiency, cross-region migration is not supported for self-built instances on CVM.
- To migrate instances over a public network, make sure that the source instance is accessible from the public network.
- After the successfully migrated data is verified by your business, the connection to the source instance can be closed and then switched to the target instance.
- Online migration is not supported for self-built single-node instances as they have no oplog.

### MariaDB data migration 
For more information, please see [MariaDB Data Migration](https://intl.cloud.tencent.com/document/product/571/19542).

