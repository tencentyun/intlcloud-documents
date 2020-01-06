## Description
This API is used to query existing styles of a bucket. If the request body is not used, all styles of the bucket are queried. If the request body is used, only the style with its name specified in the request body is queried.

## Request
#### Request sample

```
GET /?style HTTP/1.1
Host: <BucketName-APPID>.pic.<Region>.myqcloud.com 
Date: GMT Date
Authorization: Auth String
```
>Authorization: Auth String (For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).

#### Request line

```
GET /?style HTTP/1.1
```

This API allows PUT requests.

#### Request header
#### Common headers
Common request headers are used for the implementation of this request operation. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).
#### Special request headers
This request operation does not use any special request header.

#### Request body

```
<?xml version="1.0" encoding="UTF-8" ?>
<GetStyle>
  <StyleName>string</StyleName>
</GetStyle>
```

## Response
#### Response header
#### Common response headers
This response uses common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Special response headers
This response does not use any special response header.

#### Response body

```
<StyleList>
  <StyleRule>
  <StyleName>string</StyleName>
  <StyleBody>string</StyleBody>
</StyleRule>
  <StyleRule>
  <StyleName>string</StyleName>
  <StyleBody>string</StyleBody>
</StyleRule>
</StyleList>
```