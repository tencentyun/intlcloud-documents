
This document describes how to delete instances that are no longer used from a cluster.
- After a monthly-subscribed instance is deleted, it will be moved to the recycle bin and retained there for seven days. During the retention period, the instance cannot be accessed but can be restored after renewal.
- After a pay-as-you-go instance is deleted, it will be moved to the recycle bin and retained there for 24 hours. During the retention period, the instance cannot be accessed but can be restored after renewal.

## Directions
1. Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb) and click a cluster ID in the cluster list to enter the cluster management page.
2. On the **Instance List** tab, locate the desired instance and select **More** > **Delete** in the **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/72d05142cc8a417d5508662ab79c44ac.png)
3. In the pop-up dialog box, confirm that the information about the instance to be deleted is correct and click **OK**.
>! 
>- You can delete the read-write instance only after all read-only instances have been deleted.
>- If you delete a cluster, all instances in the cluster will be deleted.
>- Data is deleted only when the read-write node is deleted. Deleting read-only instances only deletes computing resources.

