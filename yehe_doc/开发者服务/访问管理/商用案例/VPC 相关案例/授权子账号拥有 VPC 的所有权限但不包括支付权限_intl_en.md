The organizational account `CompanyExample` (ownerUin: 12345678) has a sub-account `Developer` that requires full management permissions (for all operations such as creation and management) for the VPC service under `CompanyExample` except payment permissions. The sub-account should be able to place orders but cannot make payments.

Solution A:

The `CompanyExample` account directly authorizes the preset policy `QcloudVPCFullAccess` to the `Developer` sub-account. For more information on authorization, please see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

Solution B:

Step 1. Create the following policy according to the policy syntax:
```
 {
    "version": "2.0",
    "statement":[
         {
             "effect": "allow",
             "action": "vpc:*",
             "resource": "*"
         }
    ]
}
```
Step 2. Associate the policy with the sub-account. For more information on authorization, please see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

