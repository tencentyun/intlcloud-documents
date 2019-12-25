
The enterprise account, CompanyExample (ownerUin: 12345678), has a sub-account, Developer, that requires full management permissions (creation, management, ordering, and payment for CLB) for the CLB service of enterprise account CompanyExample.

Solution A:

The enterprise account, CompanyExample, associates the Developer sub-account with the preset policies QcloudCLBFullAccess and QcloudCLBFinanceAccess. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

Solution B:

Step 1: create the following policy according to policy syntax.
```
{
    "version": "2.0",
    "statement":[
         {
             "effect": "allow",
             "action": "clb:*",
             "resource": "*"
         },
         {
                "effect": "allow",
                "action": "finance:*",
                "resource": "qcs::clb:::*"
         }
    ]
}
```
Step 2: associate the sub-account with the policy. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

