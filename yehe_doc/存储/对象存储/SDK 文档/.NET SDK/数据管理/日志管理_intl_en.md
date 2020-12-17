## Overview

This document provides an overview of APIs and SDK code samples related to logging.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | -------------------------- |
| [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/17054) | Setting logging | Enables logging for a source bucket |
| [GET Bucket logging](https://intl.cloud.tencent.com/document/product/436/17053) | Querying logging | Queries the logging configuration of a source bucket |

## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, see [Api Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Setting Logging

#### API description

This API is used to enable logging for a source bucket and store the access logs in a specified destination bucket.

#### Sample code

[//]: # ".cssg-snippet-put-bucket-logging"
```cs
try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  PutBucketLoggingRequest request = new PutBucketLoggingRequest(bucket);
  // Set the destination path for storing logs
  request.SetTarget("targetbucket-1250000000", "logs/");
  // Execute the request
  PutBucketLoggingResult result = cosXml.PutBucketLogging(request);
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketLogging.cs).

## Querying Logging

#### API description

This API is used to query the logging configuration of a specified bucket.

#### Sample code

[//]: # ".cssg-snippet-get-bucket-logging"
```cs
try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  GetBucketLoggingRequest request = new GetBucketLoggingRequest(bucket);
  // Execute the request
  GetBucketLoggingResult getResult = cosXml.GetBucketLogging(request);
  // Request successful 
  BucketLoggingStatus status = getResult.bucketLoggingStatus;
  if (status != null && status.loggingEnabled != null) {
    string targetBucket = status.loggingEnabled.targetBucket;
    string targetPrefix = status.loggingEnabled.targetPrefix;
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketLogging.cs).

