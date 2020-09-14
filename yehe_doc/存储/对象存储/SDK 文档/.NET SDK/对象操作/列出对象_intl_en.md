## Overview

This document provides an overview of APIs and SDK code samples related to listing objects.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying an object list | Queries some or all objects in a bucket |
| [GET Bucket Object Versions](https://cloud.tencent.com/document/product/436/35521) | Querying a list of objects and their version history | Queries some or all objects in bucket and their version history |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [Api Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Querying an Object List

#### API description

This API is used to query some or all objects in a bucket.

#### Sample 1. Requesting the first page of data

[//]: # (.cssg-snippet-get-bucket)
```cs
try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  GetBucketRequest request = new GetBucketRequest(bucket);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Execute the request
  GetBucketResult result = cosXml.GetBucket(request);
  // Bucket information
  ListBucket info = result.listBucket;
  if (info.isTruncated) {
    // Record the marker for the next page of truncated data
    this.nextMarker = info.nextMarker;
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

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ListObjects.cs).

#### Sample 2. Requesting the next page of data

[//]: # (.cssg-snippet-get-bucket-next-page)
```cs
try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  GetBucketRequest request = new GetBucketRequest(bucket);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Use the value of nextMarker from the last request
  request.SetMarker(this.nextMarker);
  // Execute the request
  GetBucketResult result = cosXml.GetBucket(request);
  // Bucket information
  ListBucket info = result.listBucket;
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

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ListObjects.cs).

#### Sample 3. Getting an object list and subdirectories

[//]: # (.cssg-snippet-get-bucket-with-delimiter)
```cs
try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  GetBucketRequest request = new GetBucketRequest(bucket);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Get the objects and subdirectories under “a/”
  request.SetPrefix("a/");
  // Execute the request
  GetBucketResult result = cosXml.GetBucket(request);
  // Bucket information
  ListBucket info = result.listBucket;
  // Object list
  List<ListBucket.Contents> objects = info.contentsList;
  // Subdirectory list
  List<ListBucket.CommonPrefixes> subDirs = info.commonPrefixesList;
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

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ListObjects.cs).

