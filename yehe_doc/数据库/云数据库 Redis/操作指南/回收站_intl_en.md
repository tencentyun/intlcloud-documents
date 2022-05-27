This document describes the recycle bin feature of TencentDB for Redis. Terminated instances will be put into the recycle bin and can be restored.

## Background
Tencent Cloud recycle bin offers a mechanism for repossessing cloud services. If your account balance is sufficient, you can restore terminated instances that are still in the recycle bin.

## Version Requirement
Currently, TencentDB for Redis 5.0, 4.0, and 2.8 support instance repossession.

## Notes
The repossession of pay-as-you-go instances is as described below:



- **Retention period:** If your account has no overdue payments, terminated instances will be retained in the recycle bin for three days.
- **Expiration processing**: Instances that are not renewed before the retention period ends will be released and cannot be restored.

>! 
>- After the account balance becomes zero, instances will be automatically shut down and moved from the instance list to the recycle bin, and the billing will stop in 24 hours.
>- You cannot restore pay-as-you-go instances from the recycle bin if your account has overdue payments. You need to top up your account first.

## Prerequisites
- The TencentDB for Redis instance has been [terminated](https://intl.cloud.tencent.com/document/product/239/31937).
- Your Tencent Cloud account balance is sufficient.

## Directions
Instances in the recycle bin can be **renewed**, **started up**, or **eliminated now**.

### Viewing instance in recycle bin
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. On the left sidebar, select **Redis** > **Recycle Bin**.
3. Above the instance list on the right, select the region.
4. On the **Recycle Bin** page on the right, you can see the list of instances in the recycle bin.

### Restoring one instance
1. In the instance list in the recycle bin, find the target instance and click **Start Up** in the **Operation** column.
2. In the **Start Instance** window, confirm the instance information and click **OK**.
>? As TencentDB for Redis is an in-memory database, to use the batch instance restoration feature, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.

### Eliminating instance
1. In the instance list in the recycle bin, find the target instance and click **Eliminate Now** in the **Operation** column.
2. In the **Eliminate Instance** window, confirm the instance information and click **OK**.
> !The instance will be completely eliminated, and its data will not be recoverable. Therefore, you need to back up the data in advance.

