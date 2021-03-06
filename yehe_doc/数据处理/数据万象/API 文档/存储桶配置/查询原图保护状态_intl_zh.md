## 功能描述
用于查询原图保护功能是否开启。

## 请求
#### 请求示例
```
GET /?origin-protect HTTP/1.1
Host: <BucketName-APPID>.pic.<Region>.myqcloud.com 
Date: GMT Date
Authorization: Auth String
```


>? Authorization：Auth String （详情参阅 [请求签名](https://intl.cloud.tencent.com/document/product/436/7778) 文档）。
>

#### 请求头

此接口仅使用公共请求头部，详情请参见 [公共请求头部](https://intl.cloud.tencent.com/document/product/436/7728) 文档。

#### 请求体

该请求的请求体为空。

## 响应

#### 响应头

此接口仅返回公共响应头部，详情请参见 [公共响应头部](https://intl.cloud.tencent.com/document/product/436/7729) 文档。

#### 响应体
```
<?xml version="1.0" encoding="UTF-8" ?>
<OriginProtectStatus>on</OriginProtectStatus>
```

节点名称（关键字）|描述
--|--
OriginProtectStatus|on 与 off 两种状态。
  
