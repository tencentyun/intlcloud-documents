## Overview

This document provides an overview of APIs and SDK code samples related to bucket policies.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket policy](https://intl.cloud.tencent.com/document/product/436/8282) | Setting a bucket policy | Sets a permission policy for a bucket |
| [GET Bucket policy](https://intl.cloud.tencent.com/document/product/436/8276) | Querying a bucket policy | Queries the permission policy of a bucket |
| [DELETE Bucket policy](https://intl.cloud.tencent.com/document/product/436/8285) | Deleting a bucket policy | Deletes the permission policy of a bucket |

## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Setting a bucket policy

#### Feature description

This API is used to set an access policy on a bucket.

>! The COS Android SDK version should not be earlier than v5.9.8.
>

#### Sample code

[//]: # (.cssg-snippet-put-bucket-policy)
```java
// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
String bucket = "examplebucket-1250000000";
// Permission policy. For more information, visit https://cloud.tencent.com/document/product/436/12469#.E7.AD.96.E7.95.A5.E8.AF.AD.E6.B3.95.
String policy = "{\n" +
        "  \"Statement\": [\n" +
        "    {\n" +
        "      \"Principal\": {\n" +
        "        \"qcs\": [\n" +
        "          \"qcs::cam::uin/100000000001:uin/100000000011\"\n" +
        "        ]\n" +
        "      },\n" +
        "      \"Effect\": \"allow\",\n" +
        "      \"Action\": [\n" +
        "        \"name/cos:GetBucket\"\n" +
        "      ],\n" +
        "      \"Resource\": [\n" +
        "        \"qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*\"\n" +
        "      ]\n" +
        "    }\n" +
        "  ],\n" +
        "  \"version\": \"2.0\"\n" +
        "}";
PutBucketPolicyRequest putBucketPolicyRequest =
        new PutBucketPolicyRequest(bucket, policy);
cosXmlService.putBucketPolicyAsync(putBucketPolicyRequest,
        new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult result) {
                // For detailed fields, see the API documentation or SDK source code.
                PutBucketPolicyResult putBucketPolicyResult =
                        (PutBucketPolicyResult) result;
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

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketPolicy.java).

## Querying a bucket policy

#### Feature description

This API is used to query the access policy on a bucket.

>! The COS Android SDK version should not be earlier than v5.9.8.
>

#### Sample code

[//]: # (.cssg-snippet-get-bucket-policy)
```java
// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
String bucket = "examplebucket-1250000000";
final GetBucketPolicyRequest getBucketPolicyRequest =
        new GetBucketPolicyRequest(bucket);
cosXmlService.getBucketPolicyAsync(getBucketPolicyRequest,
        new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult result) {
                // For detailed fields, see the API documentation or SDK source code.
                GetBucketPolicyResult getBucketPolicyResult =
                        (GetBucketPolicyResult) result;
                String policy = getBucketPolicyResult.policy;
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

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketPolicy.java).

## Deleting a bucket policy

#### Feature description

This API is used to delete the access policy from a specified bucket.

>! The COS Android SDK version should not be earlier than v5.9.8.
>

#### Sample code

[//]: # (.cssg-snippet-delete-bucket-policy)
```java
// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
String bucket = "examplebucket-1250000000";
DeleteBucketPolicyRequest deleteBucketPolicyRequest =
        new DeleteBucketPolicyRequest(bucket);
cosXmlService.deleteBucketPolicyAsync(deleteBucketPolicyRequest,
        new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult result) {
                // For detailed fields, see the API documentation or SDK source code.
                DeleteBucketPolicyResult deleteBucketPolicyResult =
                        (DeleteBucketPolicyResult) result;
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

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketPolicy.java).


