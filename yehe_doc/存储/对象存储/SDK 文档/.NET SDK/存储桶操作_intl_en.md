## Introduction

This document provides an overview of APIs and SDK code samples related to basic operations on buckets and bucket access control list (ACL).

**Basic Operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service](https://intl.cloud.tencent.com/document/product/436/8291) | Querying bucket list | Queries the list of all buckets under a specified account |
| [PUT Bucket](https://cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under the specified account |
| [HEAD Bucket](https://cloud.tencent.com/document/product/436/7735) | Retrieving information on a bucket and its permission | Checks whether a bucket exists and you if have the permission to access it |
| [DELETE Bucket](https://cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket under the specified account |

**ACL**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | --------------------- |
| [PUT Bucket acl](https://cloud.tencent.com/document/product/436/7737) | Setting bucket ACL | Sets the ACL for a specified bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Querying bucket ACL | Queries the ACL of a bucket |

## Basic Operations

### Querying Bucket List

#### Feature Description

This API (GET Service) is used to query the list of all buckets under a specified account.

#### Method Prototype

```C#
GetServiceResult GetService(GetServiceRequest request);

void GetService(GetServiceRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample Request

[//]: # (.cssg-snippet-get-service)
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Set the connection timeout period in milliseconds, which is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Set the read/write timeout period in milliseconds, which is 45,000 ms by default
  .IsHttps(true)  // Set HTTPS as default request method
  .SetAppid("1250000000")  // Set the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION")  // Set the default bucket region
  .Build();

String secretId = "COS_SECRETID"; // TencentCloud API key SecretId
String secretKey = "COS_SECRETKEY"; // TencentCloud API key SecretKey
long durationSecond = 600;          //Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  GetServiceRequest request = new GetServiceRequest();
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Execute the request
  GetServiceResult result = cosXml.GetService(request);
  // Get a list of all buckets
  List<ListAllMyBuckets.Bucket> allBuckets = result.listAllMyBuckets.buckets;
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

#### Parameter Description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | -------- | ------------------------------- | -------------- |
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period in seconds, e.g., if a signature is valid for 1 minute, the value will be 60     | long           |
| headerKeys | SetSign | Indicates whether to verify the header for the signature | `List` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `List` |

#### Returned Result

The result of the request is returned through GetServiceResult.

| Member Variable | Type | Description |
| ---------------- | ------------------------------------------------------------ | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| listAllMyBuckets | [ListAllMyBuckets](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/ListAllMyBuckets.cs) | The list of buckets under the specified account is returned |

>If the operation fails, the system will throw a  [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### Creating a Bucket

#### Feature Description

This API (PUT Bucket) is used to create a bucket under a specified account.

#### Method Prototype

```C#
PutBucketResult PutBucket(PutBucketRequest request);

void PutBucket(PutBucketRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample Request

[//]: # (.cssg-snippet-put-bucket)
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Set the connection timeout period in milliseconds, which is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Set the read/write timeout period in milliseconds, which is 45,000 ms by default
  .IsHttps(true)  // Set HTTPS as default request method
  .SetAppid("1250000000")  // Set the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION")  // Set the default bucket region
  .Build();

String secretId = "COS_SECRETID"; // TencentCloud API key SecretId
String secretKey = "COS_SECRETKEY"; // TencentCloud API key SecretKey
long durationSecond = 600;          //Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  PutBucketRequest request = new PutBucketRequest(bucket);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Execute the request
  PutBucketResult result = cosXml.PutBucket(request);
  // Request successful
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

#### Parameter Description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | -------- | ---------------------------------- | -------------- |
| bucket | Constructor | Bucket name. Format: BucketName-APPID | string |
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period in seconds, e.g., if a signature is valid for 1 minute, the value will be 60     | long           |
| headerKeys | SetSign | Indicates whether to verify the header for the signature | `List` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `List` |

#### Returned Result

The result of the request is returned through PutBucketResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the system will throw a  [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### Retrieving Information on a Bucket and Its Permission

#### Feature Description

This API (HEAD Bucket) is used to verify whether a bucket exists and if you have the permission to access it.

#### Method Prototype

```C#
HeadBucketResult HeadBucket(HeadBucketRequest request);

void HeadBucket(HeadBucketRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample Request

[//]: # (.cssg-snippet-head-bucket)
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Set the connection timeout period in milliseconds, which is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Set the read/write timeout period in milliseconds, which is 45,000 ms by default
  .IsHttps(true)  // Set HTTPS as default request method
  .SetAppid("1250000000")  // Set the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION")  // Set the default bucket region
  .Build();

String secretId = "COS_SECRETID"; // TencentCloud API key SecretId
String secretKey = "COS_SECRETKEY"; // TencentCloud API key SecretKey
long durationSecond = 600;          //Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  HeadBucketRequest request = new HeadBucketRequest(bucket);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Execute the request
  HeadBucketResult result = cosXml.HeadBucket(request);
  // Request successful
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


### Deleting a Bucket

#### Feature Description

This API (DELETE Bucket) is used to delete the specified bucket.

#### Method Prototype

```C#
DeleteBucketResult DeleteBucket(DeleteBucketRequest request);

void DeleteBucket(DeleteBucketRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample Request

[//]: # (.cssg-snippet-delete-bucket)
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Set the connection timeout period in milliseconds, which is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Set the read/write timeout period in milliseconds, which is 45,000 ms by default
  .IsHttps(true)  // Set HTTPS as default request method
  .SetAppid("1250000000")  // Set the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION")  // Set the default bucket region
  .Build();

String secretId = "COS_SECRETID"; // TencentCloud API key SecretId
String secretKey = "COS_SECRETKEY"; // TencentCloud API key SecretKey
long durationSecond = 600;          //Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  DeleteBucketRequest request = new DeleteBucketRequest(bucket);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Execute the request
  DeleteBucketResult result = cosXml.DeleteBucket(request);
  // Request successful
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

#### Parameter Description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | -------- | ---------------------------------- | -------------- |
| bucket | Constructor | Bucket name. Format: BucketName-APPID | string |
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period in seconds, e.g., if a signature is valid for 1 minute, the value will be 60     | long           |
| headerKeys | SetSign | Indicates whether to verify the header for the signature | `List` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `List` |

#### Returned Result

The result of the request is returned through DeleteBucketResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the system will throw a  [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

## ACL

### Setting Bucket ACL

#### Feature Description

This API (PUT Object acl) is used to set the access control list (ACL) for a specified object in a bucket.

#### Method Prototype

```C#
PutBucketACLResult PutBucketACL(PutBucketACLRequest request);

void PutBucketACL(PutBucketACLRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample Request

[//]: # (.cssg-snippet-put-bucket-acl)
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Set the connection timeout period in milliseconds, which is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Set the read/write timeout period in milliseconds, which is 45,000 ms by default
  .IsHttps(true)  // Set HTTPS as default request method
  .SetAppid("1250000000")  // Set the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION")  // Set the default bucket region
  .Build();

String secretId = "COS_SECRETID"; // TencentCloud API key SecretId
String secretKey = "COS_SECRETKEY"; // TencentCloud API key SecretKey
long durationSecond = 600;          //Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  PutBucketACLRequest request = new PutBucketACLRequest(bucket);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Set private read and write permissions
  request.SetCosACL(CosACL.PRIVATE);
  // Grant read permission to account 1131975903
  COSXML.Model.Tag.GrantAccount readAccount = new COSXML.Model.Tag.GrantAccount();
  readAccount.AddGrantAccount("1131975903", "1131975903");
  request.SetXCosGrantRead(readAccount);
  // Execute the request
  PutBucketACLResult result = cosXml.PutBucketACL(request);
  // Request successful
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

#### Parameter Description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | --------------------------------------------------------- | ---------------------------------- | -------------- |
| bucket | Constructor | Bucket name. Format: BucketName-APPID | string |
| cosAcl | SetCosAcl | Sets the ACL permissions for the bucket | string |
| grantAccount | SetXCosGrantRead, SetXCosGrantWrite, or SetXCosReadWrite | Grants users read and write permissions | GrantAccount |
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period in seconds, e.g., if a signature is valid for 1 minute, the value will be 60     | long           |
| headerKeys | SetSign | Indicates whether to verify the header for the signature | `List` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `List` |

#### Returned Result

The result of the request is returned through PutBucketACLResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the system will throw a  [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### Querying Bucket ACL

#### Feature Description

This API (GET Bucket acl) is used to query the access control list (ACL) of a bucket.

#### Method Prototype

```C#
GetBucketACLResult GetBucketACL(GetBucketACLRequest request);

void GetBucketACL(GetBucketACLRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample Request

[//]: # (.cssg-snippet-get-bucket-acl)
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Set the connection timeout period in milliseconds, which is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Set the read/write timeout period in milliseconds, which is 45,000 ms by default
  .IsHttps(true)  // Set HTTPS as default request method
  .SetAppid("1250000000")  // Set the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION")  // Set the default bucket region
  .Build();

String secretId = "COS_SECRETID"; // TencentCloud API key SecretId
String secretKey = "COS_SECRETKEY"; // TencentCloud API key SecretKey
long durationSecond = 600;          //Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  GetBucketACLRequest request = new GetBucketACLRequest(bucket);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
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

#### Parameter Description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | -------- | ---------------------------------- | -------------- |
| bucket | Constructor | Bucket name. Format: BucketName-APPID | string |
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period in seconds, e.g., if a signature is valid for 1 minute, the value will be 60     | long           |
| headerKeys | SetSign | Indicates whether to verify the header for the signature | `List` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `List` |

#### Returned Result

The result of the request is returned through GetBucketACLResult.

| Member Variable | Type | Description |
| ------------------- | ------------------------------------------------------------ | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| accessControlPolicy | [AccessControlPolicy](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/AccessControlPolicy.cs) | The information of the bucket ACL is returned |

>If the operation fails, the system will throw a  [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.
