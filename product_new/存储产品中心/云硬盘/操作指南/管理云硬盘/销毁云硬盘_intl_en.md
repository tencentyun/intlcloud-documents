## Scenario
When the cloud disk is no longer in use and **important data has been backed up**, you can release the virtual resources by terminating the cloud disk. After terminating the cloud disk, you will not be billed for the cloud disk. **When the cloud disk is terminated, all data on the cloud disk will be deleted at the same time, and cannot be retrieved. Cloud disks that have been terminated cannot be recovered. Please proceed with caution.**
The lifecycle of a non-elastic cloud disk follows that of the CVM, and it can only be terminated when the CVM is terminated. For more information, see [Terminate Instances](https://intl.cloud.tencent.com/document/product/213/4930).
The lifecycle of an elastic cloud disk is independent of that of the CVM. Therefore, it can be terminated independently of the CVM. This article describes operations for terminating elastic cloud disks.
Elastic cloud disks can be terminated by the following methods:

- Manual termination
  - Manual termination is supported for pay-as-you-go cloud disks, and takes effect immediately. 
- Automatic termination
 - Pay-as-you-go cloud disk with a balance of less than 0 for more than 24 hours will be terminated. If the renewal fee is paid within the specified time, the disk can continue to be used.

## Prerequisites
- The cloud disk is in the **To Be Mounted** status. For cloud disks that are mounted, first perform [unmounting](https://intl.cloud.tencent.com/document/product/362/6740).
- You have already **backed up important data** according to business requirements**.

## Manually terminating pay-as-you-go cloud disks
1. Log in to the [CBS Console](https://console.cloud.tencent.com/cvm/cbs).
2. You can use the following methods to terminate a cloud disk:
    a. Single termination: Select **More**>**Terminate/Return** in the row of the target cloud disk with the **To Be Mounted** status.
    b. Batch termination: Select multiple target cloud disks with the status **To Be Mounted** and click **Terminate/Return** at the top of the list.

>When the cloud disk is terminated, all data on the cloud disk will be deleted at the same time, and cannot be retrieved. Cloud disks that have been terminated cannot be recovered. Please proceed with caution.
>
3. In the **Terminate Cloud Disk** pop-up box, click **Confirm** to complete the termination.
 The target cloud disk will no longer be billed, and **is completely terminated and cannot be retrieved**.

