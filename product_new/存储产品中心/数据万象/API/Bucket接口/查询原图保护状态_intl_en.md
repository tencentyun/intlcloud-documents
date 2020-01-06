## Description
This API is used to query whether the original image protection feature is enabled.

## Request
#### Request sample
```
GET /?origin-protect HTTP/1.1
Host: <BucketName-APPID>.pic.<Region>.myqcloud.com 
Date: GMT Date
Authorization: Auth String
```
>Authorization: Auth String (For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).

#### Request line
```
GET /?origin-protect HTTP/1.1
```
This API allows GET requests.

#### Request headers

#### Common headers
Common request headers are used for the implementation of this request operation. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special request headers
This request operation does not use any special request header.
#### Request body
The request body of this request is empty.

## Response

#### Response headers
#### Common response headers
This response uses common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Special response headers
This response does not use any special response header.

#### Response body
```
<?xml version="1.0" encoding="UTF-8" ?>
<OriginProtectStatus>on</OriginProtectStatus>

```

Node Name (Keyword) | Description
--|--
OriginProtectStatus | Valid values: on and off.