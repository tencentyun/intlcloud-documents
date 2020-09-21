## Feature

This API is used to initialize a multipart upload. A successful request to this API will return an UploadId that is used in the subsequent `Upload Part` requests.

## Request

#### Request samples

```plaintext
POST /<ObjectKey>uploads HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Type: Content Type
Content-Length: 0
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information)

#### Request parameters

This API does not use any request parameter.

#### Request headers

In addition to common request headers, this API also supports the following request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

| Name | Description | Type | Required |
| ------------------- | ------------------------------------------------------------ | ------ | -------- |
| Cache-Control | Cache directives as defined in RFC 2616, which are stored as part of object metadata | string | No |
| Content-Disposition | File name as defined in RFC 2616, which is stored as part of object metadata | string | No |
| Content-Encoding | Encoding format as defined in RFC 2616, which is stored as part of object metadata | string | No |
| Content-Type                                                 | HTTP request content type (MIME) as defined in RFC 2616 of the object to upload, and stored as part of object metadata<br>Example: `text/html` or `image/jpeg` | string | Yes       |
| Expires | The cache expiration time as defined in RFC 2616, which is stored as part of object metadata | string | No |
| x-cos-meta-\* | Includes custom metadata and its header suffix, which are stored as part of object metadata. Maximum size: 2 KB.<br>**Note:** custom metadata can contain underscores (_), whereas its header suffix can only contain minus signs (-). | string | No |
| x-cos-storage-class | Object storage class, such as `MAZ_STANDARD`, `MAZ_STANDARD_IA`, `STANDARD_IA`,`ARCHIVE`, and `DEEP_ARCHIVE`. Default value: STANDARD. For enumerated values, please see [Storage Class](https://intl.cloud.tencent.com/document/product/436/30925) | Enum | No |

**ACL-related headers**

You can configure object access permissions when uploading an object using the following request headers:

| Name | Description | Type | Required |
| ------------------------ | ------------------------------------------------------------ | ------ | -------- |
| x-cos-acl | Defines the access control list (ACL) attributes of the object. For enumerated values such as `default`, `private`, and `public-read`, see the Preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583).<br>**Note:** currently, COS supports up to 1,000 bucket ACL rules. If you do not need an object ACL, set this parameter to `default` (inherit bucket permissions), or leave it empty. | Enum | No |
| x-cos-grant-read | Allows grantee to read the object; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | String | No |
| x-cos-grant-read-acp | Allows grantee to read the object ACL; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | String | No |
|  x-cos-grant-write-acp | Allows grantee to write the object ACL; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | String | No |
| x-cos-grant-full-control | Allows grantee full control over the object; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | String | No |

**Headers related to server-side encryption (SSE)**

To use SSE encryption for uploading objects, see [Server-side encryption headers](https://intl.cloud.tencent.com/document/product/436/7728#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Request body

This API does not have a request body.

## Response

#### Response headers

In addition to common response headers, this API also returns the following response headers. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

**Headers related to server-side encryption (SSE)**

If you uploaded the object using SSE encryption, this API will return SSE headers. For more information, see [Server-side encryption headers](https://intl.cloud.tencent.com/document/product/436/7729#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Response body

A successful request returns **application/xml** data, including the initialization of multipart upload.

```xml
<InitiateMultipartUploadResult>
	<Bucket>string</Bucket>
	<Key>string</Key>
	<UploadId>string</UploadId>
</InitiateMultipartUploadResult>
```

The detailed nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| ----------------------------- | ------ | --------------------------------------------- | --------- |
| InitiateMultipartUploadResult | None     | Contains all results of the Initiate Multipart Upload action | Container |

**Content of the Container node `InitiateMultipartUploadResult`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ----------------------------- | ------------------------------------ | ------ |
| Bucket             | InitiateMultipartUploadResult | Destination bucket                           | string |
| Key                | InitiateMultipartUploadResult | Destination object key                           | string |
| UploadId           | InitiateMultipartUploadResult | The UploadId used in subsequent Upload Part requests | string |

#### Error codes

This API uses standardized error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) .

## Examples

#### Example 1. Simple example

#### Request

```plaintext
POST /exampleobject?uploads HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 25 Mar 2020 10:07:01 GMT
Content-Type: video/mp4
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1585130821;1585138021&q-key-time=1585130821;1585138021&q-header-list=content-length;content-type;date;host&q-url-param-list=uploads&q-signature=38c5a4b181067206cdbdf65f6a4d662b2291****
Connection: close
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 230
Connection: close
Date: Wed, 25 Mar 2020 10:07:01 GMT
Server: tencent-cos
x-cos-request-id: NWU3YjJkNDVfNDliNTJhMDlfYzZhMl8yOTVj****

<InitiateMultipartUploadResult>
	<Bucket>examplebucket-1250000000</Bucket>
	<Key>exampleobject</Key>
	<UploadId>1585130821cbb7df1d11846c073ad648e8f33b087cec2381df437acdc833cf654b9ecc6361</UploadId>
