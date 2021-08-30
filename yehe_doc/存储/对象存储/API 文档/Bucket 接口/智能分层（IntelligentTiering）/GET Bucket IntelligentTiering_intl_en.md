## Overview

This API is used to query the INTELLIGENT TIERING configuration of a bucket.

> ?
> - Only the root account and authorized sub-accounts can call this API.
> - The status of INTELLIGENT TIERING can only be enabled or suspended.
> - If you have never enabled INTELLIGENT TIERING for your bucket, the response will be:
```shell
	<IntelligentTieringConfiguration/>
```
> - If you have enabled INTELLIGENT TIERING for your bucket, the response will be:
```shell
<IntelligentTieringConfiguration xmlns="cos xmlns/"> 
       <Status>Enabled</Status>
       <Transition>
          <Days>30</Days>
       </Transition>
</IntelligentTieringConfiguration>
```

## Request

#### Sample request

```shell
GET /?intelligenttiering HTTP 1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT date
Authorization: Auth String
```

>? 
> - In `Host: <BucketName-APPID>.cos.<Region>.myqcloud.com`, <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).
> 

#### Request parameters

This API has no request parameter.

#### Request headers

This API only uses common request headers. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

The request body of this request is empty.

## Response

#### Response headers

This API returns only common response headers. For more information, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

```shell
<IntelligentTieringConfiguration xmlns="cos xmlns/"> 
  <Status>Enabled</Status>
  <Transition>
    <Days>30|60|90</Days>
  </Transition>
</IntelligentTieringConfiguration>
```

The nodes are described as follows:

| Node | Parent Node | Description | Type |
| ------------------------------- | ------------------------------------------ | ------------------------------------------------------------ | --------- |
| IntelligentTieringConfiguration | None | Configuration of INTELLIGENT TIERING | Container |
| Status | IntelligentTieringConfiguration | Whether INTELLIGENT TIERING is enabled. Enumerated values: `Suspended`, `Enabled` | Enum |
| Transition | IntelligentTieringConfiguration | Transition configuration for INTELLIGENT TIERING | Container |
| Days | IntelligentTieringConfiguration.Transition | The number of consecutive days after which objects are moved from STANDARD to STANDARD_IA. Valid values: 30 (default), 60, 90 | Int  |

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Sample

#### Request

```shell
GET /?intelligenttiering HTTP/1.1
Host: examplebucket-1250000000.cos.ap-chengdu.myqcloud.com
Connection: keep-alive
Accept-Encoding: gzip, deflate
Accept: */*
User-Agent: python-requests/2.12.4
Authorization: q-sign-algorithm=sha1&q-ak=AKID15IsskiBQKTZbAo6WhgcBqVls9Sm****&q-sign-time=1480932292;1981012292&q-key-time=1480932292;1981012292&q-url-param-list=versioning&q-header-list=host&q-signature=5118a936049f9d44482bbb61309235cf4abe****
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 120
Connection: keep-alive
Date: Sun, 23 Aug 2020 08:15:16 GMT
Server: tencent-cos
x-cos-request-id: NTk5ZDM5OTRfZDNhZDM1MGFfMjYyMTFfZmU3****

<IntelligentTieringConfiguration xmlns="cos xmlns/"> 
  <Status>Enabled</Status>
  <Transition>
    <Days>30</Days>
  </Transition>
</IntelligentTieringConfiguration>
```
