## Description
This API (DELETE Bucket) is used to delete a Bucket under the specified account.
>The data and parts that have not completed uploading in a Bucket must be cleared before the Bucket can be deleted.

## Request
### Request example
```
DELETE / HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String (For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).

### Request headers

#### Common headers
Common request headers are used for the implementation of this request operation. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special request headers
This request operation does not use any special request header.

### Request body
The request body of this request is empty.

## Response

### Response headers
#### Common response headers
This response uses common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Special response headers
This response does not use any special response header.

### Response body
The response body is empty.

### Error Codes
Here are some special and common errors that may occur with this request. For more information on COS error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

| Error Code | HTTP Status Code | Description |
|-------|------|------|
| BucketNotEmpty | 409 Conflict | The Bucket is not empty and thus cannot be deleted. |
| AccessDenied | 403 Forbidden | Signature is required when deleting a Bucket. If you request to delete a Bucket that you have no permission to access, this error is returned. |
| NoSuchBucket | 404 Not Found | The Bucket does not exist. |


## Example

### Request
```
DELETE / HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 23 Oct 2016 21:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484708950;32557604950&q-key-time=1484708950;32557604950&q-header-list=host&q-url-param-list=&q-signature=2b27b72ad2540ff2dde341dc7579a66ee8cb2afc
```

### Response
```
HTTP/1.1 204 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Wed, 23 Oct 2016 21:32:00 GMT
Server: tencent-cos
x-cos-request-id: NTg3ZWRjNjBfOTgxZjRlXzZhYjlfMTg0
```

