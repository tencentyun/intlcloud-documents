You can recover the data in TencentDB for MongoDB by following the steps below。

**Step 1:** In the backup recovery list, click **Rollback** for any backup file to open the rollback page, where you can specify the time and type of the rollback (instance rollback and table rollback). See below figure for details.

1. Click the **Instance Rollback** button:
![](https://main.qcloudimg.com/raw/b211048c4e8d23bd0f0ebea8c0c6d5f7.png)
2. Select rollback time:
![](https://main.qcloudimg.com/raw/c5dfb5d5a304a3fe67e2cc90322579b8.png)
3. Select rollback type:
![](https://main.qcloudimg.com/raw/f5d1d0fb2b5e73375fcd7ec0c4fcdd57.png)

**Step 2:** When you select **Instance Rollback**, the system creates a temporary instance free of charge to store the rollback data. The user name and password of the temporary instance are the same as those of the original instance. The original instance remains unchanged and the business will not be affected.

**Step 3:** When you select **Table Rollback**, the system performs rollback in the original instance according to the database table selected and the name of the rolled-back table and the rollback time. You’ll need to confirm that the rolled-back data is correct after the table rollback finishes.

**Step 4:** You’ll need to access the temporary instance to confirm the rolled-back data is correct within 48 hours after the instance rollback is completed.

For the temporary instance created for the rollback, you can perform:
1. Conversion: Convert the temporary instance to a formal business instance independent of the original instance.
2. Replacement: Replace the original instance with the temporary instance (bind the private IP of the original instance to the temporary instance). 
If no action is performed within 48 hours, the temporary instance will be terminated.
![](https://main.qcloudimg.com/raw/58520ca0f49c7959b22f4e616b0e09a8.png)



>1. The oplog space of an instance is a capped collection. When the collection space is used up, new inserted elements will overwrite the initial head elements. To avoid backup and recovery failures caused by overwritten oplog space, set a reasonable oplog space size.
> 2. When you frequently write, delete or update the data in the instance, you can schedule multiple backups per day to prevent the oplog from being overwritten during the gap time between two backup.
> 3. If the oplog space is overwritten during the gap time between two backup, the data recovery time may not be guaranteed.

