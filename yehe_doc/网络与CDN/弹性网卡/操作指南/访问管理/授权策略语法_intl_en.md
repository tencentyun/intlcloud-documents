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

- `version`: (Required) It must be `2.0` for now.
- `statement`: It describes the details of one or more permissions. It contains `effect`, `action`, `resource`, and `condition`. One policy can have only one `statement`.
 1. `action`: (Required) It specifies whether to allow or deny the operation. The operation can be an API (prefixed with `name`) or a feature set (a group of APIs, prefixed with `permid`). 
 2. `resource`: (Required) It describes the details of an authorization. A resource is described in a six-part format. Detailed resource definitions vary by product. For more information on how to specify a resource, see the corresponding documentation for the product for which you want to write a resource statement.
 3. `condition`: (Optional) It describes the condition for the policy to take effect. A condition consists of an operator, an action key, and an action value. A condition value may contain information such as time and IP address. Some services allow you to specify additional values in a condition. 
 4. `effect`: (Required) It describes whether the statement result is `allow` or `deny`. 

## ENI Operations[](id:caozuo)
In the statement of a CAM policy, you can specify any API operation from any service that supports CAM. For VPC, use APIs with the prefix `name/vpc:`, for example, `name/vpc:Modify`, or `name/vpc:CreateNetworkInterface`.
To specify multiple operations in a single statement, separate them with commas, as shown below:
```
"action":["name/vpc:action1","name/vpc:action2"]
```
You can also specify multiple operations by using a wildcard, such as all operations that start with "Modify" as shown below:
```
"action":["name/vpc:Modify*"]
```
To specify all operations in a VPC, use a wildcard (*) as follows:
```
"action"：["name/vpc:*"]
```

## ENI Resource Path[](id:ziyuanlujing)
Each CAM policy statement has its own applicable resources.
The general format of resource paths is as follows:
```
qcs:project_id:service_type:region:account:resource
```

- **project_id**: Describes the project information, which is only used to enable compatibility with legacy CAM logic and can be left empty.
- **service_type**: Abbreviation of the Tencent Cloud service, such as `VPC`.
- **region**: Region of the resource, for example, `bj`.
- **account**: Root account of the resource owner, such as `uin/164256472`.
- **resource**: Describes the resource details of each product, such as `eni/eni_id1` or `eni/*`.

For example, you can specify a specific instance (eni-abcdefgh) in the statement as follows:
```
"resource":[ "qcs::vpc:bj:uin/164256472:eni/eni-abcdefgh"]
```
You can also use the wildcard (*) to specify all instances that belong to a specific account as shown in the following: 
```
"resource":[ "qcs::vpc:bj:uin/164256472:eni/*"]
```
If you want to specify all resources or if a specific API operation does not support resource-level permission, you can use the wildcard (*) in the `resource` element as shown below:
```
"resource": ["*"]
```
To specify multiple resources in one policy, separate them with a comma. 
```
"resource":["resource1","resource2"]
```
