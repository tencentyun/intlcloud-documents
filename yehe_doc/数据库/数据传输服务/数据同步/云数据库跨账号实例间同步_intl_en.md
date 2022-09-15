## Overview
This document describes how to use DTS' data sync feature to perform data sync between the source and target TencentDB instances under different root accounts.

## Supported Scope
Cross-account data sync is supported between TencentDB for MySQL, TDSQL for MySQL, TDSQL-C, and TencentDB for MariaDB instances, but not between MySQL and CDWPG instances. For more information, see [Databases Supported by Data Sync](https://intl.cloud.tencent.com/document/product/571/42579).

## Prerequisites
You have created the target database instance.

## Notes
This operation involves multiple account information configuration items. The following lists the main configuration logic for easier understanding and configuration.
- Data sync direction: Source database (database instance under another account) > target database (database instance under the current account).
- The account executing the sync task can be the root account or a sub-account of the target database.
   - If you use a root account to execute the sync task, before executing the task, ask the root account of the source database to grant the root account of the target database access to the source database.
   - If you use a sub-account to execute the sync task, before executing the task, ask the root account of the source database to grant the root account of the target database access to the source database, and then ask the root account of the target database to grant the sub-account access to the source database.

## [Authorizing an Account](id:sqzh)
**To execute the sync task with a root account or a sub-account follow steps 1–6 or steps 1–11 respectively.**

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/role) with the Tencent Cloud root account of the source database (if the sub-account has CAM and role permissions, you can also log in with the sub-account).
2. Click **Role** on the left sidebar to enter the **Role Management** page. Then, click **Create Role**.
3. On the **Select role entity** page, select **Tencent Cloud Account**.<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/383f4bd0086637b5346b03797d022a2e.png" style="zoom:90%;" />
4. On the **Enter Role Entity Info** page, configure the information and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/77f8a29b40f48f4e6cc77ed7f191af13.png)
   - Tencent Cloud account: Select **Other root account**.
   - Account ID: Enter the Tencent Cloud root account ID of the target database, which can be viewed in **[Account Info](https://console.cloud.tencent.com/developer)**. Even if the target database instance is owned by a sub-account, you still need to enter the root account ID here.
   - External ID: You can enable it as needed.  
>?If an external ID is used, record and keep the ID on your own, as it cannot be queried in DTS.
5. On the **Configure Role Policy** page, select the corresponding policies of DTS and the source database and click **Next**.
 - For the DTS policy, select `QcloudDTSReadOnlyAccess`.
 - For the corresponding policy of the source database, select the policy of the Tencent Cloud service to which the source database belongs. For example, if the source database is TencentDB for MySQL, select `QcloudAccessForMySQLRole`. Select a policy based on the actual conditions.
![](https://qcloudimg.tencent-cloud.cn/raw/5d039c19c35e1d8a107a023ed5321010.png)
6. On the **Review** page, set the role name and click **Complete**.
>?Record the configured name, which needs to be entered when you create the sync task later.
>
![](https://qcloudimg.tencent-cloud.cn/raw/acb68a6dfa00e5ccd41fdd511a0fcfd6.png)
>?To execute a sync task with the root account, just follow the steps above; to execute a sync task with a sub-account, you also need to ask the root account to authorize the sub-account as follows:
7. (Optional) Log in to the [CAM console](https://console.cloud.tencent.com/cam/role) with the Tencent Cloud sub-account of the target database and click **Policies** on the left sidebar. Then, click **Create Custom Policy** on the right and select **Create by Policy Syntax**.<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/050a9318db3118de54ffefb57c144c12.png" style="zoom:90%;" />      
8. (Optional) Select **Blank Template** and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/3e779e1daa8394da22d8ee3200c10370.png)  
9. (Optional) Create a policy and enter the policy name and description as needed. After copying the sample code to the **Policy Content**, replace the content in the red box with the actual information.<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/9f877d283df7104ab5be9506d338b4a3.png" style="zoom:50%;" />
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
![](https://qcloudimg.tencent-cloud.cn/raw/ad8eb259b437793ac5a8dfe20c97b627.png) 
11. (Optional) Select the sub-account of the target database instance (i.e., the sub-account executing the sync task) and click **OK**:
<img src="https://qcloudimg.tencent-cloud.cn/raw/b28690185058f58e03eb44e6dd84161c.png" style="zoom:80%;" />

## Creating a Sync Task
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/overview) with the Tencent Cloud account of the target database instance.
2. Select **Data Sync** > **Create Sync Task** and purchase a sync task.
3. After making the purchase, return to the data sync list and click **Configure** in the **Operation** column to enter the sync task configuration page.
4. On the **Set source and target databases** page, configure the source and target database information. The following takes data sync between two TencentDB for MySQL instances as an example.
![](https://qcloudimg.tencent-cloud.cn/raw/28ba920ca242e72be84f81fc4bee665e.png)
Configure the key parameters for cross-account data sync as follows:
   - Access Type: Select **Database**, indicating that the source database is a TencentDB instance.
   - Cross-/Intra-Account: Select **Cross-account**.
   - Peer Account ID: Enter the root account ID of the source database.
   - Peer Account Role Name: The **role name** created in step 6 in [Authorizing an Account](#sqzh). For more information on roles, see [Role Overview](https://intl.cloud.tencent.com/document/product/598/19420) and [Cross-account Access Role](https://intl.cloud.tencent.com/document/product/1150/47148).
   - External Role ID: This parameter is optional, and its value can be obtained from the previous section. For more information on roles, see [Role Overview](https://intl.cloud.tencent.com/document/product/598/19420) and [Cross-account Access Role](https://intl.cloud.tencent.com/document/product/1150/47148).
>?After completing the above configuration, select the **Region** to get the instance list under the source database account. If an error occurs while getting the instances, the configuration may be incorrect, or no authorization has been performed. For more information, see [FAQs](#cjwt).
5. On the **Set sync options and objects** page, set the data initialization, data sync, and sync object options and click **Save and Go Next**.
6. On the **Verify task** page, complete the verification. After all check items are passed, click **Start Task**.
If the verification fails, fix the problem as instructed in [Check Item Overview](https://intl.cloud.tencent.com/document/product/571/42551) and initiate the verification again.
7. Return to the data sync task list, and you can see that the task has entered the **Running** status.
>?You can click **More** > **Stop** in the **Operation** column to stop a sync task. You need to ensure that data sync has been completed before stopping the task.

## [FAQs](id:cjwt)

#### 1. What should I do if the error "role not exist[InternalError.GetRoleError]" is reported when the instance list is pulled across accounts?
Confirm that the **Peer Account ID** (the root account ID of the source database) and **Peer Account Role Name** (the **role name** created in step 6 in [Authorizing an Account](#sqzh)) have been correctly configured. If the problem persists, it may be because the service permission of the source database hasn't been granted (see step 5 in [Authorizing an Account](#sqzh)).

#### 2. What should I do if the error `InternalError:InternalInnerCommonError` is reported when the database instance list is obtained?

#### The policy of the Tencent Cloud service to which the source database belongs hasn't been granted to the role. Grant it as instructed in step 5 in [Authorizing an Account](#sqzh).

#### 3. What should I do if the error "you are not authorized to perform operation (sts:AssumeRole), resource (qcs::cam::uin/1xx5:roleName/xxxx) has no permission" is reported when the instance list is pulled across accounts?

 **Error cause**: The account that you use to create the sync task is a sub-account without the `sts:AssumeRole` permission.

**Solution**:

- Use the root account to create the sync task.
- Ask the root account of the target database to authorize the sub-account as instructed in [Authorizing an Account](#sqzh) and set `resource` in the policy syntax to the field in blue in the error message.



