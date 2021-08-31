## Overview
Based on your business needs, you can manually terminate pay-as-you-go instances.
- After a pay-as-you-go instance is terminated, it will be moved to the TencentDB recycle bin and retained there for 24 hours. During the retention period, the instance cannot be accessed but can be restored.

After an instance is terminated, once its status has changed to **Isolated** or **To be deleted**, it will no longer incur fees.
>!
>- After the instance is terminated, all data will be cleared and cannot be recovered. Please be sure to back up your data first before submitting a termination task.
>- When the instance is terminated, its IP resources will be released simultaneously.


## Directions
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), locate the desired instance in the instance list, and select **More** > **Terminate** in the **Operation** column.
2. In the pop-up window, confirm that everything is correct and click **Terminate**.
3. After the termination, you will be redirected to the [instance recycle bin](https://console.cloud.tencent.com/redis/recycle), where you can **Start** or **Eliminate** the isolated instance.

