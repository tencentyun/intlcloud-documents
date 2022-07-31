## Overview

When you return an instance, your monthly subscribed instance expires, or your account balance is insufficient to pay the fees of a pay-as-you-go instance, the instance will be moved to the recycle bin. If you have backed up your data and you are sure that you don't need the instance any more, you can release all its resources during the retention period to avoid resource waste.

## Prerequisites

- The instance is isolated in the recycle bin, and the data has been backed up.
- The instance is no longer needed.

## Directions

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. On the left sidebar, select **Redis** > **Recycle Bin**.
3. Above the instance list on the right, select the region.
4. On the **Recycle Bin** page on the right, you can see the list of instances in the recycle bin, all of which are in the **Isolated** status.
5. In the instance list in the recycle bin, find the target instance and click **Eliminate Now** in the **Operation** column.
6. In the **Eliminate Now** window, confirm the instance information and click **OK**.
>!The instance will be completely eliminated, and its data will not be recoverable. Therefore, you need to back up the data in advance.

## Related APIs

| API | Description |
| ------------------------------------------------------------ | ------------------ |
| [CleanUpInstance](https://intl.cloud.tencent.com/document/product/239/32071) | Eliminates an instance in the recycle bin immediately. |

