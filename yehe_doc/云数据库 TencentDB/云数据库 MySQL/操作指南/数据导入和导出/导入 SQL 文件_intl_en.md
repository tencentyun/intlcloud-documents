## Operation Scenarios
TencentDB for MySQL supports importing SQL files in the console. This feature allows you to execute SQL statements in the selected database. You can also use this feature to create databases/tables and change table structure so as to initialize or modify the instance.

## Directions
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance name or **Manage** in the "Operation" column to enter the instance management page.
2. Select **Manage Database** > **Database List** and click **Data Import**.
![](https://main.qcloudimg.com/raw/a8854e74caebb9c69d831dc1583c10c0.png)
3. On the pop-up page, click **Add File** to import the file. After the upload is completed, click **Next**.
>
>- To avoid database unavailability caused by corruption of system tables, please do not import data from system tables such as the `mysql.user` table. 
>- Only incremental data import is supported. If there is obsolete data in the database, clear the data first before the import operation.
>- A single file should be no more than 2 GB in size. The filename can only contain letters, digits, and underscores.
>
![](https://main.qcloudimg.com/raw/fd6c70707a8722ca64a87f71978e2a2a.png)
4. On the target database selection page, select the target database and click **Next**.
5. On the confirmation page, after confirming that the imported data is correct, enter the account password and click **Import**.
>The import operation cannot be rolled back. Please confirm the import information.
>
![](https://main.qcloudimg.com/raw/e21ccbe6c1f0a95cd46b4387fea1fab1.png)

