## Description

This API (DELETE Bucket website) deletes the configuration of the static website associated with the Bucket.

## Request

### Request example

```HTTP
DELETE /?website HTTP/1.1
Host:<BucketName-APPID>.<Region>.myqcloud.com
Date:date
Authorization: Auth String
```

Authorization: Auth String (For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).

### HTTP headers

#### Common request headers

Common request headers are used for this action. For more information, see [Common Request Headers](https://cloud.tencent.com/document/product/436/7728).

#### Special request headers

Special headers are not used for this action.

### Request body

Empty.

## Response

### Response headers

#### Common response headers

Common request headers are used for this action. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Special response headers

Special headers are not used for this action.

### Response body

Empty.

### Error codes

No special error message is returned for this action. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Example

### Request

```
DELETE /?website HTTP/1.1
Host: examplebucket-1250000000.cos.ap-shanghai.myqcloud.com
Date:Thu, 21 Sep 2017 13:21:09 +0000
Authorization:q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484816036;32557712036&q-key-time=1484816036;32557712036&q-header-list=host&q-url-param-list=website&q-signature=e92eecbf0022fe7e5fd39b2c500b22da062be50a
```

### Response

```
HTTP/1.1 204 No Content
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Thu, 21 Sep 2017 13:21:18 GMT
Server: tencent-cos
x-cos-request-id: NTljM2JjY2RfMjQ4OGY3MGFfNzk4OV84Mw==
```
