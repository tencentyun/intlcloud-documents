You can recover data in TencentDB for MongoDB by following the steps below:
**Step 1:** In the backup recovery list, click **Rollback** for a backup file to go to the rollback page, where you can select the time point and type for the rollback. The rollback includes the entire instance rollback and the database table rollback. The specific operations are shown as below:
1. Click the **Instance Rollback** button:
![](https://main.qcloudimg.com/raw/f68d404c4b720bd04356485dae1bcd5a.png)
2. Select rollback time:
![](https://main.qcloudimg.com/raw/e8c3e96de22e7123cf5b79b8e5d87d9e.png)
3. Select rollback type:
![](https://main.qcloudimg.com/raw/72776d49399432f30726af3c93df069d.png)

**Step 2:** When you select **Entire Instance Rollback**, the system creates a temporary instance free of charge to store the rollback data. The user name and password of the temporary instance are the same as those of the original instance. The original instance remains unchanged and the business will not be affected.
**Step 3:** When you select **Database Table Rollback**, the system performs rollback in the original instance according to the database table selected, the name of the database table after rollback and the rollback time. You need to confirm the data after the completion of rollback.
**Step 4:** You need to access the temporary instance to confirm the rollback data within 48 hours after the completion of the entire instance rollback.
For the temporary instance generated in the rollback, you can perform any of the following:
1. Conversion: Convert the temporary instance to a formal business instance independent of the original instance.
2. Replacement: Replace the original instance with the temporary instance (bind the private IP of the original instance to the temporary instance). 
If no action is performed within 48 hours, the temporary instance will be terminated.
![](https://mc.qcloudimg.com/static/img/4729ddc8384362dfb9a601343e928807/huifu2.png)


>!
1. The oplog space of an instance is a capped collection. When the collection space is used up, new inserted elements will overwrite the initial head elements. To avoid backup and recovery failures caused by overwritten oplog space, set a reasonable oplog space size according to business details.
> 2. When a business involves frequent write, delete and update operations, you can schedule multiple backups per day to prevent the oplog between two backup time points from being overwritten.
> 3. If the oplog space between two backup time points is overwritten, the data recovery time may not be guaranteed.

