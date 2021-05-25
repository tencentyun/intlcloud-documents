## Overview
This document provides an overview of APIs and SDK code samples related to cross-origin access, lifecycle, versioning, and cross-region replication.

**Cross-origin access**

| API | Operation | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting cross-origin access configuration | Sets the cross-origin access permissions of a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying cross-origin access configuration | Queries the cross-origin access configuration of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting cross-origin access configuration | Deletes the cross-origin access configuration of a bucket |

**Lifecycle**

| API | Operation | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle | Sets the lifecycle management configuration of a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying lifecycle | Queries the lifecycle management configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting lifecycle | Deletes the lifecycle management configuration of a bucket |

**Versioning**

| API | Operation | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets the versioning configuration of a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning information of a bucket |

**Cross-region replication**

| API | Operation | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-region replication | Sets the cross-region replication rules of a bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying cross-region replication | Queries the cross-region replication rules of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting cross-region replication | Deletes the cross-region replication rules of a bucket |

## Cross-origin access
### Setting cross-origin configuration

## Feature description

This API is used to set the cross-origin access configuration of a bucket.

#### Method prototype
```C#
PutBucketCORSResult PutBucketCORS(PutBucketCORSRequest request);

void PutBucketCORS(PutBucketCORSRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request
[//]: # ".cssg-snippet-put-bucket-cors"
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
  PutBucketCORSRequest request = new PutBucketCORSRequest(bucket);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Set the configurations on cross-origin access (CORS)
  COSXML.Model.Tag.CORSConfiguration.CORSRule corsRule = 
    new COSXML.Model.Tag.CORSConfiguration.CORSRule();
  corsRule.id = "corsconfigureId";
  corsRule.maxAgeSeconds = 6000;
  corsRule.allowedOrigin = "http://cloud.tencent.com";

  corsRule.allowedMethods = new List<string>();
  corsRule.allowedMethods.Add("PUT");

  corsRule.allowedHeaders = new List<string>();
  corsRule.allowedHeaders.Add("Host");

  corsRule.exposeHeaders = new List<string>();
  corsRule.exposeHeaders.Add("x-cos-meta-x1");

  request.SetCORSRule(corsRule);

  // Execute the request
  PutBucketCORSResult result = cosXml.PutBucketCORS(request);
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
|-----|-----|-----|------|
| bucket | Construction method | Bucket name in the format: BucketName-APPID | string |
| corsRule | SetCORSRule | Sets the cross-origin access configuration of a bucket | CORSConfiguration.CORSRule |
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys | SetSign | Indicates whether the signature verifies the header | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether the signature verifies the query parameters in the request URL | `List<string>` |

#### Response description
The result of the request is returned through PutBucketCORSResult.

| Member Variable | Type | Description |
|-----|-----|----|
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |

### Querying cross-origin access configuration

## Feature description

This API is used to query the cross-origin access configuration of a bucket.

#### Method prototype
```C#
GetBucketCORSResult GetBucketCORS(GetBucketCORSRequest request);

