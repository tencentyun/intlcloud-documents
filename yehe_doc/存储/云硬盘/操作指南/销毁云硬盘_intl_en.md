## Overview
When a cloud disk is no longer in use and **important data has been backed up**, you can release the virtual resources by terminating the cloud disk. You will not be billed for the cloud disk after termination. **When the cloud disk is terminated, all data on the cloud disk will be deleted and cannot be restored. Please note that cloud disks that have been terminated cannot be recovered.**
The lifecycle of a non-elastic cloud disk is the same as the CVM. It can only be terminated when the CVM instance is terminated. For more information, see [Terminate Instances](https://intl.cloud.tencent.com/document/product/213/4930).
The lifecycle of an elastic cloud disk is independent of that of the CVM. Therefore, it can be terminated independently. This document describes how to terminate elastic cloud disks.
Elastic cloud disks can be terminated with the following methods:
- Manual termination
  - Manual termination is supported for pay-as-you-go cloud disks, and takes effect immediately. 
- Automatic termination
  - A pay-as-you-go cloud disk will be automatically terminated if your balance becomes negative for more than 24 hours. You can continue using it if you [top up](https://intl.cloud.tencent.com/document/product/362/36874) your account within the specified time.


## Data Wipe
The data deleted during the termination of the cloud disk is inaccessible to anyone, while data deleted from a CBS cloud disk is completely erased. The following mechanism ensures that all data are wiped.
* Deleting the logical space of a cloud disk will be recorded as metadata. The physical disk space will be cleared, which forcibly deletes all data permanently. All reads to the logical space return `0`.
* The metadata will be immediately destroyed when the cloud disk is released to ensure that the data can no longer be accessed. The physical storage space of the cloud disk will be repossessed and cleared before reassigning.

## Prerequisites
- The cloud disk is in the **To be attached** status. For a cloud disk in use, first [detach](https://intl.cloud.tencent.com/document/product/362/32400) it.
- **All important data are already backed up**.


## Manually Terminating Pay-as-you-go Cloud Disks
1. Log in to the [CBS console](https://console.cloud.tencent.com/cvm/cbs).
2. Terminate cloud disks as instructed below:
    a. Terminate a single cloud disk: locate the target cloud disk that is in the **To be attached** status, and click **More** > **Terminate/Return**.
    b. Terminate cloud disks in batch: select multiple target cloud disks that are in the **To be attached** status and click **Terminate/Return** at the top of the list.
>!When the cloud disk is terminated, all data on the cloud disk will also be deleted, and cannot be restored. Please note that cloud disks that have been terminated cannot be recovered.
>
3. In the **Terminate Cloud Disk** pop-up box, click **Submit** to complete the termination.
 The target cloud disk will no longer be billed. It is **permanently terminated and cannot be recovered**.

 

