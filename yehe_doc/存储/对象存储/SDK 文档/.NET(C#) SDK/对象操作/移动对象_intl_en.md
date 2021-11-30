## Overview

This document provides an overview of APIs and SDK code samples related to object movement.

| API | Operation | Description |
| ------------------------------------------------------------ | ---------------------------- | ---------------------- |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object (modifying object attributes) | Copies a file to a destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting an object | Deletes a specified object from a bucket. |

## SDK API References

For the parameters and method description of all the APIs in the SDK, see [API Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Moving an Object

Object movement involves copying the source object to the target location and deleting the source object.

Since COS uses the bucket name (`Bucket`) and object key (`ObjectKey`) to identify objects, moving an object will change the object identifier. Currently, COS’s Java SDK does not provide a standalone API to change object identifiers. However, you can still move the object with a combination of basic operations (**object copy** and **object delete**).

For example, if you want to move the `picture.jpg` object to the “doc” directory that is in the same bucket (`mybucket-1250000000`), you can copy the `picture.jpg` to the “doc” directory (making the object key `doc/picture.jpg`) and then delete the source object.

Likewise, if you need to move `picture.jpg` in the `mybucket-1250000000` bucket to another bucket `myanothorbucket-1250000000`, you can copy the object to the `myanothorbucket-1250000000` bucket first and then delete the source object.



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

// Bucket name in the format of bucketname-APPID. You can get APPID by referring to https://console.cloud.tencent.com/developer.
string bucket = "examplebucket-1250000000";
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
