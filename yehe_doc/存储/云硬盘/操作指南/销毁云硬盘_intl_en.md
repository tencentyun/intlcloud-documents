## Overview
When a cloud disk is no longer in use and **important data has been backed up**, you can release the virtual resources by terminating the cloud disk. You will not be billed for the cloud disk after termination. **When the cloud disk is terminated, all data on the cloud disk will be deleted and cannot be restored. Note that cloud disks that have been terminated cannot be recovered.**
The lifecycle of a non-elastic cloud disk is the same as the CVM instance. It can only be terminated when the CVM instance is terminated. For more information, see [Terminate Instances](https://intl.cloud.tencent.com/document/product/213/4930).
The lifecycle of an elastic cloud disk is independent of that of the CVM. Therefore, it can be terminated independently. This document describes how to terminate elastic cloud disks.
Elastic cloud disks can be terminated with the following methods:
<dx-tabs>
::: Manual termination
  - Monthly subscription cloud disks can be manually terminated before expiry. After being terminated, the cloud disks will be kept in the recycle bin for 7 days, and they can be permanently terminated in the recycle bin.
    Each entity can return one monthly subscribed cloud disk within five days unconditionally. Each account can return 199 monthly subscribed cloud disks every year. For more information, see Refund. When you hit the return limit, you will not be able to manually terminate monthly subscribed cloud disks.
  - Manual termination is supported for pay-as-you-go cloud disks, and takes effect immediately. 
:::
::: Automatic termination
 - A monthly subscription cloud disk in the recycle bin will be automatically terminated if it is not recovered within 7 days. It can be continuously used if you [renew](https://intl.cloud.tencent.com/document/product/362/36874) it within the specified time.
 - A pay-as-you-go cloud disk will be automatically terminated if your balance becomes negative for more than 24 hours. You can continue using it if you [top up](https://intl.cloud.tencent.com/document/product/362/36874) your account within the specified time.

:::
</dx-tabs>



## Data Wipe
The data deleted during the termination of the cloud disk is inaccessible to anyone, while data deleted from a CBS cloud disk is completely erased. The following mechanism ensures that all data are wiped.
* Deleting the logical space of a cloud disk will be recorded as metadata. The physical disk space will be cleared, which forcibly deletes all data permanently. All reads to the logical space return `0`.
* The metadata will be immediately destroyed when the cloud disk is released to ensure that the data can no longer be accessed. The physical storage space of the cloud disk will be repossessed and cleared before reassigning.

## Prerequisite
- The cloud disk is in **To be attached** status. For a cloud disk in use, first [detach](https://intl.cloud.tencent.com/document/product/362/32400) it.
- **All important data are already backed up**.

## Directions

<dx-tabs>
::: Manually terminating monthly subscribed cloud disks


### Manually terminating unexpired cloud disks in the console
If you no longer need a monthly subscribed cloud disk, you can terminate it manually. Once the status of the cloud disk becomes **To be repossessed**, no fees will be incurred. **The cloud disk is disabled (the cloud disk becomes unavailable, but data is retained) and kept in the recycle bin for seven days. You can recover the cloud disk and continue to use it after you [renew](https://intl.cloud.tencent.com/document/product/362/36874) it. The cloud disk will be automatically terminated if you don't renew it within seven days. You can also permanently terminate the cloud disk in the recycle bin.**
Each entity can return one monthly subscribed cloud disk within five days unconditionally. Each account can return 199 monthly subscribed cloud disks every year. For more information, see Refund. When you hit the return limit, you will not be able to manually terminate monthly subscribed cloud disks.

1. Log in to the [CBS console](https://console.cloud.tencent.com/cvm/cbs).
2. Terminate cloud disks as instructed below:
    a. **Terminate one cloud disk**: Select **More** > **Terminate/Return** on the row of the target cloud disk in **To be attached** status.
    b. **Batch terminate cloud disks**: Select multiple target cloud disks in **To be attached** status and click **Terminate/Return** above the list.
<dx-alert infotype="notice" title="">
When the cloud disk is terminated, all its data will be deleted and cannot be restored. Terminated cloud disks cannot be recovered. Proceed with caution.
</dx-alert>
3. In the **Terminate Cloud Disk** pop-up window, select **I have read and agree to Refund Policy** and click **OK**.
 The system will stop billing, disable the target cloud disk (the cloud disk will be unavailable, but data is retained), and move it to the recycle bin.





### Permanently terminate the monthly subscription cloud disk in the recycle bin
You can permanently terminate the monthly subscription cloud disk in the [Recycle Bin](https://console.cloud.tencent.com/cvm/recycle/cbs).

1. Log in to the [CBS Recycle Bin](https://console.cloud.tencent.com/cvm/recycle/cbs).
2. You can use the following methods to permanently terminate a cloud disk:
   a. **Terminate one cloud disk**: Select **Release** on the row of the target cloud disk in **To be repossessed** status.
   b. **Batch terminate cloud disks**: Select multiple target cloud disks in **To be repossessed** status and click **Batch Release** above the list.
<dx-alert infotype="notice" title="">
When the cloud disk is terminated, all its data will be deleted and cannot be restored. Terminated cloud disks cannot be recovered. Proceed with caution.
</dx-alert>
3. Enter the verification code in the pop-up window and click **OK**.
    The target cloud disk is **permanently terminated and cannot be recovered**.


:::
::: Manually terminating pay-as-you-go cloud disks
1. Log in to the [CBS console](https://console.cloud.tencent.com/cvm/cbs).
2. Terminate cloud disks as instructed below:
    a. **Terminate one cloud disk**: Select **More** > **Terminate/Return** on the row of the target cloud disk in **To be attached** status.
    b. **Batch terminate cloud disks**: Select multiple target cloud disks in **To be attached** status and click **Terminate/Return** above the list.
<dx-alert infotype="notice" title="">
When the cloud disk is terminated, all its data will be deleted and cannot be restored. Terminated cloud disks cannot be recovered. Proceed with caution.
</dx-alert>
3. In the **Terminate Cloud Disk** pop-up window, click **Submit**.
 The target cloud disk will no longer be billed. It is **permanently terminated and cannot be recovered**.
:::
</dx-tabs>



 

