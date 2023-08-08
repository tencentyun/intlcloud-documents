## [Policy syntax](id:celueyufa)
CAM policy:
```
{	 
        "version":"2.0", 
        "statement": 
        [ 
           { 
              "effect":"effect", 
              "action":["action"], 
              "resource":["resource"], 
               "condition": {"key":{"value"}} 
           } 
       ] 
} 
```
- **version** is required. Currently, only the value "2.0" is allowed.
- **statement** describes the details of one or more permissions. This element contains a permission or permission set of other elements such as `effect`, `action`, `resource`, and `condition`. One policy has only one statement.
 - **effect** is required. It describes whether the declaration result is `allow` or explicit `deny`.
 - **action** is required. It specifies whether to allow or deny the operation. The operation can be an API (prefixed with "cdb:").
 - **resource** is required. It describes the details of authorization. A resource is described in a six-segment format. Detailed resource definitions vary by product.
 - **condition** is required. It describes the condition for the policy to take effect. A condition consists of operator, action key, and action value. A condition value may contain information such as time and IP address. Some services allow you to specify additional values in a condition.

## [Operations in TencentDB](id:caozuo)
In a TencentDB policy statement, you can specify any API operation from any service that supports TencentDB. APIs prefixed with `cdb:` should be used for TencentDB, such as `cdb:CreateDBInstance` or `cdb:CreateAccounts`.

To specify multiple operations in a single statement, separate them by comma.
```
"action":["cdb:action1","cdb:action2"]
```
You can also specify multiple operations by using a wildcard. For example, you can specify all operations beginning with "Describe" in the name.
```
"action":["cdb:Describe*"]
```
To specify all operations in TencentDB, use the `*` wildcard.
```
"action":["cdb:*"]
```

## [Resources in TencentDB](id:ziyuanlujing)
Each CAM policy statement has its own applicable resources.
Resources are generally in the following format:
```
qcs:project_id:service_type:region:account:resource
```
- **project_id** describes the project information, which is only used to enable compatibility with legacy CAM logic and can be left empty.
- **service_type** describes the product abbreviation such as `cdb`.
- **region** describes the region information, such as `ap-guangzhou`.
- **account** describes the root account of the resource owner, such as `uin/65xxx763`.
- **resource** describes detailed resource information of each product, such as `instanceId/instance_id1` or `instanceId/*`.


For example, you can specify a resource for a specific instance (cdb-k05xdcta) in a statement.
```
"resource":[ "qcs::cdb:ap-guangzhou:uin/65xxx763:instanceId/cdb-k05xdcta"]
```
You can also use the wildcard "*" to specify it for all instances that belong to a specific account.
```
"resource":[ "qcs::cdb:ap-guangzhou:uin/65xxx763:instanceId/*"]
```
If you want to specify all resources or a specific API operation does not support resource-level permission control, you can use the `*` wildcard in the `resource` element.
```
"resource": ["*"]
```
To specify multiple resources in one policy, separate them by comma. In the following example, two resources are specified:
```
"resource":["resource1","resource2"]
```

The table below describes the resources that can be used by TencentDB and the corresponding resource description methods, where words prefixed with `$` are placeholders, `region` refers to a region, and `account` refers to an account ID.

| Resource | Resource Description Method in Authorization Policy |
|-------|-------|
| Instance |  `qcs::cdb:$region:$account:instanceId/$instanceId`|
| VPC |  `qcs::vpc:$region:$account:vpc/$vpcId`|
| Security group |  `qcs::cvm:$region:$account:sg/$sgId`|
