## Overview

This API is used to upload an object to a bucket in the form of parts. If an object is uploaded using the `Append Object` API, it will be automatically determined as "appendable", while objects uploaded using other APIs are determined as "normal" (if you upload an object that already exists and the object type is appendable, the object type will be overwritten to "normal"). You can call the [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) or [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) API to obtain the `x-cos-object-type` header to determine the object type. `Append Object` is available only for appendable objects.

The default maximum size of each object part is 5 GB (no minimum size limit), and the size of the object uploaded using this API can be up to 5 GB. If the value of `position` is inconsistent with the object length, COS will return the 409 status code. If the object to append is of the "normal" type, COS will return "409 ObjectNotAppendable".

>! 
>- Appendable objects do not support replication, versioning, or lifecycle management.
>- The `Append Object` API does not verify the storage class carried in the request. The storage class will be subject to that of the existing object.
>- The `Append Object` API is not available for INTELLIGENT TIERING.

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
> - In `Host: &lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com`, &lt;BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and &lt;Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).
> 

#### Request headers

#### Common request headers

This API uses common request headers. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Non-common request headers

**Required headers**
This request uses the following required request headers:

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

>?For more information about ACL requests, please see [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737).

| Header | Description | Type | Required |
| ------------------------ | ------------------------------------------------------------ | ------ | ---- |
| x-cos-acl                | Defines the ACL attribute of an object. Valid values: `private`, `public-read-write`, and `public-read`.<br>Default: `private` | String | No   |
| x-cos-grant-read         | Grants user the read permission, formatted as `x-cos-grant-read: id=" ",id=" "`.<br><li>Granting permission to a sub-account: `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>Granting permission to the root account: `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"` | String | No   |
| x-cos-grant-write        | Grants user the write permission, formatted as `x-cos-grant-write: id=" ",id=" "`. <br><li>Granting permission to a sub-account: `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>Granting permission to the root account:　`id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"` | String | No   |
| x-cos-grant-full-control | Grants user the read/write permission, formatted as `x-cos-grant-full-control: id=" ",id=" "`.<br><li>Granting permission to a sub-account: `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br> <li>Granting permission to the root account: `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"` | String | No   |

#### Request parameters

The parameter is described as follows:

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------- | ---- |
| position | Start point of the append operation, in bytes<br>For the first append operation, the value of this parameter is 0. For subsequent append operations, the value equals to the value of `Content-Length` of the current object. | Integer  | Yes |

#### Request body

The request body of this request is empty.

## Response

#### Response headers

#### Common response headers

This response uses common response headers. For more information, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Non-common response headers

The response headers of this request are as follows:

| Node Name (Keyword)         | Description                               | Type   |
| -------------------------- | ---------------------------------- | ------ |
| x-cos-next-append-position | Start point of the next append operation, in bytes | String |
| ETag                       | Unique identifier of the object                | String |


#### Response body

The response body is empty.

#### Error codes

1. If you perform an append operation on a non-appendable object, the "409 Conflict" error will be returned. The error message is as follows:
The operation is not valid for the current state of the object.
2. If the request does not contain the `position` parameter, the "400 Bad Request" error will be returned. The error message is InvalidArgument.
3. If the request does not contain the `Content-Length` header, the "411 Length Required" error will be returned. The error message is as follows:
You must provide the Content-Length HTTP header.

For more information about COS error codes or the complete list of error codes, please see Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Sample

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
