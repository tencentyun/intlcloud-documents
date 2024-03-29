## 简介

本文档提供关于防盗链的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名       | 操作描述                       |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket referer](https://www.tencentcloud.com/document/product/436/31423) | 设置防盗链配置 | 设置存储桶的防盗链     |
| [GET Bucket referer](https://www.tencentcloud.com/document/product/436/30615) | 查询防盗链配置 | 查询存储桶的防盗链配置信息 |

## SDK API 参考

SDK 所有接口的具体参数与方法说明，请参考 [SDK API 参考](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/)。

## 设置防盗链配置

#### 功能说明

设置指定存储桶的防盗链配置信息（PUT Bucket referer）。

#### 示例代码

[//]: # ".cssg-snippet-put-bucket-referer"
```java
// 存储桶名称，由bucketname-appid 组成，appid必须填入，可以在COS控制台查看存储桶名称。 https://console.cloud.tencent.com/cos5/bucket
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
                // 详细字段请查看api文档或者SDK源码
                PutBucketRefererResult putBucketRefererResult =
                        (PutBucketRefererResult) result;
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

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketReferer.java) 查看。

## 查询防盗链配置

#### 功能说明

查询指定存储桶的防盗链配置信息（GET Bucket referer）。

#### 示例代码

[//]: # ".cssg-snippet-get-bucket-referer"
```java
// 存储桶名称，由bucketname-appid 组成，appid必须填入，可以在COS控制台查看存储桶名称。 https://console.cloud.tencent.com/cos5/bucket
String bucket = "examplebucket-1250000000";
GetBucketRefererRequest getBucketRefererRequest = new GetBucketRefererRequest(bucket);
cosXmlService.getBucketRefererAsync(getBucketRefererRequest,
        new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult result) {
                // 详细字段请查看api文档或者SDK源码
                GetBucketRefererResult getBucketRefererResult =
                        (GetBucketRefererResult) result;
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

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketReferer.java) 查看。
