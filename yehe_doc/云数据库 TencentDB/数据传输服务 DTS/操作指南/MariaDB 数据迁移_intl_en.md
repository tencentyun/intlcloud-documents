
### 1. Creating a migration task
1) Log in to the [DTS console](https://console.cloud.tencent.com/dts) and click **Create Migration Task** on the data migration page.
2) Select the corresponding region in **Linkage Region** and click **Buy at 0 CNY**.
>?Please select the region with caution as it cannot be changed once the migration task is created.

### 2. Setting the source and target instances
Enter relevant information to set the task, source database, and target database.

#### Task setting
Enter the name of the migration task. If you want the migration task to be executed at a later time, you can set scheduled execution.
![](https://main.qcloudimg.com/raw/286fd5ccef05146bea9dd758d6634db5.png)

#### Source database setting
Enter the information of the source database and then click **Test Connectivity** to check whether your source database is connected.
![](https://main.qcloudimg.com/raw/dcf2c22d49e2c1e2a290f8bf79ed369f.png)

#### Target database setting
Enter the information of the target database and click **Save**.
![](https://main.qcloudimg.com/raw/58807df689398099800be9b2970ed03b.png)

### 3. Selecting type and table
Select the type and table list and click **Next step: verify task**.
![](https://main.qcloudimg.com/raw/96ed794fa406ee0004ee3682ef3b0d5e.png)

### 4. Checking the task
Check whether the source instance runs normally and whether the sets to be migrated to the target instance are in conflicts.
![](https://main.qcloudimg.com/raw/204d55e7b3c700c4ed62419c879513c5.png)

### 5. Completing migration
After the check is passed, return to the migration task list. After the incremental sync is 90% complete, click **Complete** on the right of the migration task.
![](https://main.qcloudimg.com/raw/120798d5f56bf2db4f68d6203939c718.png)
The migration task is completed.
![](https://main.qcloudimg.com/raw/030ccd93878ef42e924f6fe5cd2b510e.png)

