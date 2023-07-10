Currently, you can grant permissions to a Cloud Infinite (CI) sub-account to perform persistence operations by associating the write permission with given resources in COS. The following cases illustrate how to grant permissions to a CI sub-account to perform persistence operations on **all resources** and on **specific resources**.

>! Before configuring data persistence permissions for your sub-account, you must associate the CI full read-write access **QcloudCIFullAccess**.


When configuring a custom policy, you can copy and paste the following reference policy into the **Edit Policy Content** input box and modify it based on the actual settings. For more information, see the [CAM Policy Syntax](https://intl.cloud.tencent.com/document/product/598/10604) document.


<span id="Authorizing a sub-account to perform persistence operations on all resources"></span>
## Authorizing a sub-account to perform persistence operations on all resources

Assume that an enterprise account named CompanyExample (whose OwnerUin is 100000000001 and APPID is 1250000000) has a sub-account named Developer, which needs to perform persistence processing on all resources under CompanyExample.

In this case, the following solutions are available to authorize the CI sub-account to perform persistence processing by granting the write permission to all resources under the account CompanyExample in COS.

**Solution A:**

CompanyExample grants the **QcloudCOSDataWriteOnly** preset policy to Developer. For more information on authorization, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

**Solution B:**

Step 1: create the following policy by using policy syntax.

```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cos:ListParts",
                "cos:PostObject",
                "cos:PutObject*",
                "cos:InitiateMultipartUpload",
                "cos:UploadPart",
                "cos:UploadPartCopy",
                "cos:CompleteMultipartUpload",
                "cos:AbortMultipartUpload"
            ],
            "resource": "*"
        }
    ]
}
```

Step 2: associate this policy with the sub-account. For more information on authorization, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).


 <span id="Authorizing a sub-account to perform persistence operations on resources under a specific directory"></span>
## Authorizing a sub-account to perform persistence operations on resources under a specific directory
Assume that an enterprise account named CompanyExample (whose OwnerUin is 100000000001 and APPID is 1250000000) has a sub-account named Developer, which needs to perform persistence processing on resources under the doc directory in a bucket named examplebucket locating in the Shanghai region.

In this case, the following solutions are available to authorize the CI sub-account to perform persistence processing by granting the write permission to resources under the specified directory in COS.

**Solution A:**

