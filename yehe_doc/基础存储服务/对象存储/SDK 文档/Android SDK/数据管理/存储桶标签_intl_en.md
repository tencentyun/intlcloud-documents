## Overview

This document provides an overview of APIs and SDK code samples related to bucket tagging.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | Setting bucket tags | Sets tags for an existing bucket |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | Querying bucket tags | Queries the existing tags of a bucket |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | Deleting bucket tags | Deletes the tags of a bucket |

## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Setting Bucket Tags

#### Description

This API is used to set tags for an existing bucket.

#### Sample code

[//]: # (.cssg-snippet-put-bucket-tagging)
```java
// Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
String bucket = "examplebucket-1250000000";
PutBucketTaggingRequest putBucketTaggingRequest =
        new PutBucketTaggingRequest(bucket);
// Set a tag
putBucketTaggingRequest.addTag("key", "value");
putBucketTaggingRequest.addTag("hello", "world");

cosXmlService.putBucketTaggingAsync(putBucketTaggingRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        PutBucketTaggingResult putBucketTaggingResult =
                (PutBucketTaggingResult) result;
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

>? For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketTagging.java).

## Querying Bucket Tags

#### Description

This API is used to query the existing tags of a specified bucket.

#### Sample code

[//]: # (.cssg-snippet-get-bucket-tagging)
```java
// Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
String bucket = "examplebucket-1250000000";
GetBucketTaggingRequest getBucketTaggingRequest =
        new GetBucketTaggingRequest(bucket);

cosXmlService.getBucketTaggingAsync(getBucketTaggingRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketTaggingResult getBucketTaggingResult =
                (GetBucketTaggingResult) result;
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

>? For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketTagging.java).

## Deleting Bucket Tags

#### Description

This API is used to delete the existing tags from a bucket.

#### Sample code

[//]: # (.cssg-snippet-delete-bucket-tagging)
```java
// Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
String bucket = "examplebucket-1250000000";
DeleteBucketTaggingRequest deleteBucketTaggingRequest =
        new DeleteBucketTaggingRequest(bucket);

cosXmlService.deleteBucketTaggingAsync(deleteBucketTaggingRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        DeleteBucketTaggingResult getBucketTaggingResult =
                (DeleteBucketTaggingResult) result;
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

>? For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketTagging.java).

