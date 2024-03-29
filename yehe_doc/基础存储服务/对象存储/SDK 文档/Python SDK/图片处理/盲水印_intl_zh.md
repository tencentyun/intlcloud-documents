

## 简介

本文档提供关于盲水印的 API 概览以及 SDK 示例代码。

| API                                                          | 操作描述                                 |
| ------------------------------------------------------------ | ---------------------------------------- |
| 盲水印 | 对本地图片添加或提取盲水印并上传至存储桶 |

## 盲水印

#### 功能说明

盲水印功能基于腾讯云数据万象，是一种全新的水印模式。

#### 方法原型

```
def ci_put_object_from_local_file(self, Bucket, LocalFilePath, Key, EnableMD5=False, **kwargs)
```

#### 请求示例

[//]: #	".cssg-snippet-ci-put-object-from-local-file"

```py
# 添加盲水印
watermark_url = 'http://{bucket}.cos.{region}.myqcloud.com/watermark.png'.format(bucket='examplebucket-1250000000', region=region)
watermark_url_base64 = bytes.decode(base64.b64encode(str.encode(watermark_url)))
print(watermark_url_base64)
response, data = client.ci_put_object_from_local_file(
    Bucket='examplebucket-1250000000',
    LocalFilePath='sample.png',
    Key="sample.png",
    # pic operation json struct
    PicOperations='{"is_pic_info":1,"rules":[{"fileid": "format.png","rule": "watermark/3/type/1/image/' +
                  watermark_url_base64 + '" }]}'
)

# 提取盲水印
sample_url = 'http://{bucket}.cos.{region}.myqcloud.com/sample.png'.format(bucket='examplebucket-1250000000', region=region)
sample_url_base64 = bytes.decode(base64.b64encode(str.encode(sample_url)))
response, data = client.ci_put_object_from_local_file(
    Bucket='examplebucket-1250000000',
    LocalFilePath='format.png',
    Key="format.png",
    # pic operation json struct
    PicOperations='{"is_pic_info":1,"rules":[{"fileid": "watermark.png","rule": "watermark/4/type/1/image/' +
                  sample_url_base64 + '" }]}'
)
```

#### 参数说明

| 参数名称      | 参数描述                                                     | 类型   | 是否必填 |
| ------------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket        | 存储桶名称，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String | 是       |
| LocalFilePath | 需要处理的本地图片路径                                       | String | 是       |
| Key           | 对象键，长度不超过128字节, 支持英文字母、数字、空格、加号、减号、下划线、等号、点号、冒号、斜线 | String | 是       |
| EnableMD5     | 开启对象上传的 MD5 校验                                      | Bool   | 否       |

#### 返回结果说明

该方法返回值为请求响应头部和内容。
