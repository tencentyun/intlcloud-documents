
## Policy Syntax

A CAM policy is as follows:

```json
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

- **version**: required. Currently, only "2.0" is allowed.
- **statement**: an element that describes the details on a permission or a permission set defined by other elements including effect, action, resource, and condition. One policy has only one statement.
  - **action**: describes the action to be allowed or denied. An action can be an API (prefixed with `gse:`) or a feature set (a set of specific APIs prefixed with `permid`). This element is required.
  - **resource**: describes the resource to which the permission applies. A resource is described in a six-segment format. Detailed resource definitions vary by product. For more information on how to specify a resource, see the documentation for the product whose resources you are writing a statement for. This element is required.
  - **condition**: describes the condition for the policy to take effect. A condition consists of operator, action key, and action value. A condition value may be time, IP address, etc. Some services allow you to specify additional values in a condition. This element is optional.
  - **effect**: describes whether the result produced by the statement is "allow" or "explicitly deny". This element is required.
  
<span id="test5"></span>
## GSE Operations

In a CAM policy statement, you can set `action` to any API for any Tencent Cloud service that supports CAM. For GSE APIs, prefix them with `gse:`, such as `gse:AddMatch` or `gse:AddRule`.
To specify multiple actions in a single statement, separate them with a comma as shown below:

```json
"action":["gse:action1","gse:action2"]
```

You can also specify multiple actions by using a wildcard, such as all actions that start with "Create" as shown below:

```json
"action":["gse:Create*"]
```

To specify all GSE actions, use only the wildcard `*` as follows:

```json
"action":["gse:*"]
```
<span id="test6"></span>
## GSE Resource Paths

Each CAM policy statement for GSE is resource-specific with a resource path as shown below:

```json
qcs:project_id:service_type:region:account:resource
```

- **project_id**: describes the project information and is only used to enable compatibility with legacy CAM logic. It can be left empty.
- **service_type**: describes the product’s abbreviation, such as `gse`.
**region**: region information, for example, `bj`.
**account**: the root account of the resource owner, for example, `uin/110702656`.
- **resource**: describes details on the GSE resource, such as `fleet/fleet-28a9refi-ur5pe34j` or `fleet/*`.

For example, you can grant a sub-account the access to the fleet “fleet-28a9refi-ur5pe34j” in Beijing region under your root account by specifying it in the statement, as shown below:

```json
"resource":[ "qcs::gse:bj:uin/110702656:fleet/fleet-28a9refi-ur5pe34j"]
```

You can also use the wildcard "*" to specify all resources of a certain type in a specific account as shown below:

```json
"resource":[ "qcs::gse::uin/110702656:fleet/*"]
```

If you want to specify all resources or if a specific API does not support resource-level permission control, you can set the value of `resource` to `*` as shown below:

```json
"resource": ["*"]
```

To specify multiple resources in one policy, separate them with a comma. In the following example, two resources are specified:

```json
"resource":["resource1","resource2"]

```



