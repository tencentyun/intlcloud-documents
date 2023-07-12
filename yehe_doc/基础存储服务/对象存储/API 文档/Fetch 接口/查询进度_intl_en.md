## Description

This API is used to query the origin-pull progress.

## Request

#### Sample request

```plaintext
GET /<BucketName-APPID>/<TaskId> / HTTP 1.1
Host: <Region>.migration.myqcloud.com
Date: GMT Date
Authorization: Auth String
Content-Type: application/json
```

> ? Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)

#### Request parameters

| Parameter | Description | Type | Required |
|----|----|----|------|
| TaskId | ID of the task | String | Yes |


#### Request headers

This API only uses common request headers. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

This API does not have a request body.


## Response

#### Response headers

This API returns only common response headers. For more information, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

```json
{
  	"code":,
  	"message":,
  	"request_id":,
			"data":{"percent":,"status":}
	}
```


Parameters in the response body are described as follows:

| Parameter | Description | Type |
| ---------- | ------- | ------ |
| code | Request status code | String |
| message | Request message | String |
| request_id | Unique ID of the request | String |
| data | Data returned | Array |
| percent | Origin-pull progress | Number |
| status | Task status | String |



#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).



## Sample

#### Request

```plaintext
GET /examplebucket-1250000000/NThhNWFkM2VfOGVmYTUwXzRkYjFfMw== HTTP/1.1
Host: ap-shanghai.migration.myqcloud.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUj****&q-sign-time=1487252847;1487767647&q-key-time=1487252832;1487814447&q-header-list=host&q-url-param-list=&q-signature=1706b38d75725f12e2d9fc3d4bb67311c8ca****
Content-Type: application/json
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
			"request_id":"NThhNWFlYjJfOGVmYTUwXzRkYjVf****",
			"data":{"percent":0,"status":"TASK_DOING"}
	}
```

