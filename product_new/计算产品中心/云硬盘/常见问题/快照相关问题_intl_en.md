
### Is snapshot available in all availability zones ?
Snapshot feature is available in all availability zones.

## How are snapshots billed?
Snapshots were launched for **formal commercialization** on January 22, 2019. After commercialization, all stored snapshots and newly generated snapshots will be billed according to the storage capacity used. For more information, see [Snapshot commercialization announcement].
Before billing for formal commercialization starts, you can choose to delete all snapshots and scheduled snapshot policies to avoid associated costs generated after commercialization.

### Do I need to unmount the disk or interrupt all reads and writes before creating snapshots?
No. You can create real-time snapshots while the disk is connected and in use, without affecting normal business operation. However, snapshots can only capture data that has been written into the cloud disk, not data cached in memory by applications or operating systems. To ensure all application data is captured, we recommend you suspend all disk I/O operations before creating snapshots. For cloud disk that is used as a system disk, we recommend you shut down the CVM first to create a more complete snapshot.

### Does snapshot creation affect disk performance?
Creating a snapshot will occupy a small amount of the disk I/O. We recommend you create snapshots when business is less rigorous.

### What is the time interval between creating a snapshot and when it becomes usable?
Snapshot creation time is influenced by factors such as the number of disk writes, and the underlying read-write operations. It is hard to predict, but creating a snapshot does not affect your normal disk use.

### How do I use snapshot to create the cloud disk?
For more information, see [Creating cloud disks from snapshots](https://intl.cloud.tencent.com/document/product/362/5757).

### How do I roll back snapshots?
For more information, see [Rolling back data from snapshots](https://intl.cloud.tencent.com/document/product/362/5756).

### Do I need to shut down the CVM to roll back snapshots?
- For cloud disks that have been mounted on CVMs, you have to shut down CVMs during rollback.
- For cloud disks that are not yet mounted, you can directly perform rollback operations.

### Can I read a previous snapshot to restore a cloud disk?
Yes. You can use existing snapshots from any point in time to restore data, regardless of the snapshot’s point in time.

### Can you delete the source snapshot during its replication?
No. It can only be deleted after replication is complete.

### Is the new snapshot still associated with the source snapshot’s source disk after replication is complete?
After cross-region replication, the new snapshot and the source disk of the source snapshot are no longer associated. After replication, the rollback feature is unavailable for the new snapshot.

### How do I delete snapshots?
- For cloud disk snapshots, you can delete them directly in the console or through the API. For more information, see [Deleting Snapshots](https://intl.cloud.tencent.com/document/product/362/5758).
- For snapshots associated with custom images, you must first delete custom images, and then [delete snapshots](https://intl.cloud.tencent.com/document/product/362/5758).
