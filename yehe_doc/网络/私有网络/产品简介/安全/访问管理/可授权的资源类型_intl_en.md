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

- **version** is required. Currently, only the "2.0" value is allowed.
- **statement** describes the details of one or more permissions. This element contains a permission or permission set of other elements such as effect, action, resource, and condition. Each policy has one statement element.
 1. **action** describes the action to be allowed or denied. An action can be an API (described using the prefix "name") or a feature set (a set of specific APIs described with the prefix "permid"). This element is required.
 2. **resource** describes the details of authorization. A resource is described in a six-piece format. Detailed resource definitions vary by product. For more information on how to specify a resource, see the documentation for the product whose resources you are writing a statement for. This element is required.
 3. **condition** describes the condition for the policy to take effect. A condition consists of an operator, an action key, and an action value. A condition value may contain information such as the time and IP address. Some services allow you to specify additional values in a condition. This element is optional.
 4. **effect** describes whether the result produced by the statement is "allow" or "deny". This element is required.

## VPC Operations
In the statement of a CAM policy, you can specify any API action from any service that supports CAM. For VPC, use APIs with the prefix "name/vpc:", for example, name/vpc:Describe or name/vpc:CreateRoute.
To specify multiple actions in a single statement, separate them with commas, as shown below:
```
"action":["name/vpc:action1","name/vpc:action2"]
```

2. You can also specify multiple actions by using a wildcard. For example, you can specify all actions whose names begin with "Describe", as shown below:
```
"action":["name/vpc:Describe*"]
```

To specify all actions in VPC, use the wildcard "*" as follows:
```
"action": ["name/vpc:*"]
```

## VPC Resource Paths
Each CAM policy statement has its own resources.
The general format of a resource path is as follows:
```
****qcs**:project_id:service_type:region:account:resource**
```

- **project_id**: project information. This element is only used to enable compatibility with legacy CAM logic and can be left empty.
- **service_type**: the product abbreviation, such as VPC.
- **region**: region information, such as bj.
- **account**: the root account of the resource owner, such as uin/164256472.
- **resource**: resource details of each product, such as vpc/vpc_id1 or vpc/*.

For example, you can specify an instance (vpc-d08sl2zr in this case) in the statement, as shown below:
```
"resource":[ "qcs::vpc:bj:uin/164256472:instance/vpc-d08sl2zr"]
```

You can also use the wildcard "*" to specify all instances under a specific account, as shown below:
```
"resource":[ "qcs::vpc:bj:uin/164256472:instance/*"]
```

To specify all resources or if any API action does not support resource-level permissions, you can use the wildcard "*" in the Resource element, as shown below:
```
"resource": ["*"]
```

To specify multiple resources in one instruction, separate them with commas. In the following example, two resources are specified:
```
"resource":["resource1","resource2"]
```


The following table describes the resources that can be used by VPC and the corresponding methods of describing these resources.

In the following table, the words prefixed with "$" are all alternative names.
- `project` indicates the project ID.
- `region` indicates the region.
- `account` indicates the account ID.

| Resource | Resource Description Method in the Authorization Policy |
| ------ | ------------------------------------------ |
| VPC | qcs::vpc:$region:$account:vpc/$vpcId |
| Subnet | qcs::vpc:$region:$account:subnet/$subnetId |
| Security group | qcs::cvm:$region:$account:sg/$sgId |
| EIP | qcs::cvm:$region:$account:eip/* |
