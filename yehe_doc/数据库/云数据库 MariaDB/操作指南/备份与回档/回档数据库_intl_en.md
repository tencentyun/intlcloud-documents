
## Rollback description
TencentDB for MariaDB can roll back data to any time point in the last 30 days based on the retention of backups and logs. With the database rollback feature, system loss can be minimized.
This rollback feature doesn't affect a production instance and can directly roll back data to a newly created pay-as-you-go instance. The new rollback instance is a standard one that can be configured as needed.

#### Limits
- When a temp instance is being rolled back or created, some management features of the production instance are unavailable until the operation is completed.
- The binlogs may be forcibly sharded during the rollback operation, and files smaller than 100 MB in size will be backed up separately.
- The newly purchased instance after rollback will have the parameter information of the production instance (such as account and database parameters). Therefore, you must pay attention to account management.

## Instance rollback
1. Log in to the [TencentDB for MariaDB console](https://console.cloud.tencent.com/mariadb) and click an instance ID to enter the instance management page.
2. On the instance management page, select the **Backup and Restoration** > **Rollback Instance** tab and click **Create Rollback Instance**.
![](https://qcloudimg.tencent-cloud.cn/raw/67193b3ce2426449b8d790e89904fd50.png)
3. In the pop-up window, set the rollback time and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/5eb6c84e9f6bccdfef8d1b9fa9f4e4c4.png)
4. On the instance purchase page, adjust configuration based on your needs, click **Buy Now**, and wait for instance rollback to be completed.
5. After the rollback is completed, you can view the generated rollback instance on the **Backup and Restoration** > **Rollback Instance** page or in the instance list.

