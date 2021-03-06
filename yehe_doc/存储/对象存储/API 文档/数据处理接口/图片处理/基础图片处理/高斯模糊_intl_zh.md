## 功能描述
COS 通过数据万象接口 **imageMogr2** 提供图片模糊处理功能。

该功能支持以下处理方式：

- 下载时处理
- 上传时处理
- 云上数据处理

## 请求

#### 请求示例1：下载时处理

```shell
download_url?imageMogr2/blur/<radius>x<sigma>							
```

#### 请求示例2：上传时处理

```http
PUT /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
Pic-Operations: 
{
  "is_pic_info": 1,
  "rules": [{
      "fileid": "exampleobject",
      "rule": "imageMogr2/blur/<radius>x<sigma>"
  }]
}
```

#### 请求示例3：云上数据处理

```http
POST /<ObjectKey>?image_process HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-length: Size
Authorization: Auth String
Pic-Operations: 
{
  "is_pic_info": 1,
  "rules": [{
      "fileid": "exampleobject",
      "rule": "imageMogr2/blur/<radius>x<sigma>"
  }]
}
```

>? Authorization: Auth String （详情请参见 [请求签名](https://intl.cloud.tencent.com/document/product/436/7778) 文档）。
>

## 处理参数说明

操作名称：blur。

| 参数           | 描述                          |
| -------------- | ----------------------------- |
| download_url | 文件的访问链接，具体构成为`<BucketName-APPID>.cos.<Region>.myqcloud.com/<picture name>`，<br>例如 `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| &lt;radius> | 模糊半径，取值范围为1 - 50      |
| &lt;sigma>   | 正态分布的标准差，必须大于0 |
| `/ignore-error/1`            | 当处理参数中携带此参数时，针对文件过大导致处理失败的场景，会直接返回原图而不报错         |


## 实际案例

>? 本篇文档中的实际案例仅包含**下载时处理**，该类处理不会保存处理后的图片至存储桶。如有保存需求，您可参见 [图片持久化处理](https://cloud.tencent.com/document/product/436/54050) 文档并配置**上传时处理**或**云上数据处理**。
>

#### 模糊半径取8，sigma 值取5，进行高斯模糊处理：

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/blur/8x5
```

高斯模糊处理后效果如下：
![](https://main.qcloudimg.com/raw/d635efeeca1d160e773737361e375801.jpeg)

#### 模糊半径取8，sigma 值取5，进行高斯模糊处理，并携带私有文件签名：

处理方式同上，仅增加签名部分，并与图片处理参数以“&”连接，示例如下：

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&imageMogr2/blur/8x5
```

>? `<signature>` 为签名部分，获取方式请参考 [请求签名](https://intl.cloud.tencent.com/document/product/436/7778)。
>

