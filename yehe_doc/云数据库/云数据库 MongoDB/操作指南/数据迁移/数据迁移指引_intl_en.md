## Creating Migration Task
1. Log in to the [DTS Console](https://console.cloud.tencent.com/dtsnew/migrate/page) and click **Create Task** in the data migration list to create a migration task.
2. Select the linkage region, i.e., the region where the target instance resides.
>
>- Currently, MongoDB database migration is free of charge.
>- Please select the region with caution as it cannot be changed once the migration task is created.

### 1. Set the source and target databases
Enter relevant information to set the task, source database, and target database.

#### Task configuration
Enter the name of the migration task. If you want the migration task to be executed at a later time, you can set scheduled execution.
- Task Name: specify a name for the task.
- Scheduled Execution: specify the start time of the migration task.
>
> - To modify the scheduled task, you must click **Scheduled Start** again after verification is passed so as to make the task start at the specified time.
> - If the specified time has passed, the task will start immediately. You can also click **Start Now** to start the task immediately.
> 

#### Set the source database
Enter the information of the source database and then click **Test Connectivity** to check whether your source database is connected.
![](https://main.qcloudimg.com/raw/5418854efa1cab777d217451f5fed550.png)

#### Set the target database
Enter the information of the target database and click **Save**.
![](https://main.qcloudimg.com/raw/d789a0f2053b815f002a289bb3d845e3.png)

### 2. Select the type and database list
Select the type and object and click **Next step: verify task**.
>If the selected object is the specified database or table, only the entire database migration is supported.
>
![](https://main.qcloudimg.com/raw/a5dc2558be5db94f5121526e1690d72f.png)

### 3. Verify the task
Check whether the source instance runs normally and whether the sets to be migrated to the target instance are in conflicts.

## Completing Migration Task
After the verification is passed, return to the data migration list. After the incremental sync is 100% complete, click **Complete** in the "Operation" column to finish the migration task.
