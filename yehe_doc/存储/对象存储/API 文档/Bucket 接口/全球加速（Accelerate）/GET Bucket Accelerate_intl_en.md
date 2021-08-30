## Overview

This API is used to query the global acceleration configuration of a bucket.

**Notes**

1. If you have never enabled global acceleration for the bucket, the global acceleration status will not be returned even if you call this API.
2. Valid values of `Status` are `Enabled` and `Suspended`.
3. If a sub-account needs to call this API, it needs to have permission to read the global acceleration configuration.

## Request

#### Sample request

```shell
GET /?accelerate HTTP 1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT date
Authorization: Auth String
```

>? 
> - In `Host: <BucketName-APPID>.cos.<Region>.myqcloud.com`, <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).
> 

#### Request headers

This API only uses common request headers. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

The request body of this request is empty.

## Response

#### Response headers

This API returns only common response headers. For more information, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729). 

#### Response body

```shell
<AccelerateConfiguration xmlns="cos xmlns/"> 
  <Status>Enabled</Status> 
  <Type>COS</Type>
</AccelerateConfiguration>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| ----------------------- | ----------------------- | ---------------------------------------------------- | --------- |
| AccelerateConfiguration | None | Information about global acceleration | Container |
| Status | AccelerateConfiguration | Whether global acceleration is enabled. Enumerated values: `Suspended`, `Enabled` | Enum |
| Type | AccelerateConfiguration | Global acceleration type. Enumerated value: `COS` | Enum |

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Sample

#### Request

```shell
GET /?accelerate HTTP/1.1
Host: examplebucket-1250000000.cos.ap-chengdu.myqcloud.com
Connection: keep-alive
Authorization: authorization string
Content-Type: text/plain
```

#### Response 1 (global acceleration enabled)

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 73
Connection: keep-alive
Date: Wed, 23 Aug 2019 08:14:53 GMT
Server: tencent-cos
x-cos-request-id: NTk5ZDM5N2RfMjNiMjM1MGFfMmRiX2Y0****

<AccelerateConfiguration>
  <Status>Enabled</Status>
  <Type>COS</Type>
</AccelerateConfiguration>
```

#### Response 2 (global acceleration suspended)

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 73
Connection: keep-alive
Date: Wed, 23 Aug 2019 08:14:53 GMT
Server: tencent-cos
x-cos-request-id: NTk5ZDM5N2RfMjNiMjM1MGFfMmRiX2Y0****

<AccelerateConfiguration>
  <Status>Disabled</Status>
  <Type>COS</Type>
</AccelerateConfiguration>
```

#### Response 3 (global acceleration not enabled)

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 73
Connection: keep-alive
Date: Wed, 23 Aug 2019 08:14:53 GMT
Server: tencent-cos
x-cos-request-id: NTk5ZDM5N2RfMjNiMjM1MGFfMmRiX2Y0****

<AccelerateConfiguration/>
```
