## Overview

This document provides an overview of APIs and SDK code samples related to versioning.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets the versioning configuration of a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning information of a bucket |

## Setting versioning

#### Feature description

This API is used to set the versioning configuration of a specified bucket.

#### Method prototype
```C#
PutBucketVersioningResult PutBucketVersioning(PutBucketVersioningRequest request);
void PutBucketVersioning(PutBucketVersioningRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-versioning)
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
| bucket | Bucket for which to enable or suspend versioning in the format: BucketName-APPID. For more information, please see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| isEnable | Whether to enable versioning: <br><li>true: enable<br><li>false: suspend | bool |
| signStartTimeSecond | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys          | Signature request header                | `List<string>` |
| queryParameterKeys | SetSign | Signature request parameter | `List<string>` |


#### Response description
The result of the request is returned through PutBucketVersioningResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the system will throw a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.


## Querying versioning

#### Feature description

This API is used to query the versioning information of a specified bucket.

#### Method prototype
```C#
GetBucketVersioningResult GetBucketVersioning(GetBucketVersioningRequest request);
void GetBucketVersioning(GetBucketVersioningRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request
[//]: # (.cssg-snippet-get-bucket-versioning)
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
| bucket | Bucket for which to query versioning in the format: BucketName-APPID. For more information, please see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| signStartTimeSecond | Start time of the signature's validity period in the format of a Unix timestamp, e.g., 1557902800 | long |
| durationSecond      | Signature validity period measured in seconds, e.g., if a signature is valid for 1 minute, this value would be 60     | long           |
| headerKeys          | Signature request header                | `List<string>` |
| queryParameterKeys | SetSign | Signature request parameter | `List<string>` |


#### Response description
The result of the request is returned through GetBucketVersioningResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
|versioningConfiguration|[VersioningConfiguration](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/VersioningConfiguration.cs)|Versioning configuration information|

>If the operation fails, the system will throw a [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.
