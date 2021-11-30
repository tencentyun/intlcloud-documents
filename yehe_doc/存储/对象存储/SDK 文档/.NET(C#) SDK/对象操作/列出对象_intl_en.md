## Overview

This document provides an overview of APIs and SDK code samples related to listing objects.

| API                                                          | Operation                   | Description                                       |
| ------------------------------------------------------------ | ------------------------ | ---------------------------------------------- |
| [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying objects | Queries some or all the objects in a bucket. |
| [GET Bucket Object Versions](https://intl.cloud.tencent.com/document/product/436/31551) | Querying objects and their version history | Queries some or all the objects in a bucket and their version history. |

## SDK API References

For the parameters and method description of all the APIs in the SDK, see [API Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Querying an Object List

#### Description

This API is used to query some or all the objects in a bucket.

#### Sample 1. Getting the first page of data

[//]: #	".cssg-snippet-get-bucket"

```cs
try
{
  // Bucket name in the format of bucketname-APPID. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  GetBucketRequest request = new GetBucketRequest(bucket);
  // Execute the request
  GetBucketResult result = cosXml.GetBucket(request);
  // Bucket information
  ListBucket info = result.listBucket;
  if (info.isTruncated) {
    // The data is truncated, and the next marker of the data is recorded.
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

> ?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ListObjects.cs).

#### Sample 2. Requesting the next page of data

[//]: #	".cssg-snippet-get-bucket-next-page"

```cs
try
{
  // Bucket name in the format of bucketname-APPID. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
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

> ?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ListObjects.cs).

#### Sample 3. Getting an object list and subdirectories

[//]: #	".cssg-snippet-get-bucket-with-delimiter"

```cs
try
{
  // Bucket name in the format of bucketname-APPID. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  GetBucketRequest request = new GetBucketRequest(bucket);
  // Get the objects and subdirectories under “a/”
  request.SetPrefix("a/");
  request.SetDelimiter("/");
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

> ?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ListObjects.cs).

## Querying an Object Version List

#### Description

This API is used to query some or all objects in a versioning-enabled bucket.

#### Sample 1. Getting the object version list’s first page of data

[//]: #	".cssg-snippet-list-objects-versioning"

```cs
try
{
  // Bucket name in the format of bucketname-APPID. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  ListBucketVersionsRequest request = new ListBucketVersionsRequest(bucket);
  // Execute the request
  ListBucketVersionsResult result = cosXml.ListBucketVersions(request);
  // Bucket information
  ListBucketVersions info = result.listBucketVersions;

  List<ListBucketVersions.Version> objects = info.objectVersionList;
  List<ListBucketVersions.CommonPrefixes> prefixes = info.commonPrefixesList;

  if (info.isTruncated) {
    // The data is truncated, and the next marker of the data is recorded.
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

> ?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ListObjectsVersioning.cs).

#### Sample 2. Getting the object version list’s next page of data

[//]: #	".cssg-snippet-list-objects-versioning-next-page"

```cs
try
{
  // Bucket name in the format of bucketname-APPID. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  ListBucketVersionsRequest request = new ListBucketVersionsRequest(bucket);

  // Use the “nextMarker” from the previous request
  request.SetKeyMarker(this.keyMarker);
  request.SetVersionIdMarker(this.versionIdMarker);

  // Execute the request
  ListBucketVersionsResult result = cosXml.ListBucketVersions(request);
  ListBucketVersions info = result.listBucketVersions;

  if (info.isTruncated) {
    // The data is truncated, and the next marker of the data is recorded.
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

> ?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ListObjectsVersioning.cs).
