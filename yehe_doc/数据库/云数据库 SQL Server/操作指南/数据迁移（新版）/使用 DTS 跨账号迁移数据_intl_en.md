This document describes how to migrate data between instances with Data Transfer Service (DTS) across Tencent accounts.

## Application Scope
The source database can be TencentDB for MySQL, TencentDB for MongoDB, TencentDB for PostgreSQL, TencentDB for SQL Server, TencentDB for Redis, and TencentDB for Tendis. Only the last two options need to be applied by [submitting a ticket](https://console.cloud.tencent.com/workorder/category).

## Prerequisite
You have created the target database instance.

## Note
This operation involves multiple account information configuration items. The following lists the main configuration logic for easier understanding and configuration.
- Data migration direction: Source database (database instance under another account) > target database (database instance under the current account).
- The account executing the migration task can be the root account or a sub-account of the target database.
 - Use the root account to execute the migration task: Before executing the task, ask the root account of the source database to grant the root account of the target database access to the source database.
 - Use the sub-account to execute the migration task: Before executing the task, ask the root account of the source database to grant the root account of the target database access to the source database by role, and then ask the root account of the target database to grant its sub-account access to the source database.

[](id:SQZH)
## Authorizing Account
**To execute the migration task with a root account or a sub-account, follow steps 1–6 or steps 1–11 respectively.**
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/role) with the Tencent Cloud root account of the source database. If the sub-account has CAM and role permissions, you can also log in with the sub-account.
2. Click **Roles** on the left sidebar to enter the **Role Management** page. Then, click **Create Role**.
3. On the **Enter Role Entity Info** page, select **Tencent Cloud Account**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/tQVE421_1.png)
4. On the **Enter Role Entity Info** page, configure the relevant information and click **Next**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/4XDh257_2.png)
 - Tencent Cloud Account Type: Select **Other root account**.
 - Account ID: Enter the Tencent Cloud root account ID of the target database, which can be viewed in [Account Information](https://console.cloud.tencent.com/developer). Even if the target database is owned by a sub-account, you still need to enter the root account ID here.
 - External ID: You can enable it as needed.
>?If an external ID is used, keep it properly, as it cannot be queried in DTS.
5. On the **Configure Role Policy** page, select the corresponding policies of DTS and the source database and click **Next**.
 - Select `QcloudDTSReadOnlyAccess` as the DTS service policy.
 - For policies corresponding to the source database service, select the read-only service policy and the list acquisition policy of the source database.
 If the source database is TencentDB for SQL Server, add `QcloudSQLServerReadOnlyAccess` to obtain its read-only access permission.
>?`QcloudCDBReadOnlyAccess` must be added for the source database, otherwise you cannot obtain its instance list information while configuring the migration task.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/5yQt340_3.png)
6. Configure role tags, set the role name on the **Review** page, and click **Complete**.
>?Record the configured role name, which needs to be entered when you create the migration task later.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/jvpM496_4.png)
>?To execute a migration task with the root account, just follow the steps above; to execute a migration task with a sub-account, you need to ask the root account to authorize the sub-account as following steps 7-11.
7. (Optional) Log in to the [CAM console](https://console.cloud.tencent.com/cam/role) with the Tencent Cloud root account of the target database and click **Policies** on the left sidebar. Then, click **Create Custom Policy** on the right and select **Create by Policy Syntax**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/WvJP179_5.png)
8. (Optional) Select **Blank Template** and click **Next**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/8QQh962_6.png)
9. (Optional) Create a policy and enter the policy name and description as needed. After copying the sample code to the **Policy Content**, replace the content in the red box with the actual information.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/cBPU035_7.png)
Sample policy syntax:
```
{
    "version": "2.0",
    "statement": [
    {
        "effect": "allow",
        "action": ["name/sts:AssumeRole"],
  "resource": ["qcs::cam::uin/10*******8:roleName/DTS-role"]
    }
 ]
}
```
10. (Optional) Click **Complete**, return to the **Policy List** page, and click **Associate Users/Groups**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/TQ3A110_8.png)
11. (Optional) Select the sub-account of the target database instance (which is the sub-account used to execute the migration task) and click **OK**:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/eYky851_9.png)

## Creating Migration Task
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/overview) with the Tencent Cloud account of the target database instance.
2. Select **Data Migration > Create Migration Task** to purchase a migration task.
3. After making the purchase, return to the data migration task list and click **Configure** in the **Operation** column to enter the migration task configuration page.
4. On the source and target database configuration page, configure the database information.
Configure the key parameters for cross-account data migration as follows:
 - Access Type: Select **Database**, indicating that the source database is a TencentDB instance.
 - Cross-/Intra-Account: Select **Cross-account**.
 - Cross-Account ID: Enter the root account ID of the source database.
 - Cross-Account Role Name: The **role name** created in step 6 in [Authorizing Account](#SQZH). For more information on roles, see [Role Overview](https://intl.cloud.tencent.com/document/product/598/19420) and [Cross-account Access Role](https://intl.cloud.tencent.com/document/product/1150/47148).
 - Role External ID: This parameter is optional, and its value can be obtained from the previous section. For more information on roles, see [Role Overview](https://intl.cloud.tencent.com/document/product/598/19420) and [Cross-account Access Role](https://intl.cloud.tencent.com/document/product/1150/47148).
 >?After completing the above configuration, select the **Region** to get the instance list under the source database account. If an error occurs while getting the instances, the configuration may be incorrect, or no authorization has been performed. For more information, see [FAQs](#CJWT).
5. On the **Set migration options and select migration objects** page, set the data migration options, select migration objects, and click **Save and Go Next**.
6. On the **Verify task** page, complete the verification. After all check items are passed, click **Start Task**.
7. If the verification failed, fix the problem as instructed in [Check Item Overview](https://intl.cloud.tencent.com/document/product/571/42551) and initiate the verification task again.
8. Return to the data migration task list, and the task will be in the "Running" status.

[](id:CJWT)
## FAQs
**1. What should I do if the error "role not exist[InternalError.GetRoleError]" is reported when the instance list is pulled across accounts?**
Check whether the **Cross-Account ID** (the root account ID of the source database) and **Cross-Account Role Name** (the **role name** created in step 6 in [Authorizing Account](#SQZH)) have been correctly configured.

**2. What should I do if the error `InternalError:InternalInnerCommonError` is reported when the database instance list is obtained?**
The policy of the Tencent Cloud service to which the source database belongs hasn't been granted to the role. Grant it as instructed in step 5 in [Authorizing Account](#sqzh).

**3. What should I do if the error "you are not authorized to perform operation (sts:AssumeRole), resource (qcs::cam::uin/1xx5:roleName/xxxx) has no permission" is reported when the instance list is pulled across accounts?**
**Error cause**: The account that you use to create the migration task is a sub-account without the `sts:AssumeRole` permission.
**Solution**:

- Use the root account to create the migration task.
- Ask the root account of the target database to authorize the sub-account as instructed in [Authorizing Account](#SQZH) and set `resource` in the policy syntax to the field in blue in the error message.

