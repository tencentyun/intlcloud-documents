## Description
This API is used to query the details about hotlink protection (blacklist and whitelist) in a bucket.

## Request
#### Request sample

```
GET /?hotlink HTTP/1.1
Host: <BucketName-APPID>.pic.<Region>.myqcloud.com 
Date: GMT Date
Authorization: Auth String
```
>Authorization: Auth String (For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).

#### Request line
```
GET /?hotlink HTTP/1.1
```
This API allows PUT requests.

#### Request header
#### Common headers
Common request headers are used for the implementation of this request operation. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).
#### Special request headers
This request operation does not use any special request header.
#### Request body
This request operation does not use any special request body.

## Response
#### Response header
#### Common response headers
This response uses common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Special response headers
This response does not use any special response header.

### Response body
The response body contains the type of hotline protection and enumerates all addresses.

```
<?xml version="1.0" encoding="UTF-8" ?>
<Hotlink>
	<Status>on</Status>
	<Type>white</Type>
	<Url>xxx</Url>
	<Url>xxx</Url>
</Hotlink>
```