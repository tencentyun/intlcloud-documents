### How can I create a custom policy?

If preset policies do not meet your requirements, you can create a custom policy.
The syntax of a custom policy is as follows:

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "Action"
            ],
            "resource": "Resource",
            "effect": "Effect"
        }
    ]
}
```

- Action: replace this with the operation to be allowed or denied.
- Resource: replace this with the resources that you want to authorize.
- Effect: replace this with "Allow" or "Deny".

### How should I configure the read-only policy for a CVM?

To allow a user to query CVM instances but not to create, delete, start, or shut down the instances, enable the QcloudCVMInnerReadOnlyAccess policy.

To do this, log in to the CAM Console. On the [Policies](https://console.cloud.tencent.com/cam/policy) page, search for **CVM** to find the policy.

The policy syntax is as follows:

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/cvm:Describe*",
                "name/cvm:Inquiry*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

The preceding policy **grants users the permissions to perform the following operations**:

- All operations starting with "Describe" in CVM.
- All operations starting with "Inquiry" in CVM.

### How can I configure the read-only policy for CVM-related resources?

To allow a user to query CVM instances and relevant resources (VPC and CLB instances) but not to create, delete, start, or shut down the instances and relevant resources, enable the QcloudCVMReadOnlyAccess policy.

To do this, log in to the CAM Console. On the [Policies](https://console.cloud.tencent.com/cam/policy) page, search for **CVM** to find the policy.

The policy syntax is as follows:

```
 {
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/cvm:Describe*",
                "name/cvm:Inquiry*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "name/vpc:Describe*",
                "name/vpc:Inquiry*",
                "name/vpc:Get*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "name/clb:Describe*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "effect": "allow",
            "action": "name/monitor:*",
            "resource": "*"
        }
    ]
}
```

The preceding policy **grants users the permissions to perform the following operations**:

- All operations starting with "Describe" and "Inquiry" in CVM.
- All operations starting with "Describe", "Inquiry", and "Get" in VPC.
- All operations starting with "Describe" in CLB.
- All operations in the monitor.

