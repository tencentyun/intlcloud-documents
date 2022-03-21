
TDSQL-C can roll back databases/tables to an original cluster and roll back [an entire cluster (clone)](https://intl.cloud.tencent.com/document/product/1098/40635) to a new cluster. You can choose different rollback methods according to your business needs. This document describes how to roll back certain databases/tables in the original cluster.

## Rollback Method
- Rollback by backup file: this method restores the cluster to the dataset state of a backup file. The selection range of the backup file is determined by the data backup retention period you set.
- Rollback by time point: this method restores the cluster to any time point within the log backup retention period you set.

## Directions
1. Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb) and click a cluster name in the cluster list to enter the cluster management page.
2. On the cluster management page, select the **Backup Management** tab and click **Rollback**.
![](https://main.qcloudimg.com/raw/72eaa8dd67b4f38fd961254e663c691a.png)
2. On the database/table rollback page, select the database/table to be rolled back, rename it, and click **Rollback**.
 - For database/table rollback, you need to specify the database/table to be rolled back. If you cannot determine all the involved databases/tables, we recommend you [clone](https://intl.cloud.tencent.com/document/product/1098/40635) the original cluster and migrate back to it after determining the databases/tables.
 - If the database/table to be rolled back does not exist at the specified time point, database/table rollback will fail.
 - If the database/table to be rolled back does not exist or has been dropped, you need to log in to the database and create a database/table first before performing rollback in the console.
 - If there are primary or foreign key constraints in the specified database/table to be rolled back, please ensure that the associated databases/tables exist during the rollback process; otherwise, database/table rollback will fail.
 - Up to 500 databases or tables can be rolled back at a time.
![](https://main.qcloudimg.com/raw/99db81c2b3d00b7e671c40873266901c.png)
3. In the pop-up window, confirm that everything is correct and click **OK** to initiate the rollback task.
4. After the task is submitted, you can click **View Rollback Task** or go to the task list to view the rollback progress and task details.
![](https://main.qcloudimg.com/raw/626c1149f1735d23a1f168169c45ff59.png)
5. After the rollback is completed, you can see the new restored database/table in the original cluster and perform further operations.
