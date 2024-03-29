## 简介

本文档提供关于清单的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名       | 操作描述             |
| ------------------------------------------------------------ | ------------ | -------------------- |
| [PUT Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30625) | 设置清单任务 | 设置存储桶的清单任务 |
| [GET Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30623) | 查询清单任务 | 查询存储桶的清单任务 |
| [DELETE Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30626) | 删除清单任务 | 删除存储桶的清单任务 |

## SDK API 参考

SDK 所有接口的具体参数与方法说明，请参考 [SDK API 参考](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/)。

## 设置清单任务

#### 功能说明

PUT Bucket inventory 用于在存储桶中创建清单任务。

#### 示例代码

[//]: # (.cssg-snippet-put-bucket-inventory)
```java
// 存储桶名称，由bucketname-appid 组成，appid必须填入，可以在COS控制台查看存储桶名称。 https://console.cloud.tencent.com/cos5/bucket
String bucket = "examplebucket-1250000000";
PutBucketInventoryRequest putBucketInventoryRequest =
        new PutBucketInventoryRequest(bucket);
putBucketInventoryRequest.setInventoryId("exampleInventoryId");
// 是否在清单中包含对象版本：
// 如果设置为 All，清单中将会包含所有对象版本，
// 并在清单中增加VersionId，IsLatest，DeleteMarker 这几个字段
// 如果设置为 Current，则清单中不包含对象版本信息
putBucketInventoryRequest.setIncludedObjectVersions(InventoryConfiguration
        .IncludedObjectVersions.ALL);
// 备份频率
putBucketInventoryRequest.setScheduleFrequency(InventoryConfiguration
        .SCHEDULE_FREQUENCY_DAILY);
// 备份路径
putBucketInventoryRequest.setDestination("CSV", "1000000000",
        "examplebucket-1250000000", "region", "dir/");

cosXmlService.putBucketInventoryAsync(putBucketInventoryRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        PutBucketInventoryResult putBucketInventoryResult =
                (PutBucketInventoryResult) result;
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

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketInventory.java) 查看。


#### 错误码说明

该请求可能会发生的一些常见的特殊错误如下：

| 错误码                | 描述                                         | 状态码               |
| --------------------- | -------------------------------------------- | -------------------- |
| InvalidArgument       | 不合法的参数值                               | HTTP 400 Bad Request |
| TooManyConfigurations | 清单数量已经达到1000条的上限                 | HTTP 400 Bad Request |
| AccessDenied          | 未授权的访问。您可能不具备访问该存储桶的权限 | HTTP 403 Forbidden   |

## 查询清单任务

#### 功能说明

GET Bucket inventory 用于查询存储桶中用户的清单任务信息。

#### 示例代码

[//]: # (.cssg-snippet-get-bucket-inventory)
```java
// 存储桶名称，由bucketname-appid 组成，appid必须填入，可以在COS控制台查看存储桶名称。 https://console.cloud.tencent.com/cos5/bucket
String bucket = "examplebucket-1250000000";
GetBucketInventoryRequest getBucketInventoryRequest =
        new GetBucketInventoryRequest(bucket);
getBucketInventoryRequest.setInventoryId("exampleInventoryId");

cosXmlService.getBucketInventoryAsync(getBucketInventoryRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketInventoryResult getBucketInventoryResult =
                (GetBucketInventoryResult) result;
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

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketCORS.java) 查看。

## 删除清单任务

#### 功能说明

DELETE Bucket inventory 用于删除存储桶中指定的清单任务。

#### 示例代码

[//]: # (.cssg-snippet-delete-bucket-inventory)
```java
// 存储桶名称，由bucketname-appid 组成，appid必须填入，可以在COS控制台查看存储桶名称。 https://console.cloud.tencent.com/cos5/bucket
String bucket = "examplebucket-1250000000";
DeleteBucketInventoryRequest deleteBucketInventoryRequest =
        new DeleteBucketInventoryRequest(bucket);
deleteBucketInventoryRequest.setInventoryId("exampleInventoryId");

cosXmlService.deleteBucketInventoryAsync(deleteBucketInventoryRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        DeleteBucketInventoryResult deleteBucketInventoryResult =
                (DeleteBucketInventoryResult) result;
    }

    // 如果您使用 kotlin 语言来调用，请注意回调方法中的异常是可空的，否则不会回调 onFail 方法，即：
    // clientException 的类型为 CosXmlClientException?，serviceException 的类型为 CosXmlServiceException?
    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       @Nullable CosXmlClientException clientException,
                       @Nullable CosXmlServiceException serviceException) {
    }
});
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketCORS.java) 查看。

