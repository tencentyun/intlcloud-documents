### How to import a local SQL file to a TencentDB for MySQL instance?
Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb), click the instance name to enter the management page, and select **Database Management** > **Database List** > **Import Data**. Select the file to be imported and the target database and click **OK** to import the data.
>A single SQL file to be imported should be no more than 2 GB in size. The filename can only contain letters, digits, and underscores.

### How to export data from a database?
- To export cold backup data, download it by clicking **Backup and Restore** on the instance management page in the console.
- To export real-time data, purchase a read-only instance and get the data by running the mysqldump client.

### What is the fastest way to migrate a 7 GB database to my purchased TencentDB for MySQL instance?
You are recommended to directly connect your source database using the [data migration](http://intl.cloud.tencent.com/document/product/571/13706) feature for data sync.

### How to achieve sync of real-time data in two instances in a local dual-backup architecture?
For this purpose, you can purchase [disaster recovery instances](https://intl.cloud.tencent.com/document/product/236/7272) in the console.


