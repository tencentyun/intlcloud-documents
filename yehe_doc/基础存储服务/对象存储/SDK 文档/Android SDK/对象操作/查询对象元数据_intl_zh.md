## 简介

本文档提供关于查询对象元数据操作相关的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名         | 操作描述                                  |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | 查询对象元数据 | 查询对象的元数据信息                  |

## SDK API 参考

SDK 所有接口的具体参数与方法说明，请参考 [SDK API 参考](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/)。

## 查询对象元数据

#### 功能说明

查询 Object 的 Meta 信息。

#### 示例代码

[//]: # (.cssg-snippet-head-object)
```java
String bucket = "examplebucket-1250000000"; //存储桶名称，格式：BucketName-APPID
String cosPath = "exampleobject"; //对象位于存储桶中的位置标识符，即对象键
HeadObjectRequest headObjectRequest = new HeadObjectRequest(bucket, cosPath);
cosXmlService.headObjectAsync(headObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        HeadObjectResult headObjectResult = (HeadObjectResult) result;
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

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/HeadObject.java) 查看。

