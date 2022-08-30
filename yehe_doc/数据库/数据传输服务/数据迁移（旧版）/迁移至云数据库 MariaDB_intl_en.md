## Preparations
You need to have the permissions of the source database, including RELOAD, PROCESS, REPLICATION SLAVE, LOCK TABLES, REPLICATION CLIENT, SHOW DATABASE, EVENT, and SELECT.

If you want to migrate views in the source database, you also need to have the SHOW VIEW permission.

## Directions
### 1. Create a migration task
(1) Log in to the [DTS console](https://console.cloud.tencent.com/dts) and click **Create Migration Task** on the data migration page.
(2) On the **Create Migration Task** page, select the types and regions of the source and target databases and click **Buy Now**.

>?Select the region with caution as it cannot be changed once the migration task is created.

### 2. Set the source and target databases
Enter the information of the task, source database, and target database.

#### Task settings
Enter the name of the migration task. If you want the migration task to be executed at a later time, you can set scheduled execution.
![](https://main.qcloudimg.com/raw/286fd5ccef05146bea9dd758d6634db5.png)

#### Source database settings
Enter the source database information and click **Test Connectivity** to check whether the source database can be connected.
![](https://main.qcloudimg.com/raw/dcf2c22d49e2c1e2a290f8bf79ed369f.png)

#### Target database settings
Enter the target database information and click **Save**.
![](https://main.qcloudimg.com/raw/58807df689398099800be9b2970ed03b.png)

### 3. Select the type and databases/tables
Select the type and database list and click **Next step: verify task**.
![](https://main.qcloudimg.com/raw/96ed794fa406ee0004ee3682ef3b0d5e.png)

### 4. Verify the task
Check whether the source instance runs normally and whether the sets to be migrated to the target instance are in conflicts.
![](https://main.qcloudimg.com/raw/204d55e7b3c700c4ed62419c879513c5.png)

### 5. Complete the migration
After the verification is passed, return to the migration task list. After the incremental sync is 90% complete, click **Done** on the right of the migration task.
![](https://main.qcloudimg.com/raw/120798d5f56bf2db4f68d6203939c718.png)
Complete the migration.
![](https://main.qcloudimg.com/raw/030ccd93878ef42e924f6fe5cd2b510e.png)

