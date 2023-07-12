## Overview

This document provides an overview of APIs and SDK sample codes related to simple operations, multipart operations, and other object operations.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket（List Object）](https://intl.cloud.tencent.com/document/product/436/7734) | Querying an object list | Queries some or all objects in a bucket |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object using simple upload | Uploads an object to a bucket |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | Uploading an object using a form | Uploads an object using the form request |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Setting object replication | Copies an object to the destination path |
| [Options Object](https://intl.cloud.tencent.com/document/product/436/8288) | Configuring pre-flight requests for cross-origin-access | Sends a pre-flight request to check whether a real cross-origin access can be sent |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes a specified object from a bucket |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects in a single request |

**Multipart operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries the information of a multipart upload in-progress |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload task |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading a part | Uploads a file in multiple parts |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries the uploaded parts of a specified multipart upload operation |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of the entire file |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload operation and deletes the uploaded parts |

**Other operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting object ACL | Sets the ACL for a specified object in a bucket |
| [GET Object acl ](https://intl.cloud.tencent.com/document/product/436/7744) | Querying object ACL | Queries the ACL of an object |

## Simple operations

### Querying an object list

## Feature description

This API is used to query some or all objects in a bucket.

#### Method prototype

```C#
GetBucketResult GetBucket(GetBucketRequest request);

void GetBucketCORS(GetBucketCORSRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request

[//]: # ".cssg-snippet-get-bucket"
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Sets the connection timeout period in milliseconds; this value is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Sets the read/write timeout period in milliseconds; this value is 45,000 ms by default
  .IsHttps(true)  // Sets HTTPS as the default request method
  .SetAppid("1250000000")  // Sets the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION")  // Sets the default bucket region
  .build();

String secretId = "COS_SECRETID"; // The SecretId of your TencentCloud API key
String secretKey = "COS_SECRETKEY"; // The SecretKey of your TencentCloud API key
long durationSecond = 600;          // Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  GetBucketRequest request = new GetBucketRequest(bucket);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Get the object in a/
  request.SetPrefix("a/");
  // Execute the request
  GetBucketResult result = cosXml.GetBucket(request);
  // Bucket information
  ListBucket info = result.listBucket;
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

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | -------- | ---------------------------------- | -------------- |
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys | SetSign | Indicates whether the signature verifies the header | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether the signature verifies the query parameters in the request URL | `List<string>` |

#### Response description

The result of the request is returned through GetBucketResult.

| Member Variable | Type | Description |
| ---------- | ------------------------------------------------------------ | --------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| listBucket | [ListBucket](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/ListBucket.cs) | Returns the list of objects in a bucket |

>If the operation fails, the system will throw a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### Uploading an object using simple upload

## Feature description

This API is used to upload an object to a specified bucket. The uploaded object has a size restriction of 5GB. Please use [Multipart Upload] (#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) or [Advanced APIs] (#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89) to upload objects greater than 5GB.

#### Method prototype

```C#
PutObjectResult PutObject(PutObjectRequest request);

void PutObject(PutObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request

[//]: # ".cssg-snippet-put-object"
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Sets the connection timeout period in milliseconds; this  value is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Sets the read/write timeout period in milliseconds; this value is 45,000 ms by default
  .IsHttps(true)  // Sets HTTPS as the default request method
  .SetAppid("1250000000")  // Sets the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION")  // Sets the default bucket region
  .build();

String secretId = "COS_SECRETID"; // The SecretId of your TencentCloud API key
String secretKey = "COS_SECRETKEY"; // The SecretKey of your TencentCloud API key
long durationSecond = 600;          // Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
  string key = "exampleobject"; // The location of the object in the bucket, i.e. ObjectKey.
  string srcPath = @"temp-source-file";// Absolute path to the local file
  if (!File.Exists(srcPath)) {
    // If the target file does not exist, create a temporary file for testing
    File.WriteAllBytes(srcPath, new byte[1024]);
  }

  PutObjectRequest request = new PutObjectRequest(bucket, key, srcPath);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Set the progress callback
  request.SetCosProgressCallback(delegate(long completed, long total)
  {
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
  });
  // Execute the request
  PutObjectResult result = cosXml.PutObject(request);
  // Object etag
  string eTag = result.eTag;
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

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------- | ------------------------------------------------------------ | --------------------------- |
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| key | Constructor or SetCosPath | [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | String |
| srcPath | Constructor | Absolute path to the local file uploaded to COS | string |
| data | Constructor | The byte array of the file uploaded to COS | byte[] |
| progressCallback | SetCosProgressCallback | Sets the callback for upload progress | Callback.OnProgressCallback |
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys | SetSign | Indicates whether the signature verifies the header | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether the signature verifies the query parameters in the request URL | `List<string>` |

#### Response description

The result of the request is returned through PutObjectResult.

| Member Variable | Type | Description |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| eTag | string | Returns the eTag of an object |

>If the operation fails, the system will throw a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### Uploading an object using a form

## Feature description

This API is used to upload an object using a form.

#### Method prototype

```C#
PostObjectResult PostObject(PostObjectRequest request);

void PostObject(PostObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request

[//]: # ".cssg-snippet-post-object"
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Sets the connection timeout period in milliseconds; this value is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Sets the read/write timeout period in milliseconds; this value is 45,000 ms by default
  .IsHttps(true)  // Sets HTTPS as the default request method
  .SetAppid("1250000000")  // Sets the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION")  // Sets the default bucket region
  .build();

String secretId = "COS_SECRETID"; // The SecretId of your TencentCloud API key
String secretKey = "COS_SECRETKEY"; // The SecretKey of your TencentCloud API key 
long durationSecond = 600;          // Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
  string key = "exampleobject"; // The location of the object in the bucket, i.e. ObjectKey.
  string srcPath = @"temp-source-file";// Absolute path to the local file
  if (!File.Exists(srcPath)) {
    // If the target file does not exist, create a temporary file for testing
    File.WriteAllBytes(srcPath, new byte[1024]);
  }
  PostObjectRequest request = new PostObjectRequest(bucket, key, srcPath);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Set the progress callback
  request.SetCosProgressCallback(delegate(long completed, long total)
  {
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
  });
  // Execute the request
  PostObjectResult result = cosXml.PostObject(request);
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

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------- | ------------------------------------------------------------ | --------------------------- |
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| key | Constructor or SetCosPath | [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | String |
| srcPath | Constructor | Absolute path to the local file uploaded to COS | string |
| data | Constructor | The byte array of the file uploaded to COS | byte[] |
| progressCallback | SetCosProgressCallback | Sets the callback for upload progress | Callback.OnProgressCallback |
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys | SetSign | Indicates whether the signature verifies the header | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether the signature verifies  the query parameters in the request URL | `List<string>` |

#### Response description

The result of the request is returned through PostObjectResult.

| Member Variable | Type | Description |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| eTag | string | Returns the eTag of an object |

>If the operation fails, the system will throw a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### Querying object metadata

## Feature description

This API is used to query the metadata of an object.

#### Method prototype

```C#
HeadObjectResult HeadObject(HeadObjectRequest request);

void HeadObject(HeadObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request

[//]: # ".cssg-snippet-head-object"
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Sets the connection timeout period in milliseconds; this value is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Sets the read/write timeout period in milliseconds; this value is 45,000 ms by default
  .IsHttps(true)  // Sets HTTPS as the default request method
  .SetAppid("1250000000")  // Sets the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION")  // Sets the default bucket region
  .build();

String secretId = "COS_SECRETID"; // The SecretId of your TencentCloud API key
String secretKey = "COS_SECRETKEY"; // The SecretKey of your TencentCloud API key
long durationSecond = 600;          // Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
  string key = "exampleobject"; // The location of the object in the bucket, i.e. ObjectKey.
  HeadObjectRequest request = new HeadObjectRequest(bucket, key);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Execute the request
  HeadObjectResult result = cosXml.HeadObject(request);
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

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | --------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Construction method | Bucket name in the format: BucketName-APPID | string |
| key | Constructor or SetCosPath | [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | String |
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys | SetSign | Indicates whether the signature verifies the header | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether the signature verifies the query parameters in the request URL | `List<string>` |

#### Response description

The result of the request is returned through HeadObjectResult.

| Member Variable | Type | Description |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| eTag | string | Returns the eTag of an object |

>If the operation fails, the system will throw a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### Downloading an object

## Feature description

This API is used to download an object to the local file system.

#### Method prototype

```C#
GetObjectResult GetObject(GetObjectRequest request);

void GetObject(GetObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);

GetObjectBytesResult GetObject(GetObjectBytesRequest request);

void GetObject(GetObjectBytesRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
 
```

#### Sample request

[//]: # ".cssg-snippet-get-object"
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Sets the connection timeout period in milliseconds; this value is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Sets the read/write timeout period in milliseconds; this value is 45,000 ms by default
  .IsHttps(true)  // Sets HTTPS as the default request method
  .SetAppid("1250000000")  // Sets the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION")  // Sets the default bucket region
  .build();

String secretId = "COS_SECRETID"; // The SecretId of your TencentCloud API key
String secretKey = "COS_SECRETKEY"; // The SecretKey of your TencentCloud API key
long durationSecond = 600;          // Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
  string key = "exampleobject"; // The location of the object in the bucket, i.e. ObjectKey.
  string localDir = System.IO.Path.GetTempPath();// Local file directory
  string localFileName = "my-local-temp-file"; // Specifies the file name of the file to be saved locally
  GetObjectRequest request = new GetObjectRequest(bucket, key, localDir, localFileName);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Set the progress callback
  request.SetCosProgressCallback(delegate(long completed, long total)
  {
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
  });
  // Execute the request
  GetObjectResult result = cosXml.GetObject(request);
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

// Download the returned bytes data
try
{
  String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
  string key = "exampleobject"; // The location of the object in the bucket, i.e. ObjectKey.

  GetObjectBytesRequest request = new GetObjectBytesRequest(bucket, key);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Set the progress callback
  request.SetCosProgressCallback(delegate(long completed, long total)
  {
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
  });
  // Execute the request
  GetObjectBytesResult result = cosXml.GetObject(request);
  // Get content
  byte[] content = result.content;
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

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------- | ------------------------------------------------------------ | --------------------------- |
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| key | Constructor or SetCosPath | [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | String |
| localDir | Constructor | The absolute path to the folder where the file is downloaded and stored locally | string |
| localDir | Constructor | The name of the file downloaded and stored locally | string |
| progressCallback    | SetCosProgressCallback | Sets the callback for download progress | Callback.OnProgressCallback |
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys | SetSign | Indicates whether the signature verifies the header | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether the signature verifies the query parameters in the request URL | `List<string>` |

#### Response description

The result of the request is returned through GetObjectResult.

| Member Variable | Type | Description |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| eTag | string | Returns the eTag of an object |

>If the operation fails, the system will throw a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### Setting object replication


## Feature description
This API copies an object to the destination path (object key).

#### Method prototype

```C#
CopyObjectResult CopyObject(CopyObjectRequest request);

void CopyObject(CopyObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request

[//]: # ".cssg-snippet-copy-object"
```c#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Sets the connection timeout period in milliseconds; this value is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Sets the read/write timeout period in milliseconds; this value is 45,000 ms by default
  .IsHttps(true)  // Sets HTTPS as the default request method
  .SetAppid("1250000000")  // Sets the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION")  // Sets the default bucket region
  .build();

String secretId = "COS_SECRETID"; // The SecretId of your TencentCloud API key
String secretKey = "COS_SECRETKEY"; // The SecretKey of your TencentCloud API key 
long durationSecond = 600;          // Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  string sourceAppid = "1250000000"; // Account appid
  string sourceBucket = "sourcebucket-1250000000"; //" Source object bucket
  string sourceRegion = "COS_REGION"; // Source object bucket region
  string sourceKey = "sourceObject"; // Source object key
  // Construct source object attributes
  CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, 
    sourceRegion, sourceKey);

  String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
  string key = "exampleobject"; // The location of the object in the bucket, i.e. ObjectKey.
  CopyObjectRequest request = new CopyObjectRequest(bucket, key);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Set the copy source
  request.SetCopySource(copySource);
  // Set whether to copy or update. Copy is used here.
  request.SetCopyMetaDataDirective(COSXML.Common.CosMetaDataDirective.COPY);
  // Execute the request
  CopyObjectResult result = cosXml.CopyObject(request);
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

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ------------------------ | ------------------------------------------------------------ | -------------------- |
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| key | Constructor or SetCosPath | [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | String |
| copySource | SetCopySource | Describes the source path of the copied data | CopySourceStruct |
| metaDataDirective | SetCopyMetaDataDirective | Indicates whether to copy or update the metadata of the source file | CosMetaDataDirective |
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys | SetSign | Indicates whether the signature verifies the header | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether the signature verifies the query parameters in the request URL | `List<string>` |

#### Response description

The result of the request is returned through CopyObjectResult.

| Member Variable | Type | Description |
| ---------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| copyObject | [CopyObject](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/CopyObject.cs) | Returns the information on successfully copied objects |

>If the operation fails, the system will throw a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### Configuring pre-flight requests for cross-origin access

## Feature description

This API uses preflight requests to check whether you can send cross-origin access requests.

#### Method prototype

```C#
OptionObjectResult OptionObject(OptionObjectRequest request);

void OptionObject(OptionObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request

[//]: # ".cssg-snippet-option-object"
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Sets the connection timeout period in milliseconds; this value is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Sets the read/write timeout period in milliseconds; this value is 45,000 ms by default
  .IsHttps(true)  // Sets HTTPS as the default request method
  .SetAppid("1250000000")  // Sets the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION")  // Sets the default bucket region
  .build();

String secretId = "COS_SECRETID"; // The SecretId of your TencentCloud API key
String secretKey = "COS_SECRETKEY"; // The SecretKey of your TencentCloud API key
long durationSecond = 600;          // Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
  string key = "exampleobject"; // The location of the object in the bucket, i.e. ObjectKey.
  string origin = "http://cloud.tencent.com";
  string accessMthod = "PUT";
  OptionObjectRequest request = new OptionObjectRequest(bucket, key, origin, accessMthod);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Execute the request
  OptionObjectResult result = cosXml.OptionObject(request);
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

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| key | Constructor or SetCosPath | [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | String |
| origin | Constructor or SetOrigin | Simulates the origin of the request for cross-origin access  | string |
| accessMthod | Construction method or SetAccessControlMethod | Simulates the HTTP method of the request for cross-origin access | string |
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys | SetSign | Indicates whether the signature verifies the header | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether the signature verifies the query parameters in the request URL | `List<string>` |

#### Response description

The result of the request is returned through DeleteObjectResult.

| Member Variable | Type | Description |
| ------------------------------- | -------------- | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| accessControlAllowHeaders | `List` | Allowed request headers for cross-origin access |
| accessControlAllowMethods | `List` | Allowed HTTP request methods for cross-origin access |
| accessControlAllowExposeHeaders | `List` | Allowed custom request headers for cross-origin access |
| accessControlMaxAge | long | The validity period of the results obtained by OPTIONS |

>If the operation fails, the system will throw a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### Deleting a single object

## Feature description

This API deletes a specified object from the bucket.

#### Method prototype

```C#
DeleteObjectResult DeleteObject(DeleteObjectRequest request);

void DeleteObject(DeleteObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request

[//]: # ".cssg-snippet-delete-object"
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Sets the connection timeout period in milliseconds; this value is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Sets the read/write timeout period in milliseconds; this value is 45,000 ms by default
  .IsHttps(true)  // Sets HTTPS as the default request method
  .SetAppid("1250000000")  // Sets the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION")  // Sets the default bucket region
  .build();

String secretId = "COS_SECRETID"; // The SecretId of your TencentCloud API key
String secretKey = "COS_SECRETKEY"; // The SecretKey of your TencentCloud API key
long durationSecond = 600;          // Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
  string key = "exampleobject"; // The location of the object in the bucket, i.e. ObjectKey.
  DeleteObjectRequest request = new DeleteObjectRequest(bucket, key);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Execute the request
  DeleteObjectResult result = cosXml.DeleteObject(request);
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

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Construction method | Bucket name in the format: BucketName-APPID | string |
| key | Constructor or SetCosPath | [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | String |
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys | SetSign | Indicates whether the signature verifies the header | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether the signature verifies the query parameters in the request URL | `List<string>` |

#### Response description

The result of the request is returned through DeleteObjectResult.

| Member Variable | Type | Description |
| -------- | ---- | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the system will throw a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### Deleting multiple objects

## Feature description

This API deletes multiple objects from a bucket in a single operation.

#### Method prototype

```C#
DeleteMultiObjectResult  DeleteMultiObjects(DeleteMultiObjectRequest request);

void DeleteMultiObjects(DeleteObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request

[//]: # ".cssg-snippet-delete-multi-object"
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Sets the connection timeout period in milliseconds; this value is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Sets the read/write timeout period in milliseconds; this value is 45,000 ms by default
  .IsHttps(true)  // Sets HTTPS as the default request method
  .SetAppid("1250000000")  // Sets the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION")  // Sets the default bucket region
  .build();

String secretId = "COS_SECRETID"; // The SecretId of your TencentCloud API key
String secretKey = "COS_SECRETKEY"; // The SecretKey of your TencentCloud API key
long durationSecond = 600;          // Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
  DeleteMultiObjectRequest request = new DeleteMultiObjectRequest(bucket);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Set the return result format
  request.SetDeleteQuiet(false);
  // Object key
  string key = "exampleobject"; // The location of the object in the bucket, i.e. ObjectKey.
  List<string> objects = new List<string>();
  objects.Add(key);
  request.SetObjectKeys(objects);
  // Execute the request
  DeleteMultiObjectResult result = cosXml.DeleteMultiObjects(request);
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

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Construction method | Bucket name in the format: BucketName-APPID | string |
| quiet | SetDeleteQuiet | Returned results mode: false, verbose mode; true, quiet mode |bool |
| keys | SetObjectKeys | Set of deleted object keys |`List<string>`|
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys | SetSign | Indicates whether the signature verifies the header | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether the signature verifies the query parameters in the request URL | `List<string>` |

#### Response description

The result of the request is returned through DeleteObjectResult.

| Member Variable | Type | Description |
| -------- | ---- | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| deleteResult | [DeleteResult](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/DeleteResult.cs) | The returned result of the batch deleting operation |

>If the operation fails, the system will throw a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.


## Multipart operations


- Uploading objects with multipart upload: initialize the multipart upload, upload the parts, and complete the multipart upload
- Resuming a multipart upload: query the uploaded parts, upload the remaining parts, and complete the multipart upload
- Deleting uploaded parts

> Uploading the object via multipart upload, you can also use [Advanced APIs] (#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89) to upload (recommended).

### Querying multipart uploads

## Feature description 

This API queries the information on ongoing multipart uploads.

#### Method prototype

```C#
ListMultiUploadsResult ListMultiUploads(ListMultiUploadsRequest request);

void ListMultiUploads(ListMultiUploadsRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request

[//]: # ".cssg-snippet-list-multi-upload"
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Sets the connection timeout period in milliseconds; this value is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Sets the read/write timeout period in milliseconds; this value is 45,000 ms by default
  .IsHttps(true)  // Sets HTTPS as the default request method
  .SetAppid("1250000000")  // Sets the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION")  // Sets the default bucket region
  .build();

String secretId = "COS_SECRETID"; // The SecretId of your TencentCloud API key
String secretKey = "COS_SECRETKEY"; // The SecretKey of your TencentCloud API key
long durationSecond = 600;          // Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  ListMultiUploadsRequest request = new ListMultiUploadsRequest(bucket);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Execute the request
  ListMultiUploadsResult result = cosXml.ListMultiUploads(request);
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

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | -------- | ---------------------------------- | -------------- |
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys | SetSign | Indicates whether the signature verifies the header | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether the signature verifies the query parameters in the request URL | `List<string>` |

#### Response description

The result of the request is returned through ListMultiUploadsResult.

| Member Variable | Type | Description |
| -------------------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| listMultipartUploads | [ListMultipartUploads](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/ListMultipartUploads.cs) | Returns information on all multipart uploads in-progress in the bucket |

>If the operation fails, the system will throw a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.


### <span id = "INIT_MULIT_UPLOAD">Initializing a multipart upload </span>

## Feature description

This API initializes a multipart upload task.

#### Method prototype

```C#
InitMultipartUploadResult InitMultipartUpload(InitMultipartUploadRequest request);

void InitMultipartUpload(InitMultipartUploadRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request

[//]: # ".cssg-snippet-init-multi-upload"
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Sets the connection timeout period in milliseconds; this value is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Sets the read/write timeout period in milliseconds; this value is 45,000 ms by default
  .IsHttps(true)  // Sets HTTPS as the default request method
  .SetAppid("1250000000")  // Sets the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION")  // Sets the default bucket region
  .build();

String secretId = "COS_SECRETID"; // The SecretId of your TencentCloud API key
String secretKey = "COS_SECRETKEY"; // The SecretKey of your TencentCloud API key
long durationSecond = 600;          // Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
  string key = "exampleobject"; // The location of the object in the bucket, i.e. ObjectKey.
  InitMultipartUploadRequest request = new InitMultipartUploadRequest(bucket, key);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Execute the request
  InitMultipartUploadResult result = cosXml.InitMultipartUpload(request);
  // Request successful
  "exampleUploadId" = result.initMultipartUpload.uploadId; // To use later for uploadId multipart upload
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

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Construction method | Bucket name in the format: BucketName-APPID | string |
| key | Constructor or SetCosPath | [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | String |
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys | SetSign | Indicates whether the signature verifies the header | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether the signature verifies the query parameters in the request URL | `List<string>` |

#### Response description

The result of the request is returned through InitMultipartUploadResult.

| Member Variable | Type | Description |
| ------------------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| initMultipartUpload | [InitiateMultipartUpload](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/InitiateMultipartUpload.cs) | Returns the object's uploadId when the multipart upload is initialized |

>If the operation fails, the system will throw a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### <span id = "LIST_MULIT_UPLOAD"> Querying uploaded parts </span>

## Feature description

This API queries the uploaded parts of a specified multipart upload operation.

#### Method prototype

```C#
ListPartsResult ListParts(ListPartsRequest request);

void ListParts(ListPartsRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request

[//]: # ".cssg-snippet-list-parts"
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Sets the connection timeout period in milliseconds; this value is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Sets the read/write timeout period in milliseconds; this value is 45,000 ms by default
  .IsHttps(true)  // Sets HTTPS as the default request method
  .SetAppid("1250000000")  // Sets the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION")  // Sets the default bucket region
  .build();

String secretId = "COS_SECRETID"; // The SecretId of your TencentCloud API key
String secretKey = "COS_SECRETKEY"; // The SecretKey of your TencentCloud API key
long durationSecond = 600;          // Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
  string key = "exampleobject"; // The location of the object in the bucket, i.e. ObjectKey.
  string uploadId = "exampleUploadId"; // uploadId returned when the multipart upload is initialized
  ListPartsRequest request = new ListPartsRequest(bucket, key, uploadId);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Execute the request
  ListPartsResult result = cosXml.ListParts(request);
  // Request successful
  // List the parts that have been uploaded
  List<COSXML.Model.Tag.ListParts.Part> alreadyUploadParts = result.listParts.parts;
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

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ----------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Construction method | Bucket name in the format: BucketName-APPID | string |
| key | Constructor or SetCosPath | [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | String |
| uploadId | Constructor or SetUploadId | Identifies the uploadId of a specified multipart upload | string |
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys | SetSign | Indicates whether the signature verifies the header | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether the signature verifies the query parameters in the request URL | `List<string>` |

#### Response description

The result of the request is returned through ListPartsResult.

| Member Variable | Type | Description |
| --------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| listParts | [ListParts](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/ListParts.cs) | Returns the information on the parts uploaded to a specified uploadId in a multipart upload |

>If the operation fails, the system will throw a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### <span id = "MULIT_UPLOAD_PART"> Uploading parts</span>

## Feature description

This API uploads object parts.

#### Method prototype

```C#
UploadPartResult UploadPart(UploadPartRequest request);

void UploadPart(UploadPartRequest, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request

[//]: # ".cssg-snippet-upload-part"
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Sets the connection timeout period in milliseconds; this value is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Sets the read/write timeout period in milliseconds; this value is 45,000 ms by default
  .IsHttps(true)  // Sets HTTPS as the default request method
  .SetAppid("1250000000")  // Sets the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION")  // Sets the default bucket region
  .build();

String secretId = "COS_SECRETID"; // The SecretId of your TencentCloud API key
String secretKey = "COS_SECRETKEY"; // The SecretKey of your TencentCloud API key
long durationSecond = 600;          // Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
  string key = "exampleobject"; // The location of the object in the bucket, i.e. ObjectKey.
  string uploadId = "exampleUploadId"; // uploadId returned when the multipart upload is initialized
  int partNumber = 1; // Part number, increases with increments from 1
  string srcPath = @"temp-source-file";// Absolute path to the local file
  if (!File.Exists(srcPath)) {
    // If the target file does not exist, create a temporary file for testing
    File.WriteAllBytes(srcPath, new byte[1024]);
  }
  UploadPartRequest request = new UploadPartRequest(bucket, key, partNumber, 
    uploadId, srcPath);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Set the progress callback
  request.SetCosProgressCallback(delegate(long completed, long total)
  {
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
  });
  // Execute the request
  UploadPartResult result = cosXml.UploadPart(request);
  // Request successful
  // Get the eTag of the returned part for subsequent CompleteMultiUploads.
  "exampleETag" = result.eTag;
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

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ------------------------- | ------------------------------------------------------------ | --------------------------- |
| bucket | Construction method | Bucket name in the format: BucketName-APPID | string |
| key | Constructor or SetCosPath | [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | String |
| uploadId | Constructor or SetUploadId | Identifies the uploadId of a specified multipart upload | string |
| partNumber | Constructor or SetPartNumber | Identifies the number of a specified part; this value should be ≥ 1. | int |
| srcPath | Constructor | Absolute path to the local file uploaded to COS | string |
| data | Constructor | The byte array of the file uploaded to COS | byte[] |
| progressCallback | SetCosProgressCallback | Sets the callback for upload progress | Callback.OnProgressCallback |
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys | SetSign | Indicates whether the signature verifies the header | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether the signature verifies the query parameters in the request URL | `List<string>` |

#### Response description

The result of the request is returned through UploadPartResult.

| Member Variable | Type | Description |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| eTag | string | Returns the eTag of the object part |

>If the operation fails, the system will throw a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### <span id = "MULIT_UPLOAD_PART_COPY"> Copying a Part </span>

## Feature description
This API copies an object as a part.

#### Method prototype

```C#
UploadPartCopyResult PartCopy(UploadPartCopyRequest request)；

void PartCopy(UploadPartCopyRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request

[//]: # ".cssg-snippet-upload-part-copy"
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Sets the connection timeout period in milliseconds; this value is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Sets the read/write timeout period in milliseconds; this value is 45,000 ms by default
  .IsHttps(true)  // Sets HTTPS as the default request method
  .SetAppid("1250000000")  // Sets the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION")  // Sets the default bucket region
  .build();

String secretId = "COS_SECRETID"; // The SecretId of your TencentCloud API key
String secretKey = "COS_SECRETKEY"; // The SecretKey of your TencentCloud API key
long durationSecond = 600;          // Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  string sourceAppid = "1250000000"; // Account appid
  string sourceBucket = "sourcebucket-1250000000"; //" Source object bucket
  string sourceRegion = "COS_REGION"; // Source object bucket region
  string sourceKey = "sourceObject"; // Source object key
  // Construct source object attributes
  COSXML.Model.Tag.CopySourceStruct copySource = new CopySourceStruct(sourceAppid, 
    sourceBucket, sourceRegion, sourceKey);

  String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
  string key = "exampleobject"; // The location of the object in the bucket, i.e. ObjectKey.
  string uploadId = "exampleUploadId"; // uploadId  returned when the multipart upload is initialized
  int partNumber = 1; // Part number, increases with increments from 1
  UploadPartCopyRequest request = new UploadPartCopyRequest(bucket, key, 
    partNumber, uploadId);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Set the copy source
  request.SetCopySource(copySource);
  // Set the range of parts to be copied, e.g., 0 to 1M
  request.SetCopyRange(0, 1024 * 1024);
  // Execute the request
  UploadPartCopyResult result = cosXml.PartCopy(request);
  // Request successful
  // Get the eTag of the returned part for subsequent CompleteMultiUploads.
  "exampleETag" = result.copyObject.eTag;
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

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ------------------------- | ------------------------------------------------------------ | --------------------------- |
| bucket | Construction method | Bucket name in the format: BucketName-APPID | string |
| key | Constructor or SetCosPath | [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | String |
| uploadId | Constructor or SetUploadId | Identifies the uploadId of a specified multipart upload | string |
| partNumber | Constructor or SetPartNumber | Identifies the part number of a specified part; this value should be ≥ 1. | int |
| copySource | SetCopySource | Describes the source path of the copied data | CopySourceStruct |
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys | SetSign | Indicates whether the signature verifies the header | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether the signature verifies the query parameters in the request URL | `List<string>` |

#### Response description

The result of the request is returned through UploadPartResult.

| Member Variable | Type | Description |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| copyObject | [CopyObject](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/CopyObject.cs) | Returns the information on successfully copied objects |

>If the operation fails, the system will throw a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### <span id = "COMPLETE_MULIT_UPLOAD"> Completing a multipart upload </ span>

## Feature description

This API completes the multipart upload of the entire file.

#### Method prototype

```C#
CompleteMultipartUploadResult CompleteMultiUpload(CompleteMultipartUploadRequest request);

void CompleteMultiUpload(CompleteMultipartUploadRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request

[//]: # ".cssg-snippet-complete-multi-upload"
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Sets the connection timeout period in milliseconds; this value is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Sets the read/write timeout period in milliseconds; this value is 45,000 ms by default
  .IsHttps(true)  // Sets HTTPS as the default request method
  .SetAppid("1250000000")  // Sets the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION")  // Sets the default bucket region
  .build();

String secretId = "COS_SECRETID"; // The SecretId of your TencentCloud API key
String secretKey = "COS_SECRETKEY"; // The SecretKey of your TencentCloud API key 
long durationSecond = 600;          // Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
  string key = "exampleobject"; // The location of the object in the bucket, i.e. ObjectKey.
  string uploadId = "exampleUploadId"; // uploadId returned when the multipart upload is initialized
  CompleteMultipartUploadRequest request = new CompleteMultipartUploadRequest(bucket, 
    key, uploadId);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Concatenate uploaded parts in an ascending order by partNumber.
  // request.SetPartNumberAndETag(1, "Example Etag");
  String etag = "exampleETag";
  request.SetPartNumberAndETag(1, etag);
  // Execute the request
  CompleteMultipartUploadResult result = cosXml.CompleteMultiUpload(request);
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

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ----------------------- | ------------------------------------------------------------ | -------------------------- |
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| key | Constructor or SetCosPath | [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | String |
| uploadId | Constructor or SetUploadId | Identifies the uploadId of a specified multipart upload | string |
| partNumber | SetPartNumberAndETag | Identifies the part number of a specified part; this value must be >= 1 | int |
| eTag | SetPartNumberAndETag | Identifies the eTag returned by the upload of a specified part | string |
| partNumberAndETags | SetPartNumberAndETag | Identifies the part number and the eTag returned when a part is uploaded | `Dictionary ` |
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys | SetSign | Indicates whether the signature verifies the header | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether the signature verifies the query parameters in the request URL | `List<string>` |

#### Response description

The result of the request is returned through CompleteMultipartUploadResult.

| Member Variable | Type | Description |
| -------------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| CompleteResult | [CompleteMultipartUploadResult](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/CompleteResult.cs) | Returns the information on the successful upload of all parts |

>If the operation fails, the system will throw a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### <span id = "ABORT_MULIT_UPLOAD"> Aborting a multipart upload </ span>

## Feature description

This API aborts a multipart upload operation and deletes the uploaded parts.

#### Method prototype

```C#
AbortMultipartUploadResult AbortMultiUpload(AbortMultipartUploadRequest request);

void AbortMultiUpload(AbortMultipartUploadRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request

[//]: # ".cssg-snippet-abort-multi-upload"
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Sets the connection timeout period in milliseconds; this value is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Sets the read/write timeout period in milliseconds; this value is 45,000 ms by default
  .IsHttps(true)  // Sets HTTPS as the default request method
  .SetAppid("1250000000")  // Sets the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION")  // Sets the default bucket region
  .build();

String secretId = "COS_SECRETID"; // The SecretId of your TencentCloud API key
String secretKey = "COS_SECRETKEY"; // The SecretKey of your TencentCloud API key 
long durationSecond = 600;          // Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
  string key = "exampleobject"; // The location of the object in the bucket, i.e. ObjectKey.
  string uploadId = "exampleUploadId"; // uploadId returned when the multipart upload is initialized
  AbortMultipartUploadRequest request = new AbortMultipartUploadRequest(bucket, key, uploadId);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Execute the request
  AbortMultipartUploadResult result = cosXml.AbortMultiUpload(request);
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

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ----------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Construction method | Bucket name in the format: BucketName-APPID | string |
| key | Constructor or SetCosPath | [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | String |
| uploadId | Constructor or SetUploadId | Identifies the uploadId of a specified multipart upload | string |
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys | SetSign | Indicates whether the signature verifies the header | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether the signature verifies the query parameters in the request URL | `List<string>` |

#### Response description

The result of the request is returned through AbortMultipartUploadResult.

| Member Variable | Type | Description |
| -------- | ---- | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the system will throw a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

**Other operations**

### Restoring an archived object 

## Feature description

This API is used to restore an archived object for access.

#### Method prototype

```C#
RestoreObjectResult RestoreObject(RestoreObjectRequest request);

void RestoreObject(RestoreObjectRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request

[//]: # ".cssg-snippet-restore-object"
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Sets the connection timeout period in milliseconds; this value is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Sets the read/write timeout period in milliseconds; this value is 45,000 ms by default
  .IsHttps(true)  // Sets HTTPS as the default request method
  .SetAppid("1250000000")  // Sets the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION")  // Sets the default bucket region
  .build();

String secretId = "COS_SECRETID"; // The SecretId of your TencentCloud API key
String secretKey = "COS_SECRETKEY"; // The SecretKey of your TencentCloud API key 
long durationSecond = 600;          // Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
  string key = "exampleobject"; // The location of the object in the bucket, i.e. ObjectKey.
  RestoreObjectRequest request = new RestoreObjectRequest(bucket, key);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  Restoration time
  request.SetExpireDays(3);
  request.SetTier(COSXML.Model.Tag.RestoreConfigure.Tier.Bulk);

  // Execute the request
  RestoreObjectResult result = cosXml.RestoreObject(request);
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

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------- | ------------------------------------------------------------ | --------------------- |
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| key | Constructor or SetCosPath | [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | String |
| days | SetExpireDays | Sets the validity period of the temporary replica | int |
| tier | SetTier | For data restoration, Tier can specify the restoration type supported by CAS as Expedited, Standard, and Bulk. | RestoreConfigure.Tier |
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys | SetSign | Indicates whether the signature verifies the header | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether the signature verifies the query parameters in the request URL | `List<string>` |

#### Response description

The result of the request is returned through RestoreObjectResult.

| Member Variable | Type | Description |
| -------- | ---- | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the system will throw a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### Setting object ACL

## Feature description

This API is used to set the access control list (ACL) of a specified object in a bucket.

#### Method prototype

```C#
PutObjectACLResult PutObjectACL(PutObjectACLRequest request);

void PutObjectACL(PutObjectACLRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request

[//]: # ".cssg-snippet-put-object-acl"
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Sets the connection timeout period in milliseconds; this value is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Sets the read/write timeout period in milliseconds; this value is 45,000 ms by default
  .IsHttps(true)  // Sets HTTPS as the default request method
  .SetAppid("1250000000")  // Sets the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION")  // Sets the default bucket region
  .build();

String secretId = "COS_SECRETID"; // The SecretId of your TencentCloud API key
String secretKey = "COS_SECRETKEY"; // The SecretKey of your TencentCloud API key
long durationSecond = 600;          // Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

// To avoid hitting the ACL+policy limit of 1000
// We do not recommend setting an ACL for an individual object unless absolutely necessary. Objects are subjected to their bucket’s ACL by default. 
try
{
  String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
  string key = "exampleobject"; // The location of the object in the bucket, i.e. ObjectKey.
  PutObjectACLRequest request = new PutObjectACLRequest(bucket, key);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  Set private read and write permissions 
  request.SetCosACL(CosACL.PRIVATE);
  Grant the read permission to the account 1131975903 
  COSXML.Model.Tag.GrantAccount readAccount = new COSXML.Model.Tag.GrantAccount();
  readAccount.AddGrantAccount("1131975903", "1131975903");
  request.SetXCosGrantRead(readAccount);
  // Execute the request
  PutObjectACLResult result = cosXml.PutObjectACL(request);
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

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | --------------------------------------------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| key | Constructor or SetCosPath | [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | String |
| cosAcl | SetCosAcl | Sets the ACL permissions for the bucket | string |
| grantAccount | SetXCosGrantRead, SetXCosGrantWrite, or SetXCosReadWrite | Grants users read and write permissions | GrantAccount |
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys | SetSign | Indicates whether the signature verifies the header | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether the signature verifies the query parameters in the request URL | `List<string>` |

#### Response description

The result of the request is returned through PutObjectACLResult.

| Member Variable | Type | Description |
| -------- | ---- | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the system will throw a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### Querying object ACL

## Feature description

This API is used to query the ACL of an object.

#### Method prototype

```C#
GetObjectACLResult GetObjectACL(GetObjectACLRequest request);

void GetObjectACL(GetObjectACLRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request

[//]: # ".cssg-snippet-get-object-acl"
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Sets the connection timeout period in milliseconds; this value is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Sets the read/write timeout period in milliseconds; this value is 45,000 ms by default
  .IsHttps(true)  // Sets HTTPS as the default request method
  .SetAppid("1250000000")  // Sets the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION")  // Sets the default bucket region
  .build();

String secretId = "COS_SECRETID"; // The SecretId of your TencentCloud API key
String secretKey = "COS_SECRETKEY"; // The SecretKey of your TencentCloud API key
long durationSecond = 600;          // Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
  string key = "exampleobject"; // The location of the object in the bucket, i.e. ObjectKey.
  GetObjectACLRequest request = new GetObjectACLRequest(bucket, key);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Execute the request
  GetObjectACLResult result = cosXml.GetObjectACL(request);
  // Object’s ACL information
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

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Construction method | Bucket name in the format: BucketName-APPID | string |
| key | Constructor or SetCosPath | [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | String |
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys | SetSign | Indicates whether the signature verifies the header | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether the signature verifies the query parameters in the request URL | `List<string>` |

#### Response description

The result of the request is returned through GetObjectACLResult.

| Member Variable | Type | Description |
| ------------------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| accessControlPolicy | [AccessControlPolicy](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/AccessControlPolicy.cs) | Returns information on the object ACL |

>If the operation fails, the system will throw a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

## Advanced APIs (recommended)

### Uploading an object

## Feature description

This API automatically divides your data and lowers your usage threshold based on the size of your file when uploading to streamline the  multipart upload process.

#### Method prototype

```C#
void Upload(COSXMLUploadTask uploadTask);
```

#### Sample request

*COSXMLUploadTask** encapsulates async requests for simple upload and multipart upload APIs and supports pausing, resuming, and canceling upload requests. We recommend using this for object upload. The sample code is as follows:

[//]: # ".cssg-snippet-transfer-upload-object"
```java
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Sets the connection timeout period in milliseconds; this value is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Sets the read/write timeout period in milliseconds; this value is 45,000 ms by default
  .IsHttps(true)  // Sets HTTPS as the default request method
  .SetAppid("1250000000")  // Sets the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION")  // Sets the default bucket region
  .build();

String secretId = "COS_SECRETID"; // The SecretId of your TencentCloud API key
String secretKey = "COS_SECRETKEY"; // The SecretKey of your TencentCloud API key
long durationSecond = 600;          // Validity period of the request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

// Initialize TransferConfig
TransferConfig transferConfig = new TransferConfig();

// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
String cosPath = "exampleobject"; //The location identifier of the object in the bucket, i.e. the object key. 
string srcPath = @"temp-source-file";// Absolute path to the local file
if (!File.Exists(srcPath)) {
  // If the target file does not exist, create a temporary file for testing
  File.WriteAllBytes(srcPath, new byte[1024]);
}

// Upload the object
COSXMLUploadTask uploadTask = new COSXMLUploadTask(bucket, "COS_REGION", cosPath); // COS_REGION is the bucket region
uploadTask.SetSrcPath(srcPath);

// Synchronized call
var autoEvent = new AutoResetEvent(false);

uploadTask.progressCallback = delegate (long completed, long total)
{
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
};
uploadTask.successCallback = delegate (CosResult cosResult) 
{
    COSXML.Transfer.COSXMLUploadTask.UploadTaskResult result = cosResult as COSXML.Transfer.COSXMLUploadTask.UploadTaskResult;
    Console.WriteLine(result.GetResultInfo());
    string eTag = result.eTag;
    autoEvent.Set();
};
uploadTask.failCallback = delegate (CosClientException clientEx, CosServerException serverEx) 
{
    if (clientEx != null)
    {
        Console.WriteLine("CosClientException: " + clientEx);
    }
    if (serverEx != null)
    {
        Console.WriteLine("CosServerException: " + serverEx.GetInfo());
    }
    autoEvent.Set();
};
transferManager.Upload(uploadTask);
// Wait for the task to end
autoEvent.WaitOne();

// Cancel upload
cosxmlUploadTask.cancel();


// Pause upload
cosxmlUploadTask.pause();

// Resume upload
cosxmlUploadTask.resume();
```


#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------- | ------------------------------------------------------------ | --------------------------- |
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| key | Constructor or SetCosPath | [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | String |
| srcPath | Constructor | Absolute path to the local file uploaded to COS | string |
| progressCallback | SetCosProgressCallback | Sets the callback for upload progress | Callback.OnProgressCallback |
| successCallback | Member Variable       | Sets the callback for when the task is completed successfully                               | Callback.OnSuccessCallback          |
| failCallback      | Member Variable               | Sets the callback for when the task fails           | Callback.OnFailedCallback             |


#### Response description

The result of the request is returned through PutObjectResult.

| Member Variable | Type | Description |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| eTag | string | Returns the eTag of an object |

>If the operation fails, the system will throw a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.
