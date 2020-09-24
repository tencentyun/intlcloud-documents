## Overview

This API is used to obtain the intelligent tiering configuration on a bucket.

> ?
>
> - Only the root account or sub-accounts that are granted permission for the GET Bucket IntelligentTiering operation can call this API.
> - There are two types of responses to this API request:
>  - If you never enabled intelligent tiering configuration on the bucket before, the response will be:
```shell
	<IntelligentTieringConfiguration/>
```
>  - If you enabled intelligent tiering configuration on the bucket, the response will be:
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

> ?Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

#### Request parameters

This API does not use any request parameters.

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

This request has no request body.

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

```shell
<IntelligentTieringConfiguration xmlns="cos xmlns/"> 
  <Status>Enabled</Status>
  <Transition>
    <Days>30|60|90</Days>
  </Transition>
</IntelligentTieringConfiguration>
```

The nodes are described in details below:

| Node Name                           | Parent Node                                   | Description                                                         | Type      |
| ------------------------------- | ------------------------------------------ | ------------------------------------------------------------ | --------- |
| IntelligentTieringConfiguration | None                                         | Information on the intelligent tiering configuration                                   | Container |
| Status                          | IntelligentTieringConfiguration            | Specifies the status of the intelligent tiering configuration once enabled. Enumerated values: Suspended, Enabled     | Enum      |
| Transition                      | IntelligentTieringConfiguration            | Specifies the transition for objects in the intelligent tiering configuration                 | Container |
| Days                            | IntelligentTieringConfiguration.Transition | Specifies the number of consecutive days for which an object in the STANDARD storage tier has not been accessed before being moved to the STANDARD_IA storage tier. Default: 30 | Int       |

#### Error codes

This API returns uniform error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

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
