
The enterprise account, CompanyExample (ownerUin: 12345678), has a sub-account, Developer, that requires full management permissions (creation, management, ordering, and payment for VPCs) for the VPC service of the CompanyExample enterprise account.

Solution A:

The enterprise account, CompanyExample, associates the Developer sub-account with the preset policies QcloudVPCFullAccess and QcloudVPCFinanceAccess. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

Solution B:

Step 1: create the following policy according to policy syntax.
```
{
    "version": "2.0",
    "statement":[
         {
             "effect": "allow",
             "action": "vpc:*",
             "resource": "*"
         },
         {
                "effect": "allow",
                "action": "finance:*",
                "resource": "qcs::vpc:::*"
         }
    ]
}
```
Step 2: associate the sub-account with the policy. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

