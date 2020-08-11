## Overview

This document provides an overview of APIs and SDK code samples related to static websites.

| API | Operation | Description |
| ------------------------------------------------------------ | ---------------- | ------------------------ |
| [PUT Bucket website](https://intl.cloud.tencent.com/document/product/436/30617) | Setting a static website | Configures a static website for a bucket |
| [GET Bucket website](https://intl.cloud.tencent.com/document/product/436/30616) | Querying a static website configuration | Queries the static website configuration of a bucket |
| [DELETE Bucket website](https://intl.cloud.tencent.com/document/product/436/30629) | Deleting a static website configuration | Deletes the static website configuration of a bucket |

## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, see [SDK API References](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Setting a Static Website

#### API description

This API is used to configure a static website for a bucket.

#### Sample code

[//]: # ".cssg-snippet-put-bucket-website"
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
PutBucketWebsiteRequest putBucketWebsiteRequest =
        new PutBucketWebsiteRequest(bucket);
// Set an index document
putBucketWebsiteRequest.setIndexDocument("index.html");

cosXmlService.putBucketWebsiteAsync(putBucketWebsiteRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        PutBucketWebsiteResult putBucketWebsiteResult =
                (PutBucketWebsiteResult) result;
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

>?For more samples, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketWebsite.java).

## Querying a Static Website Configuration

#### API description

This API is used to query the static website configuration associated with a bucket.

#### Sample code

[//]: # ".cssg-snippet-get-bucket-website"
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketWebsiteRequest getBucketWebsiteRequest =
        new GetBucketWebsiteRequest(bucket);
cosXmlService.getBucketWebsiteAsync(getBucketWebsiteRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketWebsiteResult getBucketWebsiteResult =
                (GetBucketWebsiteResult) result;
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

>?For more samples, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketWebsite.java).

## Deleting a Static Website Configuration

#### API description

This API is used to delete the static website configuration of a bucket.

#### Sample code

[//]: # ".cssg-snippet-delete-bucket-website"
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
DeleteBucketWebsiteRequest deleteBucketWebsiteRequest =
        new DeleteBucketWebsiteRequest(bucket);

cosXmlService.deleteBucketWebsiteAsync(deleteBucketWebsiteRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        DeleteBucketWebsiteResult getBucketWebsiteResult =
                (DeleteBucketWebsiteResult) result;
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

>?For more samples, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketWebsite.java).

