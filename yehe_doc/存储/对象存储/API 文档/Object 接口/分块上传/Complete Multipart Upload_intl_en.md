## Feature

This API is used to complete a multipart upload after all parts are uploaded via the `Upload Part` API. When using this API, you must specify the `PartNumber` and `ETag` of each part in the request body to check if the parts are correct.

It may take minutes for COS to merge uploaded parts upon a completed multipart upload. As a result, when the merging begins, COS immediately returns a 200 status code along with the `Transfer-Encoding: chunked` response header. COS then periodically returns chunked spaces to keep the connection active until the merging ends, and returns the information about the resulting entire object in the last chunk.

- If any uploaded part is less than 1 MB in size, `400 EntityTooSmall` will be returned when this API is called.
- If the numbers of the uploaded parts are not continuous, `400 InvalidPart` will be returned when this API is called.
- If the part information entries in the request body are not sorted by number in ascending order, `400 InvalidPartOrder` will be returned when this API is called.
- If the `uploadId` does not exist, `404 NoSuchUpload` will be returned when this API is called.

> We recommend you either complete or abort a multipart upload as early as possible, as the uploaded parts of an incomplete multipart upload will take up storage capacity and incur storage fees.

#### Versioning

- If versioning is enabled for the bucket, COS will automatically generate a unique version ID for the object to be uploaded and return this ID in the response using the `x-cos-version-id` response header.
- If versioning is suspended for the bucket, COS will always use `null` as the version ID of any object in the bucket, and return the `x-cos-version-id: null` response header.

#### Request

#### Request samples

```plaintext
POST /<ObjectKey>uploadId=UploadId HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Type: application/xml
Content-Length: Content Length
Content-MD5: MD5
Authorization: Auth String

[Request Body]
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

#### Request parameters

| Name                                  | Description                                                         | Type   | Required |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| uploadId | ID that identifies the multipart upload. It’s the same as the UploadId generated when using the Initiate Multipart Upload API. | string | Yes       |

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

Submits **application/xml** request data, including all parts information.

```xml
<CompleteMultipartUpload>
	<Part>
		<PartNumber>integer</PartNumber>
		<ETag>string</ETag>
	</Part>
	<Part>
		<PartNumber>integer</PartNumber>
		<ETag>string</ETag>
	</Part>
</CompleteMultipartUpload>
```

The nodes are described in details below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ----------------------- | ------ | ------------------------------------------------- | --------- | -------- |
| CompleteMultipartUpload | None     | Contains all information in the Complete Multipart Upload request | Container | No       |

**Content of the Container node `CompleteMultipartUpload`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ----------------------- | ---------------------------------- | --------- | -------- |
| Part      | CompleteMultipartUpload | Describes information on each part in this multipart upload | Container | Yes |

**Content of the Container node `Part`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ---------------------------- | ----------------------------------------------------------- | ------- | -------- |
| PartNumber         | CompleteMultipartUpload.Part | Part number                                                      | integer | Yes       |
| ETag               | CompleteMultipartUpload.Part | The ETag header value returned when the Upload Part request succeeds | string  | Yes       |

## Response

#### Response headers

In addition to common response headers, this API also returns the following response headers. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

**Versioning-related headers**

If the object is uploaded to a versioning-enabled bucket, the following response headers will be returned:

| Name | Description | Type |
| ---------------- | ------------- | ------ |
| x-cos-version-id | Object version ID | string |

**Headers related to server-side encryption (SSE)**

If you upload an object using SSE encryption, this API will return SSE headers. For more information, see [Server-side encryption headers](https://intl.cloud.tencent.com/document/product/436/7729#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Response body

Returns **application/xml** data, including that on the resulting entire object, upon a successful request.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<CompleteMultipartUploadResult xmlns="http://www.qcloud.com/document/product/436/7751">
	<Location>string</Location>
	<Bucket>string</Bucket>
	<Key>string</Key>
	<ETag>string</ETag>
</CompleteMultipartUploadResult>
```

The detailed nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| ----------------------------- | ------ | --------------------------------------------- | --------- |
| CompleteMultipartUploadResult | None     | Contains all the results of the Complete Multipart Upload action | Container |

**Content of the Container node `CompleteMultipartUploadResult`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ----------------------------- | ------------------------------------------------------------ | ------ |
| Location           | CompleteMultipartUploadResult | Location of the object for which the multipart upload is completed. Format: `http://<BucketName-APPID>.cos.<Region>.myqcloud.com/<ObjectKey>`, e.g. `http://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject` | string |
| Bucket             | CompleteMultipartUploadResult | The destination bucket for the multipart upload. Format: `<BucketName-APPID>`, e.g. `examplebucket-1250000000` | string |
| Key                | CompleteMultipartUploadResult | Object key                                                       | string |
| ETag               | CompleteMultipartUploadResult | ETag of the object into which the parts are merged                                     | string |

#### Error codes

This API uses standardized error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) .

## Examples

By default, this API uses “Transfer-Encoding: chunked” responses. However, developers should understand that, all the examples below use responses without Transfer-Encoding, which languages and libraries can automatically process. For more information, see the language- and library-specific documentation.

