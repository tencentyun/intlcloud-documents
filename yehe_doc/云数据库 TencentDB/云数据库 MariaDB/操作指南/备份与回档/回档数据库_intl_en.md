## Rollback Description
TencentDB for MariaDB can roll back data to any time point in the last 30 days based on the retention of backups and logs. With the database rollback feature, system loss can be minimized.
The rollback feature of TencentDB for MariaDB does not affect a production instance and can directly roll back data to a temp instance created by Tencent Cloud, which supports read/write operations, so that you can modify the temp instance in a more flexible manner, such as clearing dirty data. After correcting the data in the temp instance, you can use "instance switch" to convert the temp instance to the production instance.

#### Limits
- In the process of rollback, temp instance creation, or instance switch, some management features of the production instance are unavailable. After the process is completed, such operations can be performed normally.
- The rollback operation may forcibly shard the binary logs (binlogs), i.e., a file with a size of smaller than 100 MB will also be backed up as a separate file.
- After rollback, the temp instance will inherit the parameters of the production instance such as account and database parameters, which cannot be modified.

## Instance Rollback
1. Log in to the [TencentDB for MariaDB Console](https://console.cloud.tencent.com/tdsql), click the instance name to enter the instance details page, and click **Rollback** in the top-right corner.
2. In the pop-up dialog box, set the rollback time and click **OK**.
![](https://main.qcloudimg.com/raw/5c48260e669c43c575fc9a2aaa526dd2.png)

## Temp Instance
A temp instance is an instance created by TencentDB for MariaDB based on backup and used for only temporary adjustment. It has the following features:
- It supports read/write operations.
- It is only valid for 48 hours and will be deleted after 48 hours.
- An instance has only one temp instance at a time.
- A temp instance can be deleted at any time.

After rollback, you can view the generated temp instance on the **Backup and Restore** > **Temp Instance** page.
![](https://main.qcloudimg.com/raw/2722e86dccf80680b6322de7e9cd21a2.png)

## Instance Switch
Instance switch refers to switching a temp instance to the production environment. You can switch the temp instance after confirming that the data rolled back is correct. The switch will change the private network links in the original and temp instances.
- The production instance may experience a 1-second disconnection during the switch process.
- After the switch, the temp instance will be replaced with the production instance and then deleted. 

You can click **Migrate temp instance to the network production environment** on the **Backup and Restore** > **Temp Instance** page.
![](https://main.qcloudimg.com/raw/3baf1f666025b87c8f4c3976ad4d18d0.png)

