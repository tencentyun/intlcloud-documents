## Overview

This API is used to complete a multipart upload after all parts are uploaded with the `Upload Part` API. When calling this API, you must specify the `PartNumber` and `ETag` of each part in the request body to verify the parts.

After all parts are uploaded, it will take several minutes for them to be concatenated. Therefore, when the concatenation starts, COS will immediately return status code 200 and use the `Transfer-Encoding: chunked` response header to return spaces periodically to keep the connection alive until the concatenation is completed. After that, COS will return information about the concatenated object in the last chunk.

- If any uploaded part is smaller than 1 MB, "400 EntityTooSmall" will be returned when this API is called.
- If the part numbers are not continuous, "400 InvalidPart" will be returned when this API is called.
- If the part numbers in the request body are not in ascending order, "400 InvalidPartOrder" will be returned when this API is called.
- If the `uploadId` does not exist, `404` (NoSuchUpload) will be returned when this API is called.


>?
>Only the root account or sub-accounts granted the permission of the `Complete Multipart Upload` API can call this API.
>

>! We recommend you either complete or abort a multipart upload as early as possible, as the uploaded parts of an incomplete multipart upload will take up storage capacity and incur storage fees.
>

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer (recommended)
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=CompleteMultipartUpload&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                Tencent Cloud API Explorer makes it easy for you to make online API calls, verify signatures, generate SDK code, and search for APIs. You can use it to query the request and response of each API call and generate sample SDK codes for the call.
            </div>
        </div>
    </div>
</div>


#### Versioning

- For a versioning-enabled bucket, COS will automatically generate a unique version ID for the object, and the ID will be returned in the `x-cos-version-id` response header.
- For a versioning-suspended bucket, COS will always use `null` as the version ID of the object and will return the `x-cos-version-id: null` response header.

## Request

#### Sample request

```plaintext
POST /<ObjectKey>?uploadId=UploadId HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Type: application/xml
Content-Length: Content Length
Content-MD5: MD5
Authorization: Auth String

[Request Body]
```

>? 
> - Host: <BucketName-APPID>.cos.<Region>.myqcloud.com, where <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://www.tencentcloud.com/document/product/436/6224)).
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> 

#### Request parameters

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| uploadId | Multipart upload ID obtained from the `Initiate Multipart Upload` API | string | Yes |

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

The request body contains **application/xml** data that includes information about all parts.

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

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ----------------------- | ------ | ------------------------------------------------- | --------- | -------- |
| CompleteMultipartUpload | None | All request information about `Complete Multipart Upload` | Container | No |

**Content of `CompleteMultipartUpload`**:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ----------------------- | ---------------------------------- | --------- | -------- |
| Part      | CompleteMultipartUpload | Information about each part | Container | Yes |

**Content of `Part`**:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ---------------------------- | ----------------------------------------------------------- | ------- | -------- |
| PartNumber | CompleteMultipartUpload.Part | Part number | integer | Yes |
| ETag  | CompleteMultipartUpload.Part | ETag of the part. The value is obtained from the ETag header in the response to a successful `Upload Part` request. | string  | Yes |

## Response

#### Response headers

In addition to common response headers, this API also returns the following response headers. For more information about common response headers, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

**Versioning-Related Headers**

If the object is uploaded to a versioning-enabled bucket, the following response headers will be returned:

| Header | Description | Type |
| ---------------- | ------------- | ------ |
| x-cos-version-id | Version ID of the object | string |

**SSE-related headers**

If server-side encryption is used during object upload, this API will return headers used specifically for server-side encryption. For more information, please see [Server-Side Encryption Headers](https://intl.cloud.tencent.com/document/product/436/7729#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Response body

If the request is successful, **application/xml** data that includes information about the concatenated object will be returned.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<CompleteMultipartUploadResult xmlns="http://www.qcloud.com/document/product/436/7751">
	<Location>string</Location>
	<Bucket>string</Bucket>
	<Key>string</Key>
	<ETag>string</ETag>
</CompleteMultipartUploadResult>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| ----------------------------- | ------ | --------------------------------------------- | --------- |
| CompleteMultipartUploadResult | None | Stores the result of `Complete Multipart Upload` | Container |

**Content of `CompleteMultipartUploadResult`**

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ----------------------------- | ------------------------------------------------------------ | ------ |
| Location | CompleteMultipartUploadResult | Location of the concatenated object, formatted as `http://<BucketName-APPID>.cos.<Region>.myqcloud.com/<ObjectKey>` (for example, `http://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject`) | string |
| Bucket | CompleteMultipartUploadResult | Bucket where the concatenated object resides, formatted as `<BucketName-APPID>` (for example, `examplebucket-1250000000`) | string |
| Key | CompleteMultipartUploadResult | Object key | string |
| ETag | CompleteMultipartUploadResult | ETag of the concatenated object | string |

#### Error codes

This API returns common error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).


## Examples

This API uses `Transfer-Encoding: chunked` in the response by default. For readability, samples in this document are displayed without `Transfer-Encoding`. During use, different languages and libraries can automatically process this encoding form. For more information, see the language- and library-related documents.

#### Example 1: simple use case (with versioning disabled)

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

#### Sample 2: using server-side encryption SSE-COS

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

#### Sample 3: using server-side encryption SSE-KMS

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

#### Example 4: using server-side encryption SSE-C

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

#### Example 5: versioning-enabled

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

#### Example 6: versioning-suspended

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
