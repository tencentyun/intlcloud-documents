## Overview

This document provides an overview of APIs and SDK code samples related to static websites.

| API | Operation | Description |
| ------------------------------------------------------------ | ---------------- | ------------------------ |
| [PUT Bucket website](https://intl.cloud.tencent.com/document/product/436/30617) | Setting a static website configuration | Configures a static website for a bucket |
| [GET Bucket website](https://intl.cloud.tencent.com/document/product/436/30616) | Querying a static website configuration | Queries the static website configuration of a bucket |
| [DELETE Bucket website](https://intl.cloud.tencent.com/document/product/436/30629) | Deleting a static website configuration | Deletes the static website configuration of a bucket |

## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, see [Api Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Setting a Static Website Configuration

#### API description 

This API is used to configure a static website for a bucket.

#### Sample code

[//]: # (.cssg-snippet-put-bucket-website)
```cs
try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  PutBucketWebsiteRequest putRequest = new PutBucketWebsiteRequest(bucket);
  putRequest.SetIndexDocument("index.html");
  putRequest.SetErrorDocument("eroror.html");
  putRequest.SetRedirectAllRequestTo("index.html");
  PutBucketWebsiteResult putResult = cosXml.PutBucketWebsite(putRequest);
  
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketWebsite.cs).

## Querying a Static Website Configuration

#### API description 

This API is used to query the static website configuration associated with a bucket.

#### Sample code

[//]: # (.cssg-snippet-get-bucket-website)
```cs
try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  DeleteBucketTaggingRequest request = new DeleteBucketTaggingRequest(bucket);   
  // Execute the request
  DeleteBucketTaggingResult result = cosXml.DeleteBucketTagging(request);
  
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketWebsite.cs).

## Deleting a Static Website Configuration

#### API description 

This API is used to delete the static website configuration of a bucket.

#### Sample code

[//]: # (.cssg-snippet-delete-bucket-website)
```cs
try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  DeleteBucketTaggingRequest request = new DeleteBucketTaggingRequest(bucket);   
  // Execute the request
  DeleteBucketTaggingResult result = cosXml.DeleteBucketTagging(request);
  
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketWebsite.cs).

