## Overview

This API is used to upload an object to a bucket in the form of parts. If an object is uploaded using the `APPEND Object` API, it will be automatically determined as "appendable", while objects uploaded using other APIs are determined as "normal" (if you upload an object that already exists and the object type is appendable, the object type will be overwritten to "normal"). You can call the [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) or [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) API to obtain the `x-cos-object-type` header to determine the object type. `APPEND Object` is available only for appendable objects.

The default maximum size of each object part is 5 GB (no minimum size limit), and the size of the object uploaded using this API can be up to 5 GB. If the value of `position` is inconsistent with the object length, COS will return the 409 status code. If the object to append is of the "normal" type, COS will return "409 ObjectNotAppendable".

>! 
>- Appendable objects do not support replication, versioning, or lifecycle management.
>- The `APPEND` API does not verify the storage class carried in the request. The storage class will subject to that of the existing object.
>- The `APPEND Object` API is not available for the intelligent tiering feature.
>- Buckets with multi-AZ enabled do not support the `APPEND Object` API.

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

>? 
> - Host: <BucketName-APPID>.cos.<Region>.myqcloud.com, where <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://www.tencentcloud.com/document/product/436/6224)).
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> 

#### Request headers

#### Common request headers

This API uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Non-common request headers

**Required headers**
This API uses the following required header:

| Header | Description | Type | Required |
| -------------- | ------------------------------------------- | ------ | ---- |
| Content-Length | HTTP request length (in bytes) defined in RFC 2616 | String | Yes   |

**Recommended headers**
This API uses the following recommended headers:

| Node Name (Keyword)  | Description                                                         | Type   | Required |
| ------------------- | ------------------------------------------------------------ | ------ | ---- |
| Cache-Control       | Cache policy defined in RFC 2616. It will be returned as the object metadata.          | String | No   |
| Content-Disposition | Filename defined in RFC 2616. It will be returned as the object metadata.          | String | No   |
| Content-Encoding    | Encoding format defined in RFC 2616. It will be returned as the object metadata.          | String | No   |
| Content-MD5 | Base64-encoded MD5 checksum of the request body content defined in RFC 1864. This value is a 24-character string, such as `ZzD3iDJdrMAAb00lgLLeig==`, and is used to verify whether the request body experienced any changes during transfer. | String | No |
| Content-Type        | Content type (MIME) defined in RFC 2616. It will be returned as the object metadata.  | String | No   |
| Expect              | If `Expect: 100-continue` is used, the request content can only be sent after the server’s confirmation. | String | No   |
| Expires             | Expiration time defined in RFC 2616. It will be returned as the object metadata.          | String | No   |
| x-cos-meta- *       | Customizable header. It will be returned as the object metadata of up to 2 KB | String | No   |

**Permission-related headers**
You can use the `x-cos-acl` header of the POST request to set the object access permission, which can be `public-read-write`, `public-read`, or `private` (default). You can also grant read, write, or read/write permission to a user explicitly. The content is described as follows:

>?For more information about ACL requests, see [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737).

| Header | Description | Type | Required |
| ------------------------ | ------------------------------------------------------------ | ------ | ---- |
| x-cos-acl                | Defines the ACL attribute of an object. Valid values: `private`, `public-read-write`, `public-read`.<br>Default: `private` | String | No   |
| x-cos-grant-read         | Grants user the read permission, formatted as `x-cos-grant-read: id=" ",id=" "`.<br><li>Granting permission to a sub-account: `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>Granting permission to the root account: `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"` | String | No   |
| x-cos-grant-write        | Grants user the write permission, formatted as `x-cos-grant-write: id=" ",id=" "`. <br><li>Granting permission to a sub-account: `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>Granting permission to the root account:　`id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"` | String | No   |
| x-cos-grant-full-control | Grants user the read/write permission, formatted as `x-cos-grant-full-control: id=" ",id=" "`.<br><li>Granting permission to a sub-account: `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br> <li>Granting permission to the root account: `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"` | String | No   |

#### Request parameters

The parameter is described as follows:

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------- | ---- |
| position | Starting point for the append operation (in bytes). For the first append, the value of this parameter is 0. For subsequent appends, the value is the `content-length` of the current object. | Int | Yes |

#### Request body

The request body of this request is empty.

## Response

#### Response headers

#### Common response headers

This response uses [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Non-common response headers

The response headers of this request are as follows:

| Node Name (Keyword)         | Description                               | Type   |
| -------------------------- | ---------------------------------- | ------ |
| x-cos-next-append-position | Start point of the next append operation, in bytes | String |
| ETag                       | Unique identifier of the object                | String |


#### Response body

The response body returned is empty.

#### Error codes

- If you perform an append operation on a non-appendable object, the "409 Conflict" error will be returned. The error message is as follows:
The operation is not valid for the current state of the object.
- If the request does not contain the `position` parameter, the "400 Bad Request" error will be returned. The error message is InvalidArgument.
- If the request does not contain the `Content-Length` header, the "411 Length Required" error will be returned. The error message is as follows:
You must provide the Content-Length HTTP header.

For more information about COS error codes or the complete list of error codes, [see Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

#### Request

```sh
POST /coss3/app?append&position=0 HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Tue, 16 Jan 2016 21:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDDNMEycgLRPI2axw9xa2Hhx87wZ3M****&q-sign-time=1484208848;32557104848&q-key-time=1484208848;32557104848&q-header-list=host&q-url-param-list=append;position&q-signature=855fe6b833fadf20570f7f650e2120e17ce8****
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
x-cos-request-id: NTg3NzNhZGZfMmM4OGY3X2I2Zl8x****
```
