## Overview
You can return pay-as-you-go instances in the console based on your business needs in a self-service manner.
- After a pay-as-you-go instance is returned, it will be moved to the TencentDB recycle bin and retained there for 24 hours. During the retention period, the instance cannot be accessed, but it can be restored after renewal.

When an instance is returned and its status has changed to **Isolated**, it will no longer generate fees.
>!
>- After the instance is terminated, its data cannot be recovered, and its backup files will also be terminated, so the data cannot be restored in the cloud. Store your backup files safely elsewhere in advance.
>- After the instance is terminated, its IP resources will be released simultaneously. If the instance has read-only and publish/subscribe configuration:
>  - Read-only instances will be terminated at the same time.
>  - After the instance is terminated, the existing pub/sub configuration on the instance will be deleted.
>- After the instance is terminated, the refund procedures are as detailed below:
>  - For instances that met the 5-day no-questions-asked refund policy, the payment will be returned to your Tencent Cloud account.
>  - For normal instances, the payment will be returned to your Tencent Cloud account by the proportion of the cash and gift cards paid for the purchase.
>  - For orders from promotional reward channel, the refund will be charged 25% of their actual cash payment amount. These types of orders do not support self-service refunds, and you need to request a refund.
> 

## Directions
1. Log in to the [TencentDB for SQL Server Console](https://console.cloud.tencent.com/sqlserver), select the target instance in the instance list, and select **More** > **Terminate/Return** in the "Operation" column.
![](https://main.qcloudimg.com/raw/be837273695eb17b86447852317fb45f.png)
2. In the pop-up dialog box, indicate your consent and click **Terminate**.
><img src="https://main.qcloudimg.com/raw/eed621d2fb6827d94ab5b2875a42fc84.png"  style="zoom:90%;">

