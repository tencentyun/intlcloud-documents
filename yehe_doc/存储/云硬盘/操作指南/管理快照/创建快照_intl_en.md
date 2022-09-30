

## Overview
You can create snapshots for a cloud disk to save its data at a specific point of time. The incremental snapshot only records the data change compared to the last snapshot. This process is quick if the data changes a little. Moreover, deleting a snapshot will not affect your use of snapshot data. You can also restore your cloud disks by using any remaining snapshots.
You can create a snapshot for a cloud disk in any state, but the snapshot can only capture the written data rather than data being written by an app or process. Before creating a snapshot, you can choose to suspend all disk I/O operations, or [detach](https://intl.cloud.tencent.com/document/product/362/32400) the cloud disk and [attach](https://intl.cloud.tencent.com/document/product/362/32401) it later to create a complete snapshot.

## Prerequisite
- You have [created a cloud disk](https://intl.cloud.tencent.com/document/product/362/5744).
- You've not reached the upper limits for the number and total size of snapshots in the current region. See [Snapshot Use Limits](https://intl.cloud.tencent.com/document/product/362/32406).

## Notes
A snapshot can only capture the written data but not cached data in the memory (such as files in the `/run` directory on a Linux CVM) of the cloud disk. We recommend that you shut down the instance, or write all memory data to disk and suspend disk I/O operations before creating a snapshot. This can be done at the following two levels.
### Database level
For database services, we recommend locking all tables in databases as read-only to ensure that the snapshot captures all data. Taking MySQL as an example, the procedure is as follows:
1. Run the command `FLUSH TABLES WITH READ LOCK` to close all tables and use the global read lock to lock all tables in every database, as shown below:
![](https://main.qcloudimg.com/raw/287ad27cec557a52a3386a60b937dc9b.png)
2. Create a snapshot for the cloud disk.
3. Run the command `UNLOCK TABLES` to unlock the tables, as shown below:
![](https://main.qcloudimg.com/raw/8a5fdcb0df254f0f9afcf3ef86679fc0.png)

### System level
For better system performance, data is stored in the memory buffer before it is written to the cloud disk at the proper moment. Therefore, the snapshot created for the cloud disk does not contain data stored in the memory buffer and not already written to the cloud disk. As a result, data inconsistency occurs.
To resolve this issue, run the `sync` command to forcibly write the data in the file system memory buffer immediately to the cloud disk, and then prevent new data from being written to the cloud disk. If no error message is returned after the command is executed, the data in the memory buffer has been successfully written to the cloud disk, as shown below:
![](https://main.qcloudimg.com/raw/e1b0ac245e325281a0693f7ae43946ff.png)



## Directions[](id:CreateSnapshot)
### Creating a snapshot via the console
1. Log in to the [CBS console](https://console.cloud.tencent.com/cvm/cbs).
2. Click **Create a snapshot** on the right of the target cloud disk.

3. In the **Create a snapshot** pop-up window, enter the snapshot name and click **OK**.

### Creating a snapshot via an API
You can use the `CreateSnapshot` API to create a snapshot. For more information, see [CreateSnapshot](https://intl.cloud.tencent.com/document/product/362/15648).



