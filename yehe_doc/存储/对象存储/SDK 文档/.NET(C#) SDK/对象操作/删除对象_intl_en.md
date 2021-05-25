## Overview

This document provides an overview of APIs and SDK sample codes related to deleting objects.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes a specified object from a bucket |
| [DELETE Multiple Object](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket in a single request |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, see [Api Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Deleting a Single Object

#### API description 

This API is used to delete a specified object from a bucket.

#### Sample code

[//]: # ".cssg-snippet-delete-object"
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket in the format: BucketName-APPID
  string key = "exampleobject"; // Object key
  DeleteObjectRequest request = new DeleteObjectRequest(bucket, key);
  // Execute the request
  DeleteObjectResult result = cosXml.DeleteObject(request);
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

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/DeleteObject.cs).

## Deleting Multiple Objects

#### API description 

This API is used to delete multiple objects in a single request.

#### Sample code

[//]: # ".cssg-snippet-delete-multi-object"
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket in the format: BucketName-APPID
  DeleteMultiObjectRequest request = new DeleteMultiObjectRequest(bucket);
  // Set the response mode
  request.SetDeleteQuiet(false);
  // Object key
  string key = "exampleobject"; // Object key
  List<string> objects = new List<string>();
  objects.Add(key);
  request.SetObjectKeys(objects);
  // Execute the request
  DeleteMultiObjectResult result = cosXml.DeleteMultiObjects(request);
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

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/DeleteObject.cs).

