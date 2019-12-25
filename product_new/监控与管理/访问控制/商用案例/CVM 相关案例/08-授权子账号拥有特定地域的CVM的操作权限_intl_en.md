
The enterprise account, CompanyExample (ownerUin: 12345678), has a sub-account, Developer, that requires operating permissions for all CVMs in Guangzhou region under the CompanyExample enterprise account.

The enterprise account, CompanyExample, associates the Developer sub-account with the preset policy QcloudCVMReadOnlyAccess. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

Step 2: create the following policy according to policy syntax.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "cvm:*",
            “resource": "qcs::cvm:gz::*",
            “effect": "allow"
        }
    ]
}
```
Step 2: associate the sub-account with the policy. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).
