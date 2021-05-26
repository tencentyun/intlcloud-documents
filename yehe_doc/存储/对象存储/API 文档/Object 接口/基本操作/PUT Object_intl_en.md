## Overview

This API is used to upload a local object to a specified bucket. To call this API, you need to have write permission for the bucket.

> ?
>- The `PUT Object` API supports uploading a file of up to 5 GB. If you need to upload a file larger than 5 GB, please use the [Multipart Upload](https://intl.cloud.tencent.com/document/product/436/14112) API.
> - If the `Content-Length` value in the request header is smaller than the length of the data in the actual request body, COS will still successfully create a file, but the object size will be equal to the size defined in `Content-Length`, and the remaining data will be discarded.
> - If you upload an object with the same name as an object that already exists in the bucket and versioning is not enabled, the old object will be overwritten by the new one and "200 OK" will be returned upon successful upload.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                We recommend using Tencent Cloud API Explorer.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=PutObject&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                API Explorer makes it easy for you to make online API calls, verify signatures, generate SDK code, and search for the desired APIs. You can also use it to query the content of each request as well as its response, and obtain the auto-generated SDK calling samples.
            </div>
        </div>
    </div>
</div>


#### Versioning

- If versioning is enabled for the bucket, COS will automatically generate a unique version ID for the object to be uploaded. It returns this ID in the response using the `x-cos-version-id` response header.
- If versioning is suspended for the bucket, COS will always use `null` as the version ID of the object in the bucket and will not return the `x-cos-version-id` response header.

## Request

#### Sample request

```plaintext
PUT /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Type: Content Type
Content-Length: Content Length
Content-MD5: MD5
Authorization: Auth String



[Object Content]
```

> ? Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)

#### Request parameters

This API has no request parameter.

#### Request headers

In addition to common request headers, this API also supports the following request headers. For more information about common request headers, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

| Header | Description | Type | Required |
| ------------------- | ------------------------------------------------------------ | ------- | -------- |
| Cache-Control | Cache directives as defined in RFC 2616. It will be stored as object metadata. | string | No |
| Content-Disposition | Filename as defined in RFC 2616. It will be stored as object metadata. | string | No |
| Content-Encoding | Encoding format as defined in RFC 2616. It will be stored as object metadata. | string | No |
| Content-Type | HTTP request content type (MIME) as defined in RFC 2616. This header describes the content type of the object to be uploaded and will be stored as object metadata.<br>Example: `text/html`, `image/jpeg` | string | Yes |
| Expires | The cache expiration time as defined in RFC 2616. It will be stored as object metadata. | string | No |
| Transfer-Encoding | If you want to upload the object in parts, you need to specify the `Transfer-Encoding: chunked` request header. In this case, the request body will follow the transfer encoding format defined in RFC 2616, and you cannot specify the `Content-Length` request header. | string | No |
| x-cos-meta-\* | Contains user-defined metadata and header suffixes. It will be stored as object metadata. Maximum size: 2 KB. <br>**Note:** User-defined metadata can contain underscores (_), whereas the header suffixes of user-defined metadata can only contain minus signs (−) but not underscores. | string | No |
| x-cos-storage-class | Object storage class. For the enumerated values, such as `STANDARD` (default), `INTELLIGENT_TIERING`, `STANDARD_IA`, `ARCHIVE`, and `DEEP_ARCHIVE`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | enum | No |
| x-cos-traffic-limit | Limits the speed (in bit/s) for the current upload for traffic control. Valid range: 819200-838860800 (i.e., 100 KB/s-100 MB/s). If the speed exceeds the limit, a 400 error will be returned. | integer | No |
| x-cos-tagging | A set of up to 10 object tags (for example, `Key1=Value1&Key2=Value2`). Tag key and tag value in the set must be URL-encoded. | string  | No |



**ACL-related headers**

You can configure an access control list (ACL) for the object by specifying the following request headers during the upload:

| Header | Description | Type | Required |
| ------------------------ | ------------------------------------------------------------ | ------ | -------- |
| x-cos-acl | Defines the ACL attribute of the object. For the enumerated values, such as `default`, `private`, and `public-read`, please see the **Preset ACL** section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: `default`. <br>**Note**: If you do not need to set an ACL for the object, set this parameter to `default` or leave it empty. In this way, the object will inherit the permissions of the bucket it is stored in. | enum | No |
| x-cos-grant-read | Grants a user read permission for an object in the format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use a comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | string | No |
| x-cos-grant-read-acp | Grants a user read permission for the ACL of an object in the format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use a comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | string | No |
| x-cos-grant-write-acp | Grants a user write permission for the ACL of an object in the format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use a comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | string | No |
| x-cos-grant-full-control | Grants a user full permission to operate on an object in the format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use a comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | string | No |

