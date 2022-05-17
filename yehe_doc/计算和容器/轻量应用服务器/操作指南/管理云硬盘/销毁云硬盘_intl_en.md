## Overview



When a cloud disk is no longer in use and important data has been backed up, you can release the virtual resources by terminating the cloud disk. You will not be billed for the cloud disk after termination. **When the cloud disk is terminated, all data on the cloud disk will be deleted and cannot be restored. Please note that cloud disks that have been terminated cannot be recovered.** This document describes how to terminate the data disks in the Lighthouse console.

Cloud disks have different life cycles as system disks and data disks. They can be terminated in the following ways:
<dx-tabs>
::: Data disk
The lifecycle of the cloud disk used as a data disk is independent of that of the Lighthouse instance, so the disk can be terminated independently. You can choose to terminate the cloud disk by yourself or enable auto-termination.
- **Manual termination**: The cloud disks can be manually terminated before expiry. After being terminated, the cloud disks will be kept in the recycle bin for seven days, and they can be permanently terminated in the recycle bin.
Each entity can return one cloud disk within five days without reason. Each account can also do returns for 199 cloud disks. For more information on refunds, see [Refund](https://intl.cloud.tencent.com/document/product/1103/41406). When you hit the return limit, you will not be able to manually terminate the cloud disks.
- **Automatic termination** A cloud disk in the recycle bin will be automatically terminated if it is not recovered within 7 days. To continue the use, renew the disk within the specified time. For renewal, see [Renewing a Cloud Disk](https://intl.cloud.tencent.com/document/product/1103/46569).

:::
::: System disk
The lifecycle of a cloud disk used as a system disk is the same as the Lighthouse instance. It can only be terminated when the Lighthouse instance is terminated. For more information, see [Terminating an instance](https://intl.cloud.tencent.com/document/product/1103/41558).
:::
</dx-tabs>

## Prerequisites
- The cloud disks are in **To be attached** status. To terminate the "Attached" cloud disks, you need to detach them first. See [Detaching a Cloud Disk](https://intl.cloud.tencent.com/document/product/1103/46570).
- The important data has been backed up.


## Directions

### Terminate unexpired cloud disks manually
1. Log in to the Lighthouse console and click **[Cloud Disk](https://console.cloud.tencent.com/lighthouse/cbs/index)** on the left sidebar.
2. Select a region at the top of the **Cloud Disk** page, find the target cloud disk, and click **More** > **Terminate/Return**.
![](https://qcloudimg.tencent-cloud.cn/raw/9095cca512d112a40c23aba99649c10d.png)
To terminate multiple cloud disks at the same time, select the target disks and click **Terminate/Return** at the top of the page.
3. In the **Terminate/Return Cloud Disks** pop-up window, check **I have read and agree to Refund Policy**, and click **OK**.
4. On the refund information page, confirm the refund information and click **Confirm Refund**.
<dx-alert infotype="notice" title="">
After termination, the cloud disk is in **Pending released** status and will be kept for seven days. At this time, the cloud disk is no longer available. If you don't need to retain the disk data, you can completely terminate the disk.
</dx-alert>





### Terminate cloud disks completely[](id:completelyDestroyed)
1. On the "Cloud Disk" page, select the cloud disk in "Pending released" status, click **More** > **Terminate/Return** under the operation column.
![](https://qcloudimg.tencent-cloud.cn/raw/90db0b33da6760081393463c2da4bf83.png)
To terminate multiple cloud disks at the same time, select the target disks and click **Terminate/Return** at the top of the page.
2. In the **Terminate/Return Cloud Disks** pop-up window, click **OK** to completely terminate the cloud disk.
<dx-alert infotype="notice" title="">
When a cloud disk is completely terminated, all data on the disk will be deleted and cannot be recovered. Cloud disks that have been terminated cannot be restored.
</dx-alert>

