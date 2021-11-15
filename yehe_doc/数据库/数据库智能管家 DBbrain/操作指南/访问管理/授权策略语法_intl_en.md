<span id = "gzyhsq"></span>
## Authorizing a Sub-User
1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam) with the root account, select the target sub-user in the user list, and click **Authorize**.
![](https://main.qcloudimg.com/raw/8c15b3841ea1c3efdc123028d284c330.png)
2. In the pop-up dialog box, select a preset policy and click **OK** to complete the authorization.  
 - `QcloudDBBRAINFullAccess` (DBbrain full real and write access permission): an associated user can use all features provided by DBbrain, including viewing and creating tasks such as SQL insight task, health report, and compliance security report.
 - `QcloudDBBRAINReadOnlyAccess` (DBbrain read-only access permission): an associated user can only view DBbrain pages and cannot create tasks.
![](https://main.qcloudimg.com/raw/f191cefecfeddc444216fbe48f1fe00e.png)


<span id = "clyf"></span>
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
- **statement** describes the details of one or more permissions. It contains a permission or permission set of multiple other elements such as `effect`, `action`, `resource`, and `condition`. One policy has only one `statement`.
- **effect** describes whether the statement result is "allow" or "explicit deny". This element is required.
- **action** describes the allowed or denied operation. An operation can be an API (prefixed with "cdb:"). This element is required.
- **resource** describes the objects the statement covers. A resource is described in a six-segment format. Detailed resource definitions vary by product. This element is required.
- **condition** describes the condition for the policy to take effect. A condition consists of an operator, operation key, and operation value. A condition value may contain information such as time and IP address. Some services allow you to specify additional values in a condition. This element is required.

<span id = "cz"></span>
## DBbrain Operations
In a DBbrain policy statement, you can specify any API operation from any service that supports DBbrain. APIs prefixed with `dbbrain:` should be used for DBbrain, such as `dbbrain:DescribeSlowLogTopSqls` or `dbbrain:DescribeSlowLogTimeSeriesStats`.

To specify multiple operations in a single statement, separate them with commas as shown below:
```
"action":["dbbrain:action1","dbbrain:action2"]
```

You can also specify multiple operations by using a wildcard. For example, you can specify all the names of operations beginning with "Describe" as shown below:
```
"action":["dbbrain:Describe*"]
```

If you want to specify all operations in DBbrain, use the "*" wildcard as shown below:
```
"action":["dbbrain:*"]
```

<span id = "zylj"></span> 
## Resources that can be Manipulated by DBbrain
Each CAM policy statement has its own resources. DBbrain allows you to operate on TencentDB resources.
TencentDB resources generally have following format:
```
qcs:project_id:service_type:region:account:resource
```

- **project_id** describes the project information and is only used to enable compatibility with legacy CAM logic. It can be left empty.
- **service_type** describes the product’s abbreviation, such as `cdb`.
- **region** describes the region information, such as `ap-guangzhou`.
- **account** is the root account of the resource owner, such as `uin/653339763`.
- **resource** describes the detailed resource information of each product, such as `instanceId/instance_id1` or `instanceId/*`.

For example, you can specify a resource for a specific instance (cdb-k05xdcta) in a statement as shown below:
```
"resource":[ "qcs::cdb:ap-guangzhou:uin/653339763:instanceId/cdb-k05xdcta"]
```

You can also use the wildcard "*" to specify a resource for all instances that belong to a specific account as shown below:
```
"resource":[ "qcs::cdb:ap-guangzhou:uin/653339763:instanceId/*"]
```

If you want to specify all resources or if a specific API operation does not support resource-level permission control, you can use the wildcard "*" in the `resource` element as shown below:
```
"resource": ["*"]
```

To specify multiple resources in a single command, separate them with commas. Below is an example where two resources are specified:
```
"resource":["resource1","resource2"]
```

The table below describes the resources that can be used by TencentDB and the corresponding resource description methods, where words prefixed with $ are placeholders, `project` refers to a project ID, `region` refers to a region, and `account` refers to an account ID.

| Resource | Resource Description Method in Authorization Policy |
| :--- | :----------------------------------------------------- |
| Instance | ```qcs::cdb:$region:$account:instanceId/$instanceId``` |
