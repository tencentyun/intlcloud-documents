
### How do I import a local SQL file into a TencentDB for MySQL instance?
>?Only two-node and three-node TencentDB for MySQL instances support importing SQL files.
>
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) and click an instance ID to enter the management page.
2. Select **Database Management** > **Database List** > **Import Data**. Select the file to be imported and the target database and click **OK** to import the data.
>?A single SQL file to be imported cannot exceed 2 GB. The filename can only contain letters, digits, and underscores.
>
![](https://main.qcloudimg.com/raw/a8854e74caebb9c69d831dc1583c10c0.png)
For more information, please see [Importing SQL Files](https://intl.cloud.tencent.com/document/product/236/8466).

### How do I export data from a database?
- To export backup data, click an instance ID in the [console](https://console.cloud.tencent.com/cdb) to enter the management page and select the **Backup and Restore** tab for download.
- To export real-time data, you can purchase a [read-only replica](https://intl.cloud.tencent.com/document/product/236/7270), connect to it, and then use mysqldump to get real-time data.

### What is the fastest way to migrate a 7 GB database to a TencentDB for MySQL instance?
We recommend that you connect the database to be migrated using the [data migration](https://intl.cloud.tencent.com/zh/document/product/571/34103) feature for data sync.

