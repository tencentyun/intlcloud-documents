## Overview

This document provides an overview of APIs and SDK code samples related to bucket tagging.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | Setting bucket tags | Sets tags for an existing bucket |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | Querying bucket tags | Queries the existing tags of a specified bucket |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | Deleting bucket tags | Deletes specified bucket tags |

## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, see [SDK API References](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Setting Bucket Tags

#### API description

This API is used to set tags for an existing bucket.

#### Sample code

[//]: # ".cssg-snippet-put-bucket-tagging"
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
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

    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
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

>?For more samples, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketTagging.java).

## Querying Bucket Tags

#### API description

This API is used to query the existing tags of a specified bucket.

#### Sample code

[//]: # ".cssg-snippet-get-bucket-tagging"
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketTaggingRequest getBucketTaggingRequest =
        new GetBucketTaggingRequest(bucket);

cosXmlService.getBucketTaggingAsync(getBucketTaggingRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketTaggingResult getBucketTaggingResult =
                (GetBucketTaggingResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
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

>?For more samples, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketTagging.java).

## Deleting Bucket Tags

#### API description

This API is used to delete the existing tags of a specified bucket.

#### Sample code

[//]: # ".cssg-snippet-delete-bucket-tagging"
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
DeleteBucketTaggingRequest deleteBucketTaggingRequest =
        new DeleteBucketTaggingRequest(bucket);

cosXmlService.deleteBucketTaggingAsync(deleteBucketTaggingRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        DeleteBucketTaggingResult getBucketTaggingResult =
                (DeleteBucketTaggingResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
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

>?For more samples, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketTagging.java).

