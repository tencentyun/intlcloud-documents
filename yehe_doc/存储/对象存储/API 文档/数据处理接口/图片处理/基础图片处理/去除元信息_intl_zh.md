## 功能描述

COS 通过数据万象 **imageMogr2** 接口可去除图片元信息，包括 exif 信息。

>! 图片处理功能为收费项，由数据万象收取，详细的计费说明请参见数据万象 [计费与定价](https://intl.cloud.tencent.com/document/product/1045/33431)。
>

## 接口形式
```plaintext
download_url?imageMogr2/strip
```

## 参数说明

操作名称：strip

| 参数         | 描述                                                         |
| ------------ | ------------------------------------------------------------ |
| download_url | 文件的访问链接，具体构成为`<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`，<br>例如`examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`。 |
| /ignore-error/1            | 当处理参数中携带此参数时，针对文件过大导致处理失败的场景，会直接返回原图而不报错         |

## 实际案例

#### 请求案例1：公有读
```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/strip
```

#### 请求案例2：私有读、携带签名

处理方式同上，仅增加签名部分，并与图片处理参数以“&”连接，示例如下：

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&imageMogr2/strip
```

>? `<signature>` 为签名部分，获取方式请参考 [请求签名](https://intl.cloud.tencent.com/document/product/436/7778)。
>
