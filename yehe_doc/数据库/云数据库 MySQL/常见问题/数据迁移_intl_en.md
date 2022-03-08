
### How do I import a local SQL file into a TencentDB for MySQL instance?
>?Only two-node and three-node TencentDB for MySQL instances support importing SQL files.
>
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) and click an instance ID to enter the management page.
2. Select **Database Management** > **Database List** > **Import Data**. Select the file to be imported and the target database and click **Next** to import the data.
>?
>- To avoid database unavailability caused by corruption of system tables, do not import data from system tables such as the `mysql.user` table. 
>- Only incremental import is supported. If there is obsolete data in the database, clear the data before the importing operation.
>- A single file does not exceed 10 GB. The file name only allows letters, numbers, and underscores.
>
![](https://qcloudimg.tencent-cloud.cn/raw/8475a29058e3b8e16e04a2548b85fb60.png)
For more information, see [Importing SQL Files](https://intl.cloud.tencent.com/document/product/236/8466).

### How do I export data from a database?
- To export backup data, click an instance ID in the [console](https://console.cloud.tencent.com/cdb) to enter the management page and select the **Backup and Restoration** tab for download.
- To export real-time data, you can purchase a [read-only instance](https://intl.cloud.tencent.com/document/product/236/7270), connect to it, and then use mysqldump to get real-time data.

### What is the fastest way to migrate a 7 GB database to a TencentDB for MySQL instance?
We recommend that you connect the database to be migrated using the [data migration](https://intl.cloud.tencent.com/zh/document/product/571/34103) feature for data sync.

### How do I sync real-time data in two instances with an intra-city active-active solution?
You can purchase [disaster recovery instances](https://intl.cloud.tencent.com/document/product/236/7272) in the console.

