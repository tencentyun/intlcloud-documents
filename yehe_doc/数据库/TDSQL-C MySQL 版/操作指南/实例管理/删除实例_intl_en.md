This document describes how to delete an instance from a cluster when it is  no longer used.

>! 
>- After a read-write instance is deleted, its data and backup files will also be deleted and cannot be recovered in the cloud. Store your backup files safely elsewhere in advance.
>- After an instance is deleted, its IP resources will also be released. Therefore, confirm that your business no longer needs to access the instance before deleting it.
>- The read-write instance in a cluster can be deleted only after all read-only instances in the cluster are deleted.
>- If you delete a cluster, all instances in the cluster will be deleted.
>- Data is deleted only when the read-write node is deleted. Deleting read-only instances only deletes computing resources.

## Lifecycle
- After a monthly-subscribed instance is deleted, it will be moved to the recycle bin and retained there for seven days. During the retention period, the instance cannot be accessed, but it can be restored after renewal.
- After a pay-as-you-go instance is deleted, it will be moved to the recycle bin and retained there for 24 hours. During the retention period, the instance cannot be accessed, but it can be restored after renewal.


## Directions
**Started serverless or non-serverless instances**
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb) and click the ID of the target cluster in the cluster list or **Manage** in the **Operation** column to enter the cluster management page.
2. On the cluster management page, select the **Instance List** tab, find the target read-write or read-only instance, and select **More** > **Delete** in the **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/f1625de84187cb549d5d27a211c5dae9.png)
3. In the pop-up window, confirm that the information about the instance to be deleted is correct and click **OK**.

**Paused serverless clusters**
If a serverless cluster is paused, you cannot enter its management page from the console, so you cannot delete instances from it in the way described above. You can either start the cluster and then delete instances or delete the cluster directly.

