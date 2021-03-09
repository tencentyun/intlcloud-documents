## Operation Scenario
With Cloud Block Storage (CBS), you can create snapshots and save cloud disk data at a specific point of time. Tencent Cloud creates snapshots in an incremental manner, which means it only creates data that has changed since the last snapshot. If the size of the changed data is small, snapshot creation is quick. Because snapshots are incrementally created, deleting snapshots does not affect the use of any snapshot data. Therefore, you can restore your cloud disks by using any remaining snapshots.
You can create a snapshot of a cloud disk in any state, but the snapshot will only save the data that is already written to the cloud disk at the current moment. When any app or process is writing data, the data might not yet have been saved to the snapshot that is being created. If this is the case, you can choose to suspend all writes and create the snapshot as soon as possible, or [unmount](https://intl.cloud.tencent.com/document/product/362/32400) the cloud disk and [mount](https://intl.cloud.tencent.com/document/product/362/32401) it later to ensure the integrity of snapshot data.

## Prerequisites
- You have [created a cloud disk](https://intl.cloud.tencent.com/document/product/362/5744).
- The upper limits for the number and total size of snapshots in the current region have not been reached. For more information, see [Snapshot Use Limits](https://intl.cloud.tencent.com/document/product/362/32406#use-limits-on-snapshot).

## Notes
A snapshot only contains data that is already written to the disk (but not data that is in the memory and not yet written to the disk) at the moment the snapshot is created. We strongly recommend that you shut down the instance or ensure that the memory data is already written to the cloud disk and then suspend all writes to the cloud disk before creating the snapshot. For this purpose, you need to do the following.
### Database level
For database services, we recommend that you lock all tables in databases as read-only to avoid a situation where new data is written to the cloud disk and cannot be captured by the snapshot that is being created. By using MySQL as an example, the procedure is as follows:
1. Run the command `FLUSH TABLES WITH READ LOCK` to close all opened tables and use the global read lock to lock all tables in every database, as shown below:
![](https://main.qcloudimg.com/raw/287ad27cec557a52a3386a60b937dc9b.png)
2. Create a snapshot for the cloud disk.
3. Run `UNLOCK TABLES` to unlock the tables, as shown below:
![](https://main.qcloudimg.com/raw/8a5fdcb0df254f0f9afcf3ef86679fc0.png)

### System level
For better system performance, data is stored in the memory buffer before it is written to the cloud disk, when appropriate. Therefore, when you create the snapshot, the data stored in the memory buffer and not already written to the cloud disk will not be written to or recovered from the snapshot. As a result, data inconsistency occurs.
To resolve this issue, run the `sync` command to forcibly write the data in the file system memory buffer immediately to the cloud disk and then prevent new data from being written to the cloud disk. If no error message is returned after the command is executed, the data in the memory buffer has been successfully written to the cloud disk, as shown below:
![](https://main.qcloudimg.com/raw/e1b0ac245e325281a0693f7ae43946ff.png)


e<span id="CreateSnapshot"></span>
## Procedur
### Creating a snapshot in the console
1. Log in to the [CBS console](https://console.cloud.tencent.com/cvm/cbs).
2. Click **Create Snapshot** for the target cloud disk.
3. In the **Create Snapshot** dialog box that appears, enter a snapshot name and click **Submit**.

### Creating a snapshot through the API
You can use the CreateSnapshot API to create a snapshot. For more information, see [CreateSnapshot](https://intl.cloud.tencent.com/document/product/362/15648).
