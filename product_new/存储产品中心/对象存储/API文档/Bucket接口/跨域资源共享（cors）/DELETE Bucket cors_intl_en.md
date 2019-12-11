## Description
This API is used to delete cross-origin access configuration information.

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
The implementation of this operation uses common request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special Headers
This request operation does not use any special request header.

### Request Body
The request body of this request is empty.

## Response
### Response Headers

#### Common Response Headers

This response uses common response headers. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Special Response Headers
This response does not use any special response header.

### Response Body
This response body is empty.

### Error Codes
The implementation of this operation returns the following error messages. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

Error Code | Description | HTTP Status Code
---|---|---
None| Deleted successfully. The response body is empty. |204 [No Content](https://tools.ietf.org/html/rfc7231#section-6.3.5)
NoSuchBucket| This error code will be returned if the bucket you are trying to access does not exist |404 [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)


## Example

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


