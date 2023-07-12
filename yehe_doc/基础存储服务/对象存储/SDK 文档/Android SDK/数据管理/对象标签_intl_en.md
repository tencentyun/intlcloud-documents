## Overview


This document provides an overview of APIs and SDK code samples related to object tagging.

| API | Operation | Description |
| :----------------------------------------------------------- | :----------- | :--------------------------- |
| [PUT Object tagging](https://intl.cloud.tencent.com/document/product/436/35709) | Tagging an object | Tags an uploaded object. |
| [GET Object tagging](https://intl.cloud.tencent.com/document/product/436/35710) | Querying object tags | Queries all tags of an object. |
| [DELETE Object tagging](https://intl.cloud.tencent.com/document/product/436/35711) | Deleting object tags | Deletes all tags of an object. |


## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Tagging an Object

### Adding tags when uploading an object

#### Description

When uploading an object, you can add specific header information to the request to set tags for the object. For example, you can set `x-cos-tagging` to `Key1=Value1&Key2=Value2`. The tag keys and tag values in the set must be URL-encoded.

#### Sample code

[//]: # (.cssg-snippet-put-upload-object-tagging)
```java
// Initialize TransferConfig. The default configuration is used here. To customize the configuration, please see the SDK API documentation.
TransferConfig transferConfig = new TransferConfig.Builder().build();
// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);
// Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
String bucket = "examplebucket-1250000000";
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
String srcPath = new File(context.getCacheDir(), "exampleobject")
        .toString(); // Absolute path of the local file
PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, srcPath);
try {
    // Set object tags. The tag keys and tag values in the set must be URL-encoded
    putObjectRequest.setRequestHeaders("x-cos-tagging", "Key1=Value&Key2=Value2", false);
} catch (CosXmlClientException e) {
    e.printStackTrace();
}
// If there is an `uploadId` for an initialized multipart upload, assign the value of the `uploadId` here to resume the upload; otherwise, assign `null`
String uploadId = null;
// Upload the object
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(bucket, cosPath,
        srcPath, uploadId);
// Set the response callback
cosxmlUploadTask.setCosXmlResultListener(new CosXmlResultListener() {

    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        COSXMLUploadTask.COSXMLUploadTaskResult uploadResult =
                (COSXMLUploadTask.COSXMLUploadTaskResult) result;
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
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/ObjectTagging.java).

### Adding tags to an existing object

#### Description

This API is used to set tags for an existing object. It can help you group and manage existing object resources by adding key-value pairs as object tags.

#### Sample code

[//]: # (.cssg-snippet-put-object-tagging)
```java
// Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
String bucket = "examplebucket-1250000000";
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
PutObjectTaggingRequest putObjectTaggingRequest = new PutObjectTaggingRequest(bucket, cosPath);
putObjectTaggingRequest.addTag("key", "value");
try {
    PutObjectTaggingResult putObjectTaggingResult = cosXmlService.putObjectTagging(putObjectTaggingRequest);
} catch (CosXmlClientException clientException) {
    clientException.printStackTrace();
} catch (CosXmlServiceException serviceException) {
    serviceException.printStackTrace();
}
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/ObjectTagging.java).

## Querying Object Tags

#### Description

This API is used to query the existing tags of a specified object.

#### Sample code

[//]: # (.cssg-snippet-get-object-tagging)
```java
// Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
String bucket = "examplebucket-1250000000";
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
GetObjectTaggingRequest getObjectTaggingRequest = new GetObjectTaggingRequest(bucket, cosPath);
try {
    GetObjectTaggingResult getObjectTaggingResult = cosXmlService.getObjectTagging(getObjectTaggingRequest);
} catch (CosXmlClientException clientException) {
    clientException.printStackTrace();
} catch (CosXmlServiceException serviceException) {
    serviceException.printStackTrace();
}
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/ObjectTagging.java).

## Deleting Object Tags

#### Description

This API is used to delete the existing tags of a specified object.

#### Sample code

[//]: # (.cssg-snippet-delete-object-tagging)
```java
// Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
String bucket = "examplebucket-1250000000";
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
DeleteObjectTaggingRequest deleteObjectTaggingRequest = new DeleteObjectTaggingRequest(bucket, cosPath);
try {
    DeleteObjectTaggingResult deleteObjectTaggingResult = cosXmlService.deleteObjectTagging(deleteObjectTaggingRequest);
} catch (CosXmlClientException clientException) {
    clientException.printStackTrace();
} catch (CosXmlServiceException serviceException) {
    serviceException.printStackTrace();
}
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/ObjectTagging.java).
