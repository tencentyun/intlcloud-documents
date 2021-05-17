## Overview

This document provides an overview of APIs and SDK code samples related to object movement.

| API | Operation | Description |
| ------------------------------------------------------------ | ---------------------------- | ---------------------- |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object (modifying object attributes) | Copies a file to a destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes a specified object from a bucket |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, see [Api Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Moving an object

Object movement involves copying the source object to the target location and deleting the source object.

Objects stored in COS are identified using names formatted as 'bucket+key'. Therefore, the name of an object that is moved will be changed. Currently, this SDK does not provide a standalone API for object name changes. However, you can still move objects with basic operations.

For example, within the 'mybucket' bucket, if you want to move the 'mykey' object to 'prefix/mykey', you can copy 'prefix/mykey' first and then delete 'mykey'.

Likewise, if you want to move 'mykey' to the 'myanothorbucket' bucket, you can copy the object to the destination bucket first and then delete the source object.

#### Sample code

[//]: #	".cssg-snippet-move-object"

```cs
string sourceAppid = "1250000000"; // Account appid
string sourceBucket = "sourcebucket-1250000000"; //" Source object bucket
string sourceRegion = "COS_REGION"; // Source object bucket region
string sourceKey = "sourceObject"; // Source object key
// Construct source object attributes
CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, 
    sourceRegion, sourceKey);

string bucket = "examplebucket-1250000000"; // Destination bucket in the format of BucketName-APPID
string key = "exampleobject"; // Object key of the destination bucket

COSXMLCopyTask copyTask = new COSXMLCopyTask(bucket, key, copySource);

try {
  // Copy the object.
  COSXML.Transfer.COSXMLCopyTask.CopyTaskResult result = await 
    transferManager.CopyAsync(copyTask);
  Console.WriteLine(result.GetResultInfo());

  // Delete the object.
  DeleteObjectRequest request = new DeleteObjectRequest(sourceBucket, sourceKey);
  DeleteObjectResult deleteResult = cosXml.DeleteObject(request);
  // Print results.
  Console.WriteLine(deleteResult.GetResultInfo());
} catch (Exception e) {
    Console.WriteLine("CosException: " + e);
}
```

> ?For more samples, please go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/MoveObject.cs).
