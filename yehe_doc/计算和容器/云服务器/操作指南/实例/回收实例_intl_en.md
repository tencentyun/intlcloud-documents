This document describes how to repossess a Cloud Virtual Machine (CVM) instance from the recycle bin. For more information, please see [Arrears Reminder](https://intl.cloud.tencent.com/document/product/213/2181). 

## Instance Repossession Description
Tencent Cloud recycle bin is a cloud service repossession mechanism as detailed below:
- **Pay-as-you-go instances** that are manually terminated or terminated at a scheduled time will be put into the recycle bin. If the account is in arrears, the repossession mechanism does not apply to pay-as-you-go instances, and these instances are directly released when the account is in arrears for 2 hours + 15 days.

Instance status in the recycle bin are as follows:
Pay-as-You-Go instances in the recycle bin
 - **Retention period:** if your account has no overdue payments, terminated instances will be retained in the recycle bin for 2 hours.
 - **Expiry processing:** if instances are not renewed before the retention period ends, the system will release instance resources and automatically [terminate instances](https://intl.cloud.tencent.com/zh/document/product/213/4930), which cannot be recovered. EIPs bound to these instances will be retained. If you don't need such EIPs, release them promptly.
 - **Mounting relationship:** after the instance enters the recycle bin, its mounting relationship with Cloud Load Balancer, Cloud Block Storage, and Classiclink will **not be automatically terminated**.
 - **Operation restrictions:** for instances in the recycle bin, you can only perform the following operations: **[renew and recover](https://intl.cloud.tencent.com/document/product/213/6143)**, **[terminate/return](https://intl.cloud.tencent.com/zh/document/product/213/4930)** and **[create image](https://intl.cloud.tencent.com/document/product/213/4942)** (except for special models).



<dx-alert infotype="notice" title="">
- You cannot repossess pay-as-you-go instances in the recycle bin if your account is in arrears. Please renew the payment first.
- Pay-as-you-go instances are stored in the recycle bin for a maximum of 2 hours. Please note the release time and renew the payment in time to repossess the instances.
- Pay-as-you-go instances cannot enter the recycle bin if your account is in arrears. You can view them on the CVM instance list page. The instances will be released after your account has been in arrears for 2 hours + 15 days.
</dx-alert>

:::
</dx-tabs>

## Recovering Instances
1. Log in to the CVM console and select **Recycle Bin** > **[Instance Recycle Bin](https://console.cloud.tencent.com/cvm/recycler/cvm)** on the left sidebar.
2. On the **Instance Recycle Bin** page, perform different operations as needed.
<dx-tabs>
::: Recovering one instance
Find the instance to be recovered in the list, click **Recover** in the **Operation** column, and complete the renewal payment.
:::
::: Batch recovering instances
Select all instances to be recovered in the list, click **Batch Recover** at the top, and complete the renewal payment.
:::
</dx-tabs>

