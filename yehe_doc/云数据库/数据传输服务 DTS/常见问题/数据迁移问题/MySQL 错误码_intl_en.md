
| Error Code | Description | Solution |
|---------|--------|----------|
|-254 | Failed to query the target instance information | Please make sure that the target instance is normal and is not performing any other tasks during migration. |
|-419 | The target instance version is non-compliant for migration from Alibaba Cloud | For data migration from Alibaba Cloud, only TencentDB 5.6 target instances are supported, and their synchronization status must be **async**. Migration to target instances in semi-sync or strong sync status is not supported currently. |
|-256 | Failed to connect to the source instance | Please check the connection permission of the source instance account, make sure that a connection to the source instance can be established by entering account and password, and check the connectivity of the source instance. |
|-255 | Failed to query the source instance information | Please make sure that the source instance can be connected normally during migration, and do not modify the corresponding account permission. `errormsg` contains the native MySQL error message. |
|-260 | The GTID configurations of the source and target instances are non-compliant |<li>For MySQL 5.7 target instances, GTID should be enabled or disabled for both the source and target instances at the same time. <li>For other versions of MySQL instances, migration from a GTID-enabled source instance to a GTID-disabled target instance is not supported. |
|-261 | For online migration, binlog needs to be enabled for the source instance | For online migration, if `log_bin` is not set to 1 and binlog is not enabled for the source instance, incremental data cannot be synced. |
|-262 | For online migration, binlog cannot be in `statement` format for the source instance | For online migration, binlog of the source instance should be in `row` or `mixed` format. |
|-267 | `innodb_stats_on_metadata` should be set to off for the source instance | `innodb_stats_on_metadata` should be set to off during migration. |
|-264 | For online migration, the source instance's `server_id` should be a positive integer other than 1 and different from that of the target instance | For online migration, `server_id` should be properly configured for the source instance and be different from that of the target instance. |
|-418 | For migration of specified tables (not schema), `events` should be disabled for the source instance | For migration of specified tables in online and backup modes, `events` should be disabled for the source instance (set global event_scheduler=OFF). |
|2001041 | The source instance is a syncing slave, but `log_slave_update` is not enabled | If the source instance is a slave being synced, `log_slave_updates` should be set to on. |
|2001040 | The source instance is on version 5.7, which contains unsupported column types | For v5.7 source instances, columns in JSON format and virtual columns are not supported. |
|-257 | The source instance and target instance are not compatible | Compatibility requirements: <br>Migration between instances on the same major MySQL version is supported. <br>For different major versions, only migration from v5.1 to v5.5 and from v5.5 to v5.6 is supported. <br>The source instance and target instance should have the same `character_set_server` and `lower_case_table_names` global configurations. |
|-258 | The target instance capacity is insufficient in online or backup mode | The target instance capacity needs to be at least 1.3 times that of the source instance. |
|-259 | The target instance is not empty for instance-level migration | For instance-level migration, please make sure that there are no user-created databases in the target instance so as to prevent overwrites. |
|2001037 | For table migration, the entered table is not found in the source instance | To migrate tables, please make sure that they can be found in the source instance. |
|-268 | The database name already exists | For database-level table migration, please make sure that neither identical databases nor identical tables exist in both the source instance and target instance. |
|-269 | The table name already exists. | For table migration, please make sure that no identical table names exist in both the source instance and target instance. |
|-265 | For table migration, the table that foreign keys rely on is not in the target table | - |
|-266 | The target table has an unsupported storage engine | For the source table, storage engine support is as follows: <li> V5.6 does not support 'MEMORY', 'BLACKHOLE', 'CSV', and 'ARCHIVE' engines. <li>V5.7 does not support 'MRG_MYISAM', 'MEMORY', 'BLACKHOLE', 'CSV', and 'ARCHIVE' engines. <li>The TokuDB engine is supported. |
|-420 | The source TokuDB is compressed | `row_format` of quicklz/lzma/snappy/uncompressed is not supported for Toku. |
|-421 | The source TokuDB has a cluster index | There is a table whose `column_key` is 'CLU'. |
|-292 | The RO status of the target instance is exceptional | To initiate a migration task, the target instance's RW and RO status must be normal. |
|-405 | There is a table whose `row_format` is fixed in the source instance | It is recommended to change the source instance tables to InnoDB tables (not in row_format). After the change of the format, the database table will be rebuilt. |
|-417 | The primary-secondary relationship between the source instance and target instance is exceptional. | Please check whether the network connection to the source instance is normal and whether doublewrite is caused by user writes to the target instance during migration. |
|-253 | A user request for canceling the task is received | After a user request for canceling the migration task is received, the task will be canceled and then rolled back. |
|-407 | Incorrect input parameters | The input parameters are incorrect. Please check whether the parameters are in valid format, such as table name. |
|-411 | Failed to check the account permission in the source instance | Please provide details on the eligible source instance account permission and make sure that the user account has the required permission based on the task configuration. <br>For example, session needs to be in binlog format for full detection, which requires the super permission. Solution: 1. The super permission is not required for sampling detection; 2. Grant the super permission to the account. |
|6001000 | The backup system is exceptional | Please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us. |
|-41 | Data sync failed due to a primary-secondary exception | Please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us. |
|996 | Internal error. The migration mode and comparison mode have different configurations on the backend. An error will occur if the configuration file cannot be found | Please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us. |

