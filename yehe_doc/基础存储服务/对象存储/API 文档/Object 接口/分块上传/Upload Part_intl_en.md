## Overview

This API is used to upload an object to COS in multiple parts. You can upload up to 10,000 parts. The size of each part should be 1 MB to 5 GB, and the last part can be smaller than 1 MB.

> ? 
>- Multipart upload steps:
>  1. To call this API, you need to first call the [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) API to obtain the `UploadId`, which identifies the current upload operation.
>  2. Every time you call the `Upload Part` API, you need to include the `partNumber` and `uploadId` parameters. You can upload multiple parts out of order.
>  3. When the `uploadId` and `partNumber` of a new part are the same as those of a previously uploaded part, the old part will be overwritten. If the `uploadId` does not exist, "404 NoSuchUpload" will be returned.
>- Only the root account or sub-accounts granted the permission of the `Upload Part` API can call this API.
>

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer (recommended)
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=UploadPart&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
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
PUT /<ObjectKey>?partNumber=PartNumber&uploadId=UploadId HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Type: Content Type
Content-Length: Content Length
Content-MD5: MD5
Authorization: Auth String

[Object Part]
```

>? 
> - Host: <BucketName-APPID>.cos.<Region>.myqcloud.com, where <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://www.tencentcloud.com/document/product/436/6224)).
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> 

#### Request parameters

| Parameter | Description | Type | Required |
| ---------- | ------------------------------------------------------------ | ------- | -------- |
| partNumber | Part number. Value range: 1−10000 | integer | Yes |
| uploadId | Multipart upload ID obtained from the `Initiate Multipart Upload` API | string | Yes |

#### Request headers

In addition to common request headers, this API also supports the following request headers. For more information about common request headers, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

**SSE-related headers**

If SSE-C is used during the initialization of the current multipart upload, you need to specify the encryption algorithm and key that were specified during the initialization. Otherwise, you cannot specify the following headers.

| Field |  Description | Type | Required |
| ----------------------------------------------- | ------------------------------------------------------------ | ------ | -------- |
| x-cos-server-side-encryption-customer-algorithm | Server-side encryption algorithm. Currently, only `AES256` is supported. | string | Yes |
| x-cos-server-side-encryption-customer-key       | Base64-encoded server-side encryption key. <br>Example: `MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=` | string | Yes       |
| x-cos-server-side-encryption-customer-key-MD5  | Base64-encoded MD5 checksum of the server-side encryption key. <br>Example: `U5L61r7jcwdNvT7frmUG8g==` | string | Yes       |
| x-cos-traffic-limit | Limits the speed (in bit/s) for the current multipart upload for traffic control. Value range: 819200-838860800 (i.e., 100 KB/s-100 MB/s). If the speed exceeds the limit, a 400 error will be returned. | integer | No |

#### Request body

The request body of this API is the part content of the object (file).

## Response

#### Response headers

In addition to common response headers, this API also returns the following response headers. For more information about common response headers, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

**SSE-related headers**

If server-side encryption is used during the initialization of the current multipart upload, this API will return headers used specifically for server-side encryption. For more information, please see [Server-Side Encryption Headers](https://intl.cloud.tencent.com/document/product/436/7729#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Response body

The response body of this API is empty.

#### Error codes

This API returns common error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

#### Example 1: simple use case

#### Request

```plaintext
PUT /exampleobject?partNumber=1&uploadId=1585130821cbb7df1d11846c073ad648e8f33b087cec2381df437acdc833cf654b9ecc6361 HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 25 Mar 2020 10:07:14 GMT
Content-Type: application/octet-stream
Content-Length: 1048576
Content-MD5: OScKloo1fSQgfpkRFiUH6w==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1585130834;1585138034&q-key-time=1585130834;1585138034&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=partnumber;uploadid&q-signature=a815da18232cfec87e8218f32f31b1e2c5eb****
Connection: close

[Object Part]
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Wed, 25 Mar 2020 10:07:14 GMT
ETag: "39270a968a357d24207e9911162507eb"
Server: tencent-cos
x-cos-hash-crc64ecma: 9973912126177188060
x-cos-request-id: NWU3YjJkNTJfZDBjODJhMDlfMjU4NTZfMjc5MzBh****
```

#### Sample 2: using server-side encryption SSE-COS

#### Request

```plaintext
PUT /exampleobject?partNumber=1&uploadId=1590862540251355295a5c736513d70d42b92bbde4f0fafb5e0ecb314b55aa0018cc9fa76f HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Sat, 30 May 2020 18:15:50 GMT
Content-Type: application/octet-stream
Content-Length: 13
Content-MD5: EI9SjrY7Zec08nrjMfX/qg==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1590862550;1590869750&q-key-time=1590862550;1590869750&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=partnumber;uploadid&q-signature=2a0085596de5861410bcc43f3d107dc9dda5****
Connection: close

[Object Part]
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Sat, 30 May 2020 18:15:51 GMT
ETag: "108f528eb63b65e734f27ae331f5ffaa"
Server: tencent-cos
x-cos-hash-crc64ecma: 4510578591875220731
x-cos-request-id: NWVkMmEyZDZfYjNjMjJhMDlfMmJlM18zOWI2****
x-cos-server-side-encryption: AES256
```

#### Sample 3: using server-side encryption SSE-KMS

#### Request

```plaintext
PUT /exampleobject?partNumber=1&uploadId=15908625793957d71176fa878282d266a95b79dc2aec159b4a73d1d79c80d4f931cda6ad65 HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Sat, 30 May 2020 18:16:29 GMT
Content-Type: application/octet-stream
Content-Length: 13
Content-MD5: EI9SjrY7Zec08nrjMfX/qg==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1590862589;1590869789&q-key-time=1590862589;1590869789&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=partnumber;uploadid&q-signature=2d1231c77c72727bd1c2454726813e095a7e****
Connection: close

[Object Part]
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Sat, 30 May 2020 18:16:30 GMT
ETag: "1d3e8ae9da423b440341b09f1616f074"
Server: tencent-cos
x-cos-hash-crc64ecma: 4510578591875220731
x-cos-request-id: NWVkMmEyZmRfYTRiOTJhMDlfMTE0ZGRfMmE3OTk4****
x-cos-server-side-encryption: cos/kms
x-cos-server-side-encryption-cos-kms-key-id: 48ba38aa-26c5-11ea-855c-52540085****
```

#### Example 4: using server-side encryption SSE-C

#### Request

```plaintext
PUT /exampleobject?partNumber=1&uploadId=1590862610acd643927bad05cd3947bf98b56b04b0b0b2a45a49969f87cc95b7fd5fcc065a HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Sat, 30 May 2020 18:17:01 GMT
x-cos-server-side-encryption-customer-algorithm: AES256
x-cos-server-side-encryption-customer-key: MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=
x-cos-server-side-encryption-customer-key-MD5: U5L61r7jcwdNvT7frmUG8g==
Content-Type: application/octet-stream
Content-Length: 13
Content-MD5: EI9SjrY7Zec08nrjMfX/qg==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1590862621;1590869821&q-key-time=1590862621;1590869821&q-header-list=content-length;content-md5;content-type;date;host;x-cos-server-side-encryption-customer-algorithm;x-cos-server-side-encryption-customer-key;x-cos-server-side-encryption-customer-key-md5&q-url-param-list=partnumber;uploadid&q-signature=6d0914f1db0e03569b6b5d340dc8d71616bf****
Connection: close

[Object Part]
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Sat, 30 May 2020 18:17:01 GMT
ETag: "ff14981a35a58eb97bca838b055c573b"
Server: tencent-cos
x-cos-hash-crc64ecma: 4510578591875220731
x-cos-request-id: NWVkMmEzMWRfYjRjOTJhMDlfYWRhXzFhZmYw****
x-cos-server-side-encryption-customer-algorithm: AES256
x-cos-server-side-encryption-customer-key-MD5: U5L61r7jcwdNvT7frmUG8g==
```
