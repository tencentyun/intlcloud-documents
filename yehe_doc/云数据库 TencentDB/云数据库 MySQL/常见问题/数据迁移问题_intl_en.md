### How do I import a local SQL file into a TencentDB for MySQL instance?
>High-Availability Edition and Finance Edition of TencentDB for MySQL instances support operation logs management.
>
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb) and click an instance name to enter the management page.
2. Select **Database Management** > **Database List** > **Data Importing**. Select the file to import and the target database and click **Import** to import the data.
>A single SQL file to be imported cannot exceed 2 GB. The filename can only contain letters, digits, and underscores.
>
![](https://main.qcloudimg.com/raw/a8854e74caebb9c69d831dc1583c10c0.png)

### How do I export data from a database?
- To export backup data, click an instance name in the [console](https://console.cloud.tencent.com/cdb) to enter the management page and select the **Backup and Restore** tab for download.
- To export real-time data, purchase a [read-only instance](https://intl.cloud.tencent.com/document/product/236/7270), connect to it, and use mysqldump to get the real-time data.

### What is the fastest way to migrate a 7 GB database to a TencentDB for MySQL instance?
We recommend that you use the [data migration](https://intl.cloud.tencent.com/document/product/571/34103) feature to directly connect your source database for data sync.

### How do I sync real-time data in two instances with an intra-city active-active solution?
You can purchase [disaster recovery instances](https://intl.cloud.tencent.com/document/product/236/7272) in the console.


