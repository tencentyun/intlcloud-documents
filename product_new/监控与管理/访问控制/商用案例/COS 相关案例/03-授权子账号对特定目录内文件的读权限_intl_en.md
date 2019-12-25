The enterprise account, CompanyExample (ownerUin: 12345678; appID: 1250000000), has a sub-account, Developer, that requires read permissions for files under the dir1 directory of the Bucket1 bucket of the COS service in Shanghai region under the CompanyExample enterprise account.

Solution A:

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
         "resource": "qcs::cos:ap-shanghai:uid/1250000000:Bucket1-1250000000/dir1/*"
     }
   ]
}
```
Step 2: associate the sub-account with the policy. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

Solution B:

Configure the policy and ACL in the COS Console. For more information, see the COS documentation.
