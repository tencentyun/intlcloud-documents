## Overview

This document provides an overview of APIs and SDK code samples related to versioning.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets the versioning configuration of a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning configuration of a bucket |

## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, see [SDK API References](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Setting Versioning

#### API description

This API is used to set the versioning configuration of a bucket. Once enabled, versioning can only be suspended, but not disabled.

#### Sample code

[//]: # ".cssg-snippet-put-bucket-versioning"
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
PutBucketVersioningRequest putBucketVersioningRequest =
        new PutBucketVersioningRequest(bucket);
// true: enable versioning; false: suspend versioning
putBucketVersioningRequest.setEnableVersion(true);

cosXmlService.putBucketVersionAsync(putBucketVersioningRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        PutBucketVersioningResult putBucketVersioningResult =
                (PutBucketVersioningResult) result;
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

>?For more samples, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketVersioning.java).

## Querying Versioning

#### API description

This API is used to query the versioning configuration of a bucket.

- To get the versioning status of a bucket, you need to have read permission for the bucket.
- There are three versioning statuses: not enabled, enabled, and suspended.

#### Sample code

[//]: # ".cssg-snippet-get-bucket-versioning"
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketVersioningRequest getBucketVersioningRequest =
        new GetBucketVersioningRequest(bucket);

cosXmlService.getBucketVersioningAsync(getBucketVersioningRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketVersioningResult getBucketVersioningResult =
                (GetBucketVersioningResult) result;
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

>?For more samples, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketVersioning.java).

