## Operation Scenarios
This document describes how to migrate data from Alibaba Cloud ApsaraDB for RDS to TencentDB using DTS, Tencent Cloud's data migration tool.

## Environment Requirements
- ApsaraDB RDS for MySQL 5.6 or earlier.
- A TencentDB for MySQL 5.6 instance.
>During data transfer, the data replication method of TencentDB must be async replication, which can only be changed after data transfer is completed.

## Directions

### 1. Get the basic information and AccessKey of the source database 
1.1. Log in to the [RDS Console](https://account.aliyun.com/login/login.htm?oauth_callback=https%3A%2F%2Frdsnew.console.aliyun.com%2F%3Fspm%3Da2c4g.11186623.2.5.cdjgiR) and select a target instance.
1.2. You can obtain the necessary information on the target instance's basic information page as shown below:
![](https://main.qcloudimg.com/raw/e55af45a5c36a99097418808cc542389.png)
>The public network address provided by Alibaba Cloud needs to be converted into IP format. You can query IP/server addresses [here](http://ip.chinaz.com).
>
1.3. Hover over the profile photo in the top-right corner and select **accesskeys** in the drop-down menu to get the required Accesskey.
![](https://main.qcloudimg.com/raw/2d67bd05558d5762c322d0c33d344332.png)
	
### 2. Create a DTS task for TencentDB
Log in to the [DTS Console](https://console.cloud.tencent.com/dtsnew/migrate/page), go to the data migration page, click **Create Task**, and configure the task, source database, and target database on the page redirected to.


#### 2.1. Set the task
- Task Name: specify a name for the task.
- Scheduled Execution: specify the start time of the migration task.
![](https://main.qcloudimg.com/raw/66d467a7be88d995354ab9e17d2beb05.png)

#### 2.2. Enter the information of the source database
Select a connection type as needed and enter the connection information of the source database.
>You need to add the IP of your TencentDB instance to Alibaba Cloud's whitelist for IP mapping; otherwise, the connectivity test would fail.
>- For mapping a TencentDB for MySQL instance with a public IP, you need to add the public IP of the corresponding region to Alibaba Cloud's whitelist.
>- If the source database type is configured as "Direct Connect" or "VPN" during DTS configuration, an IP for external mapping will appear after the task is generated. You need to add it to Alibaba Cloud's whitelist.
>
![](https://main.qcloudimg.com/raw/643d71c704dfd69a3b4a6f1cb80c2858.png)

#### 2.3. Enter the information of the target database
Select TencentDB instance as target instance type and enter the link information of the target instance.
![](https://main.qcloudimg.com/raw/883eb101608f68fa886d020c2b55b81d.png)

#### 2.4. Select the database to be migrated
Select the database to be migrated, create a migration task information, and check the task information.
![](https://main.qcloudimg.com/raw/5a384d22e7ee47744814a83a99c8f8a4.png)
#### 2.5. Perform data consistency check
Select a data consistency check type as needed (e.g., full check or no check).
>The check ratio fields are required if spot check is selected.
>
![](https://main.qcloudimg.com/raw/a9e2b8ed5c722602104a0ace1fb9b0ef.png)

#### 2.6. Check the migration task information
After the migration task is created, you need to click **Next: Check Task** to verify the task information. You cannot start the migration task until all the check items are passed.
 There are 3 statuses for task check:
 - Passed: The check is fully successful.
 - Warning: The check fails. Database operation may be affected during or after data migration, but the migration task can still be executed.
 - Failed: The check fails and the migration task cannot be executed. In this case, please check and modify the migration task information according to the error and then check the task again.
![](https://main.qcloudimg.com/raw/0b8c1c1cf54b071205acb9b36578773f.png)

### 3. Start migration
>Due to system design limitations, multiple migration tasks submitted or queued at the same time will be performed in sequence by queuing time.
>
After the check is passed, you can click **Start** to start data migration. Please note that if you have configured scheduled execution, the migration task will begin queuing and be executed at the specified time; otherwise, it will be executed immediately.
After the migration is started, you can view the corresponding migration progress under the migration task. The subsequent steps required for migration and the current stage will be displayed if you hover over the exclamation mark after the current step.
>If an error occurs: "errMsg": "Failed to start backup task. SDK.ServerUnreachable Unable to connect server:HTTP Error 403: Forbidden":
>You can troubleshoot the problem in the following steps:
>- Check whether your Alibaba Cloud key has permission to initiate cold backup on the ApsaraDB for RDS instance. If an Alibaba Cloud root account is used, which has all permissions, this cause can be ruled out.
>- Log in to the Alibaba Cloud Console, check whether the ApsaraDB for RDS instance is executing a conflicting task such as cold backup or upgrading; if automatic backup is enabled, you need to disable it.
>- If the problem persists after the above two steps, please contact Alibaba Cloud to find out the cause of failure in initiating a cold backup task with an [API](https://help.aliyun.com/document_detail/26272.html?spm=a2c4g.11186623.6.916.voEDSM).  

### 4. Cancel migration
To cancel an in-progress migration task, click **Cancel**.
![](https://main.qcloudimg.com/raw/9d9cf9edda859dfd44007be0d4313986.png)

### 5. Disconnect the migration task
- Make sure that there are no writes into the ApsaraDB for RDS instance at the business side. You can change the account password for business connection or adjust the permission granted to the account, while ensuring that the account used for DTS sync allows reads and writes.
- Stop business connection to ApsaraDB for RDS and run the `show processlist` command to confirm that there is no business connection.
- Run the `show master status` command to get the latest GTID of ApsaraDB for RDS and compare it with that of TencentDB obtained via `show slave status`, so as to ensure that there is no synchronization delay between TencentDB and ApsaraDB for RDS instances.
- Check whether your original ApsaraDB for RDS account can be used to log in to TencentDB; if not, try to escalate it to a privileged account in the following steps:
   While the DTS task continues syncing, add a privileged account on ApsaraDB for RDS (the password encryption method can be changed to general encryption), which will be synced to TencentDB via DTS.
- You can use the console (as shown below) or extract core table contents to check data consistency.
![](https://main.qcloudimg.com/raw/19123fc859e7ddca13cd465a0cc30077.png)
- Run the `show slave status` command to record the sync time point of TencentDB.


### 6. Complete migration
After the migration is 100% complete, you can click **Complete** on the right. You can also call the DTS [TencentCloud API](https://cloud.tencent.com/document/product/571/18122) to stop the sync.
![](https://main.qcloudimg.com/raw/6485672d5cf6feb6a4faeecb4e072c00.png)
>If the migration is in **uncompleted** status, the migration task will continue, so will data sync.

### 7. Restart your business application
Disable the read-only feature of TencentDB, restart the application, and observe the status of TencentDB to make sure that it is running normally. 


