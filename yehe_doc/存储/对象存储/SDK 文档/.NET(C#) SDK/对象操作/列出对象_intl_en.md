## Overview

This document provides an overview of APIs and SDK code samples related to listing objects.

| API | Operation Name | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying an object list | Queries some or all objects in a bucket |
| [GET Bucket Object Versions](https://intl.cloud.tencent.com/document/product/436/31551) | Querying a list of objects and their version history | Queries some or all objects in a bucket as well as their version history |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Querying an Object List

#### API description

This API is used to query some or all objects in a bucket.

#### Sample 1. Requesting the first page of objects

[//]: # ".cssg-snippet-get-bucket"
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  GetBucketRequest request = new GetBucketRequest(bucket);
  // Execute the request
  GetBucketResult result = cosXml.GetBucket(request);
  // Bucket information
  ListBucket info = result.listBucket;
  if (info.isTruncated) {
    // Record the marker for the next page of truncated listing
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

#### Sample 2. Requesting the next page of objects

[//]: # ".cssg-snippet-get-bucket-next-page"
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  GetBucketRequest request = new GetBucketRequest(bucket);
  // Use the “nextMarker” from the previous request
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

#### Sample 3. Getting an object list and common prefixes

[//]: # ".cssg-snippet-get-bucket-with-delimiter"
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  GetBucketRequest request = new GetBucketRequest(bucket);
  // List objects and common prefixes under a/
  request.SetPrefix("a/");
  // Execute the request
  GetBucketResult result = cosXml.GetBucket(request);
  // Bucket information
  ListBucket info = result.listBucket;
  // List objects
  List<ListBucket.Contents> objects = info.contentsList;
  // List common prefixes
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

## Querying an Object Version List

#### API description 

This API is used to query some or all objects in a versioning-enabled bucket.

#### Sample 1. Requesting the first page of listed object versions

[//]: # ".cssg-snippet-list-objects-versioning"
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  ListBucketVersionsRequest request = new ListBucketVersionsRequest(bucket);
  // Execute the request
  ListBucketVersionsResult result = cosXml.ListBucketVersions(request);
  // Bucket information
  ListBucketVersions info = result.listBucketVersions;

  List<ListBucketVersions.Version> objects = info.objectVersionList;
  List<ListBucketVersions.CommonPrefixes> prefixes = info.commonPrefixesList;

  if (info.isTruncated) {
    // Record the marker for the next page of truncated listing
    this.keyMarker = info.nextKeyMarker;
    this.versionIdMarker = info.nextVersionIdMarker;
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

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ListObjectsVersioning.cs).

#### Sample 2. Requesting the next page of listed object versions

[//]: # ".cssg-snippet-list-objects-versioning-next-page"
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  ListBucketVersionsRequest request = new ListBucketVersionsRequest(bucket);

  // Use the “nextMarker” from the previous request
  request.SetKeyMarker(this.keyMarker);
  request.SetVersionIdMarker(this.versionIdMarker);

  // Execute the request
  ListBucketVersionsResult result = cosXml.ListBucketVersions(request);
  ListBucketVersions info = result.listBucketVersions;

  if (info.isTruncated) {
    // Record the marker for the next page of truncated listing
    this.keyMarker = info.nextKeyMarker;
    this.versionIdMarker = info.nextVersionIdMarker;
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

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ListObjectsVersioning.cs).

