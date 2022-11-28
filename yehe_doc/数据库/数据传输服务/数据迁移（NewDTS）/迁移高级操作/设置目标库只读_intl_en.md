
## Overview
Writing data to the target database when DTS migrates data may cause data inconsistency between the source and target databases. If the read-only target database feature is enabled, DTS will revoke all the write permissions of the target database except for the migration account and prohibit authorization during data migration so as to limit writes to the target database. It will open up write permissions after migration is completed. This helps avoid data inconsistency due to double write.
>?To try out this feature, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.

## Notes
As DTS will revoke the write permissions of the target database after the read-only target database feature is enabled, the more the accounts in the target database, the longer the time the task stays in the **Preparing** and **Completed** statuses.

## Directions

**Currently, the read-only target database feature conflicts with the account migration feature. Therefore, if you want to make the target database read-only and migrate accounts, you need to perform two migration tasks** as detailed below:

- To enable read-only target database without migrating accounts, directly perform task 2.
- To enable read-only target database and migrate accounts, perform tasks 1 and 2.

#### Task 1. Account migration
>?This section describes only the different steps to set the read-only target database feature. For more information on configuration, including migrated account authorization, operation limits, and notes, see [Migration from MySQL to TencentDB for MySQL](https://www.tencentcloud.com/document/product/571/42645).

Create an empty `test` database in the source database. Then, create a full migration task, set **Migration Object** to **Specify object**, select **Migrate Account**, and select the `test` database. After migrating the accounts in the source database to the target database, complete the task.

1. Create an empty `test` database in the source database.
2. Log in to the [DTS console](https://console.cloud.tencent.com/dts/migration), select **Data Migration** on the left sidebar, click **Create Migration Task**, and enter the **Create Migration Task** page.
3. On the **Create Migration Task** page, select the types, regions, and specifications of the source and target databases and click **Buy Now**.
4. Configure the migration task.
    On the **Set source and target databases** page, configure the task, source database, and target database settings. After the source and target databases pass the connectivity test, click **Create**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/dac2f8c6ba3cd96dd46fc5b7e99a1762.png)
5. On the **Set migration options and select migration objects** page, configure the migration type and objects and click **Save**.
 - Migration Type: Select **Full migration**.
 - Data Consistency Check: Select **No check**.
 - Migration Object: Select **Specify object** and then select the `test` database.
 - Migrate Account: Enable this option.
 - Advanced Migration Object:
   ![](https://qcloudimg.tencent-cloud.cn/raw/bae750e6e1a4d363328f8db540301bbe.png)     
6. On the **Verify task** page, DTS will check the account information in the source database and will migrate eligible accounts.
>?For detailed requirements for account migration, see [Account Migration](https://www.tencentcloud.com/document/product/571/48483).
>
7. After the task status becomes **Completed**, create the next migration task.

#### Task 2. Read-only target database configuration

Migrate objects except accounts and enable read-only target database.

1. Purchase a migration task. On the **Create Migration Task** page, select the types, regions, and specifications of the source and target databases and click **Buy Now**.
2. Configure the migration task.
   On the **Set source and target databases** page, configure the task, source database, and target database settings. After the source and target databases pass the connectivity test, click **Create**. Here, **Access Type** needs to be the same as that selected in task 1.
3. On the **Set migration options and select migration objects** page, configure the migration type and objects and click **Save**.
 - Migration Type: Select as needed.
 - Data Consistency Check: Select as needed.
 - Migration Object: Select **Entire instance**.
 - Advanced Migration Object: Select as needed.
 - Read-Only Target Database: Enable this option.
 - Migrate Account: Disable this option.
4. Verify the task.
5. Return to the data migration task list, and you can see that the task has entered the **Preparing** status. After 1–2 minutes, the data migration task will be started.
The more the accounts in the target database, the longer the time the task stays in the **Preparing** and **Completed** statuses.

