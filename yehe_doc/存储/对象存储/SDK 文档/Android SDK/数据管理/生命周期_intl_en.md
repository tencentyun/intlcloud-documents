## Overview
This document provides an overview of APIs and SDK code samples related to lifecycles.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle | Sets the lifecycle management configuration of a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying lifecycle | Queries the lifecycle management configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting lifecycle | Deletes the lifecycle management configuration of a bucket |

## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, see [SDK API References](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Setting Lifecycle

#### API description

This API is used to set the lifecycle configuration of a bucket.

#### Sample code

[//]: # ".cssg-snippet-put-bucket-lifecycle"
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
// Specify the number of days after which the object is last modified that the action in the rule will be performed
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

>?For more samples, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketLifecycle.java).


## Querying Lifecycle

#### API description

This API is used to query the lifecycle management configuration of a bucket.

#### Sample code
[//]: # ".cssg-snippet-get-bucket-lifecycle"
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

>?For more samples, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketLifecycle.java).

## Deleting Lifecycle

#### API description

This API is used to delete the lifecycle management configuration of a bucket.

#### Sample code

[//]: # ".cssg-snippet-delete-bucket-lifecycle"
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

>?For more samples, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketLifecycle.java).

