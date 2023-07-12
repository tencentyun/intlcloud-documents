## Overview

This document provides an overview of APIs and SDK code samples related to object deletion.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------- |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting an object | Deletes an object from a bucket. |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket. |

## SDK API References

For the parameters and method description of all the APIs in the SDK, see [API Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Deleting a Single Object

#### Description

This API (`DELETE Object`) is used to delete a specified object.

#### Sample code

[//]: #	".cssg-snippet-delete-object"

```cs
try
{
  // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
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

> ?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/DeleteObject.cs).

## Deleting Multiple Objects

#### Description

The API (DELETE Multiple Objects) is used to delete multiple objects.

#### Sample code

[//]: #	".cssg-snippet-delete-multi-object"

```cs
try
{
  // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  DeleteMultiObjectRequest request = new DeleteMultiObjectRequest(bucket);
  // Set the return result format
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

> ?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/DeleteObject.cs).

## Deleting Objects with a Specified Prefix (Deleting a Folder)

#### Description

If you delete objects with a specified prefix, it will be like you delete a directory.
COS does not have the concept of directories, but you can use slashes (/) as the delimiter to simulate directories.
In COS, deleting a directory and the objects contained actually means deleting objects that have the same specified prefix. Currently, COS’s .NET SDK does not provide a standalone API to perform this operation. However, you can still do so with a combination of basic operations (query object list + batch delete objects).

#### Sample code

[//]: #	".cssg-snippet-delete-prefix"

```cs
try
{
  String nextMarker = null;

  // Request until there is no next page of data
  do
  {
    // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
    string bucket = "examplebucket-1250000000";
    string prefix = "folder1/"; // Specify a prefix.
    GetBucketRequest listRequest = new GetBucketRequest(bucket);
    // Obtain all objects and subdirectories in folder1/.
    listRequest.SetPrefix(prefix);
    listRequest.SetMarker(nextMarker);
    // Execute the list object request.
    GetBucketResult listResult = cosXml.GetBucket(listRequest);
    ListBucket info = listResult.listBucket;
    // List objects
    List<ListBucket.Contents> objects = info.contentsList;
    // nextMarker for the next page
    nextMarker = info.nextMarker;
    
    DeleteMultiObjectRequest deleteRequest = new DeleteMultiObjectRequest(bucket);
    // Set the return result format
    deleteRequest.SetDeleteQuiet(false);
    // List objects
    List<string> deleteObjects = new List<string>();
    foreach (var content in objects)
    {
      deleteObjects.Add(content.key);
    }
    deleteRequest.SetObjectKeys(deleteObjects);
    // Execute the batch delete request.
    DeleteMultiObjectResult deleteResult = cosXml.DeleteMultiObjects(deleteRequest);
    // Print the request result.
    Console.WriteLine(deleteResult.GetResultInfo());
  } while (nextMarker != null);
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

> ?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/DeleteObject.cs).
