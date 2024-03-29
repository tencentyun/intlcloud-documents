## 简介

本文档提供关于图片二维码相关 API 概览以及 SDK 示例代码。


| API                                                          | 操作描述                         |
| ------------------------------------------ | -------------------------- |
|  二维码识别|  二维码识别功能可识别图片中有效二维码的位置及内容，输出图像中二维码包含的文本信息（每个二维码对应的 URL 或文本），并可对识别出的二维码添加马赛克  |


## 二维码识别

二维码识别功能可识别图片中有效二维码的位置及内容，输出图像中二维码包含的文本信息（每个二维码对应的 URL 或文本），并可对识别出的二维码添加马赛克。

### 上传时识别二维码

#### 功能说明

图片上传时识别二维码的请求包与 COS 简单上传文件接口一致，只需在请求包头部增加图片处理参数 Pic-Operations。

#### 示例代码

```shell
    # 先创建 cos client
    example_object = 'example_object.jpg'
    with open(example_object, 'rb') as fp:
        opts = '{"is_pic_info":1,"rules":[{"fileid":"format.jpg","rule":"QRcode/cover/0"}]}'
        response,data = client.ci_put_object_from_local_file_and_get_qrcode(
            Bucket='example-bucket-123456789',
            LocalFilePath=example_object,
            Key='example_key',
            EnableMD5=False,
            PicOperations=opts
        )
        # 查看响应信息，可根据需要读指定数据
        print(response,data)
```

#### 参数说明

| 参数名称           | 参数描述                                                     | 类型       | 是否必填 |
| ------------------ | ------------------------------------------------------------ | ---------- | -------- |
| Bucket             | 存储桶名称，由 BucketName-APPID 构成                         | String     | 是       |
| LocalFilePath      | 图片路径                         | String | 是       |
| Key                | 对象键（Key）是对象在存储桶中的唯一标识。例如，在对象的访问域名 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg` 中，对象键为 doc/pic.jpg | String     | 是       |
| EnableMD5          | 是否需要 SDK 计算 Content-MD5，默认关闭，打开后将增加上传耗时 | Bool       | 否       |
| PicOperations      | 万象图片处理参数，请参见二维码识别 | String     | 是       |


### 云上数据识别二维码

#### 功能说明

对云上图片进行二维码识别，返回二维码识别结果。

#### 示例代码

```shell
    # 先创建 cos client
    response,data = client.ci_get_object_qrcode(
        Bucket='example_bucket-123456789',
        Key='example_object',
        Cover=0
    )
    # 查看响应信息，可根据需要读指定数据
    print(response,data)
```

#### 参数说明

| 参数名称           | 参数描述                                                     | 类型       | 是否必填 |
| ------------------ | ------------------------------------------------------------ | ---------- | -------- |
| Bucket             | 存储桶名称，由 BucketName-APPID 构成                         | String     | 是       |
| Key                | 对象键（Key）是对象在存储桶中的唯一标识。例如，在对象的访问域名 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg` 中，对象键为 doc/pic.jpg | String     | 是       |
| Cover              | 万象图片处理二维码覆盖开关，请参见二维码识别 | Int     | 是       |

