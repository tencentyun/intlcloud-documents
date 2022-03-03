This document describes CAM access policy syntax and use cases.

## CAM Policy Syntax

CAM policy:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "dnspod:*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

- **version** is required. Currently, only the value "2.0" is allowed.
- **statement** describes the details of one or more permissions, and therefore contains the permission(s) of other elements such as `effect`, `action`, `resource`, and `condition`. One policy has only one `statement`.
  1. **action** is required. It describes an allowed or denied action. An action can be an API (prefixed with "name") or a feature set (a set of specific APIs prefixed with "permid").
  2. **resource** is required. It describes the details of authorization. A resource is described in a six-segment format. Detailed resource definitions vary by product. For more information on how to specify a resource, see the documentation for the product whose resources you are writing a statement for.
  3. **condition** is optional. It describes the condition for the policy to take effect. A condition consists of operator, action key, and action value. Condition values may contain information such as time and IP address. Some services allow you to specify additional values in a condition.
  4. **effect** is required. It describes the result of a statement, which can be "allow" or "deny".



## Sample Policies

- Authorize full read-write access to DNSPod services, as follows:
	- Authorize a sub-account full access (permission of all operations, including creation and management) to DNSPod services.
	- Policy name: QcloudDNSPodFullAccess

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "dnspod:*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```



- Authorize read-only access to DNSPod services, as follows: 
	- Authorize a sub-account to access (read-only) DNSPod services, which means the sub-account user can view all DNSPod resources, but not create, update or delete them.
	- Policy name: QcloudDNSPodReadOnlyAccess

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "dnspod:Describe*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

