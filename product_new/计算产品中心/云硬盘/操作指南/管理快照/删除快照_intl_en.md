## Operation Scenarios
When there is no need to use the snapshot again, you can delete the snapshot to release virtual resources. 


## Descriptions
- When you delete a snapshot, only the data exclusive to the snapshot will be deleted, and the cloud disk for which the snapshot is created will not be affected.
- You can use a snapshot to recover a cloud disk to the data status when the snapshot is created. Deleting a snapshot created earlier for a cloud disk will not affect the continued use of snapshots created later.
- **When a snapshot is deleted, it will simultaneously delete all data in the snapshot, and the data cannot be retrieved. Deleted snapshots cannot be restored, so please use with caution.**



## Directions
### Deleting a Snapshot in Console
1. Log in to the [Snapshot List](https://console.cloud.tencent.com/cvm/snapshot) page.
2. You can delete snapshots using the following methods:
 a. Single delete: click on **Delete** in the row of the snapshot to be deleted.
 b. Batch delete: select all of the snapshots you want to delete (make sure the snapshots are not involved in any tasks) and click **Delete** at the top of the list.
3. Click **OK**.

### Deleting a Snapshot with API
You can use the DeleteSnapshots API to delete a snapshot. For detailed directions, see [Delete Snapshots](https://cloud.tencent.com/document/product/362/15645).
