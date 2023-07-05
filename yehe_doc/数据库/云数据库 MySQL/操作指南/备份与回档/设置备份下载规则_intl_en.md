By default, you can download backup files of TencentDB for MySQL instances over public or private network. To limit the download, you can adjust backup download settings.
>? Backup download settings are supported in the following regions:
>Guangzhou, Shanghai, Beijing, Shenzhen, Chengdu, Chongqing, Nanjing, Hong Kong (China), Beijing Finance, Shanghai Finance, Shenzhen Finance, Toronto, Singapore, Silicon Valley, Frankfurt, Seoul, Mumbai, Bangkok, Moscow, and Tokyo.
>

## Setting backup download rules
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), select **Database Backup** on the left sidebar, and select a region at the top.
2. On the **Download Settings** tab, view the backup download settings and click **Edit** to modify them.
>?Download over public network is enabled by default and when it is enabled, download over private network is also allowed.
>
![](https://qcloudimg.tencent-cloud.cn/raw/530fbf3e6c93eea06ff23e112cad84c0.png)
3. On the displayed page, set the download rules and click **OK**.
   - Download over public network:
     - Enabled: You cannot set any download rule.
     - Disabled: You can set the download rules for private network by allowing or blocking specific IPs and VPCs.
   - Set the download rules:
     - If you don't specify any value, the condition won't take effect.
     - You should separate the values of an IP condition with commas.
     - You can enter IPs or IP ranges as the values of an IP condition.
     - If no IP and VPC requirements are set, there will be no limit on download over private network.
     ![](https://qcloudimg.tencent-cloud.cn/raw/c2e1481c2a14a5ad8b3dde4819f783c1.png)
4. After the configuration is completed, return to the **Download Settings** tab to view the rules that take effect.
![](https://qcloudimg.tencent-cloud.cn/raw/cb4ac45dcde8a57610b0eaec9075c6cb.png)

## Authorizing sub-accounts to set backup download rules
By default, sub-accounts do not have the permission to set backup download rules for TencentDB for MySQL instances. Therefore, you need to create CAM policies to grant specific sub-accounts the permission.

[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583) is a web-based Tencent Cloud service that helps you securely manage and control access permissions to your Tencent Cloud resources. Using CAM, you can create, manage, and terminate users (groups), and control the Tencent Cloud resources that can be used by the specified user through identity and policy management.

You can use CAM to bind a user or user group to a policy which allows or denies them access to specified resources to complete specified tasks. For more information on CAM policy elements, see [Element Reference](https://www.tencentcloud.com/document/product/598/10603).

### Authorizing sub-accounts
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam) with the root account, locate the target sub-user in the user list, and click **Authorize**.
![](https://qcloudimg.tencent-cloud.cn/raw/89d7cf063bd376a0cc4f4db0c78e7e56.png)
2. In the pop-up window, select the **QcloudCDBFullAccess** preset policy and click **OK** to complete the authorization.
![](https://qcloudimg.tencent-cloud.cn/raw/0819ca9a1a81fc00968f0a263dc7727e.png)

### Policy syntax
The following policy syntax is used to authorize a sub-account to set backup download rules for TencentDB for MySQL instances:
```
{
       "version":"2.0",
       "statement":
       [
          {
             "effect":"effect",
             "action":["action"],
             "resource":["resource"]
            }
       ] 
}
```
- **version** is required. Currently, only the value "2.0" is allowed.
- **statement** element describes the details of one or more permissions. This element contains a permission or permission set of other elements such as `effect`, `action`, and `resource`. One policy has only one `statement`.
- **effect** is required. It describes the result of a statement. The result can be "allow" or an "explicit deny".
- **action** is required. It specifies whether to allow or deny the operation. The operation can be an API (prefixed with "cdb:"). which can be an API (prefixed with `name`) or a feature set (a set of specific APIs prefixed with `permid`).
- **resource** is required. It describes the details of authorization.

### API operations
In a CAM policy statement, you can specify any API operation from any service that supports CAM. For database audit, the API prefixed with `name/cdb:`  should be used. To specify multiple operations in a single statement, separate them by comma:
```
"action":["name/cdb:action1","name/cdb:action2"]
```
You can also specify multiple operations by using a wildcard. For example, you can specify all operations beginning with "Describe" in the name as shown below:
```
"action":["name/cdb:Describe*"]
```

### Resource path
Resource paths are generally in the following format:
```
qcs::service_type::account:resource
```
- service_type: Describes the product abbreviation, such as `cdb` here.
- account: Describes the root account of the resource owner, such as `uin/326xxx46`.
- resource: Describes the detailed resource information of the specific service. Each TencentDB for MySQL instance (instanceId) is a resource.

Below is a sample:
```
 "resource": ["qcs::cdb::uin/326xxx46:instanceId/cdb-kfxxh3"]
```
Here, `cdb-kfxxh3` is the ID of the TencentDB for MySQL instance resource, i.e., the `resource` in the CAM policy statement.

### Example
The following example only shows the usage of CAM. For the complete list of APIs used to set MySQL backup download rules, see the [API documentation](https://intl.cloud.tencent.com/document/product/236/43327).
```
{
       "version":"2.0",
       "statement":
       [
          {
             "effect":"allow",
             "action": ["name/cdb: ModifyBackupDownloadRestriction"],
             "resource": ["*"]
            }
       ]
}
```

### Customizing CAM policy for setting MySQL backup download rules
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/policy) with the root account, select **Policies** on the left sidebar, and click **Create Custom Policy**.
![img](https://qcloudimg.tencent-cloud.cn/raw/4ddc463dc28ee48b9dd63d862fa41ea1.png)
2. In the pop-up dialog box, select **Create by Policy Generator**.
3. On the **Select Service and Action** page, select configuration items, click **Add Statement**, and click **Next**.
   - Effect: Select **Allow** or **Deny** for the action.
   - Service: Select **TencentDB for MySQL**.
   - Action: Select all APIs of setting MySQL backup download rules. For more information, see the [API documentation](https://intl.cloud.tencent.com/document/product/236/43327).
   - Resource: For more information, see [Resource Description Method](https://intl.cloud.tencent.com/document/product/598/10606). You can enter `*` to indicate that the backup download rules of TencentDB for MySQL instances in the specified region can be set.
   ![](https://qcloudimg.tencent-cloud.cn/raw/5372ae1d2ac16ff63b63fbf175f3fccf.png)
4. On the **Edit Policy** page, enter the **Policy Name** (such as `BackupDownloadRestriction`) as required and **Description** and click **Done**.
![](https://qcloudimg.tencent-cloud.cn/raw/3c5454e0da412c0e12beebb4b045979d.png)
5. Return to the policy list and you can view the custom policy just created.
![](https://qcloudimg.tencent-cloud.cn/raw/d242b34c0b9cad83d130444d84e205e0.png)