Configure policies and the ACL for resources in COS Console. For more information, see the [Adding Bucket Policies](https://intl.cloud.tencent.com/document/product/436/30927) document for COS.

**Solution B:**

Step 1: create the following policy by using policy syntax.

```
{
   "version": "2.0",
   "statement": [
       {
           "effect": "allow",
           "action": [
                "cos:ListParts",
                "cos:PostObject",
                "cos:PutObject*",
                "cos:InitiateMultipartUpload",
                "cos:UploadPart",
                "cos:UploadPartCopy",
                "cos:CompleteMultipartUpload",
                "cos:AbortMultipartUpload"
           ],
           "resource":"qcs::cos:ap-shanghai:uid/1250000000:examplebucket-1250000000/doc/*"    
 }
    ]
}
```

Step 2: associate this policy with the sub-account. For more information on authorization, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

<span id="Authorizing a sub-account to perform persistence operations on a specific resource"></span>
## Authorizing a sub-account to perform persistence operations on a specific resource

Assume that an enterprise account named CompanyExample (whose OwnerUin is 100000000001 and APPID is 1250000000) has a sub-account named Developer, which needs to perform persistence processing on the picture.jpg image file under the doc directory in a bucket named examplebucket locating in the Shanghai region.

In this case, the following solutions are available to authorize the CI sub-account to perform persistence processing by granting the write permission to the specified resource in COS.

**Solution A:**

Configure policies and the ACL for resources in COS Console. For more information, see the [Adding Bucket Policies](https://intl.cloud.tencent.com/document/product/436/30927) document for COS.

**Solution B:**

Step 1: create the following policy by using policy syntax.

```
{
   "version": "2.0",
   "statement": [
       {
           "effect": "allow",
           "action": [
                "cos:ListParts",
                "cos:PostObject",
                "cos:PutObject*",
                "cos:InitiateMultipartUpload",
                "cos:UploadPart",
                "cos:UploadPartCopy",
                "cos:CompleteMultipartUpload",
                "cos:AbortMultipartUpload"
           ],
      "resource":"qcs::cos:ap-shanghai:uid/1250000000:examplebucket-1250000000/doc/picture.jpg"      
 }
    ]
}
```

Step 2: associate this policy with the sub-account. For more information on authorization, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).


<span id="Authorizing a sub-account to perform persistence operations on a specific resources with a specific prefix"></span>
## Authorizing a sub-account to perform persistence operations on a specific resources with a specific prefix

Assume that an enterprise account named CompanyExample (whose OwnerUin is 100000000001 and APPID is 1250000000) has a sub-account named Developer, which needs to perform persistence processing on resources with the prefix of **test** under the doc directory in a bucket named examplebucket locating in the Shanghai region.

In this case, the following solutions are available to authorize the CI sub-account to perform persistence processing by granting the write permission to resources with the specified prefix in COS.

**Solution A:**

Configure policies and the ACL for resources in COS Console. For more information, see the [Adding Bucket Policies](https://intl.cloud.tencent.com/document/product/436/30927) document for COS.

**Solution B:**

Step 1: create the following policy by using policy syntax.

```
{
   "version": "2.0",
   "statement": [
       {
           "effect": "allow",
           "action": [
                "cos:ListParts",
                "cos:PostObject",
                "cos:PutObject*",
                "cos:InitiateMultipartUpload",
                "cos:UploadPart",
                "cos:UploadPartCopy",
                "cos:CompleteMultipartUpload",
                "cos:AbortMultipartUpload"
           ],
      "resource":"qcs::cos:ap-shanghai:uid/1250000000:examplebucket-1250000000/doc/test*"      
 }
    ]
}
```

Step 2: associate this policy with the sub-account. For more information on authorization, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

<span id="Authorizing a sub-account to perform persistence operations on all resources under a specific directory except specified files"></span>
## Authorizing a sub-account to perform persistence operations on all resources under a specific directory except specified files

Assume that an enterprise account named CompanyExample (whose OwnerUin is 100000000001 and APPID is 1250000000) has a sub-account named Developer, which needs to perform persistence processing on all resources under the doc directory in a bucket except the image file picture.jpg. The bucket is named examplebucket and locates in the Shanghai region.

In this case, the following solutions are available to authorize the CI sub-account to perform persistence processing by granting the write permission to a given files under the specified directory in COS.

**Solution A:**

Configure policies and the ACL in COS Console. For more information, see the [Adding Bucket Policies](https://intl.cloud.tencent.com/document/product/436/30927) document for COS.


**Solution B:**

Step 1: create the following policy by using policy syntax.

```
{
   "version": "2.0",
   "statement": [
{
           "effect": "allow",
           "action": [
                "cos:ListParts",
                "cos:PostObject",
                "cos:PutObject*",
                "cos:InitiateMultipartUpload",
                "cos:UploadPart",
                "cos:UploadPartCopy",
                "cos:CompleteMultipartUpload",
                "cos:AbortMultipartUpload"
           ],
           "resource":"qcs::cos:ap-shanghai:uid/1250000000:examplebucket-1250000000/doc/*"    
 },
 
       {
           "effect": "deny",
           "action": [
                "cos:ListParts",
                "cos:PostObject",
                "cos:PutObject*",
                "cos:InitiateMultipartUpload",
                "cos:UploadPart",
                "cos:UploadPartCopy",
                "cos:CompleteMultipartUpload",
                "cos:AbortMultipartUpload"
           ],
      "resource":"qcs::cos:ap-shanghai:uid/1250000000:examplebucket-1250000000/doc/picture.jpg"      
 }
    ]
}
```

Step 2: associate this policy with the sub-account. For more information on authorization, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).