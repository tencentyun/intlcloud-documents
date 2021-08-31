<span id = "gzyhsq"></span>
## Authorizing a Sub-User
1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam) with the root account, select the target sub-user in the user list, and click **Authorize**.
![](https://main.qcloudimg.com/raw/8c15b3841ea1c3efdc123028d284c330.png)
2. In the pop-up dialog box, select a preset policy and click **OK** to complete the authorization.  
 - QcloudDMCFullAccess: full access to Database Management Console (DMC). It grants you permissions to use all DMC features, including adding or removing a TencentDB instance, logging in to a database, and so on.
 - QcloudDMCReadOnlyAccess: read-only access to DMC. It grants you permissions to view DMC pages but not to create any tasks.


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

- **version** is required. Currently, only the value "2.0" is allowed.
- **statement** describes the details of one or more permissions, and therefore contains the permission(s) of other elements such as `effect`, `action`, `resource`, and `condition`. One policy has only one `statement`.
- **effect** is required. It describes the result of a statement. The result can be an "allow" or an explicit "deny".
- **action** is required. It describes the allowed or denied operation. An operation can be an API (prefixed with "dmc:").
- **resource** is required. It describes the details of authorization. A resource is described in a six-segment format. Detailed resource definitions vary by product.
- **condition** is required. It describes the condition for the policy to take effect. Conditions consist of operators, operation keys, and operation values. A condition value may contain information such as time and IP address. Some services allow you to specify additional values in a condition.

<span id = "cz"></span>
## DMC Operations
You can use DMC policy statements to authorize any API operations for any services that support DMC. To authorize DMC operations, please specify the APIs prefixed with "dmc:", such as "dmc:DescribeSlowLogTopSqls" and "dmc:DescribeSlowLogTimeSeriesStats".

To specify multiple operations in a single statement, separate them with commas as shown below:
```
"action":["dmc:action1","dmc:action2"]
```
You can also specify multiple operations using a wildcard. For example, you can specify all operations whose names begin with "Describe" as shown below:
```
"action":["dmc:Describe*"]
```
To specify all DMC operations, use the wildcard (*) as shown below:
```
"action":["dmc:*"]
```


<span id = "zylj"></span> 
## Resources That Can Be Manipulated by DMC
Each CAM policy statement for DMC is resource-specific. DMC allows you to operate TencentDB resources added to DMC.
The format is shown below:
```
qcs:project_id:service_type:region:account:resource
```
- project_id: describes the project information and is only used to enable compatibility with legacy CAM logic. It can be left empty.
- service_type: product abbreviation, such as "dmc".
- region: region information, such as "ap-guangzhou".
- account: the root account information of the resource owner, such as "uin/65xxx763".
- resource: detailed resource information of each product, such as "instance/instance_id1" or "instance/*".

For example, you can specify an instance (dmc-k05xdcta) in the statement as shown below:
```
"resource":[ "qcs::dmc:ap-guangzhou:uin/65xxx763:instance/dmc-k05xdcta"]
```
You can also use the wildcard (*) to specify all instances that belong to a specific account as shown below:
```
"resource":[ "qcs::dmc:ap-guangzhou:uin/65xxx763:instance/*"]
```
If you want to specify all resources or if a specific API operation does not support resource-level permission control, you can use the wildcard (*) in the `resource` element as shown below:
```
"resource": ["*"]
```
To specify multiple resources in a single statement, separate them with commas. In the following example, we specified two resources:
```
"resource":["resource1","resource2"]
```

The table below describes the resources that can be used by TencentDB and the corresponding resource description methods, where words prefixed with "$" are placeholders, "region" refers to a region, and "account" refers to an account ID.

| Resource | Resource Description Method in Access Policies |
| :--- | :----------------------------------------------------- |
| Instance | ```qcs::dmc:$region:$account:instance/$instanceId``` |
