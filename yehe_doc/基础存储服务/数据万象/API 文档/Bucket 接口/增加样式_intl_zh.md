## 功能描述
该接口用于对某一个存储桶设置样式功能，后续上传到该存储桶的图片文件都会被添加指定的样式。

>Bucket 接口目前频控存在限制要求，写请求最多1qps，读请求最多10qps。

## 请求
#### 请求示例
```plaintext
PUT /?style HTTP/1.1
Host: <BucketName-APPID>.pic.<Region>.myqcloud.com 
Date: GMT Date
Authorization: Auth String
<XML File>
```

> Authorization: Auth String （详情请参见 [请求签名](https://intl.cloud.tencent.com/document/product/436/7778) 文档）。


#### 请求头

此接口仅使用公共请求头部，详情请参阅 [公共请求头部](https://intl.cloud.tencent.com/document/product/436/7728) 文档。

#### 请求体

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<AddStyle>
  <StyleName>string</StyleName>
  <StyleBody>string</StyleBody>
</AddStyle>
```

具体节点描述如下：

| 节点名称（关键字） | 父节点 | 描述             | 类型      | 是否必选 |
| ------------------ | ------ | ---------------- | --------- | -------- |
| AddStyle           | 无     | 待添加的样式信息 | Container | 是       |


Container 节点 AddStyle 的内容：

| 节点名称（关键字） | 父节点   | 描述     | 类型   | 是否必选 |
| ------------------ | -------- | -------- | ------ | -------- |
| StyleName          | AddStyle | 样式名称 | string | 是       |
| StyleBody          | AddStyle | 样式详情 | string | 是       |


## 响应

#### 响应头
此接口仅返回公共响应头部，详情请参阅 [公共响应头部](https://intl.cloud.tencent.com/document/product/436/7729) 文档。

#### 响应体
该响应体返回为空。

#### 错误码
此接口无特殊错误信息，全部错误信息请参见 [错误码](https://intl.cloud.tencent.com/document/product/1045/33700) 文档。

## 实际案例

#### 请求
```plaintext
PUT /?style HTTP/1.1
Host: examplebucket-1250000000.pic.ap-chengdu.myqcloud.com
Date: Tue, 03 Apr 2019 09:06:15 GMT
Authorization:XXXXXXXXXXXX

<?xml version="1.0" encoding="UTF-8" ?>
<AddStyle>
  <StyleName>style_name</StyleName>
  <StyleBody>imageMogr2/thumbnail/!50px</StyleBody>
</AddStyle>
```

#### 响应

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Date: Tue, 03 Apr 2019 09:06:16 GMT
x-cos-request-id: xxxxxxxxxxxxxxxxxx
```
