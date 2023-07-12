## Overview

This document provides an overview of APIs and SDK code samples related to the access control lists (ACLs) for buckets and objects.

**Bucket ACL**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | --------------------------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | Setting a bucket ACL | Sets an ACL for a bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Querying a bucket ACL | Queries the ACL of a bucket |

**Object ACL**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting an object ACL | Sets an ACL for an object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying an object ACL | Queries the ACL of an object |

## SDK API References

For the parameters and method description of all the APIs in the SDK, see [API Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).


## Bucket ACL

### Setting a bucket ACL

#### Description

This API is used to set an access control list (ACL) for a specified bucket.

#### Sample code

[//]: # (.cssg-snippet-put-bucket-acl)
```cs
try
{
  // Bucket name in the format of bucketname-APPID. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  PutBucketACLRequest request = new PutBucketACLRequest(bucket);
  // Set private read and write permissions
  request.SetCosACL(CosACL.Private);
  // Grant read permission for account 1131975903
  COSXML.Model.Tag.GrantAccount readAccount = new COSXML.Model.Tag.GrantAccount();
  readAccount.AddGrantAccount("1131975903", "1131975903");
  request.SetXCosGrantRead(readAccount);
  // Execute the request
  PutBucketACLResult result = cosXml.PutBucketACL(request);
  // Request succeeded
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketACL.cs).

### Querying a bucket ACL

#### Description

This API is used to query the access control list (ACL) of a specified bucket.

#### Sample code

[//]: # (.cssg-snippet-get-bucket-acl)
```cs
try
{
  // Bucket name in the format of bucketname-APPID. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  GetBucketACLRequest request = new GetBucketACLRequest(bucket);
  // Execute the request
  GetBucketACLResult result = cosXml.GetBucketACL(request);
  // Bucket ACL information
  AccessControlPolicy acl = result.accessControlPolicy;
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketACL.cs).

## Object ACL

### Setting an object ACL

#### Description

This API is used to set the access control list (ACL) for an object in a bucket.

#### Sample code

[//]: # (.cssg-snippet-put-object-acl)
```cs
// To avoid reaching the upper limit of 1,000 bucket ACLs,
// we do not recommend setting an object ACL for a single object unless absolutely necessary. The object will inherit bucket permissions by default.
try
{
  // Bucket name in the format of bucketname-APPID. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; // Object key
  PutObjectACLRequest request = new PutObjectACLRequest(bucket, key);
  // Set private read and write permissions 
  request.SetCosACL(CosACL.Private);
  // Grant read permission for account 1131975903 
  COSXML.Model.Tag.GrantAccount readAccount = new COSXML.Model.Tag.GrantAccount();
  readAccount.AddGrantAccount("1131975903", "1131975903");
  request.SetXCosGrantRead(readAccount);
  // Execute the request
  PutObjectACLResult result = cosXml.PutObjectACL(request);
  // Request succeeded
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ObjectACL.cs).

### Querying an object ACL

#### Description

This API is used to query the ACL of an object.

#### Sample code

[//]: # (.cssg-snippet-get-object-acl)
```cs
try
{
  // Bucket name in the format of bucketname-APPID. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; // Object key
  GetObjectACLRequest request = new GetObjectACLRequest(bucket, key);
  // Execute the request
  GetObjectACLResult result = cosXml.GetObjectACL(request);
  // Object ACL information
  AccessControlPolicy acl = result.accessControlPolicy;
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```
>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ObjectACL.cs).



