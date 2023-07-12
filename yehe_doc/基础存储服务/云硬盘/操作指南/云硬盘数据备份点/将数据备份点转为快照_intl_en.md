## Overview
The data backup point of a cloud disk follows the lifecycle of the cloud disk. When the cloud disk expires or is returned, the data backup point reaches the end of its lifecycle. You can convert the data backup point on a specific date into a [snapshot](https://intl.cloud.tencent.com/document/product/362/31638), so that you can make it independent of the cloud disk lifecycle and retain a data backup for a long time.

This document describes how to convert a data backup point into a snapshot in the console.


## Notes
- Snapshots have been [commercialized](https://intl.cloud.tencent.com/document/product/362/32413). If the data backup point is converted into a snapshot, a snapshot will be created and billed. For billing details, see [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413).
- After being converted into a snapshot, the data backup point will be deleted automatically and no longer occupy the quota.


## Directions
1. Log in to the [CBS console](https://console.cloud.tencent.com/cvm/cbs/index) and select the target region at the top of the page.
2. Find the target cloud disk in the list and click **ID/Name** to enter its details page.
3. On the details page, select the **Historical Data Backup Point** tab, find the target data backup point, and select **More** > **Convert Backup Point into Snapshot** on the right.

4. In the **Convert Backup Point into Snapshot** pop-up window, enter the **Snapshot Name**.
5. After confirming that everything is correct, click **OK**.
After the operations, you can view the configuration on the [Snapshot List](https://console.cloud.tencent.com/cvm/snapshot) page. 

