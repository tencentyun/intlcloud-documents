

## Overview

This document provides an overview of APIs and SDK code samples related to bucket tagging.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | Setting a bucket tag | Sets a tag for an existing bucket |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | Querying bucket tags | Queries the existing tags of a specified bucket |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | Deleting a bucket tag | Deletes a specified bucket tag |

## Setting Bucket Tag

#### Feature description

This API (PUT Bucket tagging) is used to set a tag for an existing bucket.

#### Method prototype

```
PutBucketTaggingResult putBucketTagging(PutBucketTaggingRequest request);

void putBucketTaggingAsync(PutBucketTaggingRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
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
  PutBucketTaggingRequest request = new PutBucketTaggingRequest(bucket);
  string akey = "aTagKey";
  string avalue = "aTagValue";
  string bkey = "bTagKey";
  string bvalue = "bTagValue";

  request.AddTag(akey, avalue);
  request.AddTag(bkey, bvalue);
   
  // Execute the request
  PutBucketTaggingResult result = cosXml.putBucketTagging(request);
  
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
| bucket | Bucket for which to set a tag in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | string |
| key | Tag key, which can contain letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots, colons, and slashes with a maximum length of 128 bytes | string |
| value | Tag value, which can contain letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots, colons, and slashes with a maximum length of 256 bytes | string |

#### Returned result description

| Member Variable | Description | Type |
| -------- | -------------------------------------------------------- | ---- |
| httpCode            | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed | int                 |

## Querying Bucket Tag

#### Feature description

This API (GET Bucket tagging) is used to query the existing tags of a specified bucket.

#### Method prototype

```
GetBucketTaggingResult getBucketTagging(GetBucketTaggingRequest request);

void getBucketTaggingAsync(GetBucketTaggingRequest request,COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
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
  GetBucketTaggingRequest request = new GetBucketTaggingRequest(bucket);   
  // Execute the request
  GetBucketTaggingResult result = cosXml.getBucketTagging(request);
  
  // Request succeeded
  Tagging tagging = result.tagging;
  Console.WriteLine(tagging);
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
| bucket | Bucket for which to query a tag in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | xxx  |

#### Returned result description

| Member Variable | Description | Type |
| -------- | -------------------------------------------------------- | ---- |
| httpCode            | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed | int                 |

## Deleting Bucket Tag

#### Feature description

This API (DELETE Bucket tagging) is used to delete an existing tag of a specified bucket.

#### Method prototype

```
DeleteBucketTaggingResult deleteBucketTagging(DeleteBucketTaggingRequest request);

void deleteBucketTaggingAsync(DeleteBucketTaggingRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
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
| bucket | Bucket for which to delete a tag in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | string |

#### Returned result description

| Member Variable | Description | Type |
| -------- | -------------------------------------------------------- | ---- |
| httpCode            | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed | int                 |
