## Description

This API is used to initiate an offline origin-pull task.

## Request

#### Sample request

```plaintext
POST /<BucketName-APPID>/ HTTP 1.1
Host: <Region>.migration.myqcloud.com
Date: GMT Date
Authorization: Auth String
Content-Type: application/json
```

> ? Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)

#### Request parameters

This API has no request parameter.

#### Request headers

This API only uses common request headers. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body


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

The parameters are described as follows:

| Parameter | Description | Type | Required |
| ------------------ | ----------- | ------ | ---- |
| Url | The origin server’s URL, which needs to be URL-encoded. Note that HTTPS is not supported. | String | Yes |
| MD5 | MD5 checksum of the file | String | No |
| IgnoreSameKey | Indicates whether to skip files with the same name. Enumerated values: `true`, `false` | Boolean | No |
| Key | The COS file’s path, which does not need to be URL-encoded. | String | Yes |
| SuccessCallbackUrl | Callback URL for origin-pull success | String | No |
| FailureCallbackUrl | Callback URL for origin-pull failure | String | No |
| OnKeyExist | Indicates whether to overwrite files with the same name. Enumerated values: `ignore`, `override` | Enum | No |


## Response

#### Response headers

This API returns only common response headers. For more information, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).


#### Response body

```JSON
{
			"code":,
			"message":,
			"request_id":,
			"data":{"taskid":}
	}
```


Parameters in the response body are described as follows:

| Parameter | Description | Type |
| ---------- | ---------------- | ------ |
| code | Request status code | String |
| message | Request message | String |
| request_id | Unique ID of the request | String |
| data | Data returned | Array |
| taskid | The origin-pull task’s unique ID, which can be used to query the progress | String |


#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Sample
#### Request

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

#### Response

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

