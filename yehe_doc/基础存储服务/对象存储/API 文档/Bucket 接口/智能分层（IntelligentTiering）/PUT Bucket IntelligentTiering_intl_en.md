## Feature Description

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
> - Host: <BucketName-APPID>.cos.<Region>.myqcloud.com, where <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://www.tencentcloud.com/document/product/436/6224)).
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
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
    <RequestFrequent>1</RequestFrequent>
  </Transition>
</IntelligentTieringConfiguration>
```

The nodes are described as follows:

| Name                            | Parent Node                                     | Description                                                         | Type      | Required |
| ------------------------------- | ------------------------------------------ | ------------------------------------------------------------ | --------- | -------- |
| IntelligentTieringConfiguration | No                                         | Detailed configuration of INTELLIGENT TIERING                                   | Container | Yes       |
| Status                          | IntelligentTieringConfiguration            | Whether to enable INTELLIGENT TIERING. Enumerated value: `Enabled`     | Enum      | Yes       |
| Transition                      | IntelligentTieringConfiguration            | Transition configuration for INTELLIGENT TIERING                 | Container | Yes       |
| Days                            | IntelligentTieringConfiguration</br>.Transition | The number of consecutive days used to determine whether to move objects from STANDARD to STANDARD_IA. Valid values: `30`, `60`, `90`. Default value: `30`. | Int       | Yes       |
|  RequestFrequent                | IntelligentTieringConfiguration</br>.Transition | The limit of access times used to determine whether to move objects from STANDARD to STANDARD_IA. The default value is `1`. It can achieve object transition when used with `Days`. For example, if this parameter is set to `1` and `Days` is set to `30`, objects accessed less than once in 30 consecutive days will be moved from STANDARD to STANDARD_IA.  |  Int  |  Yes  |

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body of this API is empty.

#### Error codes

This API returns common error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

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
    <RequestFrequent>1</RequestFrequent>
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
