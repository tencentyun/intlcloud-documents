## Description
This API (DELETE Bucket policy) is used to delete the permission policy of a Bucket.

>Only the Bucket owner is allowed to initiate this request. You will receive "204 No Content" if the permission policy does not exist.

## Request

### Request example

```shell
DELETE /?policy HTTP/1.1
Host:<BucketName-APPID>.cos.<Region>.myqcloud.com
Date: date
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

## Example

### Request

```shell
DELETE /?policy HTTP/1.1
Host:examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Authorization:q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484814613;32557710613&q-key-time=1484814613;32557710613&q-header-list=host&q-url-param-list=policy&q-signature=57c9a3f67b786ddabd2c208641944ec7f9b02f98
```

### Response

```shell
HTTP/1.1 204 No Content
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Thu Jan 19 16:30:21 2017
Server: tencent-cos
x-cos-request-id: NTg4MDc5MWRfNDQyMDRlXzNiMDRfZTEw
```

