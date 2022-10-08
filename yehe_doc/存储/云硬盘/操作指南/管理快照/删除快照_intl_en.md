## Overview
When there is no need to use the snapshot again, you can delete the snapshot to release virtual resources.


## Notes
- When you delete a snapshot, only the data exclusive to the snapshot will be deleted, and the cloud disk for which the snapshot is created will not be affected.
- You can use a snapshot to recover a cloud disk to the data status when the snapshot is created. Deleting a snapshot created earlier for a cloud disk will not affect the continued use of snapshots created later.
- If a snapshot has been associated with an image, [delete the image](https://intl.cloud.tencent.com/document/product/213/6036) before deleting the snapshot.
- **Deleting a snapshot will also delete all data in the snapshot, and the data cannot be retrieved. Deleted snapshots cannot be restored, so delete snapshots with caution.**



## Directions

<dx-tabs>
::: Deleting a snapshot in the console
1. Log in to the [Snapshot List](https://console.cloud.tencent.com/cvm/snapshot) page.
2. Delete a snapshot as follows:
 a. **Delete one snapshot**: Click **Delete** on the row of the target snapshot.
 b. **Batch delete snapshots**: Select all of the snapshots you want to delete (make sure the snapshots are not involved in any tasks) and click **Delete** at the top of the list.
3. Click **Confirm**.

:::
::: Deleting a snapshot via API
You can use the `DeleteSnapshots` API to delete a snapshot. For detailed directions, see [DeleteSnapshots](https://intl.cloud.tencent.com/document/product/362/15645).

:::
</dx-tabs>




