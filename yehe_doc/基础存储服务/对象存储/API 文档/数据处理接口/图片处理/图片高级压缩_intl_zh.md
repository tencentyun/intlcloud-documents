## 功能描述

COS 通过数据万象 imageMogr2 接口提供图片高级压缩功能。图片高级压缩可以更加高效地将图片转换为 TPG 或 HEIF 等高压缩比格式，有效降低图片传输链路及加载耗时，降低带宽及流量成本。

该功能支持以下的处理方式：

- 下载时处理
- 上传时处理
- 云上数据处理


| 功能      | 简介                                                         |
| :-------- | :----------------------------------------------------------- |
| TPG 压缩  | TPG 是腾讯推出的自研图片格式，可将 JPG、PNG、WEBP 等格式图片转换为 TPG 格式，大幅减小图片大小。 |
| HEIF 压缩 | 针对 iOS 环境的图片使用场景，可将 JPG、PNG、GIF、WEBP 等格式图片转换为 HEIF 格式，HEIF 格式有着超高压缩率。 |

>?
> - 使用图片高级压缩功能时，您需要在相应的存储桶配置页中通过开关按钮开启服务，详情请参见 [设置图片高级压缩](https://intl.cloud.tencent.com/document/product/436/40117)。
> - TPG 是腾讯自研的图片格式，如需使用请确认**图片加载环境支持 TPG 解码**，腾讯云数据万象提供集成 TPG 解码器的 iOS、Android、[Windows](https://main.qcloudimg.com/raw/851dd252378813d250eeca5ed55ffd36/TPG_win_SDK.zip) 终端 SDK，可帮助您快速接入和使用 TPG。
> - 目前 iOS 11以上及 Android P 系统已原生支持 HEIF 格式。
> - 图片高级压缩为付费服务，由数据万象收取，具体费用请参见数据万象的[定价文档](https://intl.cloud.tencent.com/document/product/1045/33431)。
> 

## 接口示例

#### 1. 下载时处理

```plaintext
download_url?imageMogr2/format/<Format>
```

#### 2. 上传时处理

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
      "rule": "imageMogr2/format/<Format>"
  }]
}
```

#### 3. 云上数据处理

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
      "rule": "imageMogr2/format/<Format>"
  }]
}
```

>? 本篇文档中的实际案例仅包含**下载时处理**，该类处理不会保存处理后的图片至存储桶。如有保存需求，您可查阅图片持久化处理文档并配置**上传时处理**或**云上数据处理**。

## 处理参数说明

| 参数             | 含义                                                         |
| :--------------- | :----------------------------------------------------------- |
| download_url     | 文件的访问链接，具体构成为&lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com/&lt;picture name>， 例如`examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`。 |
| /format/&lt;Format> | 压缩格式，目标缩略图的图片格式为 TPG 或 HEIF。               |

## 实际案例

假设原图格式为 PNG，图片大小为1335.2KB，如下图所示。
![img](https://main.qcloudimg.com/raw/8d539dcbea299f55ea786feb26f5c21b.png)

将原图转换为 TPG 格式，URL 地址如下：

```plaintext
http://example-1258125638.cos.ap-shanghai.myqcloud.com/sample.png?imageMogr2/format/tpg
```

将原图转换为 HEIF 格式，URL 地址如下：

```plaintext
http://example-1258125638.cos.ap-shanghai.myqcloud.com/sample.png?imageMogr2/format/heif
```

**压缩率对比**

| 格式        | 图片大小               |
| :---------- | :--------------------- |
| PNG（原图） | 1335.2KB               |
| TPG         | 36.67KB（压缩率97.3%） |
| HEIF        | 52.87KB（压缩率96.0%） |
