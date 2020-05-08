This document describes how to repossess and restore a Cloud Virtual Machine (CVM) instance. For more information, see [Arrears Reminder](https://intl.cloud.tencent.com/document/product/213/2181). 

## Reclaiming Instances
Tencent Cloud Recycle Bin provides a CVM instance repossession mechanism. Pay-as-you-go instances that are manually terminated or terminated at a scheduled time will be moved to the recycle bin. If the account is in arrears, the repossession mechanism does not apply to pay-as-you-go instances, and these instances are directly released when the account remains in arrears for 26 hours.

### Moving pay-as-you-go instances to the recycle bin

 - **Retention period**: if the account is not in arrears, instances manually terminated by users are retained in the recycle bin for 2 hours.
 - **Processing upon expiration**: if the instances are not renewed in time before the retention period expires, the system releases these instance resources and starts to automatically [terminate instances](https://intl.cloud.tencent.com/document/product/213/4930). The terminated instances cannot be reclaimed. In addition, EIPs bound to these instances are also released.
 - **Binding relationship**: after an instance is moved into the recycle bin, the binding relationships with Cloud Load Balancer, Cloud Block Storage, and Classiclink **are not automatically terminated**.
 - **Operation restriction**: instances in the recycle bin can only be **restored after renewal** or [**terminated**](https://intl.cloud.tencent.com/document/product/213/4930).
 
> 
- A pay-as-you-go instance in the recycle bin cannot be restored if the account is in arrears. To restore this instance, you must first pay the renewal fee.
- A pay-as-you-go instance can be retained for up to 2 hours in the recycle bin. Therefore, you need to renew and restore the instance in time so that you can continue to use it.
- If your account is already in arrears, the pay-as-you-go instance cannot be moved to the recycle bin. Instead, you need to check the instance in the CVM instance list. If you do not renew the instance within 26 hours after the account is in arrears, the instance will be released.

## Restoring Instances
 1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).
 2. In the left sidebar, choose **Recycle Bin** > **CVM Recycle Bin** to go to the CVM repossession list.
 3. To restore a single instance, find the target instance in the list, click **Restore**, and pay the renewal fee.
 4. To restore instances in batch, select all target instances, click **Batch Restore** at the top, and pay the renewal fee.

