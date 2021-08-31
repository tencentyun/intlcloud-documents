The organizational account `CompanyExample` (ownerUin: 12345678; appId: 1250000000) has a sub-account `Developer` that requires read/write permissions for all objects except the `Object1` object in the `dir1` directory of the `Bucket1` bucket of the COS service in the Shanghai region under the `CompanyExample` account.

Solution A:

Step 1. Create the following policy according to the policy syntax:
```
 {
    "version": "2.0",
    "statement":
    [
     {
         "effect": "allow",
         "action": "cos:*",
         "resource": "qcs::cos:ap-shanghai:uid/1250000000:Bucket1-1250000000/dir1/*"
     },
     {
         "effect": "deny",
         "action": "cos:*",
         "resource": "qcs::cos:ap-shanghai:uid/1250000000:Bucket1-1250000000/dir1/Object1"
     }     
    ]
}
```
Step 2. Associate the policy with the sub-account. For more information on authorization, please see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

Solution B:

Set the policy and ACL in the COS Console. For more information, please see [ACL Practices](https://intl.cloud.tencent.com/document/product/436/12470).
