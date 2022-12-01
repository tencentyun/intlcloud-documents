You can delete a TDSQL-C for MySQL cluster when it is no longer used.

This document describes how to delete a cluster in the console.

## Lifecycle
- After a monthly subscribed cluster/instance is deleted, it will be moved to the recycle bin and retained there for seven days. During the retention period, the cluster/instance cannot be accessed, but it can be restored after renewal.
- After a pay-as-you-go cluster/instance is deleted, it will be moved to the recycle bin and retained there for 24 hours. During the retention period, the cluster/instance cannot be accessed, but it can be restored after renewal.

## Directions
**Started serverless or non-serverless clusters**
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb).
2. Find the target cluster in the cluster list and click **More** > **Delete** in the **Operation** column.
3. In the pop-up window, read and agree to the termination rules and click **OK**.
>!  
>- After a cluster is deleted, all instances (including read-write and read-only instances) in it will also be automatically deleted.
>- After a pay-as-you-go cluster is deleted, its billing will stop automatically.
>- If a monthly subscribed cluster is deleted before it expires, the fees of all instances in it will be calculated again by the usage duration at the pay-as-you-go price, and your original payment will be refunded after fees incurred are deducted from it.
1. After a cluster is deleted, instances in it will also be moved to the recycle bin automatically. Instances in the recycle bin cannot be accessed or managed and don't incur any fees. During the isolation period, you can restore the instances from the recycle bin.


**Paused serverless clusters**
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb).
2. Find the target cluster in the cluster list and click **Delete** in the **Operation** column.
3. In the pop-up window, click **OK**.

