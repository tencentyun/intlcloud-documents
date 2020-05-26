

## Overview

This document provides an overview of APIs and SDK code samples related to inventory.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | -------------------- |
| [PUT Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30625) | Setting an inventory job | Sets an inventory job in a bucket |
| [GET Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30623) | Querying inventory jobs | Queries inventory jobs for a bucket |
| [DELETE Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30626) | Deleting an inventory job | Deletes an inventory job of a bucket |

## Setting Inventory Job

#### Feature description

This API (PUT Bucket inventory) is used to create an inventory job in a bucket.

#### Method prototype

```
PutBucketInventoryResult putBucketInventory(PutBucketInventoryRequest request);

void putBucketInventoryAsync(PutBucketInventoryRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
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
  string inventoryId = "aInventoryId";
  string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  PutBucketInventoryRequest putRequest = new PutBucketInventoryRequest(bucket);
  putRequest.SetInventoryId(inventoryId);
  putRequest.SetDestination("CSV", "100000000001", "examplebucket-1250000000", "ap-guangzhou","list1");
  putRequest.IsEnable(true);
  putRequest.SetScheduleFrequency("Daily");
  // Execute the request
  PutBucketInventoryResult putResult = cosXml.putBucketInventory(putRequest); 
  
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
| bucket  | Bucket for which to set an inventory job in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | string |

For more information on other inventory configuration parameters, please see the API documentation.

#### Returned result description

| Member Variable | Description | Type |
| -------- | -------------------------------------------------------- | ---- |
| httpCode            | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed | int                 |

#### Error code description

Some frequent special errors that may occur with this request are listed below:

| Error code | Description | Status code |
| --------------------- | -------------------------------------------- | -------------------- |
| InvalidArgument | Invalid parameter value | HTTP 400 Bad Request |
| TooManyConfigurations | The number of inventories has reached the upper limit of 1,000 | HTTP 400 Bad Request |
| AccessDenied          | Unauthorized access. You probably do not have access to the bucket. | HTTP 403 Forbidden |

## Querying Inventory Job

#### Feature description

This API (GET Bucket inventory) is used to query the inventory job information in a bucket.

#### Method prototype

```
GetBucketInventoryResult getBucketInventory(GetBucketInventoryRequest request);

void getBucketInventoryAsync(GetBucketInventoryRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);

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
  string inventoryId = "aInventoryId";
  string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  GetBucketInventoryRequest getRequest = new GetBucketInventoryRequest(bucket);
  getRequest.SetInventoryId(inventoryId);
  
  GetBucketInventoryResult getResult = cosXml.getBucketInventory(getRequest);
  
  InventoryConfiguration configuration = getResult.inventoryConfiguration;
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
| ----------- | ------------------------------------------------------------ | ------ |
| bucket | Bucket for which to query an inventory job in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | bucket |
| inventoryId | Inventory job name. Valid characters: a-z, A-Z, 0-9, -, _, .             | string |

#### Returned result description

| Member Variable | Description | Type |
| ---------------------- | -------------------------------------------------------- | ---------------------- |
| httpCode            | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed | int                 |
| inventoryConfiguration | Inventory configuration                                                 | InventoryConfiguration |

## Deleting Inventory Job

#### Feature description

This API (DELETE Bucket inventory) is used to delete a specified inventory job of a bucket.

#### Method prototype

```
DeleteBucketInventoryResult deleteBucketInventory(DeleteBucketInventoryRequest request);

void deleteInventoryAsync(DeleteBucketInventoryRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
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
  string inventoryId = "aInventoryId";
  string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  DeleteBucketInventoryRequest deleteRequest = new DeleteBucketInventoryRequest(bucket);
  deleteRequest.SetInventoryId(inventoryId);
  DeleteBucketInventoryResult deleteResult = cosXml.deleteBucketInventory(deleteRequest);
  
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
| ----------- | ------------------------------------------------------------ | ------ |
| bucket  | Bucket for which to delete an inventory job in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | string |
| inventoryId | Inventory job name. Valid characters: a-z, A-Z, 0-9, -, _, .             | string |

#### Returned result description

| Member Variable | Description | Type |
| -------- | -------------------------------------------------------- | ---- |
| httpCode            | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed | int                 |
