## Description
This API is used to launch the Cloud Infinite (CI) service and bind it to an existing Cloud Object Storage (COS) bucket. You can use COS APIs to call other features of the bucket, such as query and modification.

## Request
#### Request sample

```
PUT / HTTP/1.1
Host: <BucketName-APPID>.pic.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String (For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).

#### Request line

```
PUT / HTTP/1.1
```

This API allows PUT requests.

#### Request header
#### Common headers
Common request headers are used for the implementation of this request operation. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).
#### Special request headers
This request operation does not use any special request header.

#### Request body
The request body of this request is empty.

## Response
#### Response header
#### Common response headers
This response uses common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Special response headers
This response does not use any special response header.

#### Response body
Null is returned for the response body.