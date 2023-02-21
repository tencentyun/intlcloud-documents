## Overview
This API is used to enable the Guetzli compression feature for a bucket.

## Request

#### Sample request

```
PUT /?guetzli HTTP/1.1
Host: <BucketName-APPID>.pic.<Region>.myqcloud.com 
Date: GMT Date
Authorization: Auth String
```

>?
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
> - Guetzli compression currently cannot be used at COS domain names. Use `pic` domain names as described in the sample.
>

#### Request line

```
PUT /?guetzli HTTP/1.1
```
This API accepts `PUT` requests.

#### Request headers

#### Common request headers

This API uses common request headers. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Non-common request headers

This API does not use any non-common request header.

#### Request body
The request body of this request is empty.

## Response

#### Response headers

#### Common response headers

This API uses common response headers. For more information, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Non-common response headers

This API does not use any non-common response header.

#### Response body
The response body returned is empty.
  
