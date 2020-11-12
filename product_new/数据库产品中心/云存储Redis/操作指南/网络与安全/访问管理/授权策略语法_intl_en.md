<span id="yufa"></span>

## CAM Policy Syntax

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

- **version**: it is required. Currently, only "2.0" is allowed.
- **statement**: describes the details of one or more privileges. This element contains a privilege or privilege set of other elements such as effect, action, resource, and condition. One policy has only one statement.
 - **effect**: describes whether the result produced by the statement is "allowed" (allow) or "denied" (deny). This element is required.
 - **action**: describes the allowed or denied operation. An operation can be an API or a feature set (a set of specific APIs prefixed with "permid"). This element is required.
 - **resource**: describes the details of authorization. A resource is described in a six-piece format. Detailed resource definitions vary by product. This element is required.
 - **condition**: describes the condition for the policy to take effect. A condition consists of operator, action key, and action value. A condition value may contain information such as time and IP address. Some services allow you to specify additional values in a condition. This element is optional.

<span id="caozuo"></span>

## Redis Operations

In a CAM policy statement, you can specify any API operation from any service that supports CAM. APIs prefixed with "redis:" should be used for Redis, such as redis:CreateRedis or redis:DeleteInstance.
To specify multiple actions in a single statement, separate them with commas, as shown below:

```
"action":["redis:action1","redis:action2"]
```

You can also specify multiple actions using a wildcard. For example, you can specify all actions whose name begins with "Describe", as shown below:

```
"action":["redis:Describe*"]
```

If you want to specify all operations in Redis, use a wildcard "*" as shown below:

```
"action"：["redis:*"]
```

<span id="lujing"></span>

## Redis Resource Path

Each CAM policy statement has its own resources.
The general form of resource path is as follows:

```
qcs:project_id:service_type:region:account:resource
```

- **project_id**: describes the project information, which is only used to enable compatibility with legacy CAM logic and can be left empty.
- **service_type**: describes the product abbreviation such as Redis.
  -**region**: region information, for example, bj.
- **account**: the root account of the resource owner, such as uin/653339763.
- **resource**: describes detailed resource information of each product, such as instanceId/instance_id1 or instanceId/*.

For example, you can specify a resource for a specific instance (crs-psllioc8) in a statement as shown below:

```
"resource":[ "qcs::redis:bj:uin/12345678:instance/crs-psllioc8"]
```

You can also use the wildcard "*" to specify all instances that belong to a specific account as shown below:

```
"resource":[ "qcs::redis:bj:uin/12345678:instance/*"]
```

If you want to specify all resources or if a specific API operation does not support resource-level permission control, you can use the wildcard "*" in the "resource" element as shown below:

```
"resource": ["*"]
```

To specify multiple resources in a single command, separate them with commas. Below is an example where two resources are specified:

```
"resource":["resource1","resource2"]

```

The table below describes the resources that can be used by Redis and the corresponding resource description methods, where words prefixed with $ are placeholders, "region" refers to a region, and "account" refers to an account ID.

| Resource       | Resource Description Method in Authorization Policy |
| -------------- | --------------------------------------------------- |
| Instance       | `qcs::redis:$region:$account:instance/$instanceId`  |
| VPC            | `qcs::vpc:$region:$account:vpc/$vpcId`              |
| Security group | `qcs::cvm:$region:$account:sg/$sgId`                |
