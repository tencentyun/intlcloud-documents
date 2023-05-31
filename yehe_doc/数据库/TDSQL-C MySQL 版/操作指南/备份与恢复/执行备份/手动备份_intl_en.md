
TDSQL-C for MySQL supports automatic backup and manual backup. This document describes how to create a manual backup in the console.
>?
>- With manual backup, you can use snapshot backup to manually back up the entire cluster or use logical backup to back up the entire cluster or specified databases/tables.
>- You can delete manual backups from the backup list in the console to release backup space.

## Directions
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb).
2. Select the region at the top, find the target cluster in the cluster list, and click the cluster ID or **Manage** in the **Operation** column to enter the cluster management page.
3. On the cluster management page, select the **Backup Management** tab and click **Manual Backup**.
![](https://qcloudimg.tencent-cloud.cn/raw/d3ef28cdf05f8a0ae8acebf136188e37.png)
4. In the pop-up window, select the backup type and object, set the backup file alias, and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/d708baa3ecfd5e7cdf95fc6136e8c23c.png)
 - **Backup Type**: Snapshot backup and logical backup are supported.
 - **Object**: Snapshot backup applies to the entire instance, while logical backup applies to the entire instance or specified databases/tables.
 - **Alias**: You can set a file alias when creating a manual backup, which can contain up to 60 digits, letters, or symbols (-_./()[]+=:;@).
>!We recommend you perform a manual logical backup task during off-peak hours, as it will lock the database and affect database use.
>
5. After creating a manual backup task, you can view the task progress in the **Task List** on the left sidebar. You can also view the execution status by clicking **Backup Details** in the **Operation* column.
![](https://qcloudimg.tencent-cloud.cn/raw/b25a0fe39430902d738e386af262e44f.png)
