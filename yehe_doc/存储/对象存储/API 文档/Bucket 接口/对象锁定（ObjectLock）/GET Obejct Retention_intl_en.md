
## Overview

This API is used to obtain the expiration date of object lock.

## Request

#### Sample request

```plaintext
GET /<object-key>?retention HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String 
```

> ?Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)

#### Request headers

This API only uses common request headers. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

The request body of this request is empty.

 

## Response

#### Response headers

This API returns only common response headers. For more information, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body


```plaintext
<?xml version="1.0" encoding="UTF-8" ?>
<Retention> 
         <RetainUntilDate>timestamp</RetainUntilDate> 
</Retention> 
```


Nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | --------- | ------------ | ------------ |
| Retention  | None | Retention period (during which an object remains locked) | Container |
| RetainUntilDate | Retention | Expiration date of the retention period | String |

 

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

 