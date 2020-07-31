## Overview
This document provides an overview of APIs and SDK code samples related to lifecycle.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle | Sets lifecycle management configuration for a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying lifecycle | Queries the lifecycle management configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting lifecycle | Deletes the lifecycle management configuration from a bucket |

## SDK API References

For parameters and method descriptions of all SDK APIs, see [SDK API References](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Setting Lifecycle

#### API description

This API (PUT Bucket lifecycle) is used to set lifecycle configuration on a bucket.

#### Sample code

[//]: # (.cssg-snippet-put-bucket-lifecycle)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
PutBucketLifecycleRequest putBucketLifecycleRequest =
        new PutBucketLifecycleRequest(bucket);

// Specify a lifecycle configuration rule
LifecycleConfiguration.Rule rule = new LifecycleConfiguration.Rule();
rule.id = "Lifecycle ID";
LifecycleConfiguration.Filter filter = new LifecycleConfiguration.Filter();
// Specify the prefix to which the rule applies
filter.prefix = "dir/";
rule.filter = filter;
// Specify whether to enable the rule
rule.status = "Enabled";
// Specify the number of days after the last modified date of an object the action in the rule is performed
LifecycleConfiguration.Transition transition =
        new LifecycleConfiguration.Transition();
transition.days = 100;
transition.storageClass = COSStorageClass.STANDARD.getStorageClass();
rule.transition = transition;

putBucketLifecycleRequest.setRuleList(rule);

cosXmlService.putBucketLifecycleAsync(putBucketLifecycleRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        PutBucketLifecycleResult putBucketLifecycleResult =
                (PutBucketLifecycleResult) result;
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

>?For more samples, go to [GitHub](https://github.com/tencentyun/qcloud-sdk-android/tree/master/Demo/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketLifecycle.java).


## Querying Lifecycle

#### API description

This API (GET Bucket lifecycle) is used to query the lifecycle management configuration of a bucket.

#### Sample code
[//]: # (.cssg-snippet-get-bucket-lifecycle)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketLifecycleRequest getBucketLifecycleRequest =
        new GetBucketLifecycleRequest(bucket);

cosXmlService.getBucketLifecycleAsync(getBucketLifecycleRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketLifecycleResult getBucketLifecycleResult =
                (GetBucketLifecycleResult) result;
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

>?For more samples, go to [GitHub](https://github.com/tencentyun/qcloud-sdk-android/tree/master/Demo/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketLifecycle.java).

## Deleting Lifecycle

#### API description

This API (DELETE Bucket lifecycle) is used to delete the lifecycle management configuration from a bucket.

#### Sample code

[//]: # (.cssg-snippet-delete-bucket-lifecycle)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
DeleteBucketLifecycleRequest deleteBucketLifecycleRequest =
        new DeleteBucketLifecycleRequest(bucket);

cosXmlService.deleteBucketLifecycleAsync(deleteBucketLifecycleRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        DeleteBucketLifecycleResult deleteBucketLifecycleResult =
                (DeleteBucketLifecycleResult) result;
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

>?For more samples, go to [GitHub](https://github.com/tencentyun/qcloud-sdk-android/tree/master/Demo/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketLifecycle.java).

