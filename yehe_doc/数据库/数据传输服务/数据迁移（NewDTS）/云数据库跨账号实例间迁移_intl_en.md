## Overview
This document describes how to use the data migration feature of DTS to perform data migration between the source and target TencentDB instances under different root accounts.

## Supported Scope
- Data migration from TencentDB for MySQL/MongoDB/PostgreSQL.

## Prerequisites
You have created the target database instance.

## Notes
This operation involves multiple account information configuration items. The following lists the main configuration logic for easier understanding and configuration.

- Data migration direction: Source database (database instance under another account) > target database (database instance under the current account).
- The account executing the migration task can be the root account or a sub-account of the target database.
  - If you use a root account to execute the migration task, before executing the task, ask the root account of the source database to grant the root account of the target database access to the source database.
  - If you use a sub-account to execute the migration task, before executing the task, ask the root account of the source database to grant the root account of the target database access to the source database with a role, and then ask the root account of the target database to grant the sub-account access to the source database.

## [Authorizing an Account](id:sqzh)
**To execute the migration task with a root account or a sub-account, follow steps 1–6 or steps 1–11 respectively.**

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/role) with the Tencent Cloud root account of the source database (if the sub-account has CAM and role permissions, you can also log in with the sub-account).
2. Click **Role** on the left sidebar to enter the **Role Management** page. Then, click **Create Role**.
3. On the **Select role entity** page, select **Tencent Cloud Account**.<br>
   <img src="https://qcloudimg.tencent-cloud.cn/raw/0a085bbeedc2404ec651c380d1c51513.png" style="zoom:40%;" />
4. On the **Enter Role Entity Info** page, configure the information and click **Next**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/af0d0335bc18ba1dffe9a52c72505c3e.png)
   - Tencent Cloud account: Select **Other root account**.
   - Account ID: Enter the Tencent Cloud root account ID of the target database, which can be viewed in **[Account Info](https://console.cloud.tencent.com/developer)**. Even if the target database instance is owned by a sub-account, you still need to enter the root account ID here.
   - External ID: You can enable it as needed.  
>?If an external ID is used, record and keep the ID on your own, as it cannot be queried in DTS.
5. On the **Configure Role Policy** page, select the corresponding policies of DTS and the source database and click **Next**.
 - For the DTS policy, select `QcloudDTSReadOnlyAccess`.
 - For the corresponding policy of the source database, select the policy of the Tencent Cloud service to which the source database belongs. For example, if the source database is TencentDB for MySQL or PostgreSQL, select `QcloudAccessForMySQLRole` or `QcloudPostgreSQLReadOnlyAccess` respectively. Select a policy based on the actual conditions.
![](https://qcloudimg.tencent-cloud.cn/raw/26ccc7c5c91ab4f513ba134767b81d35.png)
6. Configure role tags. Then, on the **Review** page, set the role name and click **Complete**.
>?Record the configured role name, which needs to be entered when you create the migration task later.
>
![](https://qcloudimg.tencent-cloud.cn/raw/7f21bb7c56d5ad2712d6571fc4cff532.png)
>?To execute a migration task with the root account, just follow the steps above; to execute a migration task with a sub-account, you also need to ask the root account to authorize the sub-account as follows:
7. (Optional) Log in to the [CAM console](https://console.cloud.tencent.com/cam/role) with the Tencent Cloud root account of the target database and click **Policies** on the left sidebar. Then, click **Create Custom Policy** on the right and select **Create by Policy Syntax**.<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/203282357c80ce91222ffaf430a5a558.png" style="zoom:90%;" />      
8. (Optional) Select **Blank Template** and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/476f823438c7bc16120b44078c6926cb.png)  
9. (Optional) Create a policy and enter the policy name and description as needed. After copying the sample code to the **Policy Content**, replace the content in the red box with the actual information.<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/7956d47a1b0588a0cda26a9463a6b02b.png" style="zoom:50%;" />
<br>Sample policy syntax:  
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
![](https://qcloudimg.tencent-cloud.cn/raw/0a36bf46c25027a727f61829f4a8eacd.png) 
11. (Optional) Select the sub-account of the target database instance (i.e., the sub-account executing the migration task) and click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/2b1498e12917e9bc0ba5c82b8a248d1b.png" style="zoom:80%;" />

## Creating a Migration Task
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/overview) with the Tencent Cloud account of the target database instance.
2. Select **Data Migration** > **Create Migration Task** to purchase a migration task.
3. After making the purchase, return to the data migration task list and click **Configure** in the **Operation** column to enter the migration task configuration page.
4. On the **Set source and target databases** page, configure the source and target database information. The following takes data migration between two TencentDB for MySQL instances as an example.
   ![](https://qcloudimg.tencent-cloud.cn/raw/3ad50fd1ffaf4794a1bb6a9b9058ba06.png)
   Configure the key parameters for cross-account data migration as follows:
   - Access Type: Select **Database**, indicating that the source database is a TencentDB instance.
   - Cross-/Intra-Account: Select **Cross-account**.
   - Peer Account ID: Enter the root account ID of the source database.
   - Peer Account Role Name: The **role name** created in step 6 in [Authorizing an Account](#sqzh). For more information on roles, see [Role Overview](https://intl.cloud.tencent.com/document/product/598/19420) and [Cross-account Access Role](https://intl.cloud.tencent.com/document/product/1150/47148).
   - External Role ID: This parameter is optional, and its value can be obtained from the previous section. For more information on roles, see [Role Overview](https://intl.cloud.tencent.com/document/product/598/19420) and [Cross-account Access Role](https://intl.cloud.tencent.com/document/product/1150/47148).
>?After completing the above configuration, select the **Region** to get the instance list under the source database account. If an error occurs while getting the instances, the configuration may be incorrect, or no authorization has been performed. For more information, see [FAQs](#cjwt).
5. On the **Set migration options and select migration objects** page, set the data migration options, select migration objects, and click **Save and Go Next**.
6. On the **Verify task** page, complete the verification. After all check items are passed, click **Start Task**.
   If the verification fails, fix the problem as instructed in [Check Item Overview](https://intl.cloud.tencent.com/document/product/571/42551) and initiate the verification again.
7. Return to the data migration task list, and you can see that the task has entered the **Running** status.

## [FAQs](id:cjwt)
#### 1. What should I do if the error "role not exist[InternalError.GetRoleError]" is reported when the instance list is pulled across accounts?
Check whether the **Peer Account ID** (the root account ID of the source database) and **Peer Account Role Name** (the **role name** created in step 6 in [Authorizing an Account](#sqzh)) have been correctly configured.

#### 2. What should I do if the error `InternalError:InternalInnerCommonError` is reported when the database instance list is obtained?


The policy of the Tencent Cloud service to which the source database belongs hasn't been granted to the role. Grant it as instructed in step 5 in [Authorizing an Account](#sqzh).


#### 3. What should I do if the error "you are not authorized to perform operation (sts:AssumeRole), resource (qcs::cam::uin/1xx5:roleName/xxxx) has no permission" is reported when the instance list is pulled across accounts?


**Error cause**: The account that you use to create the migration task is a sub-account without the `sts:AssumeRole` permission.
**Solution**:

- Use the root account to create the migration task.
- Ask the root account of the target database to authorize the sub-account as instructed in [Authorizing an Account](#sqzh) and set `resource` in the policy syntax to the field in blue in the error message.
  
