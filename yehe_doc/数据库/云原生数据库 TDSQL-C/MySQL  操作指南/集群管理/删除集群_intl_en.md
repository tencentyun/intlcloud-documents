
This document describes how to delete a no longer needed TDSQL-C for MySQL cluster in the console.
- After a monthly subscribed cluster/instance is deleted, it will be moved to the recycle bin and retained there for seven days. During the retention period, the cluster/instance cannot be accessed but can be renewed and restored.
- After a pay-as-you-go cluster/instance is deleted, it will be moved to the recycle bin and retained there for 24 hours. During the retention period, the cluster/instance cannot be accessed but can be restored after renewal.

## Directions
1. Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb), locate the target cluster in the cluster list, and click **More** > **Delete** in the **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/98f288aa31ecb3fbf7c0a196a9f36f75.png)
2. In the pop-up window, confirm the deletion information and click **OK**.
>!  
>- After a cluster is deleted, all instances in it will also be automatically deleted.
>- After a pay-as-you-go cluster is deleted, its billing will stop automatically.
>- If a monthly subscribed cluster is deleted before it expires, the fees of all instances in it will be calculated again by the usage duration at the pay-as-you-go price, and your original payment will be refunded after fees incurred are deducted from it.
3. After a cluster is deleted, instances in it will also be moved to the recycle bin automatically. Instances in the recycle bin cannot be accessed or managed and don't incur any fees. During the isolation period, you can restore the instances from the recycle bin.
