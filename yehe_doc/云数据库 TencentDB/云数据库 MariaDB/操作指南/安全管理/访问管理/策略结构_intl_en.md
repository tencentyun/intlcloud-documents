## Policy Syntax
CAM policy configuration example:
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


- **version** is required. Currently, only "2.0" is allowed. (This value actually represents the version of TencentCloud APIs acceptable to CAM.)
- **statement** describes the details of one or more permissions. This element contains a permission or permission set of other elements such as effect, action, resource, and condition. One policy has only one statement.
 - **action** describes the allowed or denied action. An action entered here is a string prefixed with "mariadb:" and suffixed with an [TencentDB for MariaDB API](https://cloud.tencent.com/document/api/237/16144). This element is required.
 2. **resource** describes the details of authorization. A resource is described in a six-segment format. Detailed resource definitions vary by product. For more information on how to specify a resource, please see the documentation for the product whose resources you are writing a statement for. This element is required.
 3. **condition** describes the condition for the policy to take effect. A condition consists of operator, action key, and action value. A condition value may contain information such as time and IP address. Some services allow you to specify additional values in a condition. This element is required.
 4. **effect** describes whether the result produced by the statement is "allowed" (allow) or "denied" (deny). This element is required.

>The API keyword in CAM of TencentDB for MariaDB is "mariadb".

## Operations in TencentDB
In a TencentDB policy statement, you can specify any API operation from any service that supports TencentDB. APIs prefixed with "mariadb:" should be used for TencentDB, such as `mariadb: mariadb:CloseDBExtranetAccess` (disabling public network access).

- To specify multiple operations in a single statement, separate them with commas as shown below:
```
"action":["mariadb:action1","mariadb:action2"]
```
2. You can also specify multiple operations using a wildcard. For example, you can specify all operations beginning with "Describe" in name as shown below:
```
"action":["mariadb:Describe*"]
```
3. If you want to specify all operations in TencentDB, use a wildcard as shown below:
```
"action"：["mariadb:*"]
```

## TencentDB Resources

Each CAM policy statement has its own resources.
Resources are generally in the following format:
```
qcs:project_id:service_type:region:account:resource
```

- **project_id** describes the project information, which is only used to enable compatibility with legacy CAM logic and can be left empty.
- **service_type** describes the product abbreviation such as TencentDB for MariaDB.
- **region** describes the region information, such as ap-guangzhou. For more information, please see [Regions](https://cloud.tencent.com/document/api/213/15708).
- **account** is the root account of the resource owner, such as uin/653339763.
- **resource** describes detailed resource information of each product, such as instance/instance_id1 or instance/*.

For example:

- You can specify a resource for a specific instance (tdsql-k05xdcta) in a statement as shown below:
```
"resource":[ "qcs::mariadb:ap-guangzhou:uin/653339763:instance/tdsql-k05xdcta"]
```
2. You can also use the wildcard "*" to specify it for all instances that belong to a specific account as shown below:
```
"resource":[ "qcs::mariadb:ap-guangzhou:uin/653339763:instance/*"]
```
3. If you want to specify all resources or a specific API operation does not support resource-level permission control, you can use the wildcard "*" in the "Resource" element as shown below:
```
"resource": ["*"]
```
4. To specify multiple resources in a single command, separate them with commas. Below is an example where two resources are specified:
```
"resource":["resource1","resource2"]
```

The table below describes the resources that can be used by TencentDB and the corresponding resource description methods.
In the table, words prefixed with $ are placeholders.

- `project` is project ID.
- `region` is region.
- `account is account ID.

| Resource | Resource Description Method in Authorization Policy |
|:-------|:-------|
| Instance |  ```qcs::mariadb:$region:$account:instance/$instanceId```|