**Headers related to SSE**

Server-side encryption can be used during object upload. For more information, see [Server-side encryption headers](https://intl.cloud.tencent.com/document/product/436/7728#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Request body

The request body of this API is the object (file) content.

## Response

#### Response headers

In addition to common response headers, this API also returns the following response headers. For more information about common response headers, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

**Versioning-related headers**

If the object is uploaded to a versioning-enabled bucket, the following response headers will be returned:

| Header | Description | Type |
| ---------------- | ------------- | ------ |
| x-cos-version-id | Object version ID | string |

**Headers related to SSE**

If server-side encryption is used during object upload, this API will return the headers used specifically for server-side encryption. For more information, see [Server-side encryption headers](https://intl.cloud.tencent.com/document/product/436/7729#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Response body

The response body of this API is empty.

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

#### Example 1. Simple use case (with versioning disabled)

#### Request

``` plaintext
PUT /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 09:35:05 GMT
Content-Type: image/jpeg
Content-Length: 16
Content-MD5: 7o3pGNBWQBRbGPcPTDqmAg==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586511305;1586518505&q-key-time=1586511305;1586518505&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=&q-signature=c4147d4d457869a49b13e8e936c06a12c809****
Connection: close

[Object Content]
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Fri, 10 Apr 2020 09:35:05 GMT
ETag: "ee8de918d05640145b18f70f4c3aa602"
Server: tencent-cos
x-cos-hash-crc64ecma: 16749565679157681890
x-cos-request-id: NWU5MDNkYzlfNjRiODJhMDlfMzFmYzhfMTFm****
```

#### Example 2. Specifying metadata and ACL using request headers

#### Request

```plaintext
PUT /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 09:35:28 GMT
Content-Type: image/jpeg
Cache-Control: max-age=86400
Content-Disposition: attachment; filename=example.jpg
x-cos-meta-example-field: example-value
x-cos-acl: public-read
Content-Length: 16
Content-MD5: 7o3pGNBWQBRbGPcPTDqmAg==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586511328;1586518528&q-key-time=1586511328;1586518528&q-header-list=cache-control;content-disposition;content-length;content-md5;content-type;date;host;x-cos-acl;x-cos-meta-example-field&q-url-param-list=&q-signature=20d0cd79060cec8c560ebd239738626726f4****
Connection: close



[Object Content]
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Fri, 10 Apr 2020 09:35:28 GMT
ETag: "ee8de918d05640145b18f70f4c3aa602"
Server: tencent-cos
x-cos-hash-crc64ecma: 16749565679157681890
x-cos-request-id: NWU5MDNkZTBfZjhjMDBiMDlfNzdmN18xMGFi****
```

#### Example 3. Using server-side encryption SSE-COS

#### Request

```plaintext
PUT /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 09:35:49 GMT
Content-Type: image/jpeg
x-cos-server-side-encryption: AES256
Content-Length: 16
Content-MD5: 7o3pGNBWQBRbGPcPTDqmAg==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586511349;1586518549&q-key-time=1586511349;1586518549&q-header-list=content-length;content-md5;content-type;date;host;x-cos-server-side-encryption&q-url-param-list=&q-signature=35145bc61ae490c4959b58bc6d27b3258bf7****
Connection: close



[Object Content]
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Fri, 10 Apr 2020 09:35:49 GMT
ETag: "ee8de918d05640145b18f70f4c3aa602"
Server: tencent-cos
x-cos-hash-crc64ecma: 16749565679157681890
x-cos-request-id: NWU5MDNkZjVfYzVjNzJhMDlfMjVhNzNfMWMy****
x-cos-server-side-encryption: AES256
```

#### Example 4. Using server-side encryption SSE-KMS

#### Request

```plaintext
PUT /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 09:36:00 GMT
Content-Type: image/jpeg
x-cos-server-side-encryption: cos/kms
x-cos-server-side-encryption-cos-kms-key-id: 48ba38aa-26c5-11ea-855c-52540085****
x-cos-server-side-encryption-context: eyJhdXRob3IiOiJmeXNudGlhbiIsImNvbXBhbnkiOiJUZW5jZW50In0=
Content-Length: 16
Content-MD5: 7o3pGNBWQBRbGPcPTDqmAg==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586511360;1586518560&q-key-time=1586511360;1586518560&q-header-list=content-length;content-md5;content-type;date;host;x-cos-server-side-encryption;x-cos-server-side-encryption-context;x-cos-server-side-encryption-cos-kms-key-id&q-url-param-list=&q-signature=6cb5d6f0137bb1d87f5afe98c5289b0de375****
Connection: close



[Object Content]
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Fri, 10 Apr 2020 09:36:01 GMT
ETag: "840af7c921f4b3230049af8663145bd0"
Server: tencent-cos
x-cos-hash-crc64ecma: 16749565679157681890
x-cos-request-id: NWU5MDNlMDFfOThjMjJhMDlfMjhhMl8xNTlm****
x-cos-server-side-encryption: cos/kms
x-cos-server-side-encryption-cos-kms-key-id: 48ba38aa-26c5-11ea-855c-52540085****
```

#### Example 5. Using server-side encryption SSE-C

#### Request

```plaintext
PUT /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 09:36:12 GMT
Content-Type: image/jpeg
x-cos-server-side-encryption-customer-algorithm: AES256
x-cos-server-side-encryption-customer-key: MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=
x-cos-server-side-encryption-customer-key-MD5: U5L61r7jcwdNvT7frmUG8g==
Content-Length: 16
Content-MD5: 7o3pGNBWQBRbGPcPTDqmAg==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586511372;1586518572&q-key-time=1586511372;1586518572&q-header-list=content-length;content-md5;content-type;date;host;x-cos-server-side-encryption-customer-algorithm;x-cos-server-side-encryption-customer-key;x-cos-server-side-encryption-customer-key-md5&q-url-param-list=&q-signature=4f6f9f0a6700930f70bff31e3a2b2e622711****
Connection: close



[Object Content]

```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Fri, 10 Apr 2020 09:36:13 GMT
ETag: "582d9105f71525f3c161984bc005efb5"
Server: tencent-cos
x-cos-hash-crc64ecma: 16749565679157681890
x-cos-request-id: NWU5MDNlMGNfZTFjODJhMDlfMzVlMDFfZTk1****
x-cos-server-side-encryption-customer-algorithm: AES256
x-cos-server-side-encryption-customer-key-MD5: U5L61r7jcwdNvT7frmUG8g==
```

#### Example 6. Enabling versioning

#### Request

```plaintext
PUT /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 09:36:34 GMT
Content-Type: image/jpeg
Content-Length: 16
Content-MD5: 7o3pGNBWQBRbGPcPTDqmAg==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586511394;1586518594&q-key-time=1586511394;1586518594&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=&q-signature=371f555ec81751e1dbf38927e568af4cc67a****
Connection: close



[Object Content]
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Fri, 10 Apr 2020 09:36:35 GMT
ETag: "ee8de918d05640145b18f70f4c3aa602"
Server: tencent-cos
x-cos-hash-crc64ecma: 16749565679157681890
x-cos-request-id: NWU5MDNlMjNfMThiODJhMDlfNGQ1OF8xMWY4****
x-cos-version-id: MTg0NDUxNTc1NjIzMTQ1MDAwODg
```

#### Example 7. Suspending versioning

#### Request

```plaintext
PUT /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 09:37:07 GMT
Content-Type: image/jpeg
Content-Length: 16
Content-MD5: 7o3pGNBWQBRbGPcPTDqmAg==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586511427;1586518627&q-key-time=1586511427;1586518627&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=&q-signature=0747f6508fca37dfb5c91bbe3fa01f91b326****
Connection: close



[Object Content]
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Fri, 10 Apr 2020 09:37:07 GMT
ETag: "ee8de918d05640145b18f70f4c3aa602"
Server: tencent-cos
x-cos-hash-crc64ecma: 16749565679157681890
x-cos-request-id: NWU5MDNlNDNfZTZjNzJhMDlfMmYwMDlfMTVi****
```

#### Example 8. Using chunked transfer encoding for multipart transfer

The request in this example uses `Transfer-Encoding: chunked` encoding. This use case describes the raw data in the HTTP request. During use, calling methods vary depending on languages and libraries. Please refer to language- and library-related documents.

#### Request

```plaintext
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

```plaintext
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Thu, 08 Aug 2019 09:15:29 GMT
ETag: "aa488bb80185a6be87f4a7b936a80752"
Server: tencent-cos
x-cos-hash-crc64ecma: 7188322482464764960
x-cos-request-id: NWQ0YmU4MzFfNzFiNDBiMDlfMWJhYTlfMTY2Njll****
```
