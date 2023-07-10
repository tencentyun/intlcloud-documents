## Overview

This document provides an overview of APIs and SDK code samples related to basic bucket operations.


| API | Operation | Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service (List Buckets)](https://intl.cloud.tencent.com/document/product/436/8291) | Querying a bucket list | Queries the list of all buckets under a specified account |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates bucket under a specified account |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Checking a bucket and its permissions | Checks whether a bucket exists and you have access permission for it |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket from a specified account |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, see [Api Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Querying a Bucket List

#### API description

This API is used to query the list of all buckets under a specified account.

#### Sample code

[//]: # ".cssg-snippet-get-service"
```cs
try
{
  GetServiceRequest request = new GetServiceRequest();
  // Execute the request
  GetServiceResult result = cosXml.GetService(request);
  // Get the list of all buckets
  List<ListAllMyBuckets.Bucket> allBuckets = result.listAllMyBuckets.buckets;
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

>?For more sample, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/GetService.cs).

## Creating a Bucket

#### API description

This API is used to create a bucket.

#### Sample code

[//]: # ".cssg-snippet-put-bucket"
```cs
try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  PutBucketRequest request = new PutBucketRequest(bucket);
  // Execute the request
  PutBucketResult result = cosXml.PutBucket(request);
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/PutBucket.cs).

## Checking a Bucket and Its Permissions

#### API description

This API is used to check whether a bucket exists and whether you have the permission to access it. Possible scenarios are outlined below:

- If the bucket exists and you have permission to read it, HTTP status code 200 will be returned.
- If you do not have permission to read the bucket, HTTP status code 403 will be returned.
- If the bucket does not exist, HTTP status code 404 will be returned.

#### Sample code

[//]: # ".cssg-snippet-head-bucket"
```cs
try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  HeadBucketRequest request = new HeadBucketRequest(bucket);
  // Execute the request
  HeadBucketResult result = cosXml.HeadBucket(request);
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/HeadBucket.cs).


## Deleting a Bucket

#### API description

This API is used to delete a specified bucket.

>! Before deleting a bucket, please make sure that all the data and incomplete multipart uploads in the bucket have been deleted; otherwise, the bucket cannot be deleted.

#### Sample code

[//]: # ".cssg-snippet-delete-bucket"
```cs
try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  DeleteBucketRequest request = new DeleteBucketRequest(bucket);
  // Execute the request
  DeleteBucketResult result = cosXml.DeleteBucket(request);
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/DeleteBucket.cs).

