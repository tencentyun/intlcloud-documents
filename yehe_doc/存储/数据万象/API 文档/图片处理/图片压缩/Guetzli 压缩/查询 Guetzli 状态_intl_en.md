## Overview
This API is used to query whether the Guetzli compression feature is enabled.

## Request

#### Sample request

```
GET /?guetzli HTTP/1.1
Host: <BucketName-APPID>.pic.<Region>.myqcloud.com 
Date: GMT Date
Authorization: Auth String
```

>? 
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
> 

#### Request line

```
GET /?guetzli HTTP/1.1
```

This API accepts `GET` requests.

#### Request headers

#### Common request headers

The implementation of this operation uses common request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Non-common request headers

This API does not use any non-common request header.

#### Request body

The request body of this request is empty.

## Response

#### Response headers

#### Common response headers

This response uses common response headers. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Non-common response headers

This API does not use any non-common response header.

#### Response body

```
<?xml version="1.0" encoding="UTF-8" ?>
<GuetzliStatus>on</GuetzliStatus>
```

Valid values: `on`, `off`.
  
