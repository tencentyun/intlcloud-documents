## Overview


This document provides an overview of APIs and SDK code samples related to object movement.

| API | Operation | Description |
| :----------------------------------------------------------- | :--------------------------- | :--------------------- |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object (modifying object attributes) | Copies a file to a destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes a specified object from a bucket |

## Moving an Object

Object movement involves copying the source object to the target location and deleting the source object.

Since COS uses the bucket name (`Bucket`) and object key (`ObjectKey`) to identify objects, moving an object will change the object identifier. Currently, COS’s Java SDK does not provide a standalone API to change object identifiers. However, you can still move the object with a combination of basic operations (**object copy** and **object delete**).

For example, if you want to move the `picture.jpg` object to the “doc” directory that is in the same bucket (`mybucket-1250000000`), you can copy the `picture.jpg` to the “doc” directory (making the object key `doc/picture.jpg`) and then delete the source object.

Likewise, if you need to move `picture.jpg` in the `mybucket-1250000000` bucket to another bucket `myanothorbucket-1250000000`, you can copy the object to the `myanothorbucket-1250000000` bucket first and then delete the source object.

#### Sample code

[//]: # (.cssg-snippet-delete-object)
```
final String sourceAppid = "1250000000"; // Account appid
        final String sourceBucket = "sourcebucket-1250000000"; // Bucket of the source object
        final String sourceRegion = "COS_REGION"; // Region where the bucket of the source object resides
        final String sourceKey = "sourceObject"; // Key of the source object
        // Construct the source object attributes
        CopyObjectRequest.CopySourceStruct copySource = new CopyObjectRequest.CopySourceStruct(sourceAppid, sourceBucket,
                sourceRegion, sourceKey);
        String bucket = "examplebucket-1250000000"; // Destination bucket in the format of BucketName-APPID
        String key = "exampleobject"; // Object key of the destination bucket
        COSXMLCopyTask copyTask = transferManager.copy(bucket, key, copySource);
        copyTask.setCosXmlResultListener(new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult result) {
               
                // Delete the file after it is successfully copied.
                DeleteObjectRequest deleteObjectRequest = new DeleteObjectRequest(sourceBucket, sourceKey);
                cosXmlService.deleteObjectAsync(deleteObjectRequest, new CosXmlResultListener() {
                    @Override
                    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
                        // File deleted successfully.
                    }

                    @Override
                    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException e, CosXmlServiceException e1) {
                        // File deletion failed.
                    }
                });
            }
            @Override
            public void onFail(CosXmlRequest request, CosXmlClientException exception, CosXmlServiceException serviceException) {
            }
        });
```
