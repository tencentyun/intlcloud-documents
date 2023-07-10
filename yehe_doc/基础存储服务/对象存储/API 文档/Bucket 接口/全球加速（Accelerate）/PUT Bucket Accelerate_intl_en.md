## Overview

This API is used to enable or suspend global acceleration for a bucket.

**Notes**

1. If you have never enabled global acceleration for the bucket, the global acceleration status will not be returned even if you call this API.
2. Once enabled, global acceleration can only be suspended but cannot be disabled.
3. Valid values of global acceleration `Status` are `Enabled` and `Suspended`.
4. If a sub-account needs to set global acceleration for a bucket, it needs to have permission to write the configuration.

## Request

#### Sample request

```shell
PUT /?accelerate HTTP 1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT date
Authorization: Auth String
```

>? 
> - In `Host: <BucketName-APPID>.cos.<Region>.myqcloud.com`, <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).
> 

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

```shell
<AccelerateConfiguration xmlns="cos xmlns/"> 
  <Status>Enabled</Status> 
</AccelerateConfiguration>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| ----------------------- | ----------------------- | ---------------------------------------------------- | --------- |
| AccelerateConfiguration | None | Information about global acceleration | Container |
| Status | AccelerateConfiguration | Whether to enable global acceleration. Enumerated values: `Suspended`, `Enabled` | Enum |


## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729). 

#### Response body

The response body is empty.

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).


## Example

#### Request

```shell
PUT /?accelerate HTTP/1.1
Host: examplebucket-1250000000.cos.ap-chengdu.myqcloud.com
Connection: keep-alive
Authorization: authorization string
Content-Type: text/plain
Content-Length: 83

<AccelerateConfiguration>
    <Status>Enabled</Status>
</AccelerateConfiguration>
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Wed, 23 Aug 2019 08:14:53 GMT
Server: tencent-cos
x-cos-request-id: NTk5ZDM5N2RfMjNiMjM1MGFfMmRiX2Y0****
```
