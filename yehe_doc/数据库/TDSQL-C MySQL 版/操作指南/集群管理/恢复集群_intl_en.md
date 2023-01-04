This document describes how to restore an isolated cluster in the console.

## Overview
If a cluster is deleted by mistake, due to overdue payment, or upon instance expiration, you can restore all its read-write and read-only instances from the recycle bin before it is eliminated.
>!
>- After the cluster's read-write and read-only instances are restored, their configurations will remain unchanged.
>- A cluster cannot be deleted and recovered in consecutive attempts.

## Directions
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb).
2. Select **Recycle Bin** on the left sidebar, select the region, find the target read-write and read-only instances in the recycle bin, and click **Restore** in the **Operation** column of the read-write instance.
3. Click **Restore** in the **Operation** column of the read-only instance.
>?
>- Read-only instances can be restored only after the read-write instance is restored.
>- You can only restore an instance before it is terminated.
>- If you click **Terminate** in the **Operation** column, the instance will be eliminated immediately and cannot be restored. Therefore, proceed with caution.
>
4. After the restoration is completed, the cluster becomes **Running**, and you can see it in the cluster list.
