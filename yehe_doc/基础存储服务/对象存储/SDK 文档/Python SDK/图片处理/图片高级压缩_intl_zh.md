

## 简介

本文档提供关于图片高级压缩的 API 概览以及 SDK 示例代码。

| API                                                          | 操作描述 |
| ------------------------------------------------------------ | -------- |
| [图片高级压缩](https://intl.cloud.tencent.com/document/product/1045/40108) |   对指定存储桶下的图片进行压缩  |

## 图片高级压缩

#### 功能说明

通过数据万象 imageMogr2 接口提供图片高级压缩功能。

#### 方法原型

```
ci_download_compress_image(self, Bucket, Key, DestImagePath, CompressType, **kwargs)
```

#### 请求示例

[//]: #	".cssg-snippet-ci-download-compress-image"

```py
# TPG 压缩
response = client.ci_download_compress_image(
    Bucket='examplebucket-1250000000',
    Key='sample.png',
    DestImagePath='sample.tpg',
    CompressType='tpg'
)

# HEIF 压缩
response = client.ci_download_compress_image(
    Bucket='examplebucket-1250000000',
    Key='sample.png',
    DestImagePath='sample.heif',
    CompressType='heif'
)
```

#### 参数说明

| 参数名称      | 参数描述                                                     | 类型   | 是否必填 |
| ------------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket        | 存储桶名称，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String | 是       |
| Key           | 对象Key，长度不超过128字节, 支持英文字母、数字、空格、加号、减号、下划线、等号、点号、冒号、斜线 | String | 是       |
| DestImagePath | 压缩图片保存至本地的目的路径                                 | String | 是       |
| CompressType  | 压缩格式，支持 TPG 或 HEIF                                   | String | 是       |

#### 返回结果说明

该方法返回值为请求响应头部。
