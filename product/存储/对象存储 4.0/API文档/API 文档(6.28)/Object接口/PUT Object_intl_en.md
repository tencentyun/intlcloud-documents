## Description

A PUT Object API request is used to upload a local object to the specified bucket. The requester of this API should have write permission of the bucket.

>- If the Content-Length value in the request header is smaller than the length of the data transferred in the actual request body, COS will still successfully create a file, but the object size will only be equal to the size defined in Content-Length, and excessive data will be discarded.
>- If you try to upload an object sharing a name with an existing object in the bucket before enabling the versioning, the old object will be overwritten and 200 OK will be returned upon success.

#### Versioning

If versioning is enabled for the bucket, COS will automatically generate a unique version ID for the object to be uploaded. It returns this ID in the response using the x-cos-version-id response header.
If you suspend versioning for the bucket, COS will always use "null" as the version ID of the object stored in the bucket.

## Request

#### Request Example

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

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

#### Request Parameters

This API has no request parameters.

#### Request Header

In addition to common request headers, this API also supports the following request headers. For more information about the common request header, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

| Name | Description | Type | Required |
| --- | --- | --- | --- |
| Cache-Control | Cache policy defined in RFC 2616, which will be stored as the object's metadata | String | No |
| Content-Disposition | File name defined in RFC 2616, which will be stored as the object's metadata | String | No |
| Content-Encoding | Encoding format defined in RFC 2616, which will be stored as the object's metadata | String | No |
| Expires | Cache expiration time defined in RFC 2616, which will be stored as the object's metadata | String | No |
| x-cos-meta-\* | This includes the suffix and information of the user-defined metadata header, which will be saved as the object metadata of up to 2 KB. <br>**Note:** User-defined metadata header information contains underscores (_), but user-defined metadata header suffixes only supports minus signs (-) | String | No |
| x-cos-storage-class | Object storage class, including STANDARD, STANDARD_IA, and ARCHIVE. Default value: STANDARD. For enumerated values, see [Storage Class](https://intl.cloud.tencent.com/document/product/436/30925) | Enum | No |

**ACL-related headers**

You can set the access permissions of the object by specifying the following request headers when uploading it:

| Name | Description | Type | Required |
| --- | --- | --- | --- |
| x-cos-acl | This defines the access control list (ACL) attribute of the object. For the enumeration values such as default, private, and public-read, see the Preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: default <br>**Note: ** Currently, there can be up to 1,000 entries in one ACL. If you do not need access control for the object, set "default" for this parameter or simply leave it blank, so that the object will inherit the permissions of the bucket | Enum | No |
| x-cos-grant-read | This grants the grantee permission to read the object in the format of id="[OwnerUin]", such as id="100000000001". Multiple grantees can be separated by comma (,), such as `id="100000000001",id="100000000002"` | String | No |
| x-cos-grant-read-acp | This grants the grantee permission to read the ACL of the object in the format of id="[OwnerUin]", such as id="100000000001". Multiple grantees can be separated by comma (,), such as `id="100000000001",id="100000000002"` | String | No |
| x-cos-grant-write-acp | This grants the grantee permission to write to the ACL of the object in the format of id="[OwnerUin]", such as id="100000000001". Multiple grantees can be separated by comma (,), such as `id="100000000001",id="100000000002"` | String | No |
| x-cos-grant-full-control | This grants the grantee all permissions to manipulate the object in the format of id="[OwnerUin]", such as id="100000000001". Multiple grantees can be separated by comma (,), such as `id="100000000001",id="100000000002"` | String | No |

**Server-side Encryption-related Headers**

Server-side encryption can be used when the object is uploaded. For more information, see [Server-side Encryption-specific Headers](https://intl.cloud.tencent.com/document/product/436/7728#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Request Body

The body of this API request is the object (file) content.

## Response

#### Response Header

This API only returns a common response header. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

**Versioning-related Headers**

When the object is uploaded to a bucket where versioning is enabled or suspended, the following response header will be returned:

| Name | Description | Type |
| --- | --- | --- |
| x-cos-version-id | If versioning is enabled, the version ID of the object will be returned. If versioning is suspended, null will always be returned as the version of the uploaded object | String |

**Server-side Encryption-related Headers**

If server-side encryption is used when the object is uploaded, this API will return the server-side encryption-specific header. For more information. see [Server-side Encryption-specific Headers](https://intl.cloud.tencent.com/document/product/436/7729#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Response Body

The response body of this API is empty.

#### Error Codes

There are no special error messages for this API. For all error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

#### Example 1. A Simple Example (with Versioning Not Enabled)

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

#### Example 2. Specifying the Metadata and ACL Using the Request Header

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

#### Example 3. Using Server-side Encryption SSE-COS

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

#### Example 4. Using Server-side Encryption SSE-C

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

#### Example 5. Enabling Versioning

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

#### Example 6. Suspending Versioning

#### Request

```shell
PUT /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 21 Jun 2019 09:24:51 GMT
Content-Type: image/jpeg
Content-Length: 13
Content-MD5: ti4QvKtVqIJAvZxDbP/c+Q==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1561109091;1561116291&q-key-time=1561109091;1561116291&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=&q-signature=4bcab79bc377054f97fe8200d79d73624705****
Connection: close

[Object Content]
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Fri, 21 Jun 2019 09:24:52 GMT
ETag: "b62e10bcab55a88240bd9c436cffdcf9"
Server: tencent-cos
x-cos-request-id: NWQwY2EyNjRfM2NhZjJhMDlfMmFmZl85NWUx****
x-cos-version-id: null
```
