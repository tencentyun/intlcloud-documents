## Overview
This API is used to query whether the original image protection feature is enabled.

## Request
#### Sample request
```
GET /?origin-protect HTTP/1.1
Host: <BucketName-APPID>.pic.<Region>.myqcloud.com 
Date: GMT Date
Authorization: Auth String
```


>? Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).
>

#### Request headers

This API only uses common request headers. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

The request body of this request is empty.

## Response

#### Response headers

This API returns only common response headers. For more information, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body
```
<?xml version="1.0" encoding="UTF-8" ?>
<OriginProtectStatus>on</OriginProtectStatus>
```

Node Name (Keyword) | Description
--|--
OriginProtectStatus | Valid values: `on`, `off`
  