void GetBucketCORS(GetBucketCORSRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request
[//]: # ".cssg-snippet-get-bucket-cors"
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
  GetBucketCORSRequest request = new GetBucketCORSRequest(bucket);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Execute the request
  GetBucketCORSResult result = cosXml.GetBucketCORS(request);
  // Bucket CORS configuration 
  CORSConfiguration conf = result.corsConfiguration;
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
|-----|-----|-----|------|
| bucket | Construction method | Bucket name in the format: BucketName-APPID | string |
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys | SetSign | Indicates whether the signature verifies the header | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether the signature verifies the query parameters in the request URL | `List<string>` |

#### Response description
The result of the request is returned through GetBucketCORSResult.

| Member Variable | Type | Description |
|-----|-----|----|
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| corsConfiguration | [CORSConfiguration](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/CORSConfiguration.cs) | Returns the CORS configuration of the bucket |

### Deleting cross-origin configuration

## Feature description

This API is used to delete the cross-origin access configuration of a bucket.

#### Method prototype
```C#
DeleteBucketCORSResult DeleteBucketCORS(DeleteBucketCORSRequest request);

void DeleteBucketCORS(DeleteBucketCORSRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request
[//]: # ".cssg-snippet-delete-bucket-cors"
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
  DeleteBucketCORSRequest request = new DeleteBucketCORSRequest(bucket);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Execute the request
  DeleteBucketCORSResult result = cosXml.DeleteBucketCORS(request);
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
|-----|-----|-----|------|
| bucket | Construction method | Bucket name in the format: BucketName-APPID | string |
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys | SetSign | Indicates whether the signature verifies the header | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether the signature verifies the query parameters in the request URL | `List<string>` |

#### Response description
The result of the request is returned through DeleteBucketCORSResult.

| Member Variable | Type | Description |
|-----|-----|----|
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |


## Lifecycle
### Setting a lifecycle configuration

## Feature description

This API is used to set the lifecycle configuration of a bucket.

#### Method prototype
```C#
PutBucketLifecycleResult PutBucketLifecycle(PutBucketLifecycleRequest request);

void PutBucketLifecycle(PutBucketLifecycleRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request
[//]: # ".cssg-snippet-put-bucket-lifecycle"
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
  PutBucketLifecycleRequest request = new PutBucketLifecycleRequest(bucket);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  Set the lifecycle
  LifecycleConfiguration.Rule rule = new LifecycleConfiguration.Rule();
  rule.id = "lfiecycleConfigureId";
  rule.status = "Enabled"; //Enabled，Disabled

  rule.filter = new COSXML.Model.Tag.LifecycleConfiguration.Filter();
  rule.filter.prefix = "2/";

  Specify the operation of deleting expired parts
  rule.abortIncompleteMultiUpload = new LifecycleConfiguration.AbortIncompleteMultiUpload();
  rule.abortIncompleteMultiUpload.daysAfterInitiation = 2;

  request.SetRule(rule);

  // Execute the request
  PutBucketLifecycleResult result = cosXml.PutBucketLifecycle(request);
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
|-----|-----|-----|------|
| bucket | Construction method | Bucket name in the format: BucketName-APPID | string |
| rule | SetRule | Sets the lifecycle configuration of a bucket | LifecycleConfiguration.Rule |
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys | SetSign | Indicates whether the signature verifies the header | `List` |
| queryParameterKeys | SetSign | Indicates whether the signature verifies the query parameters in the request URL | `List<string>` |

#### Response description
The result of the request is returned through PutBucketLifecycleResult.

| Member Variable | Type | Description |
|-----|-----|----|
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |


### Querying a lifecycle configuration

## Feature description

This API is used to query the lifecycle configuration of a bucket.

#### Method prototype
```C#
GetBucketLifecycleResult GetBucketLifecycle(GetBucketLifecycleRequest request);

void GetBucketLifecycle(GetBucketLifecycleRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request
[//]: # ".cssg-snippet-get-bucket-lifecycle"
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
  GetBucketLifecycleRequest request = new GetBucketLifecycleRequest(bucket);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Execute the request
  GetBucketLifecycleResult result = cosXml.GetBucketLifecycle(request);
  // Bucket lifecycle configuration
  LifecycleConfiguration conf = result.lifecycleConfiguration;
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
|-----|-----|-----|------|
| bucket | Construction method | Bucket name in the format: BucketName-APPID | string |
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys | SetSign | Indicates whether the signature verifies the header | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether the signature verifies the query parameters in the request URL | `List<string>` |

#### Response description
The result of the request is returned through GetBucketLifecycleResult.

| Member Variable | Type | Description |
|-----|-----|----|
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| lifecycleConfiguration | [LifecycleConfiguration](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/LifecycleConfiguration.cs) | Returns the lifecycle configuration of the bucket |


### Deleting a lifecycle configuration 

## Feature description

This API is used to delete the lifecycle configuration of a bucket.

#### Method prototype
```C#
DeleteBucketLifecycleResult DeleteBucketLifecycle(DeleteBucketLifecycleRequest request);

void DeleteBucketLifecycle(DeleteBucketLifecycleRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request
[//]: # ".cssg-snippet-delete-bucket-lifecycle"
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
  DeleteBucketLifecycleRequest request = new DeleteBucketLifecycleRequest(bucket);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Execute the request
  DeleteBucketLifecycleResult result = cosXml.DeleteBucketLifecycle(request);
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
|-----|-----|-----|------|
| bucket | Construction method | Bucket name in the format: BucketName-APPID | string |
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys | SetSign | Indicates whether the signature verifies the header | `List<string>` |
| queryParameterKeys | SetSign | Indicates whether the signature verifies the query parameters in the request URL | `List<string>` |

#### Response description
The result of the request is returned through DeleteBucketLifecycleResult.

| Member Variable | Type | Description |
|-----|-----|----|
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |


## Versioning
### Setting versioning

## Feature description

This API is used to set the versioning configuration of a specified bucket.

#### Method prototype
```C#
PutBucketVersioningResult PutBucketVersioning(PutBucketVersioningRequest request);
void PutBucketVersioning(PutBucketVersioningRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request

[//]: # ".cssg-snippet-put-bucket-versioning"
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

String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
PutBucketVersioningRequest request = new PutBucketVersioningRequest(bucket);
// Set the validity period of the signature
request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
request.IsEnableVersionConfig(true); //true: enable versioning; false: suspend versioning

// Use the sync method
try
{
  PutBucketVersioningResult result = cosXml.PutBucketVersioning(request);
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

#### Parameter description

| Parameter Name | Description | Type |
| ----| ---- | ---- |
| bucket | Bucket name in the format: BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| isEnable | Whether to enable versioning: <br><li>true: enable<br><li>false: suspend | bool |
| signStartTimeSecond | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys |  Indicates whether the signature verifies the header | `List<string>`|
| queryParameterKeys |  Indicates whether the signature verifies the query parameters in the request URL | `List<string>`|


#### Response description
The result of the request is returned through PutBucketVersioningResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the system will throw a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.


### Querying versioning

## Feature description

This API is used to query the versioning information of a specified bucket.

#### Method prototype
```C#
GetBucketVersioningResult GetBucketVersioning(GetBucketVersioningRequest request);
void GetBucketVersioning(GetBucketVersioningRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request
[//]: # ".cssg-snippet-get-bucket-versioning"
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

String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketVersioningRequest request = new GetBucketVersioningRequest(bucket);

// Use the sync method
try
{
  GetBucketVersioningResult result = cosXml.GetBucketVersioning(request);
  // Bucket lifecycle configuration
  VersioningConfiguration conf =  result.versioningConfiguration;
}
catch (COSXML.CosException.CosClientException clientEx)
{
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

#### Parameter description
| Parameter Name | Description | Type |
| ----| ---- | ---- |
| bucket | Bucket name in the format: BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| signStartTimeSecond | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys |  Indicates whether the signature verifies the header | `List<string>`|
| queryParameterKeys |  Indicates whether the signature verifies the query parameters in the request URL | `List<string>`|


#### Response description
The result of the request is returned through GetBucketVersioningResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
|versioningConfiguration|[VersioningConfiguration](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/VersioningConfiguration.cs)|Versioning configuration information|

>If the operation fails, the system will throw a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.


## Cross-region replication
### Setting cross-region replication

## Feature description

This API is used to set the cross-region replication rules of a bucket.

#### Method prototype

```C#
PutBucketReplicationResult PutBucketReplication(PutBucketReplicationRequest request);
void PutBucketReplication(PutBucketReplicationRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request

[//]: # ".cssg-snippet-put-bucket-replication"
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

String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
string ownerUin = "100000000001"; //Replication initiator identifier: OwnerUin
string subUin = "100000000001"; //Replication initiator identifier: SubUin
PutBucketReplicationRequest request = new PutBucketReplicationRequest(bucket);
// Set replication
PutBucketReplicationRequest.RuleStruct ruleStruct = 
  new PutBucketReplicationRequest.RuleStruct();
ruleStruct.id = "replication_01"; // Used to identify the name of the replication rule
ruleStruct.isEnable = true; // Indicates whether the rule is enabled. true: enabled; false: not enabled
ruleStruct.appid = "1250000000"; // APPID
ruleStruct.region = "ap-beijing"; // Destination bucket region
ruleStruct.bucket = "destinationbucket-1250000000"; // Format: BucketName-APPID
ruleStruct.prefix = "34"; // Prefix matching policy
List<PutBucketReplicationRequest.RuleStruct> ruleStructs = 
  new List<PutBucketReplicationRequest.RuleStruct>();
ruleStructs.Add(ruleStruct);
request.SetReplicationConfiguration(ownerUin, subUin, ruleStructs);

// Use the sync method
try
{
  PutBucketReplicationResult result = cosXml.PutBucketReplication(request);
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

#### Parameter description
| Parameter Name | Description | Type |
| ----| ---- | ---- |
| bucket | Bucket naming in the format: BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| ownerUin  | Replication initiator identifier: OwnerUin  | string |
| subUin  | Replication initiator identifier: SubUin    | string |
| ruleStruct  | Indicates whether the signature verifies the query parameters in the request URL | RuleStruct |
| signStartTimeSecond | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys |  Indicates whether the signature verifies the header | `List<string>`|
| queryParameterKeys |  Indicates whether the signature verifies the query parameters in the request URL | `List<string>`|


#### Response description
The result of the request is returned through PutBucketReplicationResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the system will throw a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.


### Querying cross-region replication

## Feature description

This API is used to query the cross-region replication rules of a specified bucket.

#### Method prototype
```C#
GetBucketReplicationResult GetBucketReplication(GetBucketReplicationRequest request);
void GetBucketReplication(GetBucketReplicationRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request
[//]: # ".cssg-snippet-get-bucket-replication"
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

String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketReplicationRequest request = new GetBucketReplicationRequest(bucket);

// Use the sync method
try
{
  GetBucketReplicationResult result = cosXml.GetBucketReplication(request);
  // Bucket cross-region replication configuration
  ReplicationConfiguration conf =  result.replicationConfiguration;
}
catch (COSXML.CosException.CosClientException clientEx)
{
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

#### Parameter description
| Parameter Name | Description | Type |
| ----| ---- | ---- |
| bucket | Bucket name in the format: BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| signStartTimeSecond | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys |  Indicates whether the signature verifies the header | `List<string>`|
| queryParameterKeys |  Indicates whether the signature verifies the query parameters in the request URL | `List<string>`|

#### Response description
The result of the request is returned through GetBucketReplicationResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
|replicationConfiguration|[ReplicationConfiguration](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/ReplicationConfiguration.cs)|Cross-origin access configuration|


>If the operation fails, the system will throw a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.


## Deleting cross-region replication

## Feature description

This API is used to delete the cross-region replication rules of a bucket.

#### Method prototype
```C#
DeleteBucketReplicationResult DeleteBucketReplication(DeleteBucketReplicationRequest request);
void DeleteBucketReplication(DeleteBucketReplicationRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request
[//]: # ".cssg-snippet-delete-bucket-replication"
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

String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
DeleteBucketReplicationRequest request = new DeleteBucketReplicationRequest(bucket);

// Use the sync method
try
{
  DeleteBucketReplicationResult result = cosXml.DeleteBucketReplication(request);
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

#### Parameter description
| Parameter Name | Description | Type |
| ----| ---- | ---- |
| bucket | Bucket name in the format: BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| signStartTimeSecond | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys |  Indicates whether the signature verifies the header | `List<string>`|
| queryParameterKeys |  Indicates whether the signature verifies the query parameters in the request URL | `List<string>`|


#### Response description
The result of the request is returned through DeleteBucketReplicationResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the system will throw a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.
