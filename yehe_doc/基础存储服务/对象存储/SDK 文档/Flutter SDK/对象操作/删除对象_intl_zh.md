## 简介

本文档提供关于对象的删除操作相关的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名         | 操作描述                                  |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | 删除单个对象   | 在存储桶中删除指定对象 |

## 删除单个对象

#### 功能说明

删除指定的对象（DELETE Object）。

#### 示例代码

```dart
// 存储桶名称，由 bucketname-appid 组成，appid 必须填入，可以在 COS 控制台查看存储桶名称。 https://console.cloud.tencent.com/cos5/bucket
String bucket = "examplebucket-1250000000";
//对象在存储桶中的位置标识符，即对象键
String cosPath = "exampleobject";
// 存储桶所在地域简称，例如广州地区是 ap-guangzhou
String region = "COS_REGION";
try {
  await Cos().getDefaultService().deleteObject(
      bucket, cosPath,
      region: region
  );
} catch (e) {
  // 失败后会抛异常 根据异常进行业务处理
  print(e);
}
```

#### 参数说明

| 参数名称   | 描述                                                         | 类型   | 是否必选 |
| ---------- | ------------------------------------------------------------ | ------ | ------ |
| bucket | 桶名称，Bucket 的命名规则为 BucketName-APPID，详情请参见 [存储桶概述](https://intl.cloud.tencent.com/document/product/436/13312) | String | 是 |
| cosPath | 对象键 是对象在存储桶中的唯一标识。例如，在对象的访问域名 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg `中，对象键为 doc/picture.jpg | String | 是 |
| versionId | 指定要删除的版本 ID | String | 否 |

#### 返回结果说明

- 成功：无返回值。
- 失败：发生错误（如身份认证失败），抛出异常 CosXmlClientException 或者 CosXmlServiceException。详情请参见 [异常处理](https://www.tencentcloud.com/document/product/436/53963)。
