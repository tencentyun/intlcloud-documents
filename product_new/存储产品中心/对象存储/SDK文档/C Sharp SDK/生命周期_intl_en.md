## Overview
This document provides an overview of APIs and SDK code samples related to lifecycles.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle | Sets the lifecycle management configuration of a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying lifecycle | Queries the lifecycle management configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting lifecycle | Deletes the lifecycle management configuration of a bucket |

## Setting lifecycle

#### Feature description

This API is used to set the lifecycle configuration of a bucket.

#### Method prototype
```C#
PutBucketLifecycleResult PutBucketLifecycle(PutBucketLifecycleRequest request);

void PutBucketLifecycle(PutBucketLifecycleRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request
[//]: # (.cssg-snippet-put-bucket-lifecycle)
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Sets the connection timeout period in milliseconds; this value is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Sets the read/write timeout period in milliseconds; this value is 45,000 ms by default
  .IsHttps(true)  // Sets HTTPS as the default request method
  .SetAppid("1250000000") // Sets the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION") // Sets the default bucket region
  .Build();

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
  // Set the lifecycle
  LifecycleConfiguration.Rule rule = new LifecycleConfiguration.Rule();
  rule.id = "lfiecycleConfigureId";
  rule.status = "Enabled"; //Enabled，Disabled

  rule.filter = new COSXML.Model.Tag.LifecycleConfiguration.Filter();
  rule.filter.prefix = "2/";

  // Specify the operation for deleting expired parts
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
|bucket| Constructor | Bucket for which to set lifecycle in the format BucketName-APPID |string|
|rule|SetRule| Sets the lifecycle configuration of a bucket |LifecycleConfiguration.Rule|
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
|headerKeys|SetSign| Signature request header |`List<string>`|
|queryParameterKeys|SetSign| Signature request parameter |`List<string>`|

#### Response description

The result of the request is returned through PutBucketLifecycleResult.

| Member Variable | Type | Description |
|-----|-----|----|
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |


## Querying Lifecycle

#### Feature description

This API is used to query the lifecycle management configuration of a bucket.

#### Method prototype
```C#
GetBucketLifecycleResult GetBucketLifecycle(GetBucketLifecycleRequest request);

void GetBucketLifecycle(GetBucketLifecycleRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request
[//]: # (.cssg-snippet-get-bucket-lifecycle)
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Sets the connection timeout period in milliseconds; this value is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Sets the read/write timeout period in milliseconds; this value is 45,000 ms by default
  .IsHttps(true)  // Sets HTTPS as the default request method
  .SetAppid("1250000000") // Sets the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION") // Sets the default bucket region
  .Build();

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
|bucket| Constructor | Bucket for which to query lifecycle in the format BucketName-APPID |string|
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
|headerKeys|SetSign| Signature request header |`List<string>`|
|queryParameterKeys|SetSign| Signature request parameter |`List<string>`|

#### Response description

The result of the request is returned through GetBucketLifecycleResult.

| Member Variable | Type | Description |
|-----|-----|----|
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure  |
|lifecycleConfiguration|[LifecycleConfiguration](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/LifecycleConfiguration.cs)| Returns the lifecycle configuration information of a bucket |


## Deleting a lifecycle configuration

#### Feature description

This API is used to delete the lifecycle management configuration of a bucket.

#### Method prototype
```C#
DeleteBucketLifecycleResult DeleteBucketLifecycle(DeleteBucketLifecycleRequest request);

void DeleteBucketLifecycle(DeleteBucketLifecycleRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```


#### Sample request

[//]: # (.cssg-snippet-delete-bucket-lifecycle)
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Sets the connection timeout period in milliseconds; this value is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Sets the read/write timeout period in milliseconds; this value is 45,000 ms by default
  .IsHttps(true)  // Sets HTTPS as the default request method
  .SetAppid("1250000000") // Sets the APPID of your Tencent Cloud account
  .SetRegion("COS_REGION") // Sets the default bucket region
  .Build();

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
|bucket| Constructor | Bucket for which to delete the lifecycle configuration in the format BucketName-APPID |string|
| signStartTimeSecond | SetSign | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | SetSign  | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
|headerKeys|SetSign| Signature request header |`List<string>`|
|queryParameterKeys|SetSign| Signature request parameter |`List<string>`|

#### Response description

The result of the request is returned through DeleteBucketLifecycleResult.

| Member Variable | Type | Description |
|-----|-----|----|
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |

