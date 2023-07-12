## Overview

This API is used to initialize a multipart upload. After a successful operation, `UploadId` will be returned, which can be used in subsequent `Upload Part` requests.

>?
>Only the root account or sub-accounts granted the permission of the `Initiate Multipart Upload` API can call this API.
>


<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer (recommended)
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=InitiateMultipartUpload&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                Tencent Cloud API Explorer makes it easy for you to make online API calls, verify signatures, generate SDK code, and search for APIs. You can use it to query the request and response of each API call and generate sample SDK codes for the call.
            </div>
        </div>
    </div>
</div>

## Request

#### Sample request

```plaintext
POST /<ObjectKey>?uploads HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Type: Content Type
Content-Length: 0
Authorization: Auth String
```

>? 
> - Host: <BucketName-APPID>.cos.<Region>.myqcloud.com, where <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://www.tencentcloud.com/document/product/436/6224)).
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> 

#### Request parameters

This API has no request parameter.

#### Request headers

In addition to common request headers, this API also supports the following request headers. For more information about common request headers, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

| Header | Description | Type | Required |
| ------------------- | ------------------------------------------------------------ | ------ | -------- |
| Cache-Control | Cache directives as defined in RFC 2616. It will be stored as object metadata. | string | No |
| Content-Disposition | Filename defined in RFC 2616. It will be stored as object metadata. | string | No |
| Content-Encoding | Encoding format as defined in RFC 2616. It will be stored as object metadata. | string | No |
| Content-Type | HTTP request content type (MIME) as defined in RFC 2616. This header describes the content type of the object to be uploaded and will be stored as object metadata.<br>Example: `text/html`, `image/jpeg` | string | Yes |
| Expires | The cache expiration time as defined in RFC 2616. It will be stored as object metadata. | string | No |
| x-cos-meta-\* | Contains user-defined metadata and header suffixes. It will be stored as object metadata. Maximum size: 2 KB. <br>**Note:** User-defined metadata can contain underscores (_), whereas the header suffixes of user-defined metadata can only contain minus signs (−) but not underscores. | string | No |
| x-cos-storage-class | Object storage class. For the enumerated values, such as `STANDARD` (default), `INTELLIGENT_TIERING`, `STANDARD_IA`, `ARCHIVE`, and `DEEP_ARCHIVE`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | Enum | No |
| x-cos-tagging | A set of up to 10 object tags (for example, `Key1=Value1&Key2=Value2`). Tag key and tag value in the set must be URL-encoded. | string  | No |


**ACL-related headers**

You can configure an access control list (ACL) for the object by specifying the following request headers during the upload:

| Header | Description | Type | Required |
| ------------------------ | ------------------------------------------------------------ | ------ | -------- |
| x-cos-acl | Defines the ACL attribute of the object. For the enumerated values, such as `default`, `private`, and `public-read`, please see the **Preset ACL** section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: `default`. <br>**Note**: If you do not need to set an ACL for the object, set this parameter to `default` or leave it empty. In this way, the object will inherit the permissions of the bucket it is stored in. | Enum | No |
| x-cos-grant-read | Grants a user read permission for an object in the format: `id="[OwnerUin]"` (e.g., `id="100000000001"`). You can use commas (,) to separate multiple users, for example, `id="100000000001",id="100000000002"`. | string | No |
| x-cos-grant-read-acp | Grants a user read permission for the ACL of an object in the format: `id="[OwnerUin]"` (e.g., `id="100000000001"`). You can use commas (,) to separate multiple users, for example, `id="100000000001",id="100000000002"`. | string | No |
| x-cos-grant-write-acp | Grants a user write permission for the ACL of an object in the format: `id="[OwnerUin]"` (e.g., `id="100000000001"`). You can use commas (,) to separate multiple users, for example, `id="100000000001",id="100000000002"`. | string | No |
| x-cos-grant-full-control | Grants a user full permission to operate on an object in the format: `id="[OwnerUin]"` (e.g., `id="100000000001"`). You can use commas (,) to separate multiple users, for example, `id="100000000001",id="100000000002"`. | string | No |

**SSE-related headers**

Server-side encryption can be used during object upload. For more information, see [Server-side encryption headers](https://intl.cloud.tencent.com/document/product/436/7728#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Request body

This API does not have a request body.

## Response

#### Response headers

In addition to common response headers, this API also returns the following response headers. For more information about common response headers, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

**SSE-related headers**

If server-side encryption is used during object upload, this API will return headers used specifically for server-side encryption. For more information, please see [Server-Side Encryption Headers](https://intl.cloud.tencent.com/document/product/436/7729#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Response body

**application/xml** data that contains the multipart upload initialization information will be returned for a successful request.


```
<InitiateMultipartUploadResult>
       <Bucket>string</Bucket>
       <Key>string</Key>
       <UploadId>string</UploadId>
</InitiateMultipartUploadResult>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| ----------------------------- | ------ | --------------------------------------------- | --------- |
| InitiateMultipartUploadResult | None | Stores the result of `Initiate Multipart Upload` | Container |

**Content of `InitiateMultipartUploadResult**:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ----------------------------- | ------------------------------------ | ------ |
| Bucket | InitiateMultipartUploadResult | Destination bucket | string |
| Key | InitiateMultipartUploadResult | Destination object key  | string |
| UploadId | InitiateMultipartUploadResult | `UploadId` that can be used in subsequent `Upload Part` requests | string |

#### Error codes

This API returns common error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

#### Example 1: simple use case

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

#### Example 2: specifying metadata and ACL using request headers

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

#### Example 3: using server-side encryption SSE-COS

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

#### Example 4: using server-side encryption SSE-KMS

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


#### Example 5: using server-side encryption SSE-C

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
