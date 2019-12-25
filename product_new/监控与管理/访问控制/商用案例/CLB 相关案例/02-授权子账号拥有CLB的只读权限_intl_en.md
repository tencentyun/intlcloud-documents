
The enterprise account, CompanyExample (ownerUin: 12345678), has a sub-account, Developer, that requires read-only permission for the CLB service under the CompanyExample enterprise account. The sub-account is not permitted to create, update, or delete CLBs.

Solution A:

The enterprise account, CompanyExample, associates the Developer sub-account with the preset policy QcloudCLBReadOnlyAccess. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

Solution B:

Step 1: create the following policy by using policy syntax.
```
 {
    "version": "2.0",
    "statement":[
     {
         "effect": "allow",
         "action": "clb:Describe*",
         "resource": "*"
     }
  ]
}
```
Step 2: associate the sub-account with the policy. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).
