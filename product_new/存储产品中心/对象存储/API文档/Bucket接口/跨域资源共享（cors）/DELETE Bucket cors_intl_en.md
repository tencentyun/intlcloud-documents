## Description
This API (DELETE Bucket cors) is used to delete the cross-origin access configuration information.

## Request
### Sample Request

```
DELETE /?cors HTTP/1.1
Host: <Bucketname-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

### Request Headers

#### Common Headers
The implementation of this request operation uses a common request header. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special Headers
This request operation has no special request headers.

### Request Body
The request body of this request is empty.

## Response
### Response Headers

#### Common Response Headers

This response uses a common response header. For more information on the common response header, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Special Response Headers
This response has no special response headers.

### Response Body
This response body is empty.

### Error Codes
The following error messages may be returned for this request operation. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

Error Code | Description | HTTP Status Code
---|---|---
None| Deletion succeeded. The response body return is empty. |204 [No Content](https://tools.ietf.org/html/rfc7231#section-6.3.5)
NoSuchBucket| This error code will be returned if the accessed bucket does not exist |404 [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)


## Samples

### Request

```
DELETE /?cors HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 16 Aug 2017 12:59:09 GMT
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98JM&q-sign-time=1502859472;1502939472&q-key-time=1502859472;1502939472&q-header-list=host&q-url-param-list=lifecycle&q-signature=49c1414c700643f11139219384332a3ec4e9485b
```

### Response

```
HTTP/1.1 204 No Content
Content-Type: application/xml
Date: Wed, 16 Aug 2017 12:59:09 GMT
Server: tencent-cos
x-cos-request-id: NTk5NDQxOWNfMjQ4OGY3Xzc3NGRfMjE=
```


