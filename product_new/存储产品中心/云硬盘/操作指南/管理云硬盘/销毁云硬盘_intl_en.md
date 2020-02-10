## Introduction
When a cloud disk is no longer in use and **important data has been backed up**, you can release the virtual resources by terminating the cloud disk. You will not be billed for the cloud disk after termination. **When the cloud disk is terminated, all data on the cloud disk will be deleted and cannot be restored. Please note that cloud disks that have been terminated cannot be recovered.**
The lifecycle of a non-elastic cloud disk follows that of the CVM, and it can only be terminated when the CVM is terminated. For more information, see [Terminate Instances](https://intl.cloud.tencent.com/document/product/213/4930).
The lifecycle of an elastic cloud disk is independent of that of the CVM. Therefore, it can be terminated independently of the CVM. This document describes how to terminate elastic cloud disks.
Elastic cloud disks can be terminated with the following methods:

- Manual termination
  - Manual termination is supported for pay-as-you-go cloud disks, and takes effect immediately. 
- Automatic termination

  - A pay-as-you-go cloud disk will be automatically terminated if your balance becomes negative for more than 24 hours. You can continue using it if you [top up](https://intl.cloud.tencent.com/document/product/362/3064) your account within the specified time.

##  Prerequisites
- The cloud disk is in the **To Be Mounted** status. [Unmount](https://intl.cloud.tencent.com/zh/document/product/362/32400) cloud disks that are mounted.
- **All important data are already backed up**.

## Manually terminating pay-as-you-go cloud disks
1. Log in to the [CBS Console](https://console.cloud.tencent.com/cvm/cbs).
2. You can use the following methods to terminate a cloud disk:
    a. Single termination: locate the target cloud disk that is in a **To Be Mounted** status, click **More** -> **Terminate/Return**.
    b. Batch termination: select multiple target cloud disks that are in a **To Be Mounted** status and click **Terminate/Return** at the top of the list.

>When the cloud disk is terminated, all data on the cloud disk will also be deleted, and cannot be restored. Please note that cloud disks that have been terminated cannot be recovered. 
>
3. In the **Terminate Cloud Disk** pop-up box, click **Confirm** to complete the termination.
 The target cloud disk will no longer be billed. It is **permanently terminated and cannot be recovered**.

