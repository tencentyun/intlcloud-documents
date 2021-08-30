## Overview
This API is used to query which region a bucket resides in. This GET request obtains the region with the `location` parameter. Only the bucket owner has permission to call this API.

## Request
### Sample request

```shell
GET /?location HTTP/1.1
Host: <Bucketname-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? 
> - In `Host: <BucketName-APPID>.cos.<Region>.myqcloud.com`, <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).
> 

### Request headers
#### Common headers
This API uses common request headers. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).
#### Non-common request headers
This API does not use any non-common request header.


### Request body
The request body of this request is empty.

## Response

### Response headers
#### Common response headers
This API uses [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Non-common response headers
This API does not use any non-common response header.

### Response body
The region is returned in the response body.

```shell
<?xml version="1.0" encoding="UTF-8" ?>
<LocationConstraint>cos.ap-beijing</LocationConstraint>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
---|---|---|---|---
| LocationConstraint | None | Region where the bucket resides. For the enumerated values such as `ap-beijing`, `ap-hongkong`, and `eu-frankfurt`, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | string | Yes |

### Error codes
No special error message will be returned for this request. For the common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).


## Sample

### Request

```shell
GET /?location HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 18 Oct 2014 22:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUj****&q-sign-time=1484817522;32557713522&q-key-time=1484817522;32557713522&q-header-list=host&q-url-param-list=location&q-signature=ceb96fc929663dd4d2e6dc0aeb304cdde67****
```

### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 92
Connection: keep-alive
Date: Wed, 18 Oct 2014 22:32:00 GMT
Server: tencent-cos
x-cos-request-id: NTg4MDg0NzlfNDYyMDRlXzM0OWFf****

<LocationConstraint>cos.ap-beijing</LocationConstraint>
```
