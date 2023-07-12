## Overview

This document provides an overview of APIs and SDK code samples related to restoring an archived object.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access. |

## SDK API References

For the parameters and method description of all the APIs in the SDK, see [API Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Restoring an Archived Object 

#### Description

This API (`POST Object restore`) is used to restore an archived object for access.

#### Sample code

[//]: # (.cssg-snippet-restore-object)
```cs
try
{
  // Bucket name in the format of bucketname-APPID. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; // Object key
  RestoreObjectRequest request = new RestoreObjectRequest(bucket, key);
  // Restoration time
  request.SetExpireDays(3);
  request.SetTier(COSXML.Model.Tag.RestoreConfigure.Tier.Bulk);

  // Execute the request
  RestoreObjectResult result = cosXml.RestoreObject(request);
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

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/RestoreObject.cs).

