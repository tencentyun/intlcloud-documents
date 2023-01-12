TDSQL-C for MySQL backups include data and binlog backups in automatic and manual modes. Automatic backups cannot be manually deleted. You can set and adjust the backup retention period as needed, after which they will be automatically deleted.

This document describes how to set the backup retention period in the console.

>?The binlog backup retention period cannot be shorter than the data backup retention period.

## Directions
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb).
2. Select the region, find the target cluster in the cluster list, and click the cluster ID or **Manage** in the **Operation** column to enter the cluster management page.
3. On the cluster management page, select the **Backup Management** tab and click **Auto-Backup Settings**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/P9eE337_18.png)
4. In the **Backup Settings** window, set the data and binlog backup retention periods separately and click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/XaNV418_19.png)
