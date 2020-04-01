<span id = "celueyufa"></span>
## Policy Syntax
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
- **version** is required. Currently, only "2.0" is allowed.
- **statement** describes the details of one or more permissions. This element contains a permission or permission set of other elements such as effect, action, resource, and condition. One policy has only one statement.
 - **effect** describes whether the result produced by the statement is "allowed" (allow) or "denied" (deny). This element is required.
 - **action** describes the allowed or denied action (operation). An operation can be an API (prefixed with "cdb:"). This element is required.
 - **resource** describes the details of authorization. A resource is described in a six-segment format. Detailed resource definitions vary by product. This element is required.
 - **condition** describes the condition for the policy to take effect. A condition consists of operator, action key, and action value. A condition value may contain information such as time and IP address. Some services allow you to specify additional values in a condition. This element is required.

<span id = "caozuo"></span>
## TencentDB Operations
In a TencentDB policy statement, you can specify any API action from any service that supports TencentDB. APIs prefixed with "cdb:" should be used for TencentDB, such as cdb:CreateDBInstance or cdb:CreateAccounts.

To specify multiple operations in a single statement, separate them with commas, as shown below:
```
"action":["cdb:action1","cdb:action2"]
```
You can also specify multiple operations using a wildcard. For example, you can specify all operations beginning with "Describe" in name, as shown below:
```
"action":["cdb:Describe*"]
```
If you want to specify all operations in TencentDB, use a wildcard as shown below:
```
"action"：["cdb:*"]
```

<span id = "ziyuanlujing"></span> 
## TencentDB Resources
Each CAM policy statement has its own resources.
Resources are generally in the following format:
```
qcs:project_id:service_type:region:account:resource
```
- **project_id** describes the project information, which is only used to enable compatibility with legacy CAM logic and can be left empty.
- **service_type** describes the product abbreviation such as COS.
- **region** describes the region information, such as ap-guangzhou.
- **account** is the root account of the resource owner, such as uin/653339763.
- **resource** describes detailed resource information of each product, such as instanceId/instance_id1 or instanceId/*.


For example, you can specify a resource for a specific instance (cdb-k05xdcta) in a statement as shown below:
```
"resource":[ "qcs::cdb:ap-guangzhou:uin/653339763:instanceId/cdb-k05xdcta"]
```
You can also use the wildcard "*" to specify it for all instances that belong to a specific account as shown below:
```
"resource":[ "qcs::cdb:ap-guangzhou:uin/653339763:instanceId/*"]
```
If you want to specify all resources or a specific API operation does not support resource-level permission control, you can use the wildcard "*" in the "resource" element as shown below:
```
"resource": ["*"]
```
To specify multiple resources in a single command, separate them with commas. Below is an example where two resources are specified:
```
"resource":["resource1","resource2"]
```

The table below describes the resources that can be used by TencentDB and the corresponding resource description methods, where words prefixed with $ are placeholders, `project` refers to a project ID, `region` refers to a region, and `account` refers to an account ID.

| Resource | Resource Description Method in Authorization Policy |
|:-------|:-------|
| Instance |  ```qcs::cdb:$region:$account:instanceId/$instanceId```|
|VPC|  ```qcs::vpc:$region:$account:vpc/$vpcId```|
| Security group |  ```qcs::cvm:$region:$account:sg/$sgId```|
