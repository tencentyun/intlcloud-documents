
The enterprise account, CompanyExample (ownerUin: 12345678), has a sub-account, Developer, that requires permissions to operate a specific CVM (ID: ins-1) in Guangzhou region belonging to the enterprise account CompanyExample.

Step 1: create the following policy according to policy syntax.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "cvm:*",
            "resource": "qcs::cvm:gz::instance/ins-1",
            "effect": "allow"
        }
    ]
}
```
Step 2: associate the sub-account with the policy. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).
