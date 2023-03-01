TDSQL-C for MySQL can roll back databases/tables to an original cluster and roll back an entire cluster (clone) to a new cluster as instructed in [Restoring Data to New Cluster](https://www.tencentcloud.com/document/product/1098/48392). You can choose different rollback methods based on your business needs. This document describes how to roll back certain databases/tables to the original cluster.

## Rollback methods
- Rollback by backup file: This method restores the cluster to the dataset state of a backup file. The selection range of the backup file is determined by the data backup retention period you set.
- Rollback by time point: This method restores the cluster to any time point within the log backup retention period you set.

## Directions
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb) and click a cluster ID in the cluster list to enter the cluster management page.
2. On the cluster management page, select the **Backup Management** tab and click **Roll Back**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Mjdx841_14.png)
2. On the database/table rollback page, select the database/table to be rolled back, rename it, and click **Roll Back**.
   - For database/table rollback, you need to specify the database/table to be rolled back. If you are not sure about that, we recommend you [clone](https://www.tencentcloud.com/document/product/1098/48392) the original cluster first and then migrate back to it later when you can specify the rollback objects.
   - If the database/table to be rolled back does not exist at the specified time point, the rollback will fail.
   - If the database/table to be rolled back does not exist or has been dropped, you need to log in to the database and create a database/table first before performing rollback in the console.
   - If there are primary or foreign key constraints in the specified database/table to be rolled back, make sure that the associated databases/tables exist during the rollback process; otherwise, the rollback will fail.
   - Up to 500 databases or tables can be rolled back at a time.
   ![](https://staticintl.cloudcachetci.com/yehe/backend-news/6eWJ676_15.png)
3. In the pop-up window, confirm that everything is correct and click **OK** to initiate the rollback task.
5. After the task is submitted, you can click **View Rollback Task** or go to the task list to view the rollback progress and task details.
5. After the rollback is completed, you can see the new restored database/table in the original cluster and perform further operations.
