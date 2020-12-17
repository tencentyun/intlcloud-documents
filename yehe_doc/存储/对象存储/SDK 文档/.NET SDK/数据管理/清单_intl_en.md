## Overview

This document provides an overview of APIs and SDK code samples related to COS inventory.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | -------------------- |
| [PUT Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30625) | Setting an inventory job | Sets an inventory job for a bucket |
| [GET Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30623) | Querying inventory jobs | Queries the inventory jobs of a bucket |
| [DELETE Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30626) | Deleting an inventory job | Deletes an inventory job from a bucket |

## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, see [Api Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Setting an Inventory Job

#### API description 

This API is used to create an inventory job for a bucket.

#### Sample code

[//]: # (.cssg-snippet-put-bucket-inventory)
```cs
try
{
  string inventoryId = "aInventoryId";
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  PutBucketInventoryRequest putRequest = new PutBucketInventoryRequest(bucket, inventoryId);
  putRequest.SetDestination("CSV", "100000000001", "examplebucket-1250000000", "ap-guangzhou","list1");
  putRequest.IsEnable(true);
  putRequest.SetScheduleFrequency("Daily");
  // Execute the request
  PutBucketInventoryResult putResult = cosXml.PutBucketInventory(putRequest); 
  
  // Request successful 
  Console.WriteLine(putResult.GetResultInfo());
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketInventory.cs).


#### Error codes

The following describes some common errors that may occur when making requests using this API.

| Error Code | Description | Status Code |
| --------------------- | -------------------------------------------- | -------------------- |
| InvalidArgument | Invalid parameter value | HTTP 400 Bad Request |
| TooManyConfigurations | The number of inventories has reached the upper limit of 1,000 | HTTP 400 Bad Request |
| AccessDenied          | Unauthorized access. You most likely do not have access permission for the bucket | HTTP 403 Forbidden   |

## Querying Inventory Jobs

#### API description 

This API is used to query the inventory jobs of a bucket.

#### Sample code

[//]: # (.cssg-snippet-get-bucket-inventory)
```cs
try
{
  string inventoryId = "aInventoryId";
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  GetBucketInventoryRequest getRequest = new GetBucketInventoryRequest(bucket);
  getRequest.SetInventoryId(inventoryId);
  
  GetBucketInventoryResult getResult = cosXml.GetBucketInventory(getRequest);
  
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketCORS.cs).

## Deleting an Inventory Job

#### API description 

This API is used to delete an inventory job from a bucket.

#### Sample code

[//]: # (.cssg-snippet-delete-bucket-inventory)
```cs
try
{
  string inventoryId = "aInventoryId";
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  DeleteBucketInventoryRequest deleteRequest = new DeleteBucketInventoryRequest(bucket);
  deleteRequest.SetInventoryId(inventoryId);
  DeleteBucketInventoryResult deleteResult = cosXml.DeleteBucketInventory(deleteRequest);
  
  // Request successful 
  Console.WriteLine(deleteResult.GetResultInfo());
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketCORS.cs).

