## Overview

This document provides an overview of APIs and SDK sample codes related to cross-origin resource sharing (CORS).

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting CORS configuration | Sets the CORS permissions of bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying CORS configuration | Queries the CORS configuration of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting CORS configuration | Deletes the CORS configuration of a bucket |

## SDK API References

For the parameters and method description of all the APIs in the SDK, see [API Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Setting CORS Configuration

#### Description

This API is used to set the CORS configuration of a specified bucket.

#### Sample code

[//]: # (.cssg-snippet-put-bucket-cors)
```cs
try
{
  // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  PutBucketCORSRequest request = new PutBucketCORSRequest(bucket);
  // Set CORS configuration
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

## Querying CORS Configuration

#### Description

This API is used to query the CORS configuration of a bucket.

#### Sample code

[//]: # (.cssg-snippet-get-bucket-cors)
```cs
try
{
  // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  GetBucketCORSRequest request = new GetBucketCORSRequest(bucket);
  // Execute the request
  GetBucketCORSResult result = cosXml.GetBucketCORS(request);
  // Bucket CORS configuration 
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

## Deleting CORS Configuration

#### Description

This API is used to delete the CORS configuration of a bucket.

#### Sample code

[//]: # (.cssg-snippet-delete-bucket-cors)
```cs
try
{
  // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
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


