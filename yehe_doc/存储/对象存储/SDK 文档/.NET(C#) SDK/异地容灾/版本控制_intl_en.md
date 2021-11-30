## Overview

This document provides an overview of APIs and SDK code samples related to versioning.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets versioning for a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning information of a bucket |

## SDK API References

For the parameters and method description of all the APIs in the SDK, see [API Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Setting versioning

#### Description

This API is used to set the versioning configuration of a specified bucket. Once enabled, versioning can only be suspended but not disabled.

#### Sample code

[//]: # ".cssg-snippet-put-bucket-versioning"
```cs
// Bucket name in the format of bucketname-APPID. You can get APPID by referring to https://console.cloud.tencent.com/developer.
string bucket = "examplebucket-1250000000";
PutBucketVersioningRequest request = new PutBucketVersioningRequest(bucket);
request.IsEnableVersionConfig(true); //true: enable versioning; false: suspend versioning

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

## Querying versioning

#### Description

This API is used to query the versioning configuration of a specified bucket.

- To get the versioning status of a bucket, you need to have read permission for the bucket.
- There are three versioning statuses: not enabled, enabled, and suspended.

#### Sample code

[//]: # ".cssg-snippet-get-bucket-versioning"
```cs
// Bucket name in the format of bucketname-APPID. You can get APPID by referring to https://console.cloud.tencent.com/developer.
string bucket = "examplebucket-1250000000";
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

