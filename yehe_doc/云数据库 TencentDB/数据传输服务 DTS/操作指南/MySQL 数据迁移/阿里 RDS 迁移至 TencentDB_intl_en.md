This document describes how to migrate data from Alibaba Cloud ApsaraDB for RDS to TencentDB using DTS, Tencent Cloud's data migration tool.

## Environment Requirements
ApsaraDB RDS for MySQL 5.6 or 5.7.
>!During data transfer, the data replication method of TencentDB must be async replication, which can only be changed after data transfer is completed.

## Obtaining the Basic Information and AccessKey of the Source Database 
1. Log in to the [RDS console](https://account.aliyun.com/login/login.htm?oauth_callback=https%3A%2F%2Frdsnew.console.aliyun.com%2F%3Fspm%3Da2c4g.11186623.2.5.cdjgiR) and select a target instance.
2. You can obtain the necessary information on the target instance's basic information page as shown below:
![](https://main.qcloudimg.com/raw/d20077e3364fc3fa692c4e67b6760f5b.png)
>!The public network address provided by Alibaba Cloud needs to be converted into IP format. You can query IP/server addresses [here](http://ip.chinaz.com).
>
3. Hover over the profile photo in the top-right corner and select **accesskeys** in the drop-down menu to get the required Accesskey.
![](https://main.qcloudimg.com/raw/916987de380ebce2919fae56eb19936b.png)
## Creating a DTS Task for TencentDB
### 1. Creating a migration task
1) Log in to the [DTS console](https://console.cloud.tencent.com/dts) and click **Create Migration Task** on the data migration page.
2) Select the corresponding region in **Linkage Region** and click **Buy at 0 USD**.

### 2. Configuring the migration task
Configure the task, source database, and target database. After the network connectivity test is successful, click **Create**.

#### a. Task settings
- Task name: specify a name for the task.
- Scheduled Execution: specify the start time of the migration task.

<span id="ykxx" ></span>
#### b. Source database information
Select a connection type as needed, enter the connection information of the source database, and click **Test Connectivity**.
>!
>- You need to add the IP of your TencentDB instance to Alibaba Cloud's allowlist for IP mapping; otherwise, the connectivity test would fail.
>  - For mapping a TencentDB for MySQL instance with a public IP, you need to add the public IP of the corresponding region to Alibaba Cloud's allowlist.
>  -  If the source database type is configured as "Direct Connect" or "VPN" during DTS configuration, an IP for external mapping will appear after the task is generated. You need to add it to Alibaba Cloud's allowlist.
> 
>- You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to query the DTS IP allowlist of corresponding region, or click **Test Connectivity**, and the DTS IP allowlist will be displayed in the detection result when the connectivity test fails.
>
![](https://main.qcloudimg.com/raw/643d71c704dfd69a3b4a6f1cb80c2858.png)

#### c. Target database information
Select TencentDB instance as target instance type and enter the link information of the target instance.
![](https://main.qcloudimg.com/raw/883eb101608f68fa886d020c2b55b81d.png)

### 3. Select the database to migrate
Select the database to migrate, create a migration task information, and check the task information.
![](https://main.qcloudimg.com/raw/5a384d22e7ee47744814a83a99c8f8a4.png)

### 4. Performing data consistency check
Select a data consistency check type as needed (e.g., full check or no check).
>!The detection ratio fields are required if sampling detection is selected.
>
![](https://main.qcloudimg.com/raw/a9e2b8ed5c722602104a0ace1fb9b0ef.png)

### 5. Checking the migration task information
After the migration task is created, you need to click **Next: Check Task** to verify the task information. You cannot start the migration task until all the check items are passed.
 There are 3 statuses for task check:

 - Passed: the check is fully successful.
 - Warning: the check fails. Database operation may be affected during or after data migration, but the migration task can still be executed.
 - Failed: the check fails and the migration task cannot be executed. In this case, please check and modify the migration task information according to the error and then check the task again.
![](https://main.qcloudimg.com/raw/0b8c1c1cf54b071205acb9b36578773f.png)

### 6. Starting migration
>!Due to system design limitations, multiple migration tasks submitted or queued at the same time will be performed in sequence by queuing time.
>
After the check is passed, you can click **Start** to start data migration. Please note that if you have configured scheduled execution, the migration task will begin queuing and be executed at the specified time; otherwise, it will be executed immediately.
After the migration is started, you can view the corresponding migration progress under the migration task. The subsequent steps required for migration and the current stage will be displayed if you hover over the exclamation mark after the current step.
>?If an error occurs: "errMsg": "Failed to start backup task. SDK.ServerUnreachable Unable to connect server:HTTP Error 403: Forbidden":
>You can troubleshoot the problem in the following steps:
>- Check whether your Alibaba Cloud key has permission to initiate cold backup on the ApsaraDB for RDS instance. If an Alibaba Cloud root account is used, which has all permissions, this cause can be ruled out.
>- Log in to the Alibaba Cloud Console, check whether the ApsaraDB for RDS instance is executing a conflicting task such as cold backup or upgrading; if automatic backup is enabled, you need to disable it.
>- If the problem persists after the above two steps, please contact Alibaba Cloud to find out the cause of failure in initiating a cold backup task with an [API](https://help.aliyun.com/document_detail/26272.html?spm=a2c4g.11186623.6.916.voEDSM).  

### 7. Canceling migration (optional)
To cancel an in-progress migration task, click **Cancel**.
![](https://main.qcloudimg.com/raw/9d9cf9edda859dfd44007be0d4313986.png)

### 8. Disconnecting the migration task
- Make sure that there are no writes into the ApsaraDB for RDS instance at the business side. You can change the account password for business connection or adjust the permission granted to the account, while ensuring that the account used for DTS sync allows reads and writes.
- Stop business connection to ApsaraDB for RDS and run the `show processlist` command to confirm that there is no business connection.
- Run the `show master status` command to get the latest GTID of ApsaraDB for RDS and compare it with that of TencentDB obtained via `show slave status`, so as to ensure that there is no synchronization delay between TencentDB and ApsaraDB for RDS instances.
- Check whether your original ApsaraDB for RDS account can be used to log in to TencentDB; if not, try to escalate it to a privileged account in the following steps:
   While the DTS task continues syncing, add a privileged account on ApsaraDB for RDS (the password encryption method can be changed to general encryption), which will be synced to TencentDB via DTS.
- You can use the console (as shown below) or extract core table contents to check data consistency.
![](https://main.qcloudimg.com/raw/19123fc859e7ddca13cd465a0cc30077.png)
- Run the `show slave status` command to record the sync time point of TencentDB.


### 9. Completing the migration
After the migration is 100% complete, you can click **Complete** on the right. You can also call the DTS [TencentCloud API](https://cloud.tencent.com/document/product/571/18122) to stop the sync.
![](https://main.qcloudimg.com/raw/6485672d5cf6feb6a4faeecb4e072c00.png)

>!If the migration is in **uncompleted** status, the migration task will continue, so will data sync.

### 10. Restarting your business application
Disable the read-only feature of TencentDB, restart the application, and observe the status of TencentDB to make sure that it is running normally. 
