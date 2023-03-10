## Overview

This document provides an overview of APIs and SDK code samples related to object copy and movement.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object (modifying object attributes) | Copies a file to a destination path. |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting an object | Deletes a specified object from a bucket. |

**Multipart operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads/copy | Queries in-progress multipart uploads/copy. |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload/copy operation | Initializes a multipart upload/copy operation. |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part. |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded/copied parts | Queries the uploaded/copied parts of a multipart operation. |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload/copy | Completes the multipart upload/copy of a file. |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload/copy | Aborts a multipart operation and deletes the uploaded/copied parts. |


## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

### Copying objects

The advanced APIs encapsulate async requests for the simple copy and multipart copy APIs and support pausing, resuming, and canceling copy requests.

#### Sample code
[//]: # (.cssg-snippet-transfer-copy-object)
```java
// Initialize TransferConfig. The default configuration is used here. To customize the configuration, please see the SDK API documentation.
TransferConfig transferConfig = new TransferConfig.Builder().build();
// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);

String sourceAppid = "1250000000"; // Account APPID
String sourceBucket = "sourcebucket-1250000000"; // Bucket of the source object
String sourceRegion = "COS_REGION"; // Region where the bucket of the source object resides
String sourceCosPath = "sourceObject"; // Key of the source object
// Construct source object attributes
CopyObjectRequest.CopySourceStruct copySourceStruct =
        new CopyObjectRequest.CopySourceStruct(
                sourceAppid, sourceBucket, sourceRegion, sourceCosPath);
// Destination bucket
// Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
String bucket = "examplebucket-1250000000";
// Destination object
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e., the object key

// Copy the object
COSXMLCopyTask cosxmlCopyTask = transferManager.copy(bucket, cosPath,
        copySourceStruct);

// Set the response callback
cosxmlCopyTask.setCosXmlResultListener(new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        COSXMLCopyTask.COSXMLCopyTaskResult copyResult =
                (COSXMLCopyTask.COSXMLCopyTaskResult) result;
    }

    // If you use the Kotlin language to call this, please note that the exception in the callback method is nullable; otherwise, the onFail method will not be called back, that is:
    // clientException is of type CosXmlClientException? and serviceException is of type CosXmlServiceException?
    @Override
    public void onFail(CosXmlRequest request,
                       @Nullable CosXmlClientException clientException,
                       @Nullable CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
// Set the job status callback to view the job progress
cosxmlCopyTask.setTransferStateListener(new TransferStateListener() {
    @Override
    public void onStateChanged(TransferState state) {
        // todo notify transfer state
    }
});
```

### Moving an object

Object movement involves copying the source object to the target location and deleting the source object.

Since COS uses the bucket name (`Bucket`) and object key (`ObjectKey`) to identify objects, moving an object will change the object identifier. Currently, COS’s Android SDK does not provide a standalone API to change object identifiers. However, you can still move the object with a combination of basic operations (**object copy** and **object delete**).

For example, if you want to move the `picture.jpg` object to the “doc” directory that is in the same bucket (`mybucket-1250000000`), you can copy the `picture.jpg` to the “doc” directory (making the object key `doc/picture.jpg`) and then delete the source object.

Likewise, if you need to move `picture.jpg` in the `mybucket-1250000000` bucket to another bucket `myanothorbucket-1250000000`, you can copy the object to the `myanothorbucket-1250000000` bucket first and then delete the source object.

#### Sample code

[//]: # (.cssg-snippet-move-object)
```java
final String sourceAppid = "1250000000"; // Account appid
final String sourceBucket = "sourcebucket-1250000000"; // Bucket of the source object
final String sourceRegion = "COS_REGION"; // Region where the bucket of the source object resides
final String sourceKey = "sourceObject"; // Key of the source object
// Construct source object attributes
CopyObjectRequest.CopySourceStruct copySource = new CopyObjectRequest.CopySourceStruct(sourceAppid, sourceBucket,
        sourceRegion, sourceKey);

String bucket = "examplebucket-1250000000"; // Destination bucket in the format of BucketName-APPID
String key = "exampleobject"; // Object key of the destination bucket

// copy(String bucket, String cosPath, CopyObjectRequest.CopySourceStruct copySourceStruct){
COSXMLCopyTask copyTask = transferManager.copy(bucket, key, copySource);
copyTask.setCosXmlResultListener(new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        try {
            // Delete the file after it is successfully copied.
            DeleteObjectRequest deleteObjectRequest = new DeleteObjectRequest(sourceBucket, sourceKey);
            DeleteObjectResult deleteResult = cosXmlService.deleteObject(deleteObjectRequest);
        } catch (CosXmlClientException e) {
            e.printStackTrace();
        } catch (CosXmlServiceException e) {
            e.printStackTrace();
        }
    }

    @Override
    public void onFail(CosXmlRequest request, CosXmlClientException exception, CosXmlServiceException serviceException) {

    }
});
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/MoveObject.java).

### Copying an object (modifying object attributes)

This API (PUT Object-Copy) is used to copy an object to a destination path.

#### Sample 1. Copying an object with its attributes preserved

[//]: # (.cssg-snippet-copy-object)
```java
String sourceAppid = "1250000000"; // Account APPID
String sourceBucket = "sourcebucket-1250000000"; // Bucket of the source object
String sourceRegion = "COS_REGION"; // Region where the bucket of the source object resides
String sourceCosPath = "sourceObject"; // Key of the source object
// Construct the source object attributes
CopyObjectRequest.CopySourceStruct copySourceStruct =
        new CopyObjectRequest.CopySourceStruct(
        sourceAppid, sourceBucket, sourceRegion, sourceCosPath);

// Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
String bucket = "examplebucket-1250000000";
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e., the object key
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(bucket, cosPath,
        copySourceStruct);

cosXmlService.copyObjectAsync(copyObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        CopyObjectResult copyObjectResult = (CopyObjectResult) result;
    }

    // If you use the Kotlin language to call this, please note that the exception in the callback method is nullable; otherwise, the onFail method will not be called back, that is:
    // clientException is of type CosXmlClientException? and serviceException is of type CosXmlServiceException?
    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       @Nullable CosXmlClientException clientException,
                       @Nullable CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/CopyObject.java).

#### Sample 2. Copying an object while replacing its attributes

[//]: # (.cssg-snippet-copy-object-replaced)
```java
String sourceAppid = "1250000000"; // Account APPID
String sourceBucket = "sourcebucket-1250000000"; // Bucket of the source object
String sourceRegion = "COS_REGION"; // Region where the bucket of the source object resides
String sourceCosPath = "sourceObject"; // Key of the source object
// Construct the source object attributes
CopyObjectRequest.CopySourceStruct copySourceStruct =
        new CopyObjectRequest.CopySourceStruct(
        sourceAppid, sourceBucket, sourceRegion, sourceCosPath);

// Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
String bucket = "examplebucket-1250000000";
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e., the object key
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(bucket, cosPath,
        copySourceStruct);
copyObjectRequest.setCopyMetaDataDirective(MetaDataDirective.REPLACED);
copyObjectRequest.setXCOSMeta("x-cos-metadata-oldKey", "newValue");

cosXmlService.copyObjectAsync(copyObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        CopyObjectResult copyObjectResult = (CopyObjectResult) result;
    }

    // If you use the Kotlin language to call this, please note that the exception in the callback method is nullable; otherwise, the onFail method will not be called back, that is:
    // clientException is of type CosXmlClientException? and serviceException is of type CosXmlServiceException?
    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       @Nullable CosXmlClientException clientException,
                       @Nullable CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/CopyObject.java).

#### Sample 3. Modifying object metadata

[//]: # (.cssg-snippet-modify-object-metadata)
```java
String appId = "1250000000"; // Account APPID
// Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
String bucket = "examplebucket-1250000000";
String region = "COS_REGION"; // Region where the bucket of the source object resides
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e., the object key
// Construct the source object attributes
CopyObjectRequest.CopySourceStruct copySourceStruct =
        new CopyObjectRequest.CopySourceStruct(
        appId, bucket, region, cosPath);

CopyObjectRequest copyObjectRequest = new CopyObjectRequest(bucket, cosPath,
        copySourceStruct);
copyObjectRequest.setCopyMetaDataDirective(MetaDataDirective.REPLACED);
// Replace metadata
copyObjectRequest.setXCOSMeta("x-cos-metadata-oldKey", "newValue");

cosXmlService.copyObjectAsync(copyObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        CopyObjectResult copyObjectResult = (CopyObjectResult) result;
    }

    // If you use the Kotlin language to call this, please note that the exception in the callback method is nullable; otherwise, the onFail method will not be called back, that is:
    // clientException is of type CosXmlClientException? and serviceException is of type CosXmlServiceException?
    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       @Nullable CosXmlClientException clientException,
                       @Nullable CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/ModifyObjectProperty.java).

#### Sample 4. Modifying the storage class of an object

[//]: # (.cssg-snippet-modify-object-storage-class)
```java
String appId = "1250000000"; // Account APPID
// Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
String bucket = "examplebucket-1250000000";
String region = "COS_REGION"; // Region where the bucket of the source object resides
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e., the object key
// Construct the source object attributes
CopyObjectRequest.CopySourceStruct copySourceStruct =
        new CopyObjectRequest.CopySourceStruct(
        appId, bucket, region, cosPath);

CopyObjectRequest copyObjectRequest = new CopyObjectRequest(bucket, cosPath,
        copySourceStruct);
// Set the storage class to STANDARD_IA
copyObjectRequest.setCosStorageClass(COSStorageClass.STANDARD_IA);

cosXmlService.copyObjectAsync(copyObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        CopyObjectResult copyObjectResult = (CopyObjectResult) result;
    }

    // If you use the Kotlin language to call this, please note that the exception in the callback method is nullable; otherwise, the onFail method will not be called back, that is:
    // clientException is of type CosXmlClientException? and serviceException is of type CosXmlServiceException?
    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       @Nullable CosXmlClientException clientException,
                       @Nullable CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/ModifyObjectProperty.java).
