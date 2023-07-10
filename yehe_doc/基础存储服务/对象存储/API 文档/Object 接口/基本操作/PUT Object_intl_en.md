## Feature Description

This API (`PUT Object`) is used to upload a local object to the specified bucket. To call this API, you need to have the write permission of the bucket.

> ?
>- The `PUT Object` API supports uploading a file of up to 5 GB in size. If you need to upload a larger file, use the [Multipart Upload](https://intl.cloud.tencent.com/document/product/436/14112) API.
> - If the `Content-Length` value in the request header is smaller than the length of the data in the actual request body, COS will still successfully create a file, but the object size will be equal to the size defined in `Content-Length`, and the excessive data will be discarded.
> - If you upload an object with the same name as an object that already exists in the bucket and versioning is not enabled, the old object will be overwritten by the new one, and `200 OK` will be returned upon successful upload.
> - COS comes with no folders or directories. If you need to upload objects to the specified folder or path, you can use `/` to implement this; for example, to upload `picture.png` to the `doc` folder, set the object key to `doc/picture.png`; to create the `doc` folder, set the object key to `doc/`. For more information, see [Object Overview > Folder and directory](https://intl.cloud.tencent.com/document/product/436/13324).
> 

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=PutObject&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                Tencent Cloud API Explorer provides various capabilities such as online call, signature verification, SDK code generation, and quick API search. You can also use it to query the request and response of each API call as well as generate sample code for calls.
            </div>
        </div>
    </div>
</div>


#### Versioning

- For a versioning-enabled bucket, COS will automatically generate a unique version ID for the object, and the ID will be returned in the `x-cos-version-id` response header.
- For a versioning-suspended bucket, COS will always use `null` as the version ID of the object and will not return the `x-cos-version-id` response header.

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

>? 
> - Host: &lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com, where &lt;BucketName-APPID> is the bucket name followed by the `APPID`, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and &lt;Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> 

#### Request parameters

This API has no request parameters.

#### Request headers

In addition to [common request headers](https://intl.cloud.tencent.com/document/product/436/7728), this API also supports the following request headers.

| Field |  Description | Type | Required |
| ------------------- | ------------------------------------------------------------ | ------- | -------- |
| Cache-Control       | The cache directive as defined in RFC 2616, which is saved as part of the object metadata.              | string  | No       |
| Content-Disposition | The filename as defined in RFC 2616, which is saved as part of the object metadata.              | string  | No       |
| Content-Encoding    | The encoding format as defined in RFC 2616, which is saved as part of the object metadata.              | string  | No       |
| Content-Type        | The HTTP request content type (MIME) as defined in RFC 2616, which describes the content type of the object to be uploaded and is saved as part of the object metadata; for example, `text/html` and `image/jpeg`. | string | Yes       |
| Expires             | The cache expiration time as defined in RFC 2616, which is saved as part of the object metadata.              | string  | No       |
| Transfer-Encoding   | If you want to upload the object in parts, you need to specify the `Transfer-Encoding: chunked` request header. In this case, the request body will follow the transfer encoding format defined in RFC 2616, and you cannot specify the `Content-Length` request header. | string | No       |
| x-cos-meta-\*       | User-defined metadata and header suffixes, which are saved as part of the object metadata. Maximum size: 2 KB. <br>**Note**: User-defined metadata can contain underscores (_), but header suffixes can contain only minus signs (-) but not underscores (_). | string | No      |
| x-cos-storage-class | Storage class of the object. Enumerated values: `INTELLIGENT_TIERING`, `STANDARD`, `STANDARD_IA`, `ARCHIVE`, `DEEP_ARCHIVE`. Default value: `STANDARD`. For more information, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | enum | No |
| x-cos-traffic-limit | Limits the speed (in bit/s) for the current upload for traffic control. Value range: 819200−838860800 (i.e., 100 KB/s−100 MB/s). If the speed exceeds the limit, a 400 error will be returned. | integer | No      |
| x-cos-tagging | A set of up to ten object tags (for example, `Key1=Value1&Key2=Value2`). Tag keys and values in the set must be URL-encoded. | string  | No |



**ACL headers**

You can configure an access control list (ACL) for the object by specifying the following request headers during upload:

| Name | Description | Type | Required |
| ------------------------ | ------------------------------------------------------------ | ------ | -------- |
| x-cos-acl                | ACL attribute of the object. For enumerated values, such as `default`, `private`, and `public-read`, see the **Preset ACL** section in [ACL](https://intl.cloud.tencent.com/document/product/436/30583). Default value: `default`.<br>**Note:** If you don't need access control for the object, set this parameter to `default` or leave it empty, in which case the object will inherit the permissions of its bucket. | enum | No |
| x-cos-grant-read         | Grants a user read access to an object in the format of `id="[OwnerUin]"`, such as `id="100000000001"`. You can separate multiple users by comma, such as `id="100000000001",id="100000000002"`. | string | No       |
| x-cos-grant-read-acp     | Grants a user read access to an object ACL in the format of `id="[OwnerUin]"`, such as `id="100000000001"`. You can separate multiple users by comma, such as `id="100000000001",id="100000000002"`. | string | No       |
| x-cos-grant-write-acp    | Grants a user write access to an object ACL in the format of `id="[OwnerUin]"`, such as `id="100000000001"`. You can separate multiple users by comma, such as `id="100000000001",id="100000000002"`. | string | No       |
| x-cos-grant-full-control | Grants a user full access to an object ACL in the format of `id="[OwnerUin]"`, such as `id="100000000001"`. You can separate multiple users by comma, such as `id="100000000001",id="100000000002"`. | string | No       |

**Server-side encryption headers**

Server-side encryption can be used during object upload. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7728#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Request body

The request body of this API is the object (file) content.

## Response

#### Response headers

In addition to [common response headers](https://intl.cloud.tencent.com/document/product/436/7729), this API also returns the following response headers.

**Versioning headers**

If the object is uploaded to a versioning-enabled bucket, the following response headers will be returned:

| Name | Description | Type |
| ---------------- | ------------- | ------ |
| x-cos-version-id | Version ID of the object | string |

**Server-side encryption headers**

If server-side encryption is used during object upload, this API will return headers used specifically for server-side encryption. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Response body

The response body of this API is empty.

#### Error codes

This API returns common error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

#### Sample 1: Simple use case (with versioning disabled)

#### Request

<dx-codeblock>
:::  plaintext
PUT /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 09:35:05 GMT
Content-Type: image/jpeg
Content-Length: 16
Content-MD5: 7o3pGNBWQBRbGPcPTDqmAg==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586511305;1586518505&q-key-time=1586511305;1586518505&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=&q-signature=c4147d4d457869a49b13e8e936c06a12c809****
Connection: close

[Object Content]
:::
</dx-codeblock>

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

#### Sample 2: Specifying metadata and ACL by using request headers

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

#### Sample 3: Using SSE-COS for server-side encryption

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

#### Sample 4: Using SSE-KMS for server-side encryption

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

#### Sample 5: Using SSE-C for server-side encryption

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

#### Sample 6: Uploading with versioning enabled

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

#### Sample 7: Uploading with versioning suspended

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

#### Sample 8: Using chunked transfer encoding for multipart transfer

The request in this sample uses the `Transfer-Encoding: chunked` request header. This sample describes the raw data in the HTTP request. During actual use, the calling method varies by language and library. You should refer to their specific documentation.

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
