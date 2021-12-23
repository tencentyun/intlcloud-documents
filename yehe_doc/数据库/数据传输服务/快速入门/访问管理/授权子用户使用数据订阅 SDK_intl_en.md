## Overview 
You can use a sub-user to create and manage subscription tasks. You can also use the `AccessKey` and `AccessKeySecret` of a sub-user in the SDK demo for data subscription. 

When using Cloud Access Management (CAM), you can associate a policy with a user or user group to allow or forbid them to use specified resources to complete specified tasks. For more information on CAM policies, see [Syntax Logic](https://intl.cloud.tencent.com/document/product/598/10603). 

## Authorizing Sub-user
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam).
2. On the **User** > **User List** page, find the sub-user whom you want to authorize and click **Authorize** in the **Operation** column on the right as shown below:
    ![](https://qcloudimg.tencent-cloud.cn/raw/d8e55e9eb52693885c08586115770b6d.png)
3. In the pop-up window, search for "DTS" and select the permission to be granted.
    - QcloudDTSFullAccess: it indicates to grant the read and write permissions.
    - QcloudDTSReadOnlyAccess: it indicates to grant the read-only permissions.
![](https://qcloudimg.tencent-cloud.cn/raw/8ea8cea9907f9b22cc33896d01d9ac56.png)
4. Click **OK** to complete authorization.

## Policy Syntax
The CAM policy for DTS is described as follows:
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
>?As DTS needs to manipulate your database, you need to grant the sub-account access to the database resources involved in DTS tasks separately (the read permission, i.e., `Describe\*` is required). This authorization operation is not included in this document.
- **effect** is required. It describes the result of a statement. The result can be "allow" or an "explicit deny".
```
"effect": "allow"
```
- **action** is required. It describes the allowed or denied action (operation). An operation can be an API (prefixed with "name") or a feature set (a set of specific APIs prefixed with "permid").
- **resource** is required. It describes the details of authorization.

## DTS Operations
In a CAM policy statement, you can specify any API operation from any service that supports CAM. APIs prefixed with `name/dts:` should be used for DTS. To specify multiple operations in a single statement, separate them with commas as shown below:
```
"action":["name/dts:action1","name/dts:action2"]
```

You can also specify multiple operations by using a wildcard. For example, you can specify all operations beginning with "Describe" in the name as shown below:
```
"action":["name/dts:Describe*"]
```

If you want to specify all operations in DTS, use the `*` wildcard as shown below:
```
"action":["name/dts:*"]
```

## DTS Resource Path
Resource paths are generally in the following format:
```
 qcs::service_type::account:resource
```
- service_type: describes the product abbreviation, such as `dts` here.
- account: describes the root account of the resource owner, such as `uin/32xxx546`.
- resource: describes the detailed resource information of the specific service. Each DTS task (`task`) is a resource.

Below is a sample:
```
 "resource": ["qcs::dts::uin/32xxx546:task/dts-kf291vh3"]
```
Here, `dts-kf291vh3` is the ID of the DTS task, i.e., the `resource` in the CAM policy statement.

## Sample
>?The following example only shows the usage of CAM. For the complete process of a DTS task and the corresponding APIs, see [Introduction](https://intl.cloud.tencent.com/document/product/571/18135).

```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "name/dts:DescribeAccessKeys"
            ],
            "resource": [
                "*"
            ]
        },
        {
            "effect": "allow",
            "action": [
                "name/dts:CreateAccess*"
            ],
            "resource": [
                "*"
            ]
        },
        {
            "effect": "allow",
            "action": [
                "name/dts:DescribeMigrateJobs"
            ],
            "resource": [
                "qcs::dts::uin/32xxx546:task/dts-kf291vh3"
            ]
        },
        {
            "effect": "allow",
            "action": [
                "name/dts:CreateMigrateCheckJob"
            ],
            "resource": [
                "qcs::dts::uin/32xxx546:task/dts-kf291vh3"
            ]
        }
    ]
}
```

