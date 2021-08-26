
By default, sub-accounts have no permission to use TencentDB for MySQL Database Audit. Therefore, you need to create policies to allow sub-accounts to use it.
If you don't need to manage sub-accounts' access to resources related to TencentDB for MySQL Database Audit, you can ignore this document.

[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583) is a web-based Tencent Cloud service that helps you securely manage and control access to your Tencent Cloud resources. By using CAM, you can create, manage, and terminate users and user groups. You can manage identities and policies to allow specific users to access your Tencent Cloud resources.

When using CAM, you can associate a policy with a user or user group to allow or forbid them to use specified resources to complete specified tasks. For more information on CAM policies, please see [Syntax Logic](https://intl.cloud.tencent.com/document/product/598/10603).


## Authorizing Sub-account
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam) as a root account, select the target sub-user in the user list, and click **Authorize**.
![](https://main.qcloudimg.com/raw/a406ba643c22f2733699cf881ab336fb.png)
2. In the pop-up window, select the **QcloudCDBFullAccess** or **QcloudCDBInnerReadOnlyAccess** preset policy and click **OK** to complete the authorization.
>?MySQL Database Audit is a module in TencentDB for MySQL, so the above two preset policies of TencentDB for MySQL already cover the permission policies required by it. If the sub-user only needs the permission to use this module, please see [Custom MySQL Database Audit Policy](#zdymsjksjcl).
>
![](https://main.qcloudimg.com/raw/8500ea99c00fd496139e8535f45dadd2.png)


## [Policy Syntax](id:clyf)
The CAM policy for MySQL Database Audit is described as follows:
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
- **statement** describes the details of one or more permissions. It contains a permission or permission set of multiple other elements such as `effect`, `action`, and `resource`. One policy has only one `statement`.
- **effect** is required. It describes the result of a statement. The result can be "allow" or an "explicit deny".
- **action** is required. It describes the allowed or denied action (operation). An operation can be an API (prefixed with "name") or a feature set (a set of specific APIs prefixed with "permid").
- **resource** is required. It describes the details of authorization.


## API Operation
In a CAM policy statement, you can specify any API operation from any service that supports CAM. APIs prefixed with `name/cdb:` should be used for Database Audit. To specify multiple operations in a single statement, separate them with commas as shown below:
```
"action":["name/cdb:action1","name/cdb:action2"]
```

You can also specify multiple operations by using a wildcard. For example, you can specify all operations beginning with "Describe" in the name as shown below:
```
"action":["name/cdb:Describe*"]
```


## Resource Path
Resource paths are generally in the following format:
```
qcs::service_type::account:resource
```

- service_type: describes the product abbreviation, such as `cdb` here.
- account: describes the root account of the resource owner, such as `uin/326xxx46`.
- resource: describes the detailed resource information of the specific service. Each TencentDB for MySQL instance (instanceId) is a resource.

Example:
```
 "resource": ["qcs::cdb::uin/326xxx46:instanceId/cdb-kf291vh3"]
```
Here, `cdb-kf291vh3` is the ID of the TencentDB for MySQL instance resource, i.e., the `resource` in the CAM policy statement.

## Example
The following example only shows the usage of CAM. For the complete list of MySQL Database Audit APIs, please see the [API documentation](https://cloud.tencent.com/document/product/236/45460).

```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "name/cdb: DescribeAuditRules"
            ],
            "resource": [
                "*"
            ]
        },
        {
            "effect": "allow",
            "action": [
                "name/cdb: CreateAuditPolicy"
            ],
            "resource": [
                "*"
            ]
        },
       
        {
            "effect": "allow",
            "action": [
                "name/cdb: DescribeAuditLogFiles"
            ],
            "resource": [
                "qcs::cdb::uin/326xxx46:instanceId/cdb-kf291vh3"
            ]
        }
    ]
}
```

## [Custom MySQL Database Audit Policy](id:zdymsjksjcl)
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/policy) as the root account and click **Create Custom Policy** in the policy list.
![](https://main.qcloudimg.com/raw/772bd2ef82786ef54086307849606b9d.png)
2. In the pop-up window, select **Create by Policy Generator**.
3. On the **Select Service and Action** page, select configuration items, click **Add Statement**, and click **Next**.
 - Service: select **TencentDB for MySQL**.
 - Action: select all APIs of MySQL Database Audit. For more information, please see the [API documentation](https://cloud.tencent.com/document/product/236/45449).
  - Resource: for more information, please see [Resource Description Method](https://intl.cloud.tencent.com/document/product/598/10606). You can enter `*` to indicate that the audit logs of all TencentDB for MySQL instances can be manipulated.
![](https://main.qcloudimg.com/raw/ebd4dd9cc00e6caaac6c59ba397fb842.png)
4. On the **Edit Policy** page, enter the **Policy Name** (such as `SQLAuditFullAccess`) as required and **Description** and click **Done**.
![](https://main.qcloudimg.com/raw/cb5d0db2683cd54114c5d29685cd1da4.png)
5. Return to the policy list and you can view the custom policy just created.
![](https://main.qcloudimg.com/raw/050e310f11386c1b795410150af73b52.png)

