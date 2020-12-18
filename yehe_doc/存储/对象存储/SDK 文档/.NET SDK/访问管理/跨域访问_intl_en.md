## Overview

This document provides an overview of APIs and SDK sample codes related to cross-origin access.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting a cross-origin access configuration | Sets cross-origin access permissions for a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying a cross-origin access configuration | Queries the cross-origin access configuration of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting a cross-origin access configuration | Deletes the cross-origin access configuration from a bucket |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, see [Api Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Setting a Cross-Origin Access Configuration

#### API description 

This API is used to set the cross-origin access configuration for a specified bucket.

#### Sample code

[//]: # (.cssg-snippet-put-bucket-cors)
```cs
try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  PutBucketCORSRequest request = new PutBucketCORSRequest(bucket);
  // Make cross-origin access configuration
  COSXML.Model.Tag.CORSConfiguration.CORSRule corsRule = 
    new COSXML.Model.Tag.CORSConfiguration.CORSRule();
  corsRule.id = "corsconfigureId";
  corsRule.maxAgeSeconds = 6000;

  corsRule.allowedOrigins = new List<string>();
  corsRule.allowedOrigins.Add("http://cloud.tencent.com");

  corsRule.allowedMethods = new List<string>();
  corsRule.allowedMethods.Add("PUT");

  corsRule.allowedHeaders = new List<string>();
  corsRule.allowedHeaders.Add("Host");

  corsRule.exposeHeaders = new List<string>();
  corsRule.exposeHeaders.Add("x-cos-meta-x1");

  request.SetCORSRule(corsRule);

  // Execute the request
  PutBucketCORSResult result = cosXml.PutBucketCORS(request);
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

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketCORS.cs).

## Querying a Cross-Origin Access Configuration

#### API description 

This API is used to query the cross-origin access configuration of a bucket.

#### Sample code

[//]: # (.cssg-snippet-get-bucket-cors)
```cs
try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  GetBucketCORSRequest request = new GetBucketCORSRequest(bucket);
  // Execute the request
  GetBucketCORSResult result = cosXml.GetBucketCORS(request);
  // Cross-access configuration of the bucket
  CORSConfiguration conf = result.corsConfiguration;
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

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketCORS.cs).

## Deleting a Cross-Origin Access Configuration

#### API description 

This API is used to delete the cross-origin access configuration from a bucket.

#### Sample code

[//]: # (.cssg-snippet-delete-bucket-cors)
```cs
try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  DeleteBucketCORSRequest request = new DeleteBucketCORSRequest(bucket);
  // Execute the request
  DeleteBucketCORSResult result = cosXml.DeleteBucketCORS(request);
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

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketCORS.cs).


