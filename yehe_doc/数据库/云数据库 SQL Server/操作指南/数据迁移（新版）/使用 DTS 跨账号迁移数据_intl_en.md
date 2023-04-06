This document describes how to migrate data between instances with Data Transmission Service (DTS) across Tencent accounts.

## Service options
The source database can be TencentDB for MySQL, TencentDB for MongoDB, TencentDB for PostgreSQL, TencentDB for SQL Server, TencentDB for Redis, and TencentDB for Tendis. Only the last two options need to be applied by [submitting a ticket](https://console.cloud.tencent.com/workorder/category).

## Prerequisites
You have created the target database instance.

## Notes
This operation involves multiple account information configuration items. The following lists the main configuration logic for easier understanding and configuration.
- Data migration direction: Source database (database instance under another account) > target database (database instance under the current account).
- The account executing the migration task can be the root account or a sub-account of the target database.
 - Use the root account to execute the migration task. Before executing the task, ask the root account of the source database to grant the root account of the target database access to the source database.
 - Use the sub-account to execute the migration task. Before executing the task, ask the root account of the source database to grant the root account of the target database access to the source database by role, and then ask the root account of the target database to grant the sub-account access to the source database.

[](id:SQZH)
## Authorizing an account
**To execute the migration task with a root account or a sub-account, follow steps 1–6 or steps 1–11 respectively.**
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/role) with the Tencent Cloud root account of the source database (if the sub-account has CAM and role permissions, you can also log in with the sub-account).
2. Click **Role** on the left sidebar to enter the **Role Management** page. Then, click **Create Role**.
3. On the **Enter Role Entity Info** page, select **Tencent Cloud Account**.
4. On the **Enter Role Entity Info** page, configure the relevant information and click **Next**.
 - Tencent Cloud Account Type: Select **Other root account**.
 - Account ID: Enter the Tencent Cloud root account ID of the target database, which can be viewed in [Account Info](https://console.cloud.tencent.com/developer). Even if the target database is owned by a sub-account, you still need to enter the root account ID here.
 - External ID: You can enable it as needed.
>?If an external ID is used, record and keep the ID on your own, as it cannot be queried in DTS.
5. On the **Configure Role Policy** page, select the corresponding policies of DTS and the source database and click **Next**.
 - Select `QcloudDTSReadOnlyAccess` as the DTS service policy.
 - For policies corresponding to the source database service, select the read-only service policy and the list acquisition policy of the source database.
 If the source database is TencentDB for SQL Server, add `QcloudSQLServerReadOnlyAccess` to obtain its read-only access permission.
>?`QcloudCDBReadOnlyAccess` must be added for the source database, otherwise you can't obtain its instance list information while configuring migration task.
>
6. Configure role tags. Then, on the **Review** page, set the role name and click **Complete**.
>?Record the configured role name, which needs to be entered when you create the migration task later.
>?To execute a migration task with the root account, just follow the steps above; to execute a migration task with a sub-account, you need to ask the root account to authorize the sub-account as following steps 7-11.
7. (Optional) Log in to the [CAM console](https://console.cloud.tencent.com/cam/role) with the Tencent Cloud root account of the target database and click **Policies** on the left sidebar. Then, click **Create Custom Policy** on the right and select **Create by Policy Syntax**.
8. (Optional) Select **Blank Template** and click **Next**.
9. (Optional) Create a policy and enter the policy name and description as needed. After copying the sample code to the **Policy Content**, replace the content in the red box with the actual information.
Policy syntax example:
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
11. (Optional) Select the sub-account of the target database instance (i.e., the sub-account used to execute the migration task) and click **OK** as shown below:

## Creating a migration task
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/overview) with the Tencent Cloud account of the target database instance.
2. Select **Data Migration > Create Migration Task** to purchase a migration task.
3. After making the purchase, return to the data migration task list and click **Configure** in the **Operation** column to enter the migration task configuration page.
4. On the source and target database configuration page, configure information for them.
Configure the key parameters for cross-account data migration as follows:
 - Access Type: Select **Database**, indicating that the source database is a TencentDB instance.
 - Cross-/Intra-Account: Select **Cross-account**.
 - Cross-Account ID: Enter the root account ID of the source database.
 - Cross-Account Role Name: The **role name** created in step 6 in [Authorizing an account](#SQZH). For more information on roles, see [Role Overview](https://intl.cloud.tencent.com/document/product/598/19420) and [Cross-account Access Role](https://intl.cloud.tencent.com/document/product/1150/47148).
 - External Role ID: This parameter is optional, and its value can be obtained from the previous section. For more information on roles, see [Role Overview](https://intl.cloud.tencent.com/document/product/598/19420) and [Cross-account Access Role](https://intl.cloud.tencent.com/document/product/1150/47148).
 >?After completing the above configuration, select the **Region** to get the instance list under the source database account. If an error occurs while getting the instances, the configuration may be incorrect, or no authorization has been performed. For more information, see [FAQs](#CJWT).
5. On the **Set migration options and select migration objects** page, set the data migration options, select migration objects, and click **Save and Go Next**.
6. On the**Verify task** page, click **Start Task** after all the items are successfully verified.
7. If the verification failed, fix the problem as instructed in [Check Item Overview](https://intl.cloud.tencent.com/document/product/571/42551) and initiate the verification task again.
8. Return to the data migration task list, and the task will be in the "Running" status.

[](id:CJWT)
## FAQs
**1. What should I do if the error "role not exist[InternalError.GetRoleError]" is reported when the instance list is pulled across accounts?
Check whether the **Across-Account ID** (the root account ID of the source database) and **Across-Account Role Name** (the **role name** created in step 6 in [Authorizing an account](#SQZH)) have been correctly configured.

**2. What should I do if the error `InternalError:InternalInnerCommonError` is reported when the database instance list is obtained?**
The policy of the Tencent Cloud service to which the source database belongs hasn't been granted to the role. Grant it as instructed in step 5 in [Authorizing an account](#sqzh).

**3. What should I do if the error "you are not authorized to perform operation (sts:AssumeRole), resource (qcs::cam::uin/1xx5:roleName/xxxx) has no permission" is reported when the instance list is pulled across accounts?**
**Error cause**: The account that you use to create the migration task is a sub-account without the `sts:AssumeRole` permission.
**Solution**:

- Use the root account to create the migration task.
- Ask the root account of the target database to authorize the sub-account as instructed in [Authorizing an account](#SQZH) and set `resource` in the policy syntax to the field in blue in the error message.

