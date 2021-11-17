## Overview

This API is used to enable INTELLIGENT TIERING for a bucket.

> ?
> - Once enabled, INTELLIGENT TIERING cannot be disabled or modified.
> - Only the root account and authorized sub-accounts can call the `PUT Bucket IntelligentTiering` API.
> - You can use `x-cos-storage-tier` returned by the [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) API to determine the storage tier of the object.

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

>? 
> - In `Host: <BucketName-APPID>.cos.<Region>.myqcloud.com`, <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).
> 

#### Request parameters

This API has no request parameter.

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

```shell
<IntelligentTieringConfiguration xmlns="cos xmlns/"> 
  <Status>Enabled</Status>
  <Transition>
    <Days>30|60|90</Days>
  </Transition>
</IntelligentTieringConfiguration>
```

The nodes are described as follows:

| Name                            | Parent Node                                     | Description                                                         | Type      | Required |
| ------------------------------- | ------------------------------------------ | ------------------------------------------------------------ | --------- | -------- |
| IntelligentTieringConfiguration | No                                         | Detailed configuration of INTELLIGENT TIERING                                   | Container | Yes       |
| Status                          | IntelligentTieringConfiguration            | Whether to enable INTELLIGENT TIERING. Enumerated values: `Suspended`, `Enabled`     | Enum      | Yes       |
| Transition                      | IntelligentTieringConfiguration            | Specifies the transition configuration for INTELLIGENT TIERING                 | Container | Yes       |
| Days                            | IntelligentTieringConfiguration.Transition | Specifies the number of consecutive days after which objects are moved from STANDARD to STANDARD_IA. The default value is 30 (days). | Int       | Yes       |

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body of this API is empty.

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Example

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
