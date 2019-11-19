## Operation Scenario
Based on your business needs, you can manually terminate pay-as-you-go and monthly subscribed instances. After a pay-as-you-go instance is terminated, it won't incur any further fees. Monthly subscribed instances can by refunded in a self-service manner.


>- After an instance is terminated completely, its data will not be recoverable. Please back up the data in advance.
>- After an instance is terminated completely, its IP resources will be released simultaneously. If the instance has read-only instances or disaster recovery instances:
> - Read-only instances will be terminated at the same time.
>  - Disaster recovery instances will disconnect their sync connections and be promoted to master instances automatically.
> - After an instance is terminated completely, the refund procedures are as detailed below:
> - The five-day guaranteed self-service refund amount will be refunded to your Tencent Cloud account.
>  - The normal self-service refund amount will be refunded to your Tencent Cloud account at the ratio of cash and gift vouchers paid upon purchase.
>  - For an order placed from promotion rewarding channels, 25% of the actual cash payment amount will be deducted from the refund amount as a refund handling fee. Currently, self-service refund is unavailable for such kind of orders, and the refund application should be initiated by [submitting a ticket](https://console.cloud.tencent.com/workorder/category).
> - After a monthly subscribed instance is terminated, it will be moved to the TencentDB recycle bin and retained there for seven days. During the retention period, the instance cannot be accessed but can be restored.
>- After a pay-as-you-go instance is terminated, it will be moved to the TencentDB recycle bin and retained there for 24 hours. During the retention period, the instance cannot be accessed but can be restored.

## Directions
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb).
2. Select **Instance List** on the left sidebar.
3. Select the instance to be terminated and select **More** > **Terminate/Return** or **Terminate/Return & Refund** in the "Operation" column.
![](https://main.qcloudimg.com/raw/ea0d80564ad54c6c9e3ea43070c71f20.png)
4. In the pop-up dialog box, indicate your consent and click **Terminate Now**.
>
![](https://main.qcloudimg.com/raw/6e376a4a726195aefee841930577a5b3.png)