#### Example 1. Simple example (versioning not enabled)

#### Request

```plaintext
POST /exampleobject?uploadId=1585130821cbb7df1d11846c073ad648e8f33b087cec2381df437acdc833cf654b9ecc6361 HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 25 Mar 2020 10:07:26 GMT
Content-Type: application/xml
Content-Length: 353
Content-MD5: Me/0Gvtc2x4VPIOhoIRllw==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1585130846;1585138046&q-key-time=1585130846;1585138046&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=uploadid&q-signature=45dae7b1a54930587f8123954664b1b5148b****
Connection: close

<CompleteMultipartUpload>
	<Part>
		<PartNumber>1</PartNumber>
		<ETag>"39270a968a357d24207e9911162507eb"</ETag>
	</Part>
	<Part>
		<PartNumber>2</PartNumber>
		<ETag>"d899fbd1e06109ea2e4550f5751c88d6"</ETag>
	</Part>
	<Part>
		<PartNumber>3</PartNumber>
		<ETag>"762890d6c9a871b7bd136037cb2260cd"</ETag>
	</Part>
</CompleteMultipartUpload>
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 378
Connection: close
Date: Wed, 25 Mar 2020 10:07:26 GMT
Server: tencent-cos
x-cos-hash-crc64ecma: 2290339086971918696
x-cos-request-id: NWU3YjJkNWVfZDFjODJhMDlfMTk2ODJfMmEyNTA0****

<?xml version="1.0" encoding="UTF-8"?>
<CompleteMultipartUploadResult xmlns="http://www.qcloud.com/document/product/436/7751">
	<Location>http://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject</Location>
	<Bucket>examplebucket-1250000000</Bucket>
	<Key>exampleobject</Key>
	<ETag>&quot;aa259a62513358f69e98e72e59856d88-3&quot;</ETag>
</CompleteMultipartUploadResult>
```

#### Example 2. Using server-side encryption SSE-COS

#### Request

```plaintext
POST /exampleobject?uploadId=1590862540251355295a5c736513d70d42b92bbde4f0fafb5e0ecb314b55aa0018cc9fa76f HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Sat, 30 May 2020 18:16:08 GMT
Content-Type: application/xml
Content-Length: 153
Content-MD5: wmpyfdr9s/A+VCBwDdC1bA==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1590862568;1590869768&q-key-time=1590862568;1590869768&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=uploadid&q-signature=abe1fd2d2c057c8f3e4d331a0448b06ecf5b****
Connection: close

<CompleteMultipartUpload>
	<Part>
		<PartNumber>1</PartNumber>
		<ETag>"108f528eb63b65e734f27ae331f5ffaa"</ETag>
	</Part>
</CompleteMultipartUpload>
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 378
Connection: close
Date: Sat, 30 May 2020 18:16:08 GMT
Server: tencent-cos
x-cos-hash-crc64ecma: 4510578591875220731
x-cos-request-id: NWVkMmEyZThfYTJjMjJhMDlfMmQzOV8zYTM5****
x-cos-server-side-encryption: AES256

<?xml version="1.0" encoding="UTF-8"?>
<CompleteMultipartUploadResult xmlns="http://www.qcloud.com/document/product/436/7751">
	<Location>http://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject</Location>
	<Bucket>examplebucket-1250000000</Bucket>
	<Key>exampleobject</Key>
	<ETag>&quot;915fca1c3b2737c262458b3a1a43c683-1&quot;</ETag>
</CompleteMultipartUploadResult>
```

#### Example 3. Using server-side encryption SSE-KMS

#### Request

```plaintext
POST /exampleobject?uploadId=15908625793957d71176fa878282d266a95b79dc2aec159b4a73d1d79c80d4f931cda6ad65 HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Sat, 30 May 2020 18:16:40 GMT
Content-Type: application/xml
Content-Length: 153
Content-MD5: jUFgTSZThmPT3qseea0mRQ==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1590862600;1590869800&q-key-time=1590862600;1590869800&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=uploadid&q-signature=68aaf036efac07ef8d6ef101f81a1589849a****
Connection: close

<CompleteMultipartUpload>
	<Part>
		<PartNumber>1</PartNumber>
		<ETag>"1d3e8ae9da423b440341b09f1616f074"</ETag>
	</Part>
</CompleteMultipartUpload>
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 378
Connection: close
Date: Sat, 30 May 2020 18:16:40 GMT
Server: tencent-cos
x-cos-hash-crc64ecma: 4510578591875220731
x-cos-request-id: NWVkMmEzMDhfYzhjODJhMDlfMjNhYTBfMjdmNjNl****
x-cos-server-side-encryption: cos/kms
x-cos-server-side-encryption-cos-kms-key-id: 48ba38aa-26c5-11ea-855c-52540085****

<?xml version="1.0" encoding="UTF-8"?>
<CompleteMultipartUploadResult xmlns="http://www.qcloud.com/document/product/436/7751">
	<Location>http://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject</Location>
	<Bucket>examplebucket-1250000000</Bucket>
	<Key>exampleobject</Key>
	<ETag>&quot;8093dc3e18f7070444e6ca21789eb8d4-1&quot;</ETag>
</CompleteMultipartUploadResult>

```

