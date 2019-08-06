## Scenario
TencentDB for SQL Server supports data migration using COS files, which helps you migrate from Alibaba Cloud or a self-built SQL Server instance to TencentDB for SQL Server.
>- Before migration, make sure that the destination instance SQL Server edition is not simpler than that of the source instance.
>- For bak files used for migration, make sure each bak file contains only one database.
>- The name of the migrated database cannot be the same as that of the TencentDB for SQL Server instance.**

## Directions
### Uploading the Backup File to COS
1. Log in to the [Tencent Cloud Console](https://intl.cloud.tencent.com/login?s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2F) and select **Products** > **Cloud Object Storage** in the top-left corner of the page to enter the COS Console. Or, log in to the [COS Console](https://console.cloud.tencent.com/cos5) directly.
2. Select **Bucket List** and click **Create a Bucket**.
3. In the creation page that pops up, enter the relevant information and click **OK**.
 - The region of the bucket needs to be the same as that of the SQL Server instance to migrate to.
 - Cross-region migration with COS is not supported.  
4. Return to the bucket list, select the created bucket, and click **File list** in the **Operation** column.
5. On the file list page, click **Upload File** and select one or more files for upload.
6. After the file is uploaded, click **File info** in the **Action** column to view the **object address**.

### Migrating Data Through a Source File in COS
1. Log in to the [Tencent Cloud Console](https://intl.cloud.tencent.com/login?s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2F) and select **Products** > **TencentDB** > **SQL Server** in the top-left corner of the page to enter the TencentDB for SQL Server Console. Or, log in to the [TencentDB for SQL Server Console](https://console.cloud.tencent.com/sqlserver) directly.
2. Select **Data Transfer** in the left sidebar and click **Create Task** to create an offline migration task.
  - **Task Name**: Custom.
  - **Source Instance Type**: Select **SQL Server backup and restoration (in COS mode)**.
  - **Region**: The region of the source database must be the same as that of the source file in COS.
  - **Link to Source File in COS**: You can view the file information to get the COS object address after uploading the source file.
  - **Destination Database Type** and **Destination Database Region**: They are automatically populated by the system based on the source database configuration.
  - **Instance ID**: Select the destination instance. You can only select an instance in the same region.
3. After completing the configuration, click **Next**.
4. Currently, **type** and **database settings** can be changed. Click **Create Task**.
5. Return to the task list. At this time, the task status is **initializing**. Select the task and click **Start** to sync the task.
6. After the data synchronization is completed (i.e., the progress bar shows 100%), you need to click **Finish** to end the synchronization process. You can check whether the migration is successful based on the **status**.
 - If the task status is **task succeeded*, the data migration is successful.
 - If the status is **task failed*, the migration failed. Please check the failure information, fix it accordingly, and then migrate again.


