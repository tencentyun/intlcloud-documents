This document describes how to restore an isolated instance in the console.

## Overview
If an instance is deleted by mistake, due to overdue payment, or upon expiration, you can restore it from the recycle bin before it is eliminated.
>!
>- After an instance is restored, it uses the same configurations as before.
>- An instance cannot be terminated, restored and terminated again in a short time.

## Directions
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb).
2. Select **Recycle Bin** on the left sidebar, select the region, find the target instance, and click **Restore** in the **Operation** column.
>!
> - Read-only instances in a cluster can be restored only after the read-write instance in the cluster is restored.
> - You can only restore an instance before it is terminated.
> - If you click **Terminate** in the **Operation** column, the instance will be eliminated immediately and cannot be restored. Therefore, proceed with caution.
3. In the pop-up window, select a renewal period, confirm the instance information, and click **OK**.
4. After the restoration is completed, the instance becomes **Running**, and you can see it in the instance list.

