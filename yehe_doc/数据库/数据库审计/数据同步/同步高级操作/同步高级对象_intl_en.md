
## Overview
The advanced objects that can be synced with DTS include functions and stored procedures. The sync of advanced objects is a one-time operation: only advanced objects already in the source database before the task start can be synced, while those added to the source database after the task start will not be synced to the target database.

>?Currently, advanced objects can be synced between MySQL, MariaDB, and Percona.

## Notes
- We recommend you not rename tables when syncing advanced objects; otherwise, the sync may fail.
- As the failure to sync advanced objects does not affect the entire sync task, the success of the entire sync task does not necessarily mean that the advanced objects are also successfully synced. Therefore, we recommend you check whether they are synced on the **Sync Progress** page after the sync is completed.
- When stored procedures and functions are synced, DTS will check whether `user1` corresponding to `DEFINER` (`[DEFINER = user1]`) in the source database is the same as the sync account `user2`, and if not, DTS will change the `SQL SECURITY` attribute of `user1` in the target database from `DEFINER` to `INVOKER` (`[INVOKER = user1]`) after the sync, and set the `DEFINER` in the target database to the sync account `user2` (`[DEFINER = sync account user2]`).
- For cross-version sync, if the `sql_mode` set for the advanced objects in the source database is not supported by the target database, `sql_mode` will be changed to `NO_AUTO_VALUE_ON_ZERO` after the advanced objects are synced.

## Directions
1. On the **Set sync options and objects** page in the [data sync task](https://console.cloud.tencent.com/dts/replication), set the **Advanced Migration Object** feature. Advanced objects are selected by default. You can deselect unwanted advanced object options.
![](https://qcloudimg.tencent-cloud.cn/raw/1cc56ba9f83332bf6fc92ed8321872f6.png)
2. The advanced object check item will be added to the verification task. For more information, see [Advanced Object Check](https://intl.cloud.tencent.com/document/product/571/48542).

