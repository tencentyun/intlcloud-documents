A sub-account Developer under the enterprise account CompanyExample (ownerUin is 12345678 and appId is 1250000000) requires read/write permission of objects with the prefix "test" in the Bucket1's directory dir1 of the COS service in Shanghai region under the enterprise account CompanyExample.

Solution A:

Step 1: Create the following policy using policy syntax
```
{
    "version": "2.0",
    "statement":[
     {
         "effect": "allow",
         "action": "cos:*",
         "resource": "qcs::cos:ap-shanghai:uid/1250000000:Bucket1-1250000000/dir1/test*"
     }
   ]
}
```
 Step 2: Authorize the policy to the sub-account. For more information on authorization, please see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

Solution B:

Configure Policy and ACL via the COS console. For more information, please see the COS document.
