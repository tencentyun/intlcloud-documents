## Creating a Migration Task
1. Log in to the [DTS Console](https://console.cloud.tencent.com/dtsnew/migrate/page) and click **Create Task** in the data migration list to create a migration task.
2. Select the linkage region, i.e., the region where the target instance resides.
>
>- Currently, MongoDB database migration is free of charge.
>- Please select the region with caution as it cannot be changed once the migration task is created.

### 1. Set the source and target databases
Enter relevant information to set the task, source database, and target database.

#### Set the task
Enter the name of the migration task. If you want it to be executed at a later time, you can set scheduled execution.
- Task Name: Specify a name for the task.
- Scheduled Execution: Specify the start time of the migration task.
>
> - To modify the scheduled task, you must click **Scheduled Start** again after the check is passed, so as to make the task start at the specified time.
> - If the specified time has passed, the task will start immediately. You can also click **Start Now** to start the task immediately.
> 

#### Set the source database
Enter the information of the source database and then click **Check Connectivity** to check whether your source database is connected.
![](https://main.qcloudimg.com/raw/e8b4cf534fd22df74a873f66bb40fa9d.png)

#### Set the target database
Enter the information of the target database and click **Save**.
![](https://main.qcloudimg.com/raw/97b9c26ab5438c470fee83b86c43f7bc.png)

### 2. Select the type and database list
Select the type and object and click **Next: Check Task**.
![](https://main.qcloudimg.com/raw/84e8f7bc56bd3805dbc5e21a8a182dd6.png)

### 3. Check the task
Check whether the source instance runs normally and whether the sets to be migrated to the target instance are in conflicts.
![](https://main.qcloudimg.com/raw/ec09ca0a336064f5bff7f4bfa10af950.png)

## Completing the Migration Task
After the check is passed, return to the data migration list. After the incremental sync is 100% complete, click **Complete** in the "Operation" column to finish the migration task.
![](https://main.qcloudimg.com/raw/c78832f8f369c9f8fb311c1ea5790f9a.png)
