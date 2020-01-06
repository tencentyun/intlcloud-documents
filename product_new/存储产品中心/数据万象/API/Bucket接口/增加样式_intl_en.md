## Description
This API is used to add a style for a specified bucket.

## Request
#### Request sample

```
PUT /?style HTTP/1.1
Host: <BucketName-APPID>.pic.<Region>.myqcloud.com 
Date: GMT Date
Authorization: Auth String
<XML File>
```
>Authorization: Auth String (For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).

#### Request line

```
PUT /?style HTTP/1.1
```
This API allows PUT requests.

#### Request header
##### Common headers
Common request headers are used for the implementation of this request operation. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special request headers
This request operation does not use any special request header.
#### Request body

```
<?xml version="1.0" encoding="UTF-8" ?>
<AddStyle>
  <StyleName>string</StyleName>
<StyleBody>string</StyleBody>
</AddStyle>
```

## Response
#### Response header
#### Common response headers
This response uses common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Special response headers
This response does not use any special response header.
#### Response body
Null is returned for the response body.