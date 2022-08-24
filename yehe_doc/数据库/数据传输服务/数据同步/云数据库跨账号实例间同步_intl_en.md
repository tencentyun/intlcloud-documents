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
   - If the target database is owned by a root account, you need to use the root account to execute the sync task. Before executing the task, ask the root account of the source database to grant the root account of the target database access to the source database.
   - If the target database is owned by a sub-account, you need to use the sub-account to execute the sync task. Before executing the task, ask the root account of the source database to grant the root account of the target database access to the source database, and then ask the root account of the target database to grant the sub-account access to the source database.

## [Authorizing Account](id:sqzh)
**To execute the sync task with a root account or a sub-account follow steps 1–6 or steps 1–11 respectively.**

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/role) with the Tencent Cloud root account of the source database (if the sub-account has CAM and role permissions, you can also log in with the sub-account).
2. Click **Role** on the left sidebar to enter the **Role Management** page. Then, click **Create Role**.
3. On the **Select role entity** page, select **Tencent Cloud Account**.<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/b5fd492a4790c8ece15f4830b85e2df1.png" style="zoom:40%;" />
4. On the **Enter Role Entity Info** page, configure the information and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/33617c62891531013942e82ce179499d.png)
   - Tencent Cloud account: Select **Other root account**.
   - Account ID: Enter the Tencent Cloud root account ID of the target database, which can be viewed in **[Account Info](https://console.cloud.tencent.com/developer)**. Even if the target database is owned by a sub-account, you still need to enter the root account ID here.
   - External ID: You can enable it as needed.  
>?If an external ID is used, record and keep the ID on your own, as it cannot be queried in DTS.
5. On the **Configure Role Policy** page, enter **QcloudDTSReadOnlyAccess**, select the **QcloudDTSReadOnlyAccess** preset policy, and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/a70b000b9f51652c472fe223711d04d4.png)
6. On the **Review** page, set the role name and click **Complete**.
>?Record the configured name, which needs to be entered when you create the sync task later.
>
![](https://qcloudimg.tencent-cloud.cn/raw/b85ad44d6d8cac11bab863216c696fd2.png)
>?To execute a sync task with the root account, just follow the steps above; to execute a sync task with a sub-account, you also need to ask the root account to authorize the sub-account as follows:
7. (Optional) Log in to the [CAM console](https://console.cloud.tencent.com/cam/role) with the Tencent Cloud sub-account of the target database and click **Policies** on the left sidebar. Then, click **Create Custom Policy** on the right and select **Create by Policy Syntax**.<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/98feaf82b12346e6b106864be12c929e.png" style="zoom:40%;" />      
8. (Optional) Select **Blank Template** and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/22f37e1ed65e7394c3b0d32b73a8d724.png)  
9. (Optional) Create a policy and enter the policy name and description as needed. After copying the sample code to the **Policy Content**, replace the content in the red box with the actual information.<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/0b516baa18d7b242160f99ffb844681a.png" style="zoom:50%;" />
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
![](https://qcloudimg.tencent-cloud.cn/raw/a61a3c28aa711662db854e8963024d56.png) 
11. (Optional) Select the sub-account of the target database instance (i.e., the sub-account executing the sync task) and click **OK** as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/5a56dd3c69f3c2688bc9c36ddead59e5.png" style="zoom:80%;" />

## Creating Sync Task
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/overview) with the Tencent Cloud account of the target database instance.
2. Select **Data Sync** > **Create Sync Task** and purchase a sync task.
3. After making the purchase, return to the data sync list and click **Configure** in the **Operation** column to enter the sync task configuration page.
4. On the **Set source and target databases** page, configure the source and target database information. The following takes data sync between two TencentDB for MySQL instances as an example.
![](https://qcloudimg.tencent-cloud.cn/raw/87b6e9567d9e5ea078d144640498ee0d.png)
Configure the key parameters for cross-account data sync as follows:
   - Access Type: Select **Database**, indicating that the source database is a TencentDB instance.
   - Cross-/Intra-Account: Select **Cross-account**.
   - Peer Account ID: Enter the root account ID of the source database.
   - Peer Account Role Name: The **role name** created in step 6 in [Authorizing Account](#sqzh). For more information on roles, see [Role Overview](https://intl.cloud.tencent.com/document/product/598/19420) and [Cross-account Access Role](https://intl.cloud.tencent.com/document/product/1150/47148).
   - External Role ID: This parameter is optional, and its value can be obtained from the previous section. For more information on roles, see [Role Overview](https://intl.cloud.tencent.com/document/product/598/19420) and [Cross-account Access Role](https://intl.cloud.tencent.com/document/product/1150/47148).
>?After completing the above configuration, select the **Region** to get the instance list under the source database account. If an error occurs while getting the instances, the configuration may be incorrect, or no authorization has been performed. For more information, see [FAQs](#cjwt).
5. On the **Set sync options and objects** page, set the **Data Initialization Option**, **Data Sync Option**, and **Sync Object Option** and click **Save and Go Next**.
6. On the **Verify task** page, complete the verification. After all check items are passed, click **Start Task**.
If the verification fails, fix the problem as instructed in [Check Item Overview](https://intl.cloud.tencent.com/document/product/571/42551) and initiate the verification again.
7. Return to the data sync task list, and you can see that the task has entered the **Running** status.
>?You can click **More** > **Stop** in the **Operation** column to stop a sync task. You need to ensure that data sync has been completed before stopping the task.

## [FAQs](id:cjwt)
#### 1. What should I do if the error "role not exist[InternalError.GetRoleError]" is reported when the instance list is pulled across accounts?
Check whether the **Peer Account ID** (the root account ID of the source database) and **Peer Account Role Name** (the **role name** created in step 6 in [Authorizing Account](#sqzh)) have been correctly configured.

#### 2. What should I do if the error "you are not authorized to perform operation (sts:AssumeRole), resource (qcs::cam::uin/1xx5:roleName/xxxx) has no permission" is reported when the instance list is pulled across accounts?
![](https://main.qcloudimg.com/raw/16dee616c668dde14d10b892918d42a1.png)
**Error cause**: The account that you use to create the sync task is a sub-account without the `sts:AssumeRole` permission.
**Solution**:

- Use the root account to create the sync task.
- Ask the root account of the target database to authorize the sub-account as instructed in [Authorizing Account](#sqzh) and set `resource` in the policy syntax to the field in blue in the error message.
![](https://main.qcloudimg.com/raw/d978acb50ab95f7b8091854f8b8e17f7.png)


