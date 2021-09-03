<span id = "clyf"></span>
### Policy Syntax
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
- **statement** describes the details of one or more permissions, and therefore contains the permission(s) other elements such as `effect`, `action`, `resource`, and `condition`. One policy has only one `statement`.
 - **effect** is required. It describes the result of a statement. The result can be "allow" or an explicit "deny".
 - **action** is required. It describes the allowed or denied operation. An operation can be an API or a feature set (a set of specific APIs prefixed with "permid").
 - **resource** is required. It describes the details of authorization. A resource is described in a six-segment format. Detailed resource definitions vary by product.
 - **condition** describes the condition for the policy to take effect. Conditions consist of operators, operation keys, and operation values. PostgreSQL currently does not support special conditions, so this element can be left empty.

<span id = "cz"></span>
### PostgreSQL Operations
You can use CAM policy statements to authorize any API operations for any services that support CAM. To authorize PostgreSQL operations, please specify the APIs prefixed with "postgres:", such as "postgres:DescribeDBInstances" and "postgres:DescribeDBInstanceAttribute".
To specify multiple operations in a single statement, separate them with commas as shown below:
```
"action":["postgres:action1","postgres:action2"]
```

You can also specify multiple operations using a wildcard. For example, you can specify all operations whose names begin with "Describe" as shown below:
```
"action":["postgres:Describe*"]
```

To specify all PostgreSQL operations, use the wildcard (*) as shown below:
```
"action":["postgres:*"]
```

<span id = "zylj"></span> 
### PostgreSQL Resource Paths
Each CAM policy statement for PostgreSQL is resource-specific.
The general form of a resource path is as follows:
```
qcs:project_id:service_type:region:account:resource
```
**project_id** describes the project information, which is only used to enable compatibility with legacy CAM logic and can be left empty.
**service_type** describes the abbreviated service name, such as "postgres".
**region** describes the [region information](https://intl.cloud.tencent.com/document/product/213/6091), such as "ap-shanghai".
**account**: the root account information of the resource owner (which is the "Account ID" on the [Account Information](https://console.cloud.tencent.com/developer) page), such as "164xxx472".
**resource** describes detailed resource information of each product, such as "DBInstanceId/postgres-0xssvm8e" or "DBInstanceId/\*". The table below describes the resources that can be used by PostgreSQL and the corresponding resource description methods.

| Resource | Resource Description Method in Access Policies |
| ---- | ------------------------------------------------------- |
| Instance | qcs::postgres:$region:$account:DBInstanceId/$DBInstanceId |

For example, you can specify an instance (instance ID: postgres-0xssvm8e) in the statement as shown below:
```
"resource":[ "qcs::postgres:ap-shanghai:164xxx472:DBInstanceId/postgres-0xssvm8e"]
```

You can also use the wildcard (*) to specify all instances in the Shanghai region that belong to a specific account as shown below:
```
"resource":[ "qcs::postgres:ap-shanghai:164xxx472:DBInstanceId/*"]
```

If you want to specify all resources or if a specific API operation does not support resource-level permission control, you can use the wildcard (*) in the `resource` element as shown below:
```
"resource": ["*"]
```

To specify multiple resources in a single statement, separate them with commas. In the following example, we specified two instances:
```
"resource":["qcs::postgres::164xxx472:DBInstanceId/postgres-0xf1f41e","qcs::postgres::164xxx472:DBInstanceId/postgres-0xssvm8e"]
```
