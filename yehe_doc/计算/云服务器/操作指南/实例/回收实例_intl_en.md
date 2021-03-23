This document describes how to recover a Cloud Virtual Machine (CVM) instance from the recycle bin. For more information, see [Overdue Payment](https://intl.cloud.tencent.com/document/product/213/2181). 

## Recycle Bin
Tencent Cloud recycle bin provides a CVM instance repossession mechanism as follows:
- **Pay-as-you-go instances**: the pay-as-you-go instance will enter the recycle bin after it is terminated by the user or at the scheduled time. If the account is overdue, the pay-as-you-go instance will not enter the recycle bin. It will be released after the account has been overdue for 2 hours and 15 days.

### Pay-as-you-go instances in the recycle bin

 - **Retention period**: instance terminated by the user will be retained in the recycle bin for 2 hours.
 - **Expiry processing**: if instances are not renewed before the retention period ends, the system will release instance resources and automatically [terminate instances](https://intl.cloud.tencent.com/document/product/213/4930), which cannot be recovered. Elastic IPs bound to these instances are also released.
 - **Mounting relationship**: after the instance enters the recycle bin, its mounting relationship with Cloud Load Balancer, Cloud Block Storage, and Classiclink will **not be automatically terminated**.
 - **Operation restriction**: instances in the recycle bin can only be [restored after renewal](https://intl.cloud.tencent.com/document/product/213/6143) or [terminated](https://intl.cloud.tencent.com/document/product/213/4930). Some instance types support [creating custom images](https://intl.cloud.tencent.com/document/product/213/4942)
 
>! 
> - You cannot restore pay-as-you-go instances from the recycle bin if your account is overdue. Please renew the payment first.
> - Pay-as-you-go instances are retained in the recycle bin for a maximum of 2 hours. Please note the release time and renew the payment in time to restore the instances.
> - Pay-as-you-go instances cannot enter the recycle bin if your account is overdue. You can view them on the CVM instance list page. The instances will be released after your account has been overdue for 2 hours and 15 days.

## Recovering Instance
 1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/).
 2. On the left sidebar, click **Recycle Bin** -> **Instance Recycle Bin** to enter the CVM recycle list.
 3. Recover a single instance: locate the instance to be recovered in the list, click **Recover** in the **Operation** column, and complete the renewal payment.
 4. Recover instances in batches: select all instances to be recovered, click **Recover Selected** on the top, and complete the renewal payment.

