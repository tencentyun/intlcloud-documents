## Overview

This document provides an overview of APIs and SDK code samples related to static website.

| API | Operation | Description |
| ------------------------------------------------------------ | ---------------- | ------------------------ |
| [PUT Bucket website](https://intl.cloud.tencent.com/document/product/436/30617) | Setting a static website configuration | Configures a static website for a bucket |
| [GET Bucket website](https://intl.cloud.tencent.com/document/product/436/30616) | Querying a static website configuration | Queries the static website configuration of a bucket |
| [DELETE Bucket website](https://intl.cloud.tencent.com/document/product/436/30629) | Deleting a static website configuration | Deletes the static website configuration of a bucket |

## SDK API References

For the parameters and method description of all the APIs in the SDK, see [API Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Setting Static Website Configuration

#### Description

This API is used to configure a static website for a bucket.

#### Sample code

[//]: # (.cssg-snippet-put-bucket-website)
```cs
try
{
  // Bucket name in the format of bucketname-APPID. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  PutBucketWebsiteRequest putRequest = new PutBucketWebsiteRequest(bucket);
  putRequest.SetIndexDocument("index.html");
  putRequest.SetErrorDocument("eroror.html");
  putRequest.SetRedirectAllRequestTo("index.html");
  PutBucketWebsiteResult putResult = cosXml.PutBucketWebsite(putRequest);
  
  // Request succeeded
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketWebsite.cs).

## Querying Static Website Configuration

#### Description

This API is used to query the static website configuration associated with a bucket.

#### Sample code

[//]: # (.cssg-snippet-get-bucket-website)
```cs
try
{
  // Bucket name in the format of bucketname-APPID. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  GetBucketWebsiteRequest request = new GetBucketWebsiteRequest(bucket);   
  // Execute the request
  GetBucketWebsiteResult result = cosXml.GetBucketWebsite(request);
  
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketWebsite.cs).

## Deleting Static Website Configuration

#### Description

This API is used to delete the static website configuration of a bucket.

#### Sample code

[//]: # (.cssg-snippet-delete-bucket-website)
```cs
try
{
  // Bucket name in the format of bucketname-APPID. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  DeleteBucketWebsiteRequest request = new DeleteBucketWebsiteRequest(bucket);  
  // Execute the request
  DeleteBucketWebsiteResult result = cosXml.DeleteBucketWebsite(request);
  
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketWebsite.cs).

