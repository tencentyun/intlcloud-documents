
### 1. Creating a migration task
1) Log in to the [DTS console](https://console.cloud.tencent.com/dts) and click **Create Migration Task** on the data migration page.
2) Select the corresponding region in **Linkage Region** and click **Buy at 0 CNY**.
>?Please select the region with caution as it cannot be changed once the migration task is created.

### 2. Setting the source and target instances
Enter relevant information to set the task, source database, and target database.

#### Task setting
Enter the name of the migration task. If you want the migration task to be executed at a later time, you can set scheduled execution.
![](https://main.qcloudimg.com/raw/f5b1a534bd8253e35a0e0f5eec24777b.png)

#### Source database setting
Enter the information of the source database and then click **Test Connectivity** to check whether your source database is connected.
![](https://main.qcloudimg.com/raw/4a7070511fbde9cf4a5a207b6c1ee54e.png)

#### Target database setting
Enter the information of the target database and click **Save**.
![](https://main.qcloudimg.com/raw/93270ca13f74cac2f86012fd9df46549.png)

### 3. Selecting type and table
Select the type and table list and click **Next step: verify task**.
![](https://main.qcloudimg.com/raw/d9cda12bdba712013197a2434b7b0562.png)

### 4. Checking the task
Check whether the source instance runs normally and whether the sets to be migrated to the target instance are in conflicts.
![](https://main.qcloudimg.com/raw/ff67c3ca23243c5759ec78ab061f6411.png)

### 5. Completing migration
After the check is passed, return to the migration task list. After the incremental sync is 90% complete, click **Complete** on the right of the migration task.
![](https://main.qcloudimg.com/raw/2770041ad6f24bfe70a8ae64ee1ca30e.png)
The migration task is completed.
![](https://main.qcloudimg.com/raw/32ba2bfc5a3006da69893f784b9ea2b7.png)

