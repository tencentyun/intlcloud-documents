## Overview

This document provides an overview of APIs and SDK code samples related to versioning.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets a versioning configuration for a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning configuration of a bucket |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, see [Api Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Setting Versioning

#### API description

This API is used to set a versioning configuration for a specified bucket. Once enabled, versioning can only be suspended but not disabled.

#### Sample code

[//]: # ".cssg-snippet-put-bucket-versioning"
```cs
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
PutBucketVersioningRequest request = new PutBucketVersioningRequest(bucket);
request.IsEnableVersionConfig(true); //true: enables versioning; false: suspends versioning

try
{
  PutBucketVersioningResult result = cosXml.PutBucketVersioning(request);
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketVersioning.cs).

## Querying Versioning

#### API description

This API is used to query the versioning configuration of a specified bucket.

- To get the versioning status of a bucket, you need to have read permission for the bucket.
- There are three versioning statuses: not enabled, enabled, and suspended.

#### Sample code

[//]: # ".cssg-snippet-get-bucket-versioning"
```cs
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketVersioningRequest request = new GetBucketVersioningRequest(bucket);

try
{
  GetBucketVersioningResult result = cosXml.GetBucketVersioning(request);
  // Bucket lifecycle configuration
  VersioningConfiguration conf =  result.versioningConfiguration;
}
catch (COSXML.CosException.CosClientException clientEx)
{
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketVersioning.cs).

