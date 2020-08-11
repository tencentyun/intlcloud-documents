## Overview

This document provides an overview of APIs and SDK code samples related to logging.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | -------------------------- |
| [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/17054) | Setting logging | Enables logging for a source bucket |
| [GET Bucket logging](https://intl.cloud.tencent.com/document/product/436/17053) | Querying logging | Queries the logging configuration of a source bucket |

## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, see [SDK API References](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Setting Logging

#### API description

This API is used to enable logging for a source bucket and store the access logs in a specified destination bucket.

#### Sample code

[//]: # ".cssg-snippet-put-bucket-logging"
```java
String srcBucket = "examplebucket-1250000000"; //Format: BucketName-APPID
String targetBucket = "examplebucket-1250000000"; //Format: BucketName-APPID
PutBucketLoggingRequest putBucketLoggingRequest =
        new PutBucketLoggingRequest(srcBucket);
// Destination bucket
putBucketLoggingRequest.setTargetBucket(targetBucket);
// Specified location in which to store the logs
putBucketLoggingRequest.setTargetPrefix("dir/");

cosXmlService.putBucketLoggingAsync(putBucketLoggingRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        PutBucketLoggingResult putBucketLoggingResult =
                (PutBucketLoggingResult) result;
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

>?For more samples, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketLogging.java).

## Querying Logging

#### API description

This API is used to query the logging configuration of a specified bucket.

#### Sample code

[//]: # ".cssg-snippet-get-bucket-logging"
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketLoggingRequest getBucketLoggingRequest =
        new GetBucketLoggingRequest(bucket);

cosXmlService.getBucketLoggingAsync(getBucketLoggingRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketLoggingResult getBucketLoggingResult =
                (GetBucketLoggingResult) result;
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

>?For more samples, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketLogging.java).

