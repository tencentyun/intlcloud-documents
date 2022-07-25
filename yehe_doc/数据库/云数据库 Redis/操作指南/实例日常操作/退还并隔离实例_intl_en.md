## Overview

- If you no longer need pay-as-you-go instances and your Tencent Cloud account has no overdue payments, you can directly terminate them in the console to avoid further fee deduction. Terminated instances are retained in the recycle bin for two hours, and you can start them up to restore them. After two hours, the system will directly eliminate them, and all their data will be permanently deleted.

## Notes

After an instance is returned, once its status changes to **Isolated** or **To be deleted**, it will no longer incur fees.
>!
> - After the instance is terminated, all its data will be cleared and cannot be recovered. Be sure to back up your data first before submitting a termination task.
> - When the instance is terminated, its IP resources will be released simultaneously.

## Terminating a pay-as-you-go instance

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. Above the instance list on the right, select the region.
3. In the **Instance List**, select the target pay-as-you-go instance and click **More** > **Terminate** in its **Operation** column. 
![](https://qcloudimg.tencent-cloud.cn/raw/d58f890f17d7a7be5f63268235724493.png)
4. In the **Terminate Instance** pop-up window, confirm the information of the target instance, understand the impact of instance termination, and click **Terminate**.
5. On the left sidebar, select **Recycle Bin**, and you can see that the terminated pay-as-you-go instance is isolated there. The instance is in **Isolated** status and will no longer incur fees.
![](https://qcloudimg.tencent-cloud.cn/raw/66441a757e4107270e7489521e8fe401.png)
6. (Optional) Click **Start Up** to restore the instance, or click **Eliminate Now** to directly eliminate it. For detailed directions, see [Recycle Bin](https://intl.cloud.tencent.com/document/product/239/46561).

## Related APIs

| API | Description |
| ------------------------------------------------------------ | ---------------- |
| [DestroyPostpaidInstance](https://intl.cloud.tencent.com/document/product/239/32063) | Terminates a pay-as-you-go instance. |

