TencentDB for SQL Server now supports data migration using COS files. Te specific steps are as follows:

### 1. Upload the backup file to COS
If a bucket has already been created, you can skip steps 1.1 and 1.2.
1.1. Log in to the [Tencent Cloud Console](https://cloud.tencent.com/login?s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2F), click **Products** > **Cloud Object Storage** in the upper right corner of the page;
![](https://main.qcloudimg.com/raw/062794e8beff4e38f47d9f875ae14874.png)
1.2. Select **Bucket List** and click **Create bucket** in the upper left corner of the page;
![](https://main.qcloudimg.com/raw/a28c4a31de1c406b8f154ae11a024530.png)
![](https://main.qcloudimg.com/raw/183b14813cf347f2c53fd8842b014e61.png)
>Note 1: The region of the bucket needs to be the same of the SQL Server instance to migrate to.
Cross-region migration with COS is not supported.

1.3. Click **Select bucket** > **Upload file** > **File information**;
![](https://main.qcloudimg.com/raw/968885446c9b7752c833ac166e5f8713.png)
![](https://main.qcloudimg.com/raw/59032f360cf78fd670a6acfc1dceffd0.png)
Get the **source file link**;

### 2. Restore the backup from the COS source file link
2.1. Log in to the [Tencent Cloud Console](https://cloud.tencent.com/login?s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2F), click **Products** > **Relational Database** in the upper left corner of the page, click **SQL Server** > **Data Transfer** in the left navigation bar, and then click **Create Task** in the upper left corner of the page.
![](https://main.qcloudimg.com/raw/a42addc7282971bd635cc293d9be8086.png)
![](https://main.qcloudimg.com/raw/bbf3e56be9709c6cc423218fe6e90e07.png)
2.2. Create a task and click **Next**;
![](https://main.qcloudimg.com/raw/daef0287956bf1fe61ae8a869092f2f7.png)
>Note 2: The **COS source file link** is the one obtained in step 1. Please note that the region must be the same as the region of the COS source file link.
Note 3: Select the destination instance ID. (You can only select an instance in the same region.)

2.3. Migration with COS currently does not support type selection and database settings. Click **Create Task** > **Start** in the lower right corner;
![](https://main.qcloudimg.com/raw/0d6fd452e28c76b5a18ca67ab3293e41.png)
You can view the created migration task in the data transfer list.
![](https://main.qcloudimg.com/raw/e95aed63e9143b3af10231f760dda419.png)
Click **Start** to start the migration task and wait for it to complete.

### FAQs
1. The backup file must contain only one database and be resolvable.
2. The version of the backup instance must be lower than or the same as the destination instance. For example, migrating from a SQL Server 2012 instance to a SQL Server 2008 instance is not supported.
3. Confirm that there is no database with the same name in the destination SQL Server instance; otherwise, the migration will fail.
