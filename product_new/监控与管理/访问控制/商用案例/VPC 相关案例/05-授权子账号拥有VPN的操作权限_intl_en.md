
The enterprise account, CompanyExample (ownerUin: 12345678), has a sub-account, Developer, that requires view permission for all VPC resources in the VPC service under the CompanyExample enterprise account, but is only allowed to perform CRUD operations on VPNs.

Step 1: create the following policy by using policy syntax.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "vpc:Describe*",
                "vpc:Inquiry*",
                "vpc:Get*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "vpc:*Vpn*",
                "vpc:*UserGw*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
Step 2: associate the sub-account with the policy. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

