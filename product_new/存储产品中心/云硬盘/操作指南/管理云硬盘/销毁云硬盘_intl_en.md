## Introduction
When a cloud disk is no longer in use and **important data has been backed up**, you can release the virtual resources by terminating the cloud disk. You will not be billed for the cloud disk after termination. **When the cloud disk is terminated, all data on the cloud disk will be deleted and cannot be restored. Please note that cloud disks that have been terminated cannot be recovered.**
The lifecycle of a non-elastic cloud disk follows that of the CVM, and it can only be terminated when the CVM is terminated. For more information, see [Terminate Instances](https://intl.cloud.tencent.com/document/product/213/4930).
The lifecycle of an elastic cloud disk is independent of that of the CVM. Therefore, it can be terminated independently of the CVM. This document describes how to terminate elastic cloud disks.
Elastic cloud disks can be terminated with the following methods:
- Manual termination
  - Monthly subscription cloud disks can be manually terminated before expiry. After being terminated, the cloud disks will be kept in the recycle bin for 7 days, and they can be permanently terminated in the recycle bin.
  Each Tencent Cloud account can return one monthly subscription cloud disk within five days without reason. Each account can also do self-service returns for three monthly subscription cloud disks. For more information on refunds, see [Refunds] (https://cloud.tencent.com/document/product/362/18072). When you hit the return limit, you will not be able to manually terminate the monthly subscription cloud disks.
  - Manual termination is supported for pay-as-you-go cloud disks, and takes effect immediately. 
- Automatic termination
 - A monthly subscription cloud disk in the recycle bin will be automatically terminated if it is not recovered within 7 days. It can be continuously used if you [renew](https://cloud.tencent.com/document/product/362/6739) it within the specified time.
 - A pay-as-you-go cloud disk will be automatically terminated if your balance becomes negative for more than 24 hours. You can continue using it if you [top up](https://intl.cloud.tencent.com/document/product/362/3064) your account within the specified time.

##  Prerequisites
- The cloud disk is in the **To Be Mounted** status. [Unmount](https://intl.cloud.tencent.com/document/product/362/6740) cloud disks that are mounted.
- **All important data are already backed up**.

## Manually terminating monthly subscription cloud disks
### Manually terminating unexpired cloud disks in the console
If you no longer need a monthly subscription cloud disk, you can terminate it manually. Once the status of the cloud disk becomes **To be repossessed**, no fees will be incurred. **The cloud disk is disabled (the cloud disk will be unavailable, but data is retained) and kept in the recycle bin for 7 days. You can recover the cloud disk and continue to use it after you [renew](https://cloud.tencent.com/document/product/362/6739) it. The cloud disk will be automatically terminated if you do not renew it within 7 days. You can also permanently terminate the cloud disk in the recycle bin.**
Each Tencent Cloud account can return one monthly subscription cloud disk within five days without reason. Each account can also do self-service returns for three monthly subscription cloud disks. For more information on refunds, see [Refunds] (https://cloud.tencent.com/document/product/362/18072). When you hit the return limit, you will not be able to manually terminate the monthly subscription cloud disks.

1. Log in to the [CBS Console](https://console.cloud.tencent.com/cvm/cbs).
2. You can use the following methods to terminate a cloud disk:
  a. Single termination: locate the target cloud disk that is in a **To Be Mounted** status, click **More** -> **Terminate/Return**.
  b. Batch termination: select multiple target cloud disks that are in a **To Be Mounted** status and click **Terminate/Return** at the top of the list.

>!When the cloud disk is terminated, all data on the cloud disk will also be deleted, and cannot be restored. Please note that cloud disks that have been terminated cannot be recovered. 
>
3. In the **Terminate Cloud Disk** pop-up box, check **Read and agree to [Refunding Policy](https://cloud.tencent.com/document/product/362/18072)]**, and click **OK**.
 The system will stop billing, disable the target cloud disk (the cloud disk will be unavailable, but data is retained), and move it to the recycle bin.
 ![](https://main.qcloudimg.com/raw/77f046711195bdd9094bf3bd6ac842fc.png)

### Permanently terminate the monthly subscription cloud disk in the recycle bin
You can permanently terminate the monthly subscription cloud disk in the [Recycle Bin](https://console.cloud.tencent.com/cvm/recycle/cbs).

1. Log in to the [CBS Recycle Bin](https://console.cloud.tencent.com/cvm/cbs).
2. You can use the following methods to permanently terminate a cloud disk:
   a. Single termination: select **Release** in the row of the target cloud disk in the **To be repossessed** status.
   b. Batch termination: select multiple target cloud disks in the **To be repossessed** status and click **Batch release** at the top of the list.

>!When the cloud disk is terminated, all data on the cloud disk will also be deleted, and cannot be restored. Please note that cloud disks that have been terminated cannot be recovered. 
>
5. Enter the verification code in the pop-up box, and click **OK** to complete the termination process.
  The target cloud disk is **permanently terminated and cannot be recovered**.

## Manually terminating pay-as-you-go cloud disks
1. Log in to the [CBS Console](https://console.cloud.tencent.com/cvm/cbs).
2. You can use the following methods to terminate a cloud disk:
  a. Single termination: locate the target cloud disk that is in a **To Be Mounted** status, click **More** -> **Terminate/Return**.
  b. Batch termination: select multiple target cloud disks that are in a **To Be Mounted** status and click **Terminate/Return** at the top of the list.

>!When the cloud disk is terminated, all data on the cloud disk will also be deleted, and cannot be restored. Please note that cloud disks that have been terminated cannot be recovered. 
>
3. In the **Terminate Cloud Disk** pop-up box, click **Confirm** to complete the termination.
 The target cloud disk will no longer be billed. It is **permanently terminated and cannot be recovered**.

