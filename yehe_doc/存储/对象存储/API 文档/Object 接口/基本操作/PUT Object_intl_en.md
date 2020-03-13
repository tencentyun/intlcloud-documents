## Feature

This API is used to upload a local object to a specified bucket. To make this request, you need to have the permission to write to the bucket.

>
>- The PUT Object API supports uploading up to 5GB files. If you need to upload files greater than 5GB, please use the [Multipart Upload](https://intl.cloud.tencent.com/document/product/436/14112) API.
>- If the `Content-Length` value in the request header is smaller than the length of the data in the actual request body, COS will still successfully create a file, but the object size will equal the size defined in `Content-Length`, and the remaining data will be discarded.
>- If you upload an object whose name already exists in the bucket and versioning is not enabled, the old object will be overwritten by the new one and `200 OK` will be returned upon success.

#### Versioning

- If versioning is enabled for the bucket, COS will automatically generate a unique version ID for the object to be uploaded and return this ID in the response using the `x-cos-version-id` response header.
- If versioning is suspended for the bucket, COS will always use `null` as the version ID of the object in the bucket and will not return the `x-cos-version-id` response header.

## Request

#### Sample Request

```shell
PUT /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Type: Content Type
Content-Length: Content Length
Content-MD5: MD5
Authorization: Auth String

[Object Content]
```

> Authorization: Auth String (see [Request Signature](https://cloud.tencent.com/document/product/436/7778) for details).

#### Request Parameters

This API does not use any request parameter.

#### Request Header

In addition to common request headers, this API also supports the following request headers. For more information on common request headers, see [Common Request Headers](https://cloud.tencent.com/document/product/436/7728).

| Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Type | Required |
| --- | --- | --- | --- |
| Cache-Control | Cache directives as defined in RFC 2616, which will be stored in the object metadata | String | No |
| Content-Disposition | File name as defined in RFC 2616, which will be stored in the object metadata | String | No |
| Content-Encoding | Encoding format as defined in RFC 2616, which will be stored in the object metadata | String | No |
| Expires | Cache expiration time as defined in RFC 2616, which will be stored in the object metadata | String | No |
| Transfer-Encoding | If you want to upload the object in parts, you need to specify the `Transfer-Encoding: chunked` request header. In this case, the request body will follow the transfer encoding format as defined in RFC 2616 and you cannot specify the `Content-Length` request header | String | No |
| x-cos-meta-\* | Header suffix and information of user-defined metadata, which will be stored in the object metadata. Maximum size: 2 KB. <br>**Note:** User-defined metadata information can contain underscores (_), whereas header suffixes of user-defined metadata can only contain minus signs (-), not underscores | String | No |
| x-cos-storage-class | Object storage class, such as `STANDARD_IA` and `ARCHIVE`. Default value: `STANDARD`. For enumerated values, see [Storage Class](https://intl.cloud.tencent.com/document/product/436/30925) | Enum | No |

**ACL-related Headers**

You can configure access permissions for the object by specifying the following request headers during object upload:

| Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Type | Required |
| --- | --- | --- | --- |
| x-cos-acl | Defines the access control list (ACL) attribute of the object. For enumerated values such as `default`, `private`, and `public-read`, see preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: default <br>**Note:** Currently, one ACL supports up to 1,000 entries. If you do not need access control for the object, configure this parameter as `default` or leave it blank, and bucket permissions will be inherited by default | Enum | No |
| x-cos-grant-read | Allows grantee to read the object; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | String | No |
| x-cos-grant-read-acp | Allows grantee to read the ACL of the object; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | String | No |
| x-cos-grant-write-acp | Allows grantee to write to the ACL of the object; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | String | No |
| x-cos-grant-full-control | Grants a user full permission to operate on the object; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | String | No |

**Headers related to server-side encryption (SSE)**

Server-side encryption can be used during object upload. For more information, see [Server-side encryption headers](https://cloud.tencent.com/document/product/436/7728#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Request Body

The request body of this API request is the object (file) content.

## Response

#### Response Headers

In addition to common response headers, this API also returns the following response headers. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

**Versioning-related Headers**

When the object is uploaded to a bucket where versioning is enabled, the following response headers will be returned:

| Name | Description | Type |
| --- | --- | --- |
| x-cos-version-id | Object version ID | string |

**Headers related to server-side encryption (SSE)**

If server-side encryption is used during object upload, this API will return headers used specifically for server-side encryption. For more information. see [Server-side encryption headers](https://cloud.tencent.com/document/product/436/7729#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Response Body

The response body of this API is empty.

#### Error Codes

There are no special error messages for this API. For all error messages, see [Error Codes](https://cloud.tencent.com/document/product/436/7730).

## Examples

#### Example 1. Simple example (versioning not enabled)

#### Request

```shell
PUT /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 21 Jun 2019 09:24:28 GMT
Content-Type: image/jpeg
Content-Length: 13
Content-MD5: ti4QvKtVqIJAvZxDbP/c+Q==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1561109068;1561116268&q-key-time=1561109068;1561116268&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=&q-signature=998bfc8836fc205d09e455c14e3d7e623bd2****
Connection: close

[Object Content]
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Fri, 21 Jun 2019 09:24:28 GMT
ETag: "b62e10bcab55a88240bd9c436cffdcf9"
Server: tencent-cos
x-cos-request-id: NWQwY2EyNGNfYThjMDBiMDlfMTA0ZmVfYTJm****
```

#### Example 2. Specifying metadata and ACL using request headers

#### Request

```shell
PUT /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 21 Jun 2019 09:24:31 GMT
Content-Type: image/jpeg
Cache-Control: max-age=86400
Content-Disposition: attachment; filename=example.jpg
x-cos-meta-example-field: example-value
x-cos-acl: public-read
Content-Length: 13
Content-MD5: ti4QvKtVqIJAvZxDbP/c+Q==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1561109071;1561116271&q-key-time=1561109071;1561116271&q-header-list=cache-control;content-disposition;content-length;content-md5;content-type;date;host;x-cos-acl;x-cos-meta-example-field&q-url-param-list=&q-signature=da483c6b1c2506142a128aba8e6d35781dd1****
Connection: close

[Object Content]
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Fri, 21 Jun 2019 09:24:32 GMT
ETag: "b62e10bcab55a88240bd9c436cffdcf9"
Server: tencent-cos
x-cos-request-id: NWQwY2EyNGZfN2ViMTJhMDlfYmYxN185MjA2****
```

#### Example 3. Using server-side encryption SSE-COS

#### Request

```shell
PUT /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 21 Jun 2019 09:24:35 GMT
Content-Type: image/jpeg
x-cos-server-side-encryption: AES256
Content-Length: 13
Content-MD5: ti4QvKtVqIJAvZxDbP/c+Q==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1561109075;1561116275&q-key-time=1561109075;1561116275&q-header-list=content-length;content-md5;content-type;date;host;x-cos-server-side-encryption&q-url-param-list=&q-signature=3e21f7fba71e04d5c7f3aee7ff39753b240a****
Connection: close

[Object Content]
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Fri, 21 Jun 2019 09:24:35 GMT
ETag: "b62e10bcab55a88240bd9c436cffdcf9"
Server: tencent-cos
x-cos-request-id: NWQwY2EyNTNfN2JiMTJhMDlfNDM2ZF85OTA1****
x-cos-server-side-encryption: AES256
```

#### Example 4. Using server-side encryption SSE-KMS

#### Request

```shell
PUT /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 24 Jul 2019 02:51:28 GMT
Content-Type: image/jpeg
x-cos-server-side-encryption: cos/kms
x-cos-server-side-encryption-cos-kms-key-id: 48ba38aa-26c5-11ea-855c-52540085****
x-cos-server-side-encryption-context: eyJhdXRob3IiOiJmeXNudGlhbiIsImNvbXBhbnkiOiJUZW5jZW50In0=
Content-Length: 13
Content-MD5: ti4QvKtVqIJAvZxDbP/c+Q==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1561109078;1561116278&q-key-time=1561109078;1561116278&q-header-list=content-length;content-md5;content-type;date;host;x-cos-server-side-encryption-customer-algorithm;x-cos-server-side-encryption-customer-key;x-cos-server-side-encryption-customer-key-md5&q-url-param-list=&q-signature=d04a5d70af5f08c7db4f89a91628a7eacf90****
Connection: close

[Object Content]
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Wed, 24 Jul 2019 02:51:28 GMT
ETag: "fa8a7921998a9b9ed489d7ad39d35c91"
Server: tencent-cos
x-cos-request-id: NWUwMzI1NWZfN2RjODJhMDlfMzUyMDhfMWZm****
x-cos-server-side-encryption: cos/kms
x-cos-server-side-encryption-cos-kms-key-id: 48ba38aa-26c5-11ea-855c-52540085****
```

#### Example 4. Using server-side encryption SSE-C

#### Request

```shell
PUT /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 21 Jun 2019 09:24:38 GMT
Content-Type: image/jpeg
x-cos-server-side-encryption-customer-algorithm: AES256
x-cos-server-side-encryption-customer-key: MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=
x-cos-server-side-encryption-customer-key-MD5: U5L61r7jcwdNvT7frmUG8g==
Content-Length: 13
Content-MD5: ti4QvKtVqIJAvZxDbP/c+Q==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1561109078;1561116278&q-key-time=1561109078;1561116278&q-header-list=content-length;content-md5;content-type;date;host;x-cos-server-side-encryption-customer-algorithm;x-cos-server-side-encryption-customer-key;x-cos-server-side-encryption-customer-key-md5&q-url-param-list=&q-signature=d04a5d70af5f08c7db4f89a91628a7eacf90****
Connection: close

[Object Content]
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Fri, 21 Jun 2019 09:24:38 GMT
ETag: "492b458ec33eaf0a824e7dd1bdd403b3"
Server: tencent-cos
x-cos-request-id: NWQwY2EyNTZfZjBhODBiMDlfMTJiOTJfOWY0****
x-cos-server-side-encryption-customer-algorithm: AES256
x-cos-server-side-encryption-customer-key-MD5: U5L61r7jcwdNvT7frmUG8g==
```

#### Example 6: Enabling Versioning

#### Request

```shell
PUT /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 21 Jun 2019 09:24:45 GMT
Content-Type: image/jpeg
Content-Length: 13
Content-MD5: ti4QvKtVqIJAvZxDbP/c+Q==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1561109085;1561116285&q-key-time=1561109085;1561116285&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=&q-signature=20c8b3f8f887cab343124b2330e280486e1f****
Connection: close

[Object Content]
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Fri, 21 Jun 2019 09:24:45 GMT
ETag: "b62e10bcab55a88240bd9c436cffdcf9"
Server: tencent-cos
x-cos-request-id: NWQwY2EyNWRfYThjMDBiMDlfMTA1MDlfYTQ1****
x-cos-version-id: MTg0NDUxODI5NjQ2MjM5OTMyNzM
```

#### Example 7：Suspending Versioning

#### Request

```shell
PUT /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 24 Jul 2019 02:51:28 GMT
Content-Type: image/jpeg
Content-Length: 13
Content-MD5: ti4QvKtVqIJAvZxDbP/c+Q==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1563936688;1563943888&q-key-time=1563936688;1563943888&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=&q-signature=aab4bfeb62a7a86725da58d4ad06deb5cba1****
Connection: close

[Object Content]
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Wed, 24 Jul 2019 02:51:28 GMT
ETag: "b62e10bcab55a88240bd9c436cffdcf9"
Server: tencent-cos
x-cos-request-id: NWQzN2M3YjBfN2ViMTJhMDlfYTkxMl9iY2Fj****
```

#### Example 7. Using chunked transfer encoding for multipart transfer

The request in this example uses Transfer-Encoding: chunked encoding. This use case describes the raw data in the HTTP request. During use, calling methods vary depending on languages and libraries. Please refer to language- and library-related documents.

#### Request

```shell
PUT /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 08 Aug 2019 09:15:29 GMT
Content-Type: text/plain
Transfer-Encoding: chunked
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1565255729;1565262929&q-key-time=1565255729;1565262929&q-header-list=content-type;date;host;transfer-encoding&q-url-param-list=&q-signature=0b05b6bda75afbc159caa0da4e4051ec6939****
Connection: close

11
[Chunked Content]
b
[2nd chunk]
b
[3rd chunk]
b
[4th chunk]
0
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Thu, 08 Aug 2019 09:15:29 GMT
ETag: "aa488bb80185a6be87f4a7b936a80752"
Server: tencent-cos
x-cos-request-id: NWQ0YmU4MzFfNzFiNDBiMDlfMWJhYTlfMTY2Njll****
```
