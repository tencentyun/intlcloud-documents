## Overview

This document provides an overview of APIs and SDK code samples related to querying object metadata.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, see [Api Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

### Querying object metadata

#### API description 

This API is used to query the metadata of an object.

#### Sample code

[//]: # ".cssg-snippet-head-object"
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket name in the format: BucketName-APPID
  string key = "exampleobject"; // Object key
  HeadObjectRequest request = new HeadObjectRequest(bucket, key);
  // Execute the request
  HeadObjectResult result = cosXml.HeadObject(request);
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

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/HeadObject.cs).

