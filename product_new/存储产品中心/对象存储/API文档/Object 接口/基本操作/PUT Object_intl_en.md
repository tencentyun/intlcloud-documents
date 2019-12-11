## Description

This API is used to upload a local object to a specified bucket. To make this request, you need to have the permission to write to the bucket.

> ?
>- If the `Content-Length` value in the request header is smaller than the length of the data in the actual request body, COS will still successfully create a file, but the object size will equal the size defined in `Content-Length`, and the remaining data will be discarded.
>- If there is an object in the bucket with the same name as the object to be uploaded, and versioning is not enabled, the old object will be overwritten by the new one and `200 OK` will be returned upon success.

#### Versioning

- If versioning is enabled for the bucket, COS will automatically generate a unique version ID for the object to be uploaded and return this ID in the response using the `x-cos-version-id` response header.
- If versioning is suspended for the bucket, COS will always use `null` as the version ID of the objects in the bucket and will not return the `x-cos-version-id` response header.

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

>? Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

#### Request Parameters

This API does not use any request parameter.

#### Request Headers

In addition to common request headers, this API also supports the following request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

| Name | Description | Type | Required |
| ------------------- | ------------------------------------------------------------ | ------ | -------- |
| Cache-Control | Cache directives as defined in RFC 2616, which will be stored in the object metadata | String | No |
| Content-Disposition | Filename as defined in RFC 2616, which will be stored in the object metadata | String | No |
| Content-Encoding | Encoding format as defined in RFC 2616, which will be stored in the object metadata | String | No |
| Expires | Cache expiration time as defined in RFC 2616, which will be stored in the object metadata | String | No |
| Transfer-Encoding   | If you want to upload the object in parts, you need to specify the `Transfer-Encoding: chunked` request header. In such a case, the request body must follow the transfer encoding format as defined in RFC 2616 and you cannot specify the `Content-Length` request header | string | No |
| x-cos-meta-\* | Header suffix and information of the user-defined metadata, which will be stored in the object metadata; maximum size: 2 KB. <br>**Note:** User-defined metadata information can contain underscores (_), whereas the header suffixes of user-defined metadata can only contain minus signs (-), not underscores | String | No |
| x-cos-storage-class | Object storage class, such as `STANDARD_IA` and `ARCHIVE`. Default value: `STANDARD`. For enumerated values, see [Storage Class](https://intl.cloud.tencent.com/document/product/436/30925) | Enum | No |

**ACL-related headers**

You can configure access permissions for the object by specifying the following request headers when uploading it:

| Name | Description | Type | Required |
| ------------------------ | ------------------------------------------------------------ | ------ | -------- |
| x-cos-acl | Defines the access control list (ACL) attribute of the object. For the enumerated values such as `default`, `private`, and `public-read`, see the Preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: default <br>**Note:** Currently, there can be up to 1,000 entries in one ACL. If you do not need access control for the object, set `default` for this parameter or simply leave it blank, and the object will inherit the permissions of the bucket | Enum | No |
| x-cos-grant-read | Allows grantee to read the object; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | String | No |
| x-cos-grant-read-acp | Allows grantee to read the ACL of the object; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | String | No |
| x-cos-grant-write-acp | Allows grantee to write to the ACL of the object; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | String | No |
| x-cos-grant-full-control | Grants a user full permission to perform operations on the object; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | String | No |

**Server-side encryption-related headers**

You can use server-side encryption when uploading an object. For more information, see [Server-side Encryption Headers](https://intl.cloud.tencent.com/document/product/436/7728#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Request Body

The request body of this API request is the object (file) content.

## Response

#### Response Headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

**Versioning-related headers**

When the object is uploaded to a bucket where versioning is enabled, the following response headers will be returned:

| Name | Description | Type |
| ---------------- | ------------- | ------ |
| x-cos-version-id | Object version ID | string |

**Server-side encryption-related headers**

If server-side encryption is used when the object is uploaded, this API will return the server-side encryption headers. For more information, see [Server-side Encryption Headers](https://intl.cloud.tencent.com/document/product/436/7729#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Response Body

The response body of this API is empty.

#### Error Codes

There is no special error message for this API. For all error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

#### Example 1. Basic example (versioning not enabled)

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

#### Example 5. With versioning enabled

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

#### Example 6. With versioning suspended

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

#### Example 7. Using the chunked transfer encoding for multipart transfer

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
