## Isolating Instances
An isolated instance cannot be used or accessed; however, it is not terminated or deleted, so you can restore it in the console. The resource space of the isolated instance will not be released, and basic data replicas will be retained. When the isolated instance expires, it will be completely terminated.
- A pay-as-you-go instance can be returned manually in the [console](https://console.cloud.tencent.com/mariadb/instance/index). After the instance is returned, it will be in **Isolated* status and retained for 24 hours, during which it cannot be accessed. If you want to restore it, you can do so in the instance list.

When an instance is returned and its status changes to **Isolated**, it will no longer generate fees.

>!
>- After an instance is isolated, its IP will be released, and you may not get back the original IP after the instance is restored.
>- After an instance is isolated, you cannot upgrade it, modify its parameters, create or modify an account for it, roll it back, or rename it.
>

### Directions
1. Log in to the [MariaDB console](https://console.cloud.tencent.com/mariadb). In the instance list, select an instance, and click **More** > **Terminate/Return** at the top.
2. In the pop-up dialog box, indicate your consent and click **Confirm**.
![](https://main.qcloudimg.com/raw/6fdd575dba4ca3989f946089327d1f7d.png)
Return to the instance list. The status of the instance has changed to **Isolated**, and you can choose to **Restore/Start up** it.

## Restoring Instances
An isolated instance can be restored to its normal running status, which may take several minutes. The restored instance may have a new IP rather than the original IP before isolation.

## Terminating Instances
If you don't need an instance anymore, you can return it, and when it is returned, its status changes to **Isolated**. Instances in isolation are completely terminated when they expire.

### Precautions
- After an instance is terminated completely, its data will not be recoverable. Please back up the data in advance.
- If an instance is terminated, its IP resources will be released simultaneously, and its disaster recovery instance will stop the sync connection and automatically promote to primary instance.
- After an instance is terminated completely, the refund procedures are as detailed below:
  - The 5-day free returns will be refunded to your Tencent Cloud account.
  - The standard returns will be refunded to your Tencent Cloud account at the ratio of cash and gift cards paid upon purchase.
  - For an order placed from promotion rewarding channels, 25% of the actual cash payment amount will be deducted from the refund amount as a refund handling fee. Currently, self-service refund is unavailable for such kind of orders, and the refund application should be initiated by [submitting a ticket](https://console.cloud.tencent.com/workorder/category).

 
