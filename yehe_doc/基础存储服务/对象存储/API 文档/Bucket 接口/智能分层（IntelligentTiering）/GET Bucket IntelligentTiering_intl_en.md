## Feature Description

This API is used to query the INTELLIGENT TIERING configuration of a bucket.

> ?
> - Only the root account and authorized sub-accounts can call this API.
> - The status of INTELLIGENT TIERING can only be enabled or suspended.
> - If you have never enabled INTELLIGENT TIERING for your bucket, the response will be:
   ```shell
	<IntelligentTieringConfiguration/>
   ```
> - If you have enabled INTELLIGENT TIERING for your bucket, the response will be:
>```shell
<IntelligentTieringConfiguration xmlns="cos xmlns/"> 
       <Status>Enabled</Status>
       <Transition>
          <Days>30</Days>
		  <RequestFrequent>1</RequestFrequent>
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
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> 

#### Request parameters

This API has no request parameter.

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

The request body of this request is empty.

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

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

| Node                            | Parent Node                                     | Description                                                         | Type      |
| ------------------------------- | ------------------------------------------ | ------------------------------------------------------------ | --------- |
| IntelligentTieringConfiguration | None                                         | Configuration of INTELLIGENT TIERING                                   | Container |
| Status                          | IntelligentTieringConfiguration            | Whether INTELLIGENT TIERING is enabled. Enumerated values: `Enabled` | Enum      |
| Transition                      | IntelligentTieringConfiguration            | Transition configuration for INTELLIGENT TIERING                 | Container |
| Days                            | IntelligentTieringConfiguration.Transition | The number of consecutive days used to determine whether to move objects from STANDARD to STANDARD_IA. Valid values: `30` (default), `60`, `90` | Int  |
| RequestFrequent               |  IntelligentTieringConfiguration.Transition | The limit of access times used to determine whether to move objects from STANDARD to STANDARD_IA. The default value is `1`. It can achieve object transition when used with `Days`. For example, if this parameter is set to `1` and `Days` is set to `30`, objects accessed less than once in 30 consecutive days will be moved from STANDARD to STANDARD_IA.   |   Int       |


#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

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
    <RequestFrequent>1</RequestFrequent>
  </Transition>
</IntelligentTieringConfiguration>
```
