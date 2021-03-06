## 功能描述

该请求用于发起离线回源任务。

## 请求

#### 请求示例

```plaintext
POST /<BucketName-APPID>/ HTTP 1.1
Host: <Region>.migration.myqcloud.com
Date: GMT Date
Authorization: Auth String
Content-Type: application/json
```

> ? Authorization: Auth String （详情请参见 [请求签名](https://intl.cloud.tencent.com/document/product/436/7778) 文档）。

#### 请求参数

此接口无请求参数。

#### 请求头

此接口仅使用公共请求头部，详情请参见 [公共请求头部](https://intl.cloud.tencent.com/document/product/436/7728) 文档。

#### 请求体


```plaintext
{
				"Url": 
				"MD5"
				"IgnoreSameKey":
				"Key":
				"SuccessCallbackUrl":
				"FailureCallbackUrl":
				"OnKeyExist":
	}
```

参数说明如下：

| 名称                 | 描述          | 类型     | 是否必选   |
| ------------------ | ----------- | ------ | ---- |
| Url                | 源站资源地址，需要 url encode，不支持 HTTPS     | String | 是    |
| MD5                | 文件 MD5 校验值  | String | 否    |
| IgnoreSameKey               | 是否跳过同名文件，枚举值为 true、false  | Boolean | 否    |
| Key                | COS 中的文件路径，不需要 url encode   | String | 是    |
| SuccessCallbackUrl | 回源拉取成功的回调地址 | String | 否    |
| FailureCallbackUrl | 回源拉取失败的回调地址 | String | 否    |
| OnKeyExist                | 是否覆盖同名文件，枚举值为 ignore、override     | Enum | 否    |


## 响应

#### 响应头

此接口仅返回公共响应头部，详情请参见 [公共响应头部](https://intl.cloud.tencent.com/document/product/436/7729) 文档。


#### 响应体

```JSON
{
			"code":,
			"message":,
			"request_id":,
			"data":{"taskid":}
	}
```


返回的参数说明如下：

| 名称         | 描述               | 类型     |
| ---------- | ---------------- | ------ |
| code       | 请求状态码            | String |
| message    | 请求信息             | String |
| request_id | 请求唯一标示           | String |
| data       | 请求返回细节           | Array    |
| taskid     | 回源任务唯一 ID，用于查询进度 | String |


#### 错误码

此接口遵循统一的错误响应和错误码，详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) 文档。

## 实际案例
#### 请求

```plaintext
POST /examplebucket-1250000000/ HTTP/1.1
Host: ap-shanghai.migration.myqcloud.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUj****&q-sign-time=1487249006;1487763806&q-key-time=1487248991;1487810606&q-header-list=host&q-url-param-list=&q-signature=ef00b89b12f556d47bc8610d4b8572928981****
Content-Type: application/json
Content-Length: 159



{
			"Url": "examplebucket-1250000000.ap-beijing.myqcloud.com/doc",
			"Key":"movie.mp4",
			"SuccessCallbackUrl":"http://example.com/api/mocker/cos/",
			"FailureCallbackUrl":"http://example.com/api/mocker/cos/"
	}
```

#### 响应

```plaintext
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Content-Length: 122
Connection: keep-alive
Date: Thu Feb 16 21:52:50 2017
Server: tencent-cos
x-cos-request-id: NThhNWFlYjJfOGVmYTUwXzRkYjVf****



{
			"code":0,
			"message":"SUCCESS",
			"request_id":"NThhNjZiOTRfOGZmYTUwXzJlNWRf****",
			"data":{"taskid":"NThhNjZiOTRfOGZmYTUwXzJlNWRfMw=="}
	}
```

