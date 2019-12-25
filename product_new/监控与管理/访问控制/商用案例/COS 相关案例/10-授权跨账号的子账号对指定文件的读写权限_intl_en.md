The enterprise account, CompanyGranter (ownerUin: 12345678; appID: 1250000000), has an object, Object1, that is located in the dir1 directory of the Bucket1 bucket in the Guangzhou region. The sub-account of another enterprise account, CompanyGrantee (ownerUin: 87654321), requires read/write permission for Object1.

This involves permission propagation.

Step 1: CompanyGrantee creates the following policy according to policy syntax.
```
 {
    "version": "2.0",
    "statement":[
     {
         "effect": "allow",
         "action": "cos:*",
         "resource": "qcs::cos:ap-shanghai:uid/1250000000:Bucket1-1250000000/dir1/Object1"
     }
    ]
}
```
Step 2: associate the sub-account with the policy. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

Step 3: the CompanyGranter enterprise account grants CompanyGrantee enterprise account access to Object1 by configuring the policy and ACL in the COS Console. For more information, see COS documentation.
