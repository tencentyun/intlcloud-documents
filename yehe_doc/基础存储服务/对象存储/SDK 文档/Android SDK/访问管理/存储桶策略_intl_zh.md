## 简介

本文档提供关于存储桶策略的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名       | 操作描述                       |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket policy](https://intl.cloud.tencent.com/document/product/436/8282) | 设置存储桶策略 | 设置指定存储桶的权限策略     |
| [GET Bucket policy](https://intl.cloud.tencent.com/document/product/436/8276) | 查询存储桶策略 | 查询指定存储桶的权限策略 |
| [DELETE Bucket policy](https://intl.cloud.tencent.com/document/product/436/8285) | 删除存储桶策略 | 删除指定存储桶的权限策略 |

## SDK API 参考

SDK 所有接口的具体参数与方法说明，请参考 [SDK API 参考](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/)。

## 设置存储桶策略

#### 功能说明

设置指定存储桶的权限策略（PUT Bucket policy）。

>! COS Android SDK 版本需要大于等于 v5.9.8。
>

#### 示例代码

[//]: # (.cssg-snippet-put-bucket-policy)
```java
// 存储桶名称，由bucketname-appid 组成，appid必须填入，可以在COS控制台查看存储桶名称。 https://console.cloud.tencent.com/cos5/bucket
String bucket = "examplebucket-1250000000";
// 权限策略，详情请参见 访问管理策略语法 https://cloud.tencent.com/document/product/436/12469#.E7.AD.96.E7.95.A5.E8.AF.AD.E6.B3.95
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
                // 详细字段请查看api文档或者SDK源码
                PutBucketPolicyResult putBucketPolicyResult =
                        (PutBucketPolicyResult) result;
            }
            // 如果您使用 kotlin 语言来调用，请注意回调方法中的异常是可空的，否则不会回调 onFail 方法，即：
            // clientException 的类型为 CosXmlClientException?，serviceException 的类型为 CosXmlServiceException?
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

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketPolicy.java) 查看。

## 查询存储桶策略

#### 功能说明

查询指定存储桶的权限策略（GET Bucket policy）。

>! COS Android SDK 版本需要大于等于 v5.9.8。
>

#### 示例代码

[//]: # (.cssg-snippet-get-bucket-policy)
```java
// 存储桶名称，由bucketname-appid 组成，appid必须填入，可以在COS控制台查看存储桶名称。 https://console.cloud.tencent.com/cos5/bucket
String bucket = "examplebucket-1250000000";
final GetBucketPolicyRequest getBucketPolicyRequest =
        new GetBucketPolicyRequest(bucket);
cosXmlService.getBucketPolicyAsync(getBucketPolicyRequest,
        new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult result) {
                // 详细字段请查看api文档或者SDK源码
                GetBucketPolicyResult getBucketPolicyResult =
                        (GetBucketPolicyResult) result;
                String policy = getBucketPolicyResult.policy;
            }
            // 如果您使用 kotlin 语言来调用，请注意回调方法中的异常是可空的，否则不会回调 onFail 方法，即：
            // clientException 的类型为 CosXmlClientException?，serviceException 的类型为 CosXmlServiceException?
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

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketPolicy.java) 查看。

## 删除存储桶策略

#### 功能说明

删除指定存储桶的权限策略（DELETE Bucket policy）。

>! COS Android SDK 版本需要大于等于 v5.9.8。
>

#### 示例代码

[//]: # (.cssg-snippet-delete-bucket-policy)
```java
// 存储桶名称，由bucketname-appid 组成，appid必须填入，可以在COS控制台查看存储桶名称。 https://console.cloud.tencent.com/cos5/bucket
String bucket = "examplebucket-1250000000";
DeleteBucketPolicyRequest deleteBucketPolicyRequest =
        new DeleteBucketPolicyRequest(bucket);
cosXmlService.deleteBucketPolicyAsync(deleteBucketPolicyRequest,
        new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult result) {
                // 详细字段请查看api文档或者SDK源码
                DeleteBucketPolicyResult deleteBucketPolicyResult =
                        (DeleteBucketPolicyResult) result;
            }
            // 如果您使用 kotlin 语言来调用，请注意回调方法中的异常是可空的，否则不会回调 onFail 方法，即：
            // clientException 的类型为 CosXmlClientException?，serviceException 的类型为 CosXmlServiceException?
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

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketPolicy.java) 查看。


