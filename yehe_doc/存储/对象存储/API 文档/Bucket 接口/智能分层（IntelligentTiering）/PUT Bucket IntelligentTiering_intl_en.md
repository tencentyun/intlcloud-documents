## Overview

This API is used to enable intelligent tiering configuration on a bucket.

> ?
>
> - Once enabled, the intelligent tiering configuration can only allow modifying the days for moving objects between storage tiers, but cannot be disabled.
> - Only the root account or sub-accounts that are granted permission for the PUT Bucket IntelligentTiering action can call this API.
> - You can obtain the object’s storage tier from the `x-cos-storage-tier` returned by calling the HEAD Object API.

## Request

#### Sample request

```plaintext
PUT /?intelligenttiering HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Connection: keep-alive
Authorization: authorization string
Content-Type: text/plain
Content-Length: Int
```

> ?Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

#### Request parameters

This API does not use any request parameters.

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

```shell
<IntelligentTieringConfiguration xmlns="cos xmlns/"> 
  <Status>Enabled</Status>
  <Transition>
    <Days>30|60|90</Days>
  </Transition>
</IntelligentTieringConfiguration>
```

The nodes are described in detail below:


| Node Name                           | Parent Node                                   | Description                                                         | Type      | Required |
| ------------------------------- | ------------------------------------------ | ------------------------------------------------------------ | --------- | -------- |
| IntelligentTieringConfiguration | None                                         | Information on the intelligent tiering configuration                               | Container | Yes       |
| Status                          | IntelligentTieringConfiguration            | Specifies the status of the intelligent tiering configuration once enabled. Enumerated values: Suspended, Enabled     | Enum      | Yes       |
| Transition                      | IntelligentTieringConfiguration            | Specifies the transition for objects in the intelligent tiering configuration                 | Container | Yes       |
| Days                            | IntelligentTieringConfiguration.Transition | Specifies the number of consecutive days for which an object in the STANDARD storage tier has not been accessed before being moved to the STANDARD_IA storage tier. Default: 30 | Int       | Yes       |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body of this API is empty.

#### Error codes

This API returns uniform error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

#### Request

```shell
PUT /?intelligenttiering HTTP/1.1
Host: examplebucket-1250000000.cos.ap-chengdu.myqcloud.com
Connection: keep-alive
Accept-Encoding: gzip, deflate
Accept: */*
User-Agent: python-requests/2.12.4
Content-Type: application/xml
Authorization: q-sign-algorithm=sha1&q-ak=AKID15IsskiBQKTZbAo6WhgcBqVls9Sm****&q-sign-time=1480932292;1981012292&q-key-time=1480932292;1981012292&q-url-param-list=versioning&q-header-list=host&q-signature=47ec2b80c73788ecd394d3b9ad90e120a32f****
Content-Length: 83

<IntelligentTieringConfiguration xmlns="cos xmlns/"> 
  <Status>Enabled</Status>
  <Transition>
    <Days>30</Days>
  </Transition>
</IntelligentTieringConfiguration>
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Sun, 23 Aug 2020 08:14:53 GMT
Server: tencent-cos
x-cos-request-id: NTk5ZDM5N2RfMjNiMjM1MGFfMmRiX2Y0****
```
