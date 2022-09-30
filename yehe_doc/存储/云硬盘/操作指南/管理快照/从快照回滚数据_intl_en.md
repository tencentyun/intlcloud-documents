## Overview
When a data error occurs or data is lost due to a change, you can roll back the snapshot data to the corresponding cloud disk, so that data in the cloud disk can be restored to the status when the snapshot is created.
- The snapshot data can be rolled back only to the source cloud disk but not other cloud disks.
- You can roll back the data in the following scenarios:
  - If the source cloud disk is in **To be attached** status (that is, it has not been attached to a CVM instance), you can directly perform the rollback.
  - If the source cloud disk has been attached to a CVM instance, you can perform the rollback when the CVM instance is shut down.

## Directions
### Rolling back the data in the console
1. Log in to the [Snapshot List](https://console.cloud.tencent.com/cvm/snapshot) page.
2. Click **Rollback** in the row of the target snapshot.
<dx-alert infotype="notice" title="">
The data of the source cloud disk will be rolled back to the status when the snapshot is created, and all the data after this time will be cleared.
</dx-alert>
3. On the **Roll-back Data** page, confirm the rollback information and click **OK**.

### Rolling back the data via an API
You can use the `ApplySnapshot` API to roll back the data. For detailed directions, see [ApplySnapshot](https://intl.cloud.tencent.com/document/product/362/15643).

