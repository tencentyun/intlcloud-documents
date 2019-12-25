
The enterprise account, CompanyExample (ownerUin: 12345678), has a sub-account, Developer, that requires read/write permissions for VPCs and relevant resources (except for routing tables) belonging to the CompanyExample enterprise account.

Step 1: create the following policy by using policy syntax.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "vpc:*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "vpc:AssociateRouteTable",
                "vpc:CreateRoute",
                "vpc:CreateRouteTable",
                "vpc:DeleteRoute",
                "vpc:DeleteRouteTable",
                "vpc:ModifyRouteTableAttribute"
            ],
            "resource": "*",
            "effect": "deny"
        }
    ]
}
```
Step 2: associate the sub-account with the policy. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).
