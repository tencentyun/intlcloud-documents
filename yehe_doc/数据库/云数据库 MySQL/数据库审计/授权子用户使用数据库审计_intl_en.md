By default, sub-users have no permission to use TencentDB for MySQL database audit. Therefore, you need to create policies to allow sub-users to use it.
If you don't need to manage sub-users' access to resources related to TencentDB for MySQL Database Audit, you can ignore this document.

Cloud Access Management (CAM) is a web-based Tencent Cloud service that helps you securely manage and control access permissions to your Tencent Cloud resources. Using CAM, you can create, manage, and terminate users (groups), and control the Tencent Cloud resources that can be used by the specified user through identity and policy management.

You can use CAM to bind a user or user group to a policy which allows or denies them access to specified resources to complete specified tasks.

## Authorizing Sub-User
1. Log in to the CAM console with the root account, locate the target sub-user in the user list, and click **Authorize**.
2. In the pop-up window, select the **QcloudCDBFullAccess** or **QcloudCDBInnerReadOnlyAccess** preset policy and click **OK** to complete the authorization.
>?MySQL Database Audit is a module in TencentDB for MySQL, so the above two preset policies of TencentDB for MySQL already cover the permission policies required by it. If the sub-user only needs the permission to use this module, see [Custom MySQL Database Audit Policy](#zdymsjksjcl).
>

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
 
- service_type: Describes the product abbreviation, such as `cdb` here.
- account: Describes the root account of the resource owner, such as `uin/326xxx46`.
- resource: Describes the detailed resource information of the specific service. Each TencentDB for MySQL instance (instanceId) is a resource.

Below are examples:
```
 "resource": ["qcs::cdb::uin/326xxx46:instanceId/cdb-kf291vh3"]
```
Here, `cdb-kf291vh3` is the ID of the TencentDB for MySQL instance resource, i.e., the `resource` in the CAM policy statement.

## Example
The following example only shows the usage of CAM.

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
            "action":[
                "name/cdb: CreateAuditPolicy"
            ],
            "resource": [
                "*"
            ]
        },
       
        {
            "effect": "allow",
            "action":[
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
1. Log in to the CAM console with the root account and click **Create Custom Policy** in the policy list.
2. In the pop-up dialog box, select **Create by Policy Generator**.
3. On the **Select Service and Action** page, select configuration items, and click **Next**.
 - Service: Select **TencentDB for MySQL**.
 - Action: Select all APIs of MySQL Database Audit.
 - Resource: Selecting all resources indicates that the audit logs of all TencentDB for MySQL instances can be manipulated.
 - Condition (optional): Set the conditions that must be met for the authorization to take effect.
4. On the **Bind User/Group/Role** page, enter the **Policy Name** (such as `SQLAuditFullAccess`) and **Description** as required, then click **Complete**.
5. Return to the policy list and you can view the custom policy just created.