</InitiateMultipartUploadResult>
```

#### Sample 2. Specifying metadata and ACL using request headers

#### Request

```plaintext
POST /exampleobject?uploads HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 28 May 2020 08:35:34 GMT
Content-Type: video/mp4
Cache-Control: max-age=86400
Content-Disposition: attachment; filename=example.jpg
x-cos-meta-example-field: example-value
x-cos-acl: public-read
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1590654934;1590662134&q-key-time=1590654934;1590662134&q-header-list=cache-control;content-disposition;content-length;content-type;date;host;x-cos-acl;x-cos-meta-example-field&q-url-param-list=uploads&q-signature=5465e9e05cd638e549f66457235d488bfb02****
Connection: close
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 230
Connection: close
Date: Thu, 28 May 2020 08:35:34 GMT
Server: tencent-cos
x-cos-request-id: NWVjZjc3ZDZfOThjMjJhMDlfMjg5N18zNWYy****

<InitiateMultipartUploadResult>
	<Bucket>examplebucket-1250000000</Bucket>
	<Key>exampleobject</Key>
	<UploadId>1590654934dfb1343b4323b711afc22569c18af51596d4f2e40faf392fe1bb469c5b77115f</UploadId>
</InitiateMultipartUploadResult>
```

#### Example 3. Using server-side encryption SSE-COS

#### Request

```plaintext
POST /exampleobject?uploads HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 28 May 2020 08:43:58 GMT
Content-Type: video/mp4
x-cos-server-side-encryption: AES256
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1590655438;1590662638&q-key-time=1590655438;1590662638&q-header-list=content-length;content-type;date;host;x-cos-server-side-encryption&q-url-param-list=uploads&q-signature=24fccaa68a5eb5e0a9e959dfd9493e3a0671****
Connection: close
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 230
Connection: close
Date: Thu, 28 May 2020 08:43:58 GMT
Server: tencent-cos
x-cos-request-id: NWVjZjc5Y2VfZjhjODBiMDlfMjIyOGFfMzYxYWVm****
x-cos-server-side-encryption: AES256

<InitiateMultipartUploadResult>
	<Bucket>examplebucket-1250000000</Bucket>
	<Key>exampleobject</Key>
	<UploadId>15906554384f160dd0a272ebb6fbcdb0ffbb61adb2b46fa6b9f2ffabcfb2940b8f72277952</UploadId>
</InitiateMultipartUploadResult>
```

#### Example 4. Using server-side encryption SSE-KMS

#### Request

```plaintext
POST /exampleobject?uploads HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 28 May 2020 08:44:19 GMT
Content-Type: video/mp4
x-cos-server-side-encryption: cos/kms
x-cos-server-side-encryption-cos-kms-key-id: 48ba38aa-26c5-11ea-855c-52540085****
x-cos-server-side-encryption-context: eyJhdXRob3IiOiJmeXNudGlhbiIsImNvbXBhbnkiOiJUZW5jZW50In0=
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1590655459;1590662659&q-key-time=1590655459;1590662659&q-header-list=content-length;content-type;date;host;x-cos-server-side-encryption;x-cos-server-side-encryption-context;x-cos-server-side-encryption-cos-kms-key-id&q-url-param-list=uploads&q-signature=11ab592d5aba2e740be67f69dfa254631293****
Connection: close
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 230
Connection: close
Date: Thu, 28 May 2020 08:44:20 GMT
Server: tencent-cos
x-cos-request-id: NWVjZjc5ZTNfMmZiOTJhMDlfMzJlNDJfMjkzNGJi****
x-cos-server-side-encryption: cos/kms
x-cos-server-side-encryption-cos-kms-key-id: 48ba38aa-26c5-11ea-855c-52540085****

<InitiateMultipartUploadResult>
	<Bucket>examplebucket-1250000000</Bucket>
	<Key>exampleobject</Key>
	<UploadId>15906554607990121702e8e4b706eb0f12b8568a3f3b0b76b884e4df676ed50291f0b17131</UploadId>
</InitiateMultipartUploadResult>
```

#### Example 5. Using server-side encryption SSE-C

#### Request

```plaintext
POST /exampleobject?uploads HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 28 May 2020 08:44:41 GMT
Content-Type: video/mp4
x-cos-server-side-encryption-customer-algorithm: AES256
x-cos-server-side-encryption-customer-key: MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=
x-cos-server-side-encryption-customer-key-MD5: U5L61r7jcwdNvT7frmUG8g==
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1590655481;1590662681&q-key-time=1590655481;1590662681&q-header-list=content-length;content-type;date;host;x-cos-server-side-encryption-customer-algorithm;x-cos-server-side-encryption-customer-key;x-cos-server-side-encryption-customer-key-md5&q-url-param-list=uploads&q-signature=abd12e9b8c4334a803b5ed8cc03c697904f8****
Connection: close
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 230
Connection: close
Date: Thu, 28 May 2020 08:44:41 GMT
Server: tencent-cos
x-cos-request-id: NWVjZjc5ZjlfOGJjOTJhMDlfNzJmYV8xOTcy****
x-cos-server-side-encryption-customer-algorithm: AES256
x-cos-server-side-encryption-customer-key-MD5: U5L61r7jcwdNvT7frmUG8g==

<InitiateMultipartUploadResult>
	<Bucket>examplebucket-1250000000</Bucket>
	<Key>exampleobject</Key>
	<UploadId>15906554815fb0c8bda2edae20d895ad7452e949bf51541b31ca14a029fb6f1617f10ca186</UploadId>
</InitiateMultipartUploadResult>
```
