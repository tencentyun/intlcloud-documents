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

>? 
> - Host: <BucketName-APPID>.cos.<Region>.myqcloud.com, where <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://www.tencentcloud.com/document/product/436/6224)).
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> 

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

The request body of this request is empty.

 

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

```plaintext
<?xml version="1.0" encoding="UTF-8" ?>
<Retention> 
         <RetainUntilDate>timestamp</RetainUntilDate> 
</Retention> 
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | --------- | ------------ | ------------ |
| Retention  | None | Retention period (during which an object remains locked) | Container |
| RetainUntilDate | Retention | Expiration date of the retention period | String |

 

#### Error codes

This API returns common error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples


#### Request


```plaintext
GET /temp.txt?retention HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Authorization: Auth String
```


#### Response


```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 87
Connection: keep-alive
Date: Fri, 09 Dec 2022 08:35:49 GMT
Server: tencent-cos
x-cos-request-id: NjM5MmYzNjVfMjBkMDM4MGJfMWM2ND****
 
<Retention>
	<RetainUntilDate>2022-12-10T08:34:48.000Z</RetainUntilDate>
</Retention>
```

