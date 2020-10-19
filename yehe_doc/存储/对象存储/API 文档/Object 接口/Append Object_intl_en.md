## Overview

This API is used to append data in the form of parts to an object uploaded in a specific bucket. COS automatically determines new objects uploaded using the Append Object API as appendable objects, and those uploaded using other APIs as normal objects (existing objects will be overwritten as such). To see if an object is appendable or normal, you can use the [GET Object](https ://intl.cloud.tencent.com/document/product/436/7753) or [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) API to get the `x-cos-object-type` response header. This API only allows appending data to appendable objects.
In this API, the size of an object part uploaded ranges from 1 B to 5 GB while the maximum size of an object is 5 GB. If `position` has a value different from the object length, COS will return a 409 error. If data is appended to a normal object, COS will return 409 ObjectNotAppendable.

>!Appendable objects cannot be copied, nor can they be involved in versioning, lifecycle management or cross-region replication.

## Request

#### Sample request

```sh
POST /ObjectName?append&position=*position* HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Content-Length: size
Content-Type: ContentType
Date: GMT Date
Authorization: Auth String
```

>?Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

#### Request headers

#### Common headers

This API uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special headers

**Required headers**
This request uses the following required request headers:

| Name | Description | Type | Required |
| -------------- | ------------------------------------------- | ------ | ---- |
| Content-Length | HTTP request length (measured in bytes) as defined in RFC 2616 | String | Yes |

**Recommended headers**
This request uses the following recommended request headers:

| Node Name (Keyword) | Description | Type | Required |
| ------------------- | ------------------------------------------------------------ | ------ | ---- |
| Cache-Control | Cache policy defined in RFC 2616, which will be returned as part of object metadata | String | No |
| Content-Disposition | File name defined in RFC 2616, which will be returned as part of object metadata | String | No |
| Content-Encoding | Encoding format defined in RFC 2616, which will be returned as part of object metadata | String | No |
| Content-MD5 | **Base64-encoded** 128-bit MD5 checksum defined in RFC 1864. This header is used to verify whether the file content has changed | String | No |
| Content-Type | Content type (MIME) defined in RFC 2616, which will be returned as part of object metadata | String | No |
| Expect | If `Expect: 100-continue` is used, the request content will be sent only after confirmation from the server is received | String | No |
| Expires | Expiration time as defined in RFC 2616, which will be returned as part of object metadata | String | No |
| x-cos-meta- * | Headers that can be customized, which will be returned as part of object metadata of up to 2 KB | String | No |

**Permission-related headers**
To modify object access permissions through this API, you can use the `x-cos-acl` header. These permissions include public-read-write, public-read and private (default). You can also explicitly grant read, write, or read/write permissions to individual users. The header nodes are detailed as follows:

>?For more information on ACLs, please see [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737).

| Node                             | Description                                       | Type        | Required             |
| ------------------------ | ------------------------------------------------------------ | ------ | ---- |
| x-cos-acl | Defines the ACL attribute of an object. Valid values: private, public-read-write, and public-read<br>Default: private |String | No  |
| x-cos-grant-read         | Grants read permission in the format of `x-cos-grant-read: id=" "`<br><li>When granting the permission to a sub-account, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>When granting the permission to a root account, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"` | String | No   |
| x-cos-grant-write        | Grants write permission in the format of `x-cos-grant-write: id=" "`<br><li>When granting the permission to a sub-account, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>When granting the permission to a root account, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"` | String | No   |
| x-cos-grant-full-control | Grants read/write permission in the format of `x-cos-grant-full-control: id=" "`<br><li>When granting the permission to a sub-account, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>When granting the permission to a root account, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"` | String | No   |

#### Request parameters

The parameters are described in details below:

| Parameter Name                     | Description                                       | Type     | Required   |
| -------- | ------------------------------------------------------------ | ------- | ---- |
| position | Start point of the append operation in bytes<br>The value is `0` for initial append operation, and equals to the content-length of the current object for subsequent ones | Integer  | Yes |

#### Request body

This request has no request body.

## Response

#### Response headers

#### Common response headers

This response uses common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Special response headers

The response headers specific to this request are as follows:

| Node Name (Keyword) | Description | Type |
| -------------------------- | ---------------------------------- | ------ |
| x-cos-next-append-position | Start point of the next append operation in bytes | String |
| ETag                       | Uniquely identifies the object                     | String |


#### Response body

The response body of this response is empty.

#### Error codes

1. To APPEND data to a non-appendable file will return 409 Conflict with an error message:
The operation is not valid for the current state of the object.
2. If your request does not include the `position` parameter, 400 Bad Request will be returned with an error message: InvalidArgument.
3. If the Content-Length header is missing in your request, 411 Length Required will be returned with an error message:
You must provide the Content-Length HTTP header.

For more COS error codes or a complete list of errors, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

#### Request

```sh
POST /coss3/app?append&position=0 HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Tue, 16 Jan 2016 21:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDDNMEycgLRPI2axw9xa2Hhx87wZ3M****&q-sign-time=1484208848;32557104848&q-key-time=1484208848;32557104848&q-header-list=host&q-url-param-list=append;position&q-signature=855fe6b833fadf20570f7f650e2120e17ce8a2fe
Content-Length: 4096

[Object]
```

#### Response

```sh
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Tue, 16 Jan 2016 21:32:00 GMT
ETag: 1ce5b469b7d6600ecc2fd112e570917b
Server: tencent-cos
x-cos-content-sha1: 1ceaf73df40e531df3bfb26b4fb7cd95fb7bff1d
x-cos-next-append-position: 4096
x-cos-request-id: NTg3NzNhZGZfMmM4OGY3X2I2Zl8xMTBm
```