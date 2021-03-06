## Description
The PUT Bucket versioning API is used to enable or suspend versioning for a bucket.

#### Notes

1. If you have never enabled versioning for the bucket, GET Bucket versioning will not return a versioning state value.
2. Once enabled, versioning can only be suspended but cannot be disabled.
3. Set the versioning state value to Enabled or Suspended to enable or suspend versioning, respectively.
4. To set versioning for a bucket, you need to have the permission to write to the bucket.

## Request
#### Sample Request

```shell
PUT /?versioning HTTP 1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT date
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

#### Request Headers

This API only uses common request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request Body

```shell
<VersioningConfiguration>
  <Status></Status>
</VersioningConfiguration>
```

Please find the details below:

| Node Name (Keyword) | Parent Node | Description | Type |
| --------------------------------------- | --------------------- | --------- | ------- |
| VersioningConfiguration | None | Describes the detailed information on versioning | Container |
| Status | VersioningConfiguration | Indicates whether versioning is enabled; enumerators: Suspended, Enabled | Enum |

## Response

#### Response Headers

This API only uses common response headers. For more information on common request headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response Body
This response body is empty.

#### Error Codes

This API uses standardized error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) .


## Samples
#### Request
```shell
PUT /?versioning HTTP/1.1
Host: examplebucket-1250000000.cos.ap-chengdu.myqcloud.com
Connection: keep-alive
Accept-Encoding: gzip, deflate
Accept: */*
User-Agent: python-requests/2.12.4
Content-Type: application/xml
Authorization: q-sign-algorithm=sha1&q-ak=AKID15IsskiBQKTZbAo6WhgcBqVls9Sm****&q-sign-time=1480932292;1981012292&q-key-time=1480932292;1981012292&q-url-param-list=versioning&q-header-list=host&q-signature=47ec2b80c73788ecd394d3b9ad90e120a32f****
Content-Length: 83

<VersioningConfiguration>
    <Status>Enabled</Status>
</VersioningConfiguration>
```

#### Response
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Wed, 23 Aug 2017 08:14:53 GMT
Server: tencent-cos
x-cos-request-id: NTk5ZDM5N2RfMjNiMjM1MGFfMmRiX2Y0****
```
