## 功能描述

DELETE Bucket encryption 接口用于删除指定存储桶下的默认加密配置。

要执行此接口，必须拥有 DeleteBucketEncryption 权限。默认情况下，Bucket 的持有者直接拥有权限使用该 API 接口，Bucket 持有者也可以将权限授予其他用户。

## 请求

**请求示例**

```sh
DELETE /?encryption HTTP 1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? 
> - Host: &lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com，其中 &lt;BucketName-APPID> 为带 APPID 后缀的存储桶名字，例如 examplebucket-1250000000，可参阅 [存储桶概览 > 基本信息](https://intl.cloud.tencent.com/document/product/436/38493) 和 [存储桶概述 > 存储桶命名规范](https://intl.cloud.tencent.com/document/product/436/13312) 文档；&lt;Region> 为 COS 的可用地域，可参阅 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224)文档。
> - Authorization: Auth String（详情请参见 [请求签名](https://intl.cloud.tencent.com/document/product/436/7778) 文档）。
> 

**请求参数**

此接口无请求参数。

**请求头**

此接口仅使用公共请求头部，详情请参见 [公共请求头部](https://intl.cloud.tencent.com/document/product/436/7728) 文档。

**请求体**

该请求的请求体为空。

## 响应

**响应头**

此接口仅返回公共响应头部，详情请参见 [公共响应头部](https://intl.cloud.tencent.com/document/product/436/7729) 文档。

**响应体**

该请求的响应体返回为空。

**错误码**

此接口遵循统一的错误响应和错误码，详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) 文档。

## 实际案例

**请求**

以下示例表示从存储桶 examplebucket-1250000000 中删除默认 SSE-COS 加密配置。

```sh
DELETE /?encryption HTTP 1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Mon, 17 Jun 2019 08:37:35 GMT
Authorization: signatureValue
```

**响应**

```sh
HTTP/1.1 204 No Content
Server: tencent-cos
Date: Mon, 17 Jun 2019 08:37:36 GMT
x-cos-request-id: NWQwNzUxNTBfMzdiMDJhMDlfOWM0Nl85NDFk****
```
