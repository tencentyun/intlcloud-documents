## API Description

This API is used to delete the cross-origin resource sharing (CORS) access control configuration from a bucket.

## Request

#### Sample request

```plaintext
DELETE /?cors HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

#### Request parameters

This API does not use any request parameters.

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

This API does not have a request body.

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body of this API is empty.

#### Error codes

This API returns uniform error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

#### Request

```plaintext
DELETE /?cors HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 09 Jul 2020 11:52:50 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1594295570;1594302770&q-key-time=1594295570;1594302770&q-header-list=date;host&q-url-param-list=cors&q-signature=1994d46c0ec515f5433016e17f0e49c72e4c****
Connection: close
```

#### Response

```plaintext
HTTP/1.1 204 No Content
Connection: close
Date: Thu, 09 Jul 2020 11:52:50 GMT
Server: tencent-cos
x-cos-request-id: NWYwNzA1MTJfNjRiODJhMDlfMWMyMzlfMWMyNzhl****
x-cos-trace-id: OGVmYzZiMmQzYjA2OWNhODk0NTRkMTBiOWVmMDAxODczNTBmNjMwZmQ0MTZkMjg0NjlkNTYyNmY4ZTRkZTk0NzJmZTI0ZmJhYTZmZjYyNmU5ZGNlZDI5YjkyODkwYjNhYjJkOWQzYWJlOGRjYzY5N2ZlMGJhZjdlNDA4YjkzODc=
Content-Length: 0
```
