## Feature

This API is used to upload an object in multiple parts to COS. It supports up to 10,000 parts for a single request, each between 1 MB to 5 GB in size, except the last part that can be less than 1 MB.

> 
> 1. To call this request, first use the [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) API to get an UploadId that uniquely identifies this Upload Part operation.
> 2. Every time you request the `Upload Part` API, you need to pass in `partNumber` (the part number) and your `uploadId`. You can upload multiple parts out of order.
> 3. When the `uploadId` and `partNumber` of a new part are the same as those of a previously uploaded part, the old part will be overwritten by the new one. A 404 error, `NoSuchUpload`, will be returned if the `uploadId` does not exist.

#### Request

#### Request samples

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

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information)

#### Request parameters

| Name                                  | Description                                                         | Type   | Required |
| ---------- | ------------------------------------------------------------ | ------- | -------- |
| partNumber | Number that identifies a part to upload. Value range: 1 - 10000                | integer | Yes       |
| uploadId | ID that identifies the multipart upload. It’s the same as the UploadId generated when using the Initiate Multipart Upload API. | string | Yes       |

#### Request headers

In addition to common request headers, this API also supports the following request headers. For more information on the common request header, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

**Headers related to server-side encryption (SSE)**

If you used SSE-C to initialize the multipart upload, then you should specify the SSE-C encryption algorithm and key in the Upload Part request. Otherwise, the following headers cannot be used:

| Name                                                         | Description                                                         | Type   | Required |
| ----------------------------------------------- | ------------------------------------------------------------ | ------ | -------- |
| x-cos-server-side-encryption-customer-algorithm | Server-side encryption algorithm; currently only AES256 is supported | string | Yes |
| x-cos-server-side-encryption-customer-key       | Base64-encoded server-side encryption key. <br>For example, `MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=` | string | Yes       |
| x-cos-server-side-encryption-customer-key-MD5  | Base64-encoded MD5 hash of the server-side encryption key. <br>For example, `U5L61r7jcwdNvT7frmUG8g==` | string | Yes       |
| x-cos-traffic-limit | Specifies the traffic limit in bit/s on this upload. Value range: 819200-838860800, that is, 100 KB/s-100 MB/s. if this range is exceeded, a 400 error will be returned | integer | No       |

#### Request body

The request body of this API request is the object (file) content.

## Response

#### Response headers

In addition to common response headers, this API also returns the following response headers. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

**Headers related to server-side encryption (SSE)**

If you initiated the multipart upload using SSE encryption, this API will return SSE headers. For more information, see [Server-side encryption headers](https://intl.cloud.tencent.com/document/product/436/7729#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Response body

The response body of this API is empty.

#### Error codes

This API uses standardized error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) .

## Examples

#### Example 1. Simple example

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

#### Example 2. Using server-side encryption SSE-COS

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

#### Example 3. Using server-side encryption SSE-KMS

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

#### Sample 4. Using Server-side Encryption SSE-C

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
