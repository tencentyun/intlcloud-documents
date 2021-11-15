
## [CAM Policy Syntax](id:yufa)
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
- **statement** describes the details of one or more permissions. It contains a permission or permission set of multiple other elements such as `effect`, `action`, `resource`, and `condition`. One policy has only one `statement`.
 - **effect** is required. It describes the result of a statement. The result can be "allow" or an "explicit deny".
 - **action** is required. It describes the allowed or denied operation. An operation can be an API or a feature set (a set of specific APIs prefixed with "permid").
 - **resource** is required. It describes the details of authorization. A resource is described in a six-segment format. Detailed resource definitions vary by product.
 - **condition** is required. It describes the condition for the policy to take effect. A condition consists of operator, action key, and action value. A condition value may contain information such as time and IP address. Some services allow you to specify additional values in a condition.

## [TDSQL-C Operations](id:caozuo)
In a CAM policy statement, you can specify any API operation from any service that supports CAM. APIs prefixed with `cynosdb:` should be used for TDSQL-C, such as `cynosdb:DescribeClusters` or `cynosdb:ResetAccountPassword`.
To specify multiple operations in a single statement, separate them with commas as shown below:
```
"action":["cynosdb:action1","cynosdb:action2"]
```
You can also specify multiple operations by using a wildcard. For example, you can specify all operations beginning with "Describe" in the name as shown below:
```
"action":["cynosdb:Describe*"]
```
If you want to specify all operations in TDSQL-C, use the `*` wildcard as shown below:
```
"action":["cynosdb:*"]
```

## [TDSQL-C Resource Path](id:lujing)
Each CAM policy statement has its own applicable resources.
Resource paths are generally in the following format:
```
qcs:project_id:service_type:region:account:resource
```
- **project_id**: describes the project information, which is only used to enable compatibility with legacy CAM logic and can be left empty.
- **service_type**: describes the product abbreviation such as `cynosdb`.
- **region**: describes the region information, such as `bj`.
- **account**: describes the root account of the resource owner, such as `uin/12345678`.
- **resource**: describes the detailed resource information of each product, such as `instance/clusterId` or `instance/*`.

For example, you can specify a resource for a specific cluster (cynosdbmysql-123abc) in a statement as shown below:
```
"resource":[ "qcs::cynosdb:bj:uin/12345678:instance/cynosdbmysql-123abc"]
```
You can also use the `*` wildcard to specify it for all clusters that belong to a specific account as shown below:
```
"resource":[ "qcs::cynosdb:bj:uin/12345678:instance/*"]
```
If you want to specify all resources or a specific API operation does not support resource-level permission control, you can use the `*` wildcard in the `resource` element as shown below:
```
"resource": ["*"]
```
To specify multiple resources in one policy, separate them with commas. In the following example, two resources are specified:
```
"resource":["resource1","resource2"]
```

The table below describes the resources that can be used by TDSQL-C and the corresponding resource description methods, where words prefixed with `$` are placeholders, `region` refers to a region, and `account` refers to an account ID.

| Resource | Resource Description Method in Authorization Policy |
| -------- | -------------------------------------------------- |
| Cluster     | `qcs::cynosdb:$region:$account:instance/$clusterId` |
| VPC      | `qcs::vpc:$region:$account:vpc/$vpcId`               |
| Security group   | `qcs::cvm:$region:$account:sg/$sgId`             |
