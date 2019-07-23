## Scenario
TencentDB for SQL Server supports migrating data from an SQL Server database created by an CVM instance to a TencentDB for SQL Server instance. This document describes how to configure and run a migration task.
>!
>- Before migration, make sure that the destination instance SQL Server edition is not simpler than that of the source instance.
>- For the bak files used for migration, please make sure that each bak file contains only one database.
>- The name of the migrated database cannot be the same as that of the TencentDB for SQL Server instance.**

## Directions
### Creating a Migration Task
1. Log in to the [TencentDB for SQL Server Console](https://console.cloud.tencent.com/sqlserver) and select **Data Transfer** in the left sidebar.
2. Click **Create Task**, enter the task name, source database information, and destination database information, and select **SQL Server instance created by CVM** as the source instance type.
![](https://main.qcloudimg.com/raw/da77fa7fe6ed5dc4c493861d1850ee3d.png)
3. After clicking **Next**, you need to [configure the source SQL Server instance](https://cloud.tencent.com/document/product/238/32585#.E9.85.8D.E7.BD.AE.E6.BA.90-sql-server-.E5.AE.9E.E4.BE.8B) first and then [configure the migration task](https://cloud.tencent.com/document/product/238/32585#.E9.85.8D.E7.BD.AE.E8.BF.81.E7.A7.BB.E4.BB.BB.E5.8A.A1).
>? If the error message "Source instance info checking failed!" is prompted, please check the following items for troubleshooting:
>- Whether the sa account of the source SQL Server instance exists.
>- Whether the sa account password of the source SQL Server instance is correct.
>- Whether the IP and port of the source SQL Server instance work properly.

### Configuring the Source SQL Server Instance
1. Enable the sa account for the source SQL Server instance.
2. Select **Allow remote connections to this server** in **Connections** and set a reasonable remote query timeout.
![](https://main.qcloudimg.com/raw/5f0cec5032756cbf39c3260447746781.png)
3. Select **SQL Server and Windows Authentication mode** in **Security**.
![](https://main.qcloudimg.com/raw/8665101c74549911a0e6ee8e90850151.png)
4. Enable TCP/IP.
![](https://main.qcloudimg.com/raw/21b80c7353bf17fc2d867cc70b2a6f8c.png)
5. Enable the built-in account and select **localsystem**.
![](https://main.qcloudimg.com/raw/5b929ede440766e2913f4e96a448acb6.png)
6. Allow SQL Server port communication and open port 445 (for a basic network) or 49001 (for a private network) in Windows Firewall.
7. (Optional) If **VPC** is selected as the **CVM network**, you need to configure the freeSSHd tool.
 1. Download and install [freeSSHd](http://www.freesshd.com/freeSSHd.exe) with the default options, and agree to start the freeSSHd service.
 2. Double-click the freeSSHd icon on the desktop. Then, right-click the freeSSHd icon in the taskbar to open the Settings page for configuration.
 3. Select the **SSH** tab and set the port to 49001 (the default port here is 22, which should be changed to 49001). ![](https://main.qcloudimg.com/raw/72d8780b85afa18524dc2fb81bcd6baf.png)
 4. Select the **Server status** tab and start the SSH server.
 5. Select the **Authentication** tab and select **Allowed** for password authentication.
 6. Select the **Users** tab and enter the user tencent_vpc_migrate (this username cannot be changed) and the password tencent_vpc_migrate (this password cannot be changed) as shown below:
 ![](https://main.qcloudimg.com/raw/9d8658d6f44517e7554c3416780f0a58.png)
 7. Use D:\dbbackup\ (**this path cannot be changed**) as the backup folder used during SQL Server migration. Select the **SFTP** tab and configure this path as the "SFTP home path".

### Configuring the Migration Task
Select the migration type, set the database (by selecting the database tables to be migrated), and click **Save and Verify**. If the verification fails, you can troubleshoot as prompted.
![](https://main.qcloudimg.com/raw/6ea9a3c3c3496a3c3782037e0e988ff3.png)

### Starting the Migration Task
After the task is created, return to the task list. At this time, the task status is **initializing**. Select the task and click **Start** to sync the task.

### Completing the Migration Task
After the data synchronization is completed (i.e., the progress bar shows 100%), you need to click **Finish** to end the synchronization process. If you selected **Incremental Synchronization** when configuring the migration task, you need to click **Finish** when the progress bar shows 99%. You can check whether the migration is successful based on the **status**.
 - If the task status is **task succeeded*, the data migration is successful.
 - If the status is **task failed*, the migration failed. Please check the failure information, fix it accordingly, and then re-migrate.
