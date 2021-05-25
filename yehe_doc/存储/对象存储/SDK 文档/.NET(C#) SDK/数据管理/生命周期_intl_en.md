## Overview
This document provides an overview of APIs and SDK code samples related to lifecycle.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting a lifecycle configuration | Sets a lifecycle management configuration for a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying a lifecycle configuration | Queries the lifecycle management configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting a lifecycle configuration | Deletes the lifecycle management configuration from a bucket |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, see [Api Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Setting a Lifecycle Configuration

#### API description 

This API is used to set a lifecycle configuration for a specified bucket.

#### Sample code

[//]: # (.cssg-snippet-put-bucket-lifecycle)
```cs
try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  PutBucketLifecycleRequest request = new PutBucketLifecycleRequest(bucket);
  // Set lifecycle
  LifecycleConfiguration.Rule rule = new LifecycleConfiguration.Rule();
  rule.id = "lfiecycleConfigureId";
  rule.status = "Enabled"; // Enabled, or Disabled

  rule.filter = new COSXML.Model.Tag.LifecycleConfiguration.Filter();
  rule.filter.prefix = "2/";

  // Specify the delete operation for incomplete multipart uploads
  rule.abortIncompleteMultiUpload = new LifecycleConfiguration.AbortIncompleteMultiUpload();
  rule.abortIncompleteMultiUpload.daysAfterInitiation = 2;

  request.SetRule(rule);

  // Execute the request
  PutBucketLifecycleResult result = cosXml.PutBucketLifecycle(request);
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

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketLifecycle.cs).


## Querying a Lifecycle Configuration

#### API description 

This API is used to query the lifecycle management configuration of a bucket.

#### Sample code

[//]: # (.cssg-snippet-get-bucket-lifecycle)
```cs
try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  GetBucketLifecycleRequest request = new GetBucketLifecycleRequest(bucket);
  // Execute the request
  GetBucketLifecycleResult result = cosXml.GetBucketLifecycle(request);
  // Bucket lifecycle configuration
  LifecycleConfiguration conf = result.lifecycleConfiguration;
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

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketLifecycle.cs).

## Deleting a Lifecycle Configuration

#### API description 

This API is used to delete the lifecycle management configuration from a bucket.

#### Sample code

[//]: # (.cssg-snippet-delete-bucket-lifecycle)
```cs
try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  DeleteBucketLifecycleRequest request = new DeleteBucketLifecycleRequest(bucket);
  // Execute the request
  DeleteBucketLifecycleResult result = cosXml.DeleteBucketLifecycle(request);
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

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketLifecycle.cs).

