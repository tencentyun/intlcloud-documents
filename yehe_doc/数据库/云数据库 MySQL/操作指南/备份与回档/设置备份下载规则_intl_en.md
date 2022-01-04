
By default, you can download backup files of TencentDB for MySQL instances over public or private network. To limit the download, you can adjust backup download settings.
>?
>- Backup download settings are supported in the following regions:
>Guangzhou, Shanghai, Beijing, Shenzhen, Chengdu, Chongqing, Nanjing, Hong Kong (China), Beijing Finance, Shanghai Finance, Shenzhen Finance, Toronto, Singapore, Silicon Valley, Frankfurt, Seoul, Mumbai, Bangkok, Moscow, and Tokyo.
>- How to enable backup download settings:
>  - Before November 9, 2021, you need to [submit a ticket](https://console.cloud.tencent.com/workorder/category) to enable this feature.
>  - Starting from November 9, 2021, this feature is available in the console.

## Setting Backup Download Rules
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), select **Database Backup** on the left sidebar, and select a region at the top.
2. On the **Download Settings** tab, view the backup download settings and click **Edit** to modify them.
>?Download over public network is enabled by default and when it is enabled, download over private network is also allowed.
>
![](https://qcloudimg.tencent-cloud.cn/raw/530fbf3e6c93eea06ff23e112cad84c0.png)
3. On the displayed page, set the download rules and click **OK**.
   - Download over public network:
     - Enabled: you cannot set any download rule.
     - Disabled: you can set the download rules by allowing or blocking specific IPs and VPCs.
   - Set the download rules:
     - If you don't specify any value, the condition won't take effect.
     - You should separate the values of an IP condition with commas.
     - You can enter IPs or IP ranges as the values of an IP condition.
     - If no IP and VPC requirements are set, there will be no limit on download over private network.
![](https://qcloudimg.tencent-cloud.cn/raw/7e0a4a48af62fdd643259f8902fcd95f.png)
4. After the configuration is completed, return to the **Download Settings** tab to view the rules that take effect.
![](https://qcloudimg.tencent-cloud.cn/raw/cb4ac45dcde8a57610b0eaec9075c6cb.png)

## Authorizing Sub-accounts to Set Backup Download Rules
By default, sub-accounts do not have the permission to set backup download rules for TencentDB for MySQL instances. Therefore, you need to create CAM policies to grant specific sub-accounts the permission.

[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583) is a web service provided by Tencent Cloud that helps you securely manage access to the resources under your Tencent Cloud account. CAM allows you to create, manage, or terminate users or user groups and control who is allowed to use your Tencent Cloud resources through identity and policy management.

When using CAM, you can associate a policy with a user or user group to allow or forbid them to use specified resources to complete specified tasks. For more information on CAM policies, please see [Syntax Logic](https://intl.cloud.tencent.com/document/product/598/10603).

### Authorizing sub-accounts
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam) with the root account, locate the target sub-user in the user list, and click **Authorize**.
![img](https://qcloudimg.tencent-cloud.cn/raw/89d7cf063bd376a0cc4f4db0c78e7e56.png)
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
- **statement** describes the details of one or more permissions. This element contains a permission or permission set of other elements such as effect, action, and resource. One policy has only one statement.
- **effect** is required. It describes the result of a statement. The result can be "allow" or an explicit "deny".
- **action** is required. It describes the allowed or denied operation. An operation can be an API (prefixed with “name”) or a feature set (a set of specific APIs prefixed with "permid").
- **resource** is required. It describes the details of authorization.

### API operations
In a CAM policy statement, you can specify any API operation from any service that supports CAM. APIs prefixed with `name/cdb:` should be used for TencentDB for MySQL. To specify multiple operations in a single statement, separate them with commas as shown below:
```
"action":["name/cdb:action1","name/cdb:action2"]
```
You can also specify multiple operations using a wildcard. For example, you can specify all operations whose names begin with "Describe" as shown below:
```
"action":["name/cdb:Describe*"]
```

### Resource path
The general format of resource paths is as follows:
```
qcs::service_type::account:resource
```
- service_type: describes the product abbreviation, such as `cdb` here.
- account: is the root account of the resource owner, such as "uin/326xxx46".
- resource: describes the detailed resource information of the specific service. Each TencentDB for MySQL instance (instanceId) is a resource.

The example is as follows:
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

### Customizing a CAM policy for setting MySQL backup download rules
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/policy) with the root account, select **Policies** on the left sidebar, and click **Create Custom Policy**.
![img](https://qcloudimg.tencent-cloud.cn/raw/4ddc463dc28ee48b9dd63d862fa41ea1.png)
2. In the pop-up dialog box, select **Create by Policy Generator**.
3. On the **Select Service and Action** page, select configuration items, click **Add Statement**, and click **Next**.
   - Service: select **TencentDB for MySQL**.
   - Action: select all APIs of setting MySQL backup download rules. For more information, see the [API documentation](https://intl.cloud.tencent.com/document/product/236/43327).
   - Resource: for more information, see [Resource Description Method](https://intl.cloud.tencent.com/document/product/598/10606). You can enter `*` to indicate that the backup download rules of TencentDB for MySQL instances in the specified region can be set.
![](https://qcloudimg.tencent-cloud.cn/raw/5372ae1d2ac16ff63b63fbf175f3fccf.png)
4. On the **Edit Policy** page, enter the **Policy Name** (such as `BackupDownloadRestriction`) as required and **Description** and click **Done**.
![](https://qcloudimg.tencent-cloud.cn/raw/3c5454e0da412c0e12beebb4b045979d.png)
5. Return to the policy list and you can view the custom policy just created.
![](https://qcloudimg.tencent-cloud.cn/raw/d242b34c0b9cad83d130444d84e205e0.png)

