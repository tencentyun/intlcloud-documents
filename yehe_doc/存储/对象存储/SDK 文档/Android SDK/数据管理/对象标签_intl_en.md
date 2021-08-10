## Overview

This document provides an overview of APIs and SDK code samples related to object tagging.

| API | Operation | Description |
| :----------------------------------------------------------- | :----------- | :--------------------------- |
| [PUT Object tagging](https://intl.cloud.tencent.com/document/product/436/35709) | Setting object tags | Sets tags for an uploaded object |
| [GET Object tagging](https://intl.cloud.tencent.com/document/product/436/35710) | Querying object tags | Queries all tags of an object |
| [DELETE Object tagging](https://intl.cloud.tencent.com/document/product/436/35711) | Deleting object tags | Deletes all tags of an object |


## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Setting Object Tags

### Adding tags when uploading an object

#### API description

When uploading an object, you can add specific header information to the request to set tags for the object. For example, you can set `x-cos-tagging` to `Key1=Value1&Key2=Value2`. The tag keys and tag values in the set must be URL-encoded.

#### Sample code

```
String bucket = "examplebucket-1250000000"; // Bucket, formatted as `BucketName-APPID`
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
// Upload the file
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(bucket, cosPath,
        srcPath, uploadId);
// Set the response callback
cosxmlUploadTask.setCosXmlResultListener(new CosXmlResultListener() {

    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        COSXMLUploadTask.COSXMLUploadTaskResult cOSXMLUploadTaskResult =
                (COSXMLUploadTask.COSXMLUploadTaskResult) result;
    }
    @Override
    public void onFail(CosXmlRequest request,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

### Adding tags to an existing object

#### API description

This API is used to set tags for an existing object. It can help you group and manage existing object resources by adding key-value pairs as object tags.

#### Sample code

```
String bucket = "examplebucket-1250000000"; // Bucket, formatted as `BucketName-APPID`
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
PutObjectTaggingRequest putObjectTaggingRequest = new PutObjectTaggingRequest(TestConst.PERSIST_BUCKET, TestConst.PERSIST_BUCKET_SMALL_OBJECT_PATH);
putObjectTaggingRequest.addTag("Key1", "Value1");
putObjectTaggingRequest.addTag("Key2", "Hello");
try {
    PutObjectTaggingResult result = cosXmlService.putObjectTagging(putObjectTaggingRequest);
} catch (CosXmlClientException clientException) {
    clientException.printStackTrace();
} catch (CosXmlServiceException serviceException) {
    serviceException.printStackTrace();
}
```

## Querying Object Tags

#### API description

This API is used to query the existing tags of a specified object.

#### Sample code

```
String bucket = "examplebucket-1250000000"; // Bucket, formatted as `BucketName-APPID`
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

## Deleting Object Tags

#### API description

This API is used to delete the existing tags of a specified object.

#### Sample code

```
String bucket = "examplebucket-1250000000"; // Bucket, formatted as `BucketName-APPID`
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
