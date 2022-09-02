
## Overview
The advanced objects that can be migrated with DTS include functions, triggers, stored procedures, and events. The migration of advanced objects is a one-time operation: only advanced objects already in the source database before the task start can be migrated, while those added to the source database after the task start will not be synced to the target database.

>?Currently, advanced objects can be migrated between MySQL, MariaDB, and Percona.

## Scope of application
Advanced objects can be migrated only with NewDTS.

## Notes
- We recommend you not rename tables when migrating advanced objects; otherwise, the migration may fail.
- As the failure to migrate advanced objects does not affect the entire migration task, the success of the entire migration task does not necessarily mean that the advanced objects are also successfully migrated. Therefore, we recommend you check whether they are migrated on the **Migration Progress** page after the migration is completed.
- When stored procedures and functions are migrated, DTS will check whether `user1` corresponding to `DEFINER` (`[DEFINER = user1]`) in the source database is the same as the migration account `user2`, and if not, DTS will change the `SQL SECURITY` attribute of `user1` in the target database from `DEFINER` to `INVOKER` (`[INVOKER = user1]`) after the migration, and set the `DEFINER` in the target database to the migration account `user2` (`[DEFINER = migration account user2]`).
- Stored procedures and functions will be migrated during **source database export**. If there are no incremental migration tasks, triggers and events will be migrated when the task stops; otherwise, they will be migrated after you click <b>Done</b>, in which case the transition will take a longer time.
- For cross-version migration, if the `sql_mode` set for the advanced objects in the source database is not supported by the target database, `sql_mode` will be changed to `NO_AUTO_VALUE_ON_ZERO` after the advanced objects are migrated.
- When migrating triggers and events, you need to grant the migration account the `TRIGGER` and `EVENT` permissions of the source database.

## Directions
1. On the **Set migration options and select migration objects** page of the [data migration task](https://console.cloud.tencent.com/dts/migration), set the **Advanced Object** feature as needed, which is not enabled by default. 
![](https://qcloudimg.tencent-cloud.cn/raw/6994ede78d4f8e62351918fe477f88b9.png)
3. The advanced object check item will be added to the verification task. For more information, see [Checking Advanced Object](https://intl.cloud.tencent.com/document/product/571/48542).

