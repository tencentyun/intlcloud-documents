## Overview

When there is no need to use the snapshot again, you can delete the snapshot to release virtual resources. 


## Notes

- When you delete a snapshot, only the data exclusive to the snapshot will be deleted, and the file system for which the snapshot is created will not be affected.
- You can use a snapshot to restore a file system to the data status when the snapshot is created. Deleting a snapshot created earlier for a file system will not affect the continued use of snapshots created later.
- **Deleting a snapshot will also delete all data in the snapshot, and the data cannot be retrieved. Deleted snapshots cannot be restored, so please delete snapshots with caution.**



## Directions

1. Log in to the CFS console and go to the [Snapshot List](https://console.intl.cloud.tencent.com/cfs/snapshot/list?rid=1) page.
2. Delete a snapshot as follows:
 Click **Delete** in the row of the snapshot to be deleted.
3. Click **Confirm**.



