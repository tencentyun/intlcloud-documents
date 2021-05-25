## Overview

This document provides an overview of APIs and SDK code samples related to bucket tagging.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | Setting bucket tags | Sets tags for an existing bucket |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | Querying bucket tags | Queries the existing tags of a specified bucket |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | Deleting bucket tags | Deletes specified bucket tags |

## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, see [Api Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Setting Bucket Tags

#### API description

This API is used to set tags for an existing bucket.

#### Sample code

[//]: # (.cssg-snippet-put-bucket-tagging)
```cs
try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  PutBucketTaggingRequest request = new PutBucketTaggingRequest(bucket);
  string akey = "aTagKey";
  string avalue = "aTagValue";
  string bkey = "bTagKey";
  string bvalue = "bTagValue";

  request.AddTag(akey, avalue);
  request.AddTag(bkey, bvalue);
  
  // Execute the request
  PutBucketTaggingResult result = cosXml.PutBucketTagging(request);
  
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketTagging.cs).

## Querying Bucket Tags

#### API description

This API is used to query the existing tags of a specified bucket.

#### Sample code

[//]: # (.cssg-snippet-get-bucket-tagging)
```cs
try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  GetBucketTaggingRequest request = new GetBucketTaggingRequest(bucket);   
  // Execute the request
  GetBucketTaggingResult result = cosXml.GetBucketTagging(request);
  
  // Request successful 
  Tagging tagging = result.tagging;
  Console.WriteLine(tagging);
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketTagging.cs).

## Deleting Bucket Tags

#### API description

This API is used to delete the existing tags of a specified bucket.

#### Sample code

[//]: # (.cssg-snippet-delete-bucket-tagging)
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketTagging.cs).

