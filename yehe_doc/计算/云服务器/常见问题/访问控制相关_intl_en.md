### How to create the custom policy?

If preset policies cannot meet your requirements, you can create custom policies.
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

- Replace "Action" with the operation to be allowed or denied.
- Replace "Resource" with the resources that you want to authorize the user to operate on.
- Replace "Effect" with Allow or Deny.

### How to configure the read-only policy for CVMs?

If you want to allow a user to query CVM instances, but not create, delete, and start/shut down instances, you can implement the policy named QcloudCVMInnerReadOnlyAccess.

Log in to the CAM console and search for **CVM** on the [Policies](https://console.cloud.tencent.com/cam/policy) page to find the policy quickly.

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

The above policy is designed to **grant users the permissions to perform the following operations**:

- All operations starting with "Describe" in CVM.
- All operations starting with "Inquiry" in CVM.

### How to configure the read-only policy for CVM resources?

If you want to allow a user to query CVM instances and relevant resources (VPC, CLB), but not create, delete, and start/shut down instances, you can implement the policy named QcloudCVMReadOnlyAccess.

Log in to the CAM console and search for **CVM** on the [Policies](https://console.cloud.tencent.com/cam/policy) page to find the policy quickly.

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

The above policy is designed to **grant users the permissions to perform the following operations**:

- All operations starting with "Describe" and "Inquiry" in CVM.
- All operations starting with "Describe", "Inquiry" and "Get" in VPC.
- All operations starting with "Describe" in CLB.
- All operations in Monitor.

