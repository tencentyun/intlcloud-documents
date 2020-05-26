## Overview

This document provides an overview of APIs and SDK code samples related to log management.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | -------------------------- |
| [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/17054) | Setting log management | Enables logging for the source bucket |
| [GET Bucket logging](https://intl.cloud.tencent.com/document/product/436/17053) | Querying log management | Queries the logging configuration information of the source bucket |

## Setting Log Management

#### Feature description

This API (PUT Bucket logging) is used to enable logging for the source bucket and store its access logs in a specified destination bucket.

#### Method prototype

```
PutBucketLoggingResult putBucketLogging(PutBucketLoggingRequest request);

void putBucketLoggingAsync(PutBucketLoggingRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request

```
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Set the connection timeout period in milliseconds, which is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Set the read/write timeout period in milliseconds, which is 45,000 ms by default
  .IsHttps(true)  // Set HTTPS as default request method
  .SetAppid("1250000000") // Set the `APPID` of your Tencent Cloud account
  .SetRegion("ap-guangzhou") // Set the default bucket region
  .Build();

string secretId = "COS_SECRETID";   //TencentCloud API key's SecretId
string secretKey = "COS_SECRETKEY"; // TencentCloud API key's SecretKey
long durationSecond = 600;          // Validity period of each request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  PutBucketLoggingRequest request = new PutBucketLoggingRequest(bucket);
  request.SetTarget("targetbucket-1250000000", "/abc");
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Execute the request
  PutBucketLoggingResult result = cosXml.putBucketLogging(request);
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

#### Parameter description

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| bucket            | Source bucket for which to enable the logging feature in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | string |
| targetBucket | Destination bucket where to store logs in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | string |
| prefix | Specified path in the destination bucket for storing logs | string

#### Returned result description

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |

## Querying Log Management

#### Feature description

This API (GET Bucket logging) is used to query the log configuration information of a specified bucket.

#### Method prototype

```
GetBucketLoggingResult getBucketLogging(GetBucketLoggingRequest request);

void getBucketLoggingAsync(GetBucketLoggingRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### Sample request

```
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  // Set the connection timeout period in milliseconds, which is 45,000 ms by default
  .SetReadWriteTimeoutMs(40000)  // Set the read/write timeout period in milliseconds, which is 45,000 ms by default
  .IsHttps(true)  // Set HTTPS as default request method
  .SetAppid("1250000000") // Set the `APPID` of your Tencent Cloud account
  .SetRegion("ap-guangzhou") // Set the default bucket region
  .Build();

string secretId = "COS_SECRETID";   //TencentCloud API key's SecretId
string secretKey = "COS_SECRETKEY"; // TencentCloud API key's SecretKey
long durationSecond = 600;          // Validity period of each request signature in seconds
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

try
{
  string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  GetBucketLoggingRequest request = new GetBucketLoggingRequest(bucket);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Execute the request
  GetBucketLoggingResult result = cosXml.getBucketLogging(request);
  // Request succeeded
  BucketLoggingStatus status = getResult.bucketLoggingStatus;
  if (status != null && status.loggingEnabled != null) {
    string targetBucket = status.loggingEnabled.targetBucket;
    string targetPrefix = status.loggingEnabled.targetPrefix;
  }
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

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| bucket            | Source bucket in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | string |

#### Returned result description

| Member Variable | Description | Type |
| ------------ | -------------------------------------------------------- | ------ |
| httpCode            | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed | int                 |
| targetBucket | Destination bucket for storing logs | string |
| targetPrefix | Destination bucket path for storing logs | string |
