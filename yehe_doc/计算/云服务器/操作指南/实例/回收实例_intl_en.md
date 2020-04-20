This document describes how to repossess a Cloud Virtual Machine (CVM) instance from the recycle bin. For more information, please see [Arrears Reminder](https://intl.cloud.tencent.com/document/product/213/2181). 

## Recycle Bin
The pay-as-you-go instance will enter the recycle bin after it is terminated by the user or at the scheduled time. If the account is in arrears, the pay-as-you-go instance will not enter the recycle bin. It will be released after the account has been in arrears for 26 hours.

### Pay-as-you-go instances in the recycle bin

 - **Retention period:** instance terminated by the user will be retained in the recycle bin for 2 hours.
 - **Expiry processing:** if instances are not renewed before the retention period ends, the system will release instance resources and automatically [terminate instances](https://intl.cloud.tencent.com/document/product/213/4930), which cannot be repossessed. Elastic IPs bound to these instances are also released.
 - **Mounting relationship:** after the instance enters the recycle bin, its mounting relationship with Cloud Load Balancer, Cloud Block Storage, and Classiclink will **not be automatically terminated**.
 - **Operation limit:** you can only [**terminate instances**](https://intl.cloud.tencent.com/document/product/213/4930) in the recycle bin.
 
> 
- You cannot repossess pay-as-you-go instances in the recycle bin if your account is in arrears. Please renew the payment first.
- Pay-as-you-go instances are stored in the recycle bin for a maximum of 2 hours. Please note the release time and renew the payment in time to repossess the instances.
- Pay-as-you-go instances cannot enter the recycle bin if your account is in arrears. You can view them on the CVM instance list page. The instances will be released after your account has been in arrears for 26 hours.

## Repossessing Instances
 1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).
 2. On the left sidebar, click **Recycle Bin** > **Instance Recycle Bin** to enter the CVM recycle list.
 3. Recover a single instance: find the instance to be recovered in the list, click **Recover**, and complete the renewal payment.
 4. Recover instances in batches: select all instances to be recovered, click **Recover in Batch** on the top, and complete the renewal payment.

