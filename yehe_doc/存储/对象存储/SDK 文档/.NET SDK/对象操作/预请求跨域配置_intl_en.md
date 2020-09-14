## Overview

This document provides an overview of APIs and SDK sample codes related to preflight request for cross-origin access.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [Options Object](https://intl.cloud.tencent.com/document/product/436/8288) | Sending a preflight request for cross-origin access | Sends a preflight request to check whether a real cross-origin access request can be sent |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, see [Api Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Sending a Preflight Request for Cross-origin Access

#### API description 
This API is used to send a preflight request for the cross-origin access configuration.

#### Sample code

[//]: # (.cssg-snippet-option-object)
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket in the format: BucketName-APPID
  string key = "exampleobject"; // Object key
  string origin = "http://cloud.tencent.com";
  string accessMthod = "PUT";
  OptionObjectRequest request = new OptionObjectRequest(bucket, key, origin, accessMthod);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Execute the request
  OptionObjectResult result = cosXml.OptionObject(request);
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

