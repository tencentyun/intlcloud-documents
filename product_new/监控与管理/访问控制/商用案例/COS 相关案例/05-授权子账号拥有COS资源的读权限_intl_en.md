The enterprise account, CompanyExample (ownerUin: 12345678), has a sub-account, Developer, that requires read-only access permissions to COS buckets, objects, and object lists belonging to the CompanyExample enterprise account.

Solution A:

The enterprise account, CompanyExample, associates the Developer sub-account with the preset policy QcloudCOSReadOnlyAccess. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

Solution B:

Step 1: create the following policy by using policy syntax.
```
 {
    "version": "2.0",
    "statement":[
     {
         "effect": "allow",
         "action":  [
                    "cos:List*",
                    "cos:Get*",
                    "cos:Head*",
                    "cos:OptionsObject"
                ],
         "resource": "*"
     }
   ]
}
```
Step 2: associate the sub-account with the policy. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).