#### Sample 4. Using Server-side Encryption SSE-C

#### Request

```plaintext
POST /exampleobject?uploadId=1590862610acd643927bad05cd3947bf98b56b04b0b0b2a45a49969f87cc95b7fd5fcc065a HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Sat, 30 May 2020 18:17:11 GMT
Content-Type: application/xml
Content-Length: 153
Content-MD5: MnXmb3yvrbwMfBlUwUE1Hg==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1590862631;1590869831&q-key-time=1590862631;1590869831&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=uploadid&q-signature=5ce15a35c591eb797e8abaf210313e58ac03****
Connection: close

<CompleteMultipartUpload>
	<Part>
		<PartNumber>1</PartNumber>
		<ETag>"ff14981a35a58eb97bca838b055c573b"</ETag>
	</Part>
</CompleteMultipartUpload>
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 378
Connection: close
Date: Sat, 30 May 2020 18:17:11 GMT
Server: tencent-cos
x-cos-hash-crc64ecma: 4510578591875220731
x-cos-request-id: NWVkMmEzMjdfODljOTJhMDlfMzQ2ZDNfMWMwZWYy****
x-cos-server-side-encryption-customer-algorithm: AES256
x-cos-server-side-encryption-customer-key-MD5: U5L61r7jcwdNvT7frmUG8g==

<?xml version="1.0" encoding="UTF-8"?>
<CompleteMultipartUploadResult xmlns="http://www.qcloud.com/document/product/436/7751">
	<Location>http://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject</Location>
	<Bucket>examplebucket-1250000000</Bucket>
	<Key>exampleobject</Key>
	<ETag>&quot;55973f71e8e892273053617e6b83d1c7-1&quot;</ETag>
</CompleteMultipartUploadResult>
```

#### Example 5. Enabling versioning

#### Request

```plaintext
POST /exampleobject?uploadId=15908626631e1995018f81a5e563837d6d7f1b51d7c97dff09989296403e32366e52f2877b HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Sat, 30 May 2020 18:18:04 GMT
Content-Type: application/xml
Content-Length: 153
Content-MD5: wmpyfdr9s/A+VCBwDdC1bA==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1590862684;1590869884&q-key-time=1590862684;1590869884&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=uploadid&q-signature=5409509944602014d1b61cb4bbe1e39003b4****
Connection: close

<CompleteMultipartUpload>
	<Part>
		<PartNumber>1</PartNumber>
		<ETag>"108f528eb63b65e734f27ae331f5ffaa"</ETag>
	</Part>
</CompleteMultipartUpload>
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 378
Connection: close
Date: Sat, 30 May 2020 18:18:04 GMT
Server: tencent-cos
x-cos-hash-crc64ecma: 4510578591875220731
x-cos-request-id: NWVkMmEzNWNfOGNjOTJhMDlfMWQ4NjJfMWM0NGUw****
x-cos-version-id: MTg0NDUxNTMyMTEwNDU1NDc3OTc

<?xml version="1.0" encoding="UTF-8"?>
<CompleteMultipartUploadResult xmlns="http://www.qcloud.com/document/product/436/7751">
	<Location>http://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject</Location>
	<Bucket>examplebucket-1250000000</Bucket>
	<Key>exampleobject</Key>
	<ETag>&quot;42318fc0ec58952b0d9ab4d7a006f595-1&quot;</ETag>
</CompleteMultipartUploadResult>
```

#### Example 6. Suspending versioning

#### Request

```plaintext
POST /exampleobject?uploadId=1590862705b4349d597c0db1281e1c666bc431eb468b3a64076be7093c91a963bc5ead2ea4 HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Sat, 30 May 2020 18:18:45 GMT
Content-Type: application/xml
Content-Length: 153
Content-MD5: wmpyfdr9s/A+VCBwDdC1bA==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1590862725;1590869925&q-key-time=1590862725;1590869925&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=uploadid&q-signature=b212e42daaeabcd2b8e9f6722b62fe8d618b****
Connection: close

<CompleteMultipartUpload>
	<Part>
		<PartNumber>1</PartNumber>
		<ETag>"108f528eb63b65e734f27ae331f5ffaa"</ETag>
	</Part>
</CompleteMultipartUpload>
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 378
Connection: close
Date: Sat, 30 May 2020 18:18:45 GMT
Server: tencent-cos
x-cos-hash-crc64ecma: 4510578591875220731
x-cos-request-id: NWVkMmEzODVfZjZjMjBiMDlfNGYzZV8zODc4****
x-cos-version-id: null

<?xml version="1.0" encoding="UTF-8"?>
<CompleteMultipartUploadResult xmlns="http://www.qcloud.com/document/product/436/7751">
	<Location>http://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject</Location>
	<Bucket>examplebucket-1250000000</Bucket>
	<Key>exampleobject</Key>
	<ETag>&quot;491509b1fdf8e13d1f51d323c4a6d0e8-1&quot;</ETag>
</CompleteMultipartUploadResult>
```
