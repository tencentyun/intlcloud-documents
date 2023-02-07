
## Overview
Based on your business needs, you can return pay-as-you-go and monthly subscribed instances in the console in a self-service manner.
- After a monthly subscribed instance is returned, it will be moved to the TencentDB recycle bin and retained there for seven days. During the retention period, the instance cannot be accessed, but it can be restored after renewal.
- After a pay-as-you-go instance is returned, it will be moved to the TencentDB recycle bin and retained there for 24 hours. During the retention period, the instance cannot be accessed, but it can be restored after renewal.

After an instance is returned, once its status has changed to **Isolating**, it will no longer generate fees.
>!
>- After the instance is terminated, its data and backup files will also be terminated and cannot be recovered in the cloud. Store your backup files safely elsewhere in advance.
>- After an instance is terminated, its IP resources will be released simultaneously. Its:
>  - Read-only instances will be terminated at the same time.
>  - Disaster recovery instances will stop the sync connection and automatically promote to source instance.
>- After an instance is terminated, the refund procedures are as detailed below:
>  - For instances that meet the 5-day unconditional refund policy, the payment will be returned to your Tencent Cloud account.
>  - For normal instances, the payment will be returned to your Tencent Cloud account by the proportion of the cash and gift cards paid for the purchase.
> - For an order placed from promotion rewarding channels, 25% of the actual cash payment amount will be deducted from the refund amount as service charges. Currently, self-service refund is unavailable for such kind of orders, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply for the refund.
> 

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), select the target instance in the instance list, and select **More** > **Terminate/Return** or **Terminate/Return & Refund** in the **Operation** column.
2. In the pop-up window, read and select **I have read and agree to Termination Rules** and click **OK**.
>?
>- If you want to terminate a monthly subscribed instance but find the **Terminate** button unavailable, it means that the self-service return quota under the account has run out, and the instance cannot be manually terminated; instead, it will be automatically terminated upon expiration.
>- You can batch terminate instances by selecting them in the instance list and clicking **More** > **Terminate/Return** at the top.
>
![](https://main.qcloudimg.com/raw/6e376a4a726195aefee841930577a5b3.png)
