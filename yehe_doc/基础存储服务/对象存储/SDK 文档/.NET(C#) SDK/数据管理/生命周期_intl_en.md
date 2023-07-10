## Overview
This document provides an overview of APIs and SDK code samples related to lifecycles.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle configuration | Sets lifecycle for a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying a lifecycle configuration | Queries the lifecycle configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting a lifecycle configuration | Deletes the lifecycle configuration of a bucket |

## SDK API References

For the parameters and method description of all the APIs in the SDK, see [API Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Setting a Lifecycle Configuration

#### Description

This API is used to set the lifecycle configuration of a specified bucket.

#### Sample code

[//]: # (.cssg-snippet-put-bucket-lifecycle)
```cs
try
{
  // Bucket name in the format of bucketname-APPID. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  PutBucketLifecycleRequest request = new PutBucketLifecycleRequest(bucket);
  // Set the lifecycle
  LifecycleConfiguration.Rule rule = new LifecycleConfiguration.Rule();
  rule.id = "lfiecycleConfigureId";
  rule.status = "Enabled"; //Enabled，Disabled

  rule.filter = new COSXML.Model.Tag.LifecycleConfiguration.Filter();
  rule.filter.prefix = "2/";

  // Specify the operation for deleting expired parts
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

#### Description

This API is used to query the lifecycle management configuration of a bucket.

#### Sample code

[//]: # (.cssg-snippet-get-bucket-lifecycle)
```cs
try
{
  // Bucket name in the format of bucketname-APPID. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
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

#### Description

This API is used to delete the lifecycle management configuration of a bucket.

#### Sample code

[//]: # (.cssg-snippet-delete-bucket-lifecycle)
```cs
try
{
  // Bucket name in the format of bucketname-APPID. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
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

