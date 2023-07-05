## Overview
TencentDB for MySQL supports importing SQL files via the console, allowing you to execute SQL statements in the selected database. You can also use this feature to create databases/tables and change table structures to initialize or modify the instance.
>?Only two-node and three-node TencentDB for MySQL instances support importing SQL files.

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance management page.
2. On the instance management page, select **Database Management** > **Database List** and click **Data Import**.
![](https://qcloudimg.tencent-cloud.cn/raw/eb01b7c4ff2ad548955f54d0a17971e7.png)
3. In the pop-up window, click **Add File** to import the file. After the upload is completed, click **Next**.
>?
>- To avoid database unavailability caused by corruption of system tables, do not import data from system tables such as the `mysql.user` table. 
>- Only incremental import is supported. Clear any obsolete data in the database before importing.
>- You can import an unencrypted .zip file. The unzipped files must be .sql files with a total size of no more than 5 GB.
>- A single file should not exceed 10 GB (if it is zipped, the file should not exceed 5 GB after being unzipped), and the file name can contain only letters, digits, and underscores.
>- Uploaded files are valid for 14 days and will be automatically deleted after expiration.
>
![](https://main.qcloudimg.com/raw/fd6c70707a8722ca64a87f71978e2a2a.png)
4. On the **Select the target database** page, select the target database and click **Next**.
5. On the confirmation page, confirm that the imported data is correct, enter the account password, and click **Import**.
>!
>- The import cannot be rolled back. Confirm the import information before proceeding.
>- If you forgot the password, reset it as instructed in [Resetting Password](https://www.tencentcloud.com/document/product/236/31901).
> 
![](https://main.qcloudimg.com/raw/e21ccbe6c1f0a95cd46b4387fea1fab1.png)

