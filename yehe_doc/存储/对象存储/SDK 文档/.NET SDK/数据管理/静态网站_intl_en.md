

## Overview

This document provides an overview of APIs and SDK code samples related to static website.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ---------------- | ------------------------ |
| [PUT Bucket website](https://intl.cloud.tencent.com/document/product/436/30617) | Setting a static website | Sets static website configuration for a bucket |
| [GET Bucket website](https://intl.cloud.tencent.com/document/product/436/30616) | Querying static website configuration | Queries the static website configuration information of a bucket |
| [DELETE Bucket website](https://intl.cloud.tencent.com/document/product/436/30629) | Deleting static website configuration | Deletes the static website configuration of a bucket |

## Setting Static Website

#### Feature description

This API (PUT Bucket website) is used to configure a static website for a bucket.

#### Method prototype

```
PutBucketWebsiteResult putBucketWebsite(PutBucketWebsiteRequest request);

void putBucketWebsiteAsync(PutBucketWebsiteRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
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
  PutBucketWebsiteRequest putRequest = new PutBucketWebsiteRequest(instance.bucketForBucketTest);
  putRequest.SetIndexDocument("index.html");
  putRequest.SetErrorDocument("eroror.html");
  putRequest.SetRedirectAllRequestTo("index.html");
  PutBucketWebsiteResult putResult = cosXml.putBucketWebsite(putRequest);
  
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
| --------------------- | ------------------------------------------------------------ | ------ |
| bucket | Bucket for which to set a static website in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | string |
| IndexDocument               | Index document                                                     | string |
| ErrorDocument         | Error document                                                     | string |
| RedirectAllRequestsTo       | Redirects all requests                                               | string    |
| rules                 | Redirect rule                                                   | object |

#### Returned result description

| Member Variable | Description | Type |
| -------- | -------------------------------------------------------- | ---- |
| httpCode            | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed | int                 |

## Querying Static Website Configuration

#### Feature description

This API (GET Bucket website) is used to query the configuration information of a static website associated with a bucket.

#### Method prototype

```
etBucketWebsiteResult getBucketWebsite(GetBucketWebsiteRequest request);

void getBucketWebsiteAsync(GetBucketWebsiteRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
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
  DeleteBucketTaggingRequest request = new DeleteBucketTaggingRequest(bucket);   
  // Execute the request
  DeleteBucketTaggingResult result = cosXml.deleteBucketTagging(request);
  
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
| -------- | ------------------------------------------------------------ | ---- |
| bucket | Bucket for which to query static website configuration in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | xxx  |

#### Returned result description

| Member Variable | Description | Type |
| -------- | -------------------------------------------------------- | ---- |
| httpCode            | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed | int                 |

## Deleting Static Website Configuration

#### Feature description

This API (DELETE Bucket website) is used to delete the static website configuration of a bucket.

#### Method prototype

```
DeleteBucketWebsiteResult deleteBucketWebsite(DeleteBucketWebsiteRequest request);

void deleteBucketWebsiteAsync(DeleteBucketWebsiteRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
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
  DeleteBucketTaggingRequest request = new DeleteBucketTaggingRequest(bucket);   
  // Execute the request
  DeleteBucketTaggingResult result = cosXml.deleteBucketTagging(request);
  
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
| -------- | ------------------------------------------------------------ | ------ |
| bucket | Bucket for which to delete static website configuration in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | string |

#### Returned result description

| Member Variable | Description | Type |
| -------- | -------------------------------------------------------- | ---- |
| httpCode            | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed | int                 |
