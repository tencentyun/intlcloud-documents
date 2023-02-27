## Overview

This document provides an overview of APIs and SDK code samples for hotlink protection.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket referer](https://www.tencentcloud.com/document/product/436/31423) | Setting hotlink protection | Sets hotlink protection for a bucket     |
| [GET Bucket referer](https://www.tencentcloud.com/document/product/436/30615) | Querying the hotlink protection configuration | Queries the hotlink protection configuration of a bucket |

## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Setting Hotlink Protection

#### Feature description

This API (`PUT Bucket referer`) is used to set hotlink protection for a bucket.

#### Sample code

[//]: # ".cssg-snippet-put-bucket-referer"
```java
// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
String bucket = "examplebucket-1250000000";
PutBucketRefererRequest putBucketRefererRequest = new PutBucketRefererRequest(
        bucket, true, RefererConfiguration.RefererType.White);
putBucketRefererRequest.setAllowEmptyRefer(false);
ArrayList<RefererConfiguration.Domain> domainList = new ArrayList<>();
domainList.add(new RefererConfiguration.Domain("*.qq.com"));
domainList.add(new RefererConfiguration.Domain("*.qcloud.com"));
domainList.add(new RefererConfiguration.Domain("*.google.com"));
putBucketRefererRequest.setDomainList(domainList);
cosXmlService.putBucketRefererAsync(putBucketRefererRequest,
        new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult result) {
                // For detailed fields, see the API documentation or SDK source code.
                PutBucketRefererResult putBucketRefererResult =
                        (PutBucketRefererResult) result;
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

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketReferer.java).

## Querying Hotlink Protection Configuration

#### Feature description

This API (`GET Bucket referer`) is used to query the hotlink protection configuration of a bucket.

#### Sample code

[//]: # ".cssg-snippet-get-bucket-referer"
```java
// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
String bucket = "examplebucket-1250000000";
GetBucketRefererRequest getBucketRefererRequest = new GetBucketRefererRequest(bucket);
cosXmlService.getBucketRefererAsync(getBucketRefererRequest,
        new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult result) {
                // For detailed fields, see the API documentation or SDK source code.
                GetBucketRefererResult getBucketRefererResult =
                        (GetBucketRefererResult) result;
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

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketReferer.java).
