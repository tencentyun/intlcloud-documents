### Operation Scenario
Based on your business needs, you can manually terminate a pay-as-you-go instance. After the pay-as-you-go instance is terminated, it won't incur any further fees.

> - After an instance is terminated completely, its data will not be recoverable. Please back up the data in advance.
> - After an instance is terminated completely, its IP resources will be released simultaneously. If the instance has read-only instances or disaster recovery instances:
> -  Disaster recovery instances will disconnect their sync connections and be promoted to master instances automatically.
> -  After an instance is terminated completely, the refund procedures are as detailed below:
> - The five-day guaranteed self-service refund amount will be refunded to your Tencent Cloud account.
> - The normal self-service refund amount will be refunded to your Tencent Cloud account at the ratio of cash and gift vouchers paid upon purchase.
> -  For orders from promotional reward channel, the refund will be charged 25% of their actual cash payment amount. These types of orders do not support self-service refunds, please submit a ticket to request a refund.
> -  After a pay-as-you-go instance is terminated, it will be moved to the TencentDB recycle bin and retained there for 24 hours. During the retention period, the instance cannot be accessed but can be restored after renewal.
## Directions
1. Log in to the [TencentDB for TDSQL Console](https://console.cloud.tencent.com/dcdb).
2. Select the pay-as-you-go instance you want to terminate.
3. Click **More**>**Terminate/Return** in the instance list.
4. In the pop-up dialog box, confirm your operation and click **Terminate Now**.