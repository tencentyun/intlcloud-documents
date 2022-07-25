## Overview

Tencent Cloud recycle bin is a cloud service repossession mechanism. When you return an instance or your account balance is insufficient to pay the fees of a pay-as-you-go instance, the instance will be moved to the recycle bin. You can restore the pay-as-you-go instance from the recycle bin in the retention period.

### Pay-as-you-go instance repossession mechanism

- If you no longer need pay-as-you-go instances and your Tencent Cloud account has no overdue payments, you can directly return them into the recycle bin as instructed in [Returning and Isolating Instance](https://intl.cloud.tencent.com/document/product/239/31937). Terminated instances are retained in the recycle bin for two hours, and you can start them up to restore them. After two hours, the system will directly eliminate them, and all their data will be deleted and cannot be recovered.
- For pay-as-you-go instances, billing will continue within 24 hours after your account balance drops below 0. After 24 hours, the instances will be automatically moved to the recycle bin for isolation, billing will stop, and you won't be able to use instance resources. In case of overdue payments, the instances will be retained in the recycle bin for 24 hours. If you top up your account within 24 hours, you can restore instance resources; otherwise, the system will automatically terminate them after 24 hours, and all data will be cleared and cannot be recovered.

## Prerequisites

- The instance is isolated in the recycle bin.
- Your Tencent Cloud account balance is sufficient.

## Restoring one isolated instance

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. On the left sidebar, select **Redis** > **Recycle Bin**.
3. Above the instance list on the right, select the region.
4. On the **Recycle Bin** page on the right, you can see the list of instances in the recycle bin, all of which are in the **Isolated** status.
![img](https://qcloudimg.tencent-cloud.cn/raw/3aa2d7cd336d2360f6920890d3028113.png)
5. In the instance list in the recycle bin, find the target instance and click **Start Up** in the **Operation** column.
6. Confirm the instance information and restore it.
 - If the instance is pay-as-you-go, confirm the instance information and click **OK** in the **Start Instance** window to restore it.
>? As TencentDB for Redis is an in-memory database, to use the batch instance restoration feature, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.

## Related APIs

| API | Description |
| ------------------------------------------------------------ | ---------- |
| [StartupInstance](https://intl.cloud.tencent.com/document/api/239/33291) | Restores an isolated instance. |

