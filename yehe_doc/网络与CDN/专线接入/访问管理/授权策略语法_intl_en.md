This document describes CAM access policy syntax and use cases.

## CAM Policy Syntax
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
  1. **effect** is required. It describes the result of a statement. The result can be "allow" or an explicit "deny".
  2. **action** is required. It describes the allowed or denied operation. An operation can be an API (prefixed with “name” or a feature set (a set of specific APIs prefixed with "permit").
  3. **resource** is required. It describes the details of authorization. A resource is described in a six-segment format. Detailed resource definitions vary by product. For more information on how to specify a resource, see the documentation for the product whose resources you are writing a statement for.
  4. **condition** is optional. It describes the condition for the policy to take effect. A condition consists of operator, action key, and action value. A condition value may contain information such as time and IP address. Some services allow you to specify additional values in a condition.

## Policy Examples
- Specify a full read/write permission policy for dedicated tunnel as follows:
  - Grant the sub-accounts all operation permissions for dedicated tunnels, such as creation and management.
  - Policy name: QcloudDCFullAccess
```shell
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "dc:*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
- Specify a read-only permission policy for dedicated tunnel as follows:
  - Grant the sub-account read-only permission for dedicated tunnels. The authorized sub-account can view all resources of the dedicated tunnels, but cannot create, update or delete resources.
  - Policy name: QcloudDCReadOnlyAccess
```shell
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "dc:Describe*",
                "dc:Is*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
```

