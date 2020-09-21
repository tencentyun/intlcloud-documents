## Feature

This API is used to create a copy of an object that already exists in COS, i.e., copying an object from the source path (object key) to the destination path (object key). The recommended object size is between 1 MB and 5 GB. For objects over 5 GB, use [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287).

You can choose to either copy metadata of the source object (default option), or specify new metadata in this API request. Unless the request otherwise explicitly specifies, the destination object will always be stored into STANDARD, inherit (default) the ACLs of the destination bucket, and have SSE disabled.

You can use this API to move or rename an object, modify object metadata, or create copies.

The requester of this API needs to have read permission to the copied object, or the copied object allows read permission (public read) to everyone, and write permission to the destination bucket.

> 
>
> - COS returns a standard error response for an error that occurs before the PUT Object - Copy operation, and a HTTP 200 OK with error content as response body for an error that occurs during the operation. Therefore, you may not determine whether your request succeeds until you check the body of the HTTP 200 OK response.
> - The MAZ_STANDARD storage class only supports replication into the exact same class rather than STANDARD, STANDARD_IA and ARCHIVE.

#### Versioning

- By default, COS copies the latest version of the source object in a versioning-enabled bucket. You can copy a specified version by specifying `versionId` in the x-cos-copy-source request header.
- COS automatically generates a unique version ID for the destination object in a versioning-enabled bucket.

## Request

#### Request samples

```plaintext
PUT /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
x-cos-copy-source: <SourceBucketName-SourceAPPID>.cos.<SourceRegion>.myqcloud.com/<SourceObjectKey>
Content-Length: 0
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

#### Request parameters

This API does not use any request parameter.

#### Request headers

In addition to common request headers, this API also supports the following request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

| Name                                  | Description                                                         | Type   | Required |
| ------------------------------------- | ------------------------------------------------------------ | ------ | -------- |
| x-cos-copy-source | URL of the source object, where the object key needs to be URLEncoded, and an object version can be specified in `versionId`. Example: <br>`sourcebucket-1250000001.cos.ap-shanghai.myqcloud.com/example-%E8%85%BE%E8%AE%AF%E4%BA%91.jpg`<br>, or `sourcebucket-1250000001.cos.ap-shanghai.myqcloud.com/example-%E8%85%BE%E8%AE%AF%E4%BA%91.jpg?versionId=MTg0NDUxNzYzMDc0NDMzNDExOTc` | String | Yes |
| x-cos-metadata-directive | Indicates whether to copy source object metadata. Enumerated values: Copy (default), Replaced.<br><li>If set to Copy, the source metadata is copied. <li>If set to Replaced, this request uses metadata in the request header for the destination object.<br>If you want to modify the metadata by setting the source and destination objects as the same, you must set this value to Replaced. | Enum | No |
| x-cos-copy-source-If-Modified-Since | The PUT Object - Copy operation is performed if the object is modified after the specified time. Otherwise, HTTP status code 412 (Precondition Failed) is returned. | String | No |
| x-cos-copy-source-If-Unmodified-Since | The PUT Object - Copy operation is performed if the object is not modified after the specified time. Otherwise, HTTP status code 412 (Precondition Failed) is returned. | String | No |
| x-cos-copy-source-If-Match | The PUT Object - Copy operation is performed if the object ETag matches the specified value. Otherwise, HTTP status code 412 (Precondition Failed) is returned.  | String | No |
| x-cos-copy-source-If-None-Match | The PUT Object - Copy operation is performed if the object ETag does not match the specified value. Otherwise, HTTP status code 412 (Precondition Failed) is returned.  | String | No |
| x-cos-storage-class | Storage class of the destination object, such as `STANDARD_IA` , `ARCHIVE`and `DEEP_ARCHIVE`. Default value: `STANDARD`. For enumerated values, see [Storage Class](https://intl.cloud.tencent.com/document/product/436/30925). | Enum | No |

**Headers related to destination object metadata**

This API operation allows you to configure new metadata for the destination object using the following request headers. In this case, the request header `x-cos-metadata-directive` must be specified as Replaced; otherwise, the destination object will use the source object metadata, and you cannot specify any of these headers:

| Name                                                         | Description                                                         | Type   | Required |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------ | -------- |
| Cache-Control | Cache directives as defined in RFC 2616, which are stored as part of destination object metadata | String | No |
| Content-Disposition | File name as defined in RFC 2616, which is stored as part of the destination object metadata | String | No |
| Content-Encoding | Encoding format as defined in RFC 2616, which is stored as part of destination object metadata | String | No |
| Content-Type                                                 | HTTP request content type (MIME) as defined in RFC 2616 of the destination object, and stored as part of destination object metadata<br>Example: `text/html` or `image/jpeg` | String | Yes       |
| Expires | The cache expiration time as defined in RFC 2616, which is stored as part of destination object metadata | String | No |
| x-cos-meta-\* | Includes custom metadata and its header suffix, which are stored as part of destination object metadata. Maximum size: 2 KB.<br>**Note:** custom metadata can contain underscores (_), whereas its header suffix can only contain minus signs (-). | String | No |

**Headers related to destination object ACLs**

This API operation allows you to configure access permissions for the destination object using the following request headers:

| Name                                                         | Description                                                         | Type   | Required |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------ | -------- |
| x-cos-acl | Defines the access control list (ACL) attributes of the destination object. For enumerated values such as `default`, `private`, and `public-read`, see the Preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). <br>**Note:** currently, COS supports up to 1,000 bucket ACL rules. If you do not need an object ACL, set this parameter to `default` (inherit bucket permissions), or leave it empty. | Enum | No |
| x-cos-grant-read | Grants the permission to read the destination object; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | String | No |
| x-cos-grant-read-acp | Grants the permission to read ACLs of the destination object; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | String | No |
| x-cos-grant-write-acp | Grants the permission to write to the ACLs of the destination object; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | String | No |
| x-cos-grant-full-control | Grants full permission to operate on the destination object; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | String | No |

**Headers related to server-side encryption (SSE) for source object**

If the source object is encrypted with server-side encryption SSE-C, specify the following request headers to decrypt the object:

| Name                                                        | Description                                                         | Type   | Required&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;                          |
| ----------------------------------------------------------- | ------------------------------------------------------------ | ------ | ----------------------------------- |
|  x-cos-copy-source-server-side-encryption-customer-algorithm  | Server-side encryption algorithm; currently only AES256 is supported | String | Required when the source object uses SSE-C encryption |
| x-cos-copy-source-server-side-encryption-customer-key | Base64-encoded server-side encryption key, e.g. <code>MDEyMzQ1Njc4OUFCQ<br>0RFRjAxMjM0NTY3ODlBQkNERUY=</code> | String | Required if the source object uses SSE-C |
| x-cos-copy-source-server-side-encryption-customer-key-MD5  | Base64-encoded MD5 hash of the server-side encryption key. <br>Example: `U5L61r7jcwdNvT7frmUG8g==` | String | Required if the source object uses SSE-C  |

**Headers related to server-side encryption (SSE) for destination object**

You can encrypt copied objects with SSE. For more information, see [Server-side encryption headers](https://intl.cloud.tencent.com/document/product/436/7728#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Request body

This API does not have a request body.

## Response

#### Response headers

In addition to common response headers, this API also returns the following response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

**Versioning-related headers**

When the version ID of the source object is specified, the following response headers are returned:

| Name | Description | Type |
| ---------------------------- | --------------- | ------ |
| x-cos-copy-source-version-id | Version ID of the source object | String |

**Headers related to server-side encryption (SSE)**

If you copy an object using SSE encryption, this API will return SSE headers. For more information, see [Server-side encryption headers](https://intl.cloud.tencent.com/document/product/436/7729#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Response body

A successful request returns the **application/xml** data, which includes the object’s copying results.

```plaintext
<?xml version="1.0" encoding="UTF-8"?>
<CopyObjectResult>
	<ETag>string</ETag>
	<CRC64>number</CRC64>
	<LastModified>date</LastModified>
	<VersionId>string</VersionId>
</CopyObjectResult>
```

The detailed nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------ | ------------------------------------- | --------- |
CopyObjectResult | None | Contains all PUT Object-Copy results | Container |

**Content of Container node CopyObjectResult:**

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ---------------- | ------------------------------------------------------------ | ------ |
| ETag | CopyObjectResult | Entity Tag of an object that identifies the content of the object when it is created, and can be used to check whether the content has changed.<br>Example: `8e0b617ca298a564c3331da28dcb50df`. This header does not necessarily return the MD5 value of the object, depending on how the object is uploaded and encrypted. | String |
| CRC64 | CopyObjectResult |CRC64 value of the object. For more information, see [CRC64 Check](https://intl.cloud.tencent.com/document/product/436/34078). | number |
| LastModified | CopyObjectResult | Last modified time of the object in ISO8601 format, such as `2019-05-24T10:56:40Z` | date |
| VersionId | CopyObjectResult | The version ID of the object, which is returned only if the destination bucket has versioning enabled | String |

#### Error codes

This API returns uniform error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

By default, this API uses “Transfer-Encoding: chunked” responses. However, developers should understand that, all the examples below use responses without Transfer-Encoding, which languages and libraries can automatically process. For more information, see the language- and library-specific documentation.

#### Example 1. Simple example

#### Request

```plaintext
PUT /exampleobject HTTP/1.1
Host: destinationbucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 18:20:30 GMT
x-cos-copy-source: sourcebucket-1250000001.cos.ap-shanghai.myqcloud.com/example-%E8%85%BE%E8%AE%AF%E4%BA%91.jpg
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586542830;1586550030&q-key-time=1586542830;1586550030&q-header-list=content-length;date;host;x-cos-copy-source&q-url-param-list=&q-signature=f91b02809317616d993e14625996e416e08e****
Connection: close
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 219
Connection: close
Date: Fri, 10 Apr 2020 18:20:30 GMT
Server: tencent-cos
x-cos-request-id: NWU5MGI4ZWVfNzljMDBiMDlfMWM3MjlfMWQ1****

<?xml version="1.0" encoding="UTF-8"?>
<CopyObjectResult>
	<ETag>"ee8de918d05640145b18f70f4c3aa602"</ETag>
	<CRC64>16749565679157681890</CRC64>
	<LastModified>2020-04-10T18:20:30Z</LastModified>
</CopyObjectResult>
```

#### Example 2. Replacing source metadata

#### Request

```plaintext
PUT /exampleobject HTTP/1.1
Host: destinationbucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 18:20:41 GMT
x-cos-metadata-directive: Replaced
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=example.jpg
x-cos-copy-source: sourcebucket-1250000001.cos.ap-shanghai.myqcloud.com/example-%E8%85%BE%E8%AE%AF%E4%BA%91.jpg
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586542841;1586550041&q-key-time=1586542841;1586550041&q-header-list=content-disposition;content-length;content-type;date;host;x-cos-copy-source;x-cos-metadata-directive&q-url-param-list=&q-signature=aa2522c12b0ac82e29a812fca4334705cc96****
Connection: close
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 219
Connection: close
Date: Fri, 10 Apr 2020 18:20:41 GMT
Server: tencent-cos
x-cos-request-id: NWU5MGI4ZjlfYTZjMDBiMDlfN2Y1YV8xYjI4****

<?xml version="1.0" encoding="UTF-8"?>
<CopyObjectResult>
	<ETag>"ee8de918d05640145b18f70f4c3aa602"</ETag>
	<CRC64>16749565679157681890</CRC64>
	<LastModified>2020-04-10T18:20:41Z</LastModified>
</CopyObjectResult>
```

#### Example 3. Modifying object metadata

#### Request

```plaintext
PUT /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 18:20:52 GMT
x-cos-metadata-directive: Replaced
Cache-Control: max-age=86400
Content-Type: image/jpeg
x-cos-copy-source: examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586542852;1586550052&q-key-time=1586542852;1586550052&q-header-list=cache-control;content-length;content-type;date;host;x-cos-copy-source;x-cos-metadata-directive&q-url-param-list=&q-signature=1bcab704e474e46359d97c8c1fbb93642069****
Connection: close
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 219
Connection: close
Date: Fri, 10 Apr 2020 18:20:52 GMT
Server: tencent-cos
x-cos-request-id: NWU5MGI5MDRfNmRjMDJhMDlfZGNmYl8yMDVh****

<?xml version="1.0" encoding="UTF-8"?>
<CopyObjectResult>
	<ETag>"ee8de918d05640145b18f70f4c3aa602"</ETag>
	<CRC64>16749565679157681890</CRC64>
	<LastModified>2020-04-10T18:20:52Z</LastModified>
</CopyObjectResult>
```

#### Example 4. Transitioning an object

This example shows you how to use this API to transition an object from STANDARD to ARCHIVE storage class, or between STANDARD and STANDARD_IA storage classes. To transition an archived object into any other storage class using this API, first call the API [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) to restore it.

#### Request

```plaintext
PUT /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 18:21:02 GMT
x-cos-metadata-directive: Replaced
x-cos-storage-class: ARCHIVE
x-cos-copy-source: examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586542862;1586550062&q-key-time=1586542862;1586550062&q-header-list=content-length;date;host;x-cos-copy-source;x-cos-metadata-directive;x-cos-storage-class&q-url-param-list=&q-signature=8726a359b342cb1cace6945812ee8379c3ad****
Connection: close
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 219
Connection: close
Date: Fri, 10 Apr 2020 18:21:02 GMT
Server: tencent-cos
x-cos-request-id: NWU5MGI5MGVfN2RiNDBiMDlfMTk1MjhfMWZm****

<?xml version="1.0" encoding="UTF-8"?>
<CopyObjectResult>
	<ETag>"ee8de918d05640145b18f70f4c3aa602"</ETag>
	<CRC64>16749565679157681890</CRC64>
	<LastModified>2020-04-10T18:21:55Z</LastModified>
</CopyObjectResult>
```

#### Example 5. Copying an unencrypted object to a destination object encrypted with SSE-COS

#### Request

```plaintext
PUT /exampleobject HTTP/1.1
Host: destinationbucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 18:21:12 GMT
x-cos-server-side-encryption: AES256
x-cos-copy-source: sourcebucket-1250000001.cos.ap-shanghai.myqcloud.com/example-%E8%85%BE%E8%AE%AF%E4%BA%91.jpg
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586542872;1586550072&q-key-time=1586542872;1586550072&q-header-list=content-length;date;host;x-cos-copy-source;x-cos-server-side-encryption&q-url-param-list=&q-signature=ee94ef60dfb512882b368be12c6d47526433****
Connection: close
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 219
Connection: close
Date: Fri, 10 Apr 2020 18:21:13 GMT
Server: tencent-cos
x-cos-request-id: NWU5MGI5MTlfYmIwMmEwOV9hMmUxXzFkMDQ2****
x-cos-server-side-encryption: AES256

<?xml version="1.0" encoding="UTF-8"?>
<CopyObjectResult>
	<ETag>"ee8de918d05640145b18f70f4c3aa602"</ETag>
	<CRC64>16749565679157681890</CRC64>
	<LastModified>2020-04-10T18:21:13Z</LastModified>
</CopyObjectResult>
```

#### Example 6: Copying an unencrypted object to a destination object encrypted with SSE-KMS

#### Request

```plaintext
PUT /exampleobject HTTP/1.1
Host: destinationbucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 18:21:23 GMT
x-cos-server-side-encryption: cos/kms
x-cos-server-side-encryption-cos-kms-key-id: 48ba38aa-26c5-11ea-855c-52540085****
x-cos-server-side-encryption-context: eyJhdXRob3IiOiJmeXNudGlhbiIsImNvbXBhbnkiOiJUZW5jZW50In0=
x-cos-copy-source: sourcebucket-1250000001.cos.ap-shanghai.myqcloud.com/example-%E8%85%BE%E8%AE%AF%E4%BA%91.jpg
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586542883;1586550083&q-key-time=1586542883;1586550083&q-header-list=content-length;date;host;x-cos-copy-source;x-cos-server-side-encryption;x-cos-server-side-encryption-context;x-cos-server-side-encryption-cos-kms-key-id&q-url-param-list=&q-signature=28055a7cf07d7dde858fd924d6c0963b0c68****
Connection: close
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 219
Connection: close
Date: Fri, 10 Apr 2020 18:21:23 GMT
Server: tencent-cos
x-cos-request-id: NWU5MGI5MjNfMTliOTJhMDlfMjRiYThfMTdk****
x-cos-server-side-encryption: cos/kms
x-cos-server-side-encryption-cos-kms-key-id: 48ba38aa-26c5-11ea-855c-52540085****

<?xml version="1.0" encoding="UTF-8"?>
<CopyObjectResult>
	<ETag>"f69901ec9755a5defc29057e9ec69126"</ETag>
	<CRC64>16749565679157681890</CRC64>
	<LastModified>2020-04-10T18:22:16Z</LastModified>
</CopyObjectResult>
```

#### Example 7. Copying an object encrypted with SSE-C and replacing its key

#### Request

```plaintext
PUT /exampleobject HTTP/1.1
Host: destinationbucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 18:21:44 GMT
x-cos-copy-source-server-side-encryption-customer-algorithm: AES256
x-cos-copy-source-server-side-encryption-customer-key: MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=
x-cos-copy-source-server-side-encryption-customer-key-MD5: U5L61r7jcwdNvT7frmUG8g==
x-cos-server-side-encryption-customer-algorithm: AES256
x-cos-server-side-encryption-customer-key: MDEyMzQ1Njc4OWFiY2RlZjAxMjM0NTY3ODlhYmNkZWY=
x-cos-server-side-encryption-customer-key-MD5: hRasmdxgYDKV3nvbahU1MA==
x-cos-copy-source: sourcebucket-1250000001.cos.ap-shanghai.myqcloud.com/example-%E8%85%BE%E8%AE%AF%E4%BA%91.jpg
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586542904;1586550104&q-key-time=1586542904;1586550104&q-header-list=content-length;date;host;x-cos-copy-source;x-cos-copy-source-server-side-encryption-customer-algorithm;x-cos-copy-source-server-side-encryption-customer-key;x-cos-copy-source-server-side-encryption-customer-key-md5;x-cos-server-side-encryption-customer-algorithm;x-cos-server-side-encryption-customer-key;x-cos-server-side-encryption-customer-key-md5&q-url-param-list=&q-signature=dece274320f748bb0c736b13e5409cd1c35f****
Connection: close
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 219
Connection: close
Date: Fri, 10 Apr 2020 18:21:44 GMT
Server: tencent-cos
x-cos-request-id: NWU5MGI5MzhfZmFjODJhMDlfMTdlYzZfYmU1****
x-cos-server-side-encryption-customer-algorithm: AES256
x-cos-server-side-encryption-customer-key-MD5: hRasmdxgYDKV3nvbahU1MA==

<?xml version="1.0" encoding="UTF-8"?>
<CopyObjectResult>
	<ETag>"bf314b89d34119395d5610982d6581b1"</ETag>
	<CRC64>16749565679157681890</CRC64>
	<LastModified>2020-04-10T18:22:31Z</LastModified>
</CopyObjectResult>
```

#### Example 8. Decrypting an SSE-C encrypted object

#### Request

```plaintext
PUT /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 18:22:05 GMT
x-cos-metadata-directive: Replaced
x-cos-copy-source-server-side-encryption-customer-algorithm: AES256
x-cos-copy-source-server-side-encryption-customer-key: MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=
x-cos-copy-source-server-side-encryption-customer-key-MD5: U5L61r7jcwdNvT7frmUG8g==
x-cos-copy-source: examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586542925;1586550125&q-key-time=1586542925;1586550125&q-header-list=content-length;date;host;x-cos-copy-source;x-cos-copy-source-server-side-encryption-customer-algorithm;x-cos-copy-source-server-side-encryption-customer-key;x-cos-copy-source-server-side-encryption-customer-key-md5;x-cos-metadata-directive&q-url-param-list=&q-signature=b57bc8f6d666e9d722d30ad7d3ab442d9c43****
Connection: close
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 219
Connection: close
Date: Fri, 10 Apr 2020 18:22:05 GMT
Server: tencent-cos
x-cos-request-id: NWU5MGI5NGRfOWFjOTJhMDlfMjg2NDdfMTA0****

<?xml version="1.0" encoding="UTF-8"?>
<CopyObjectResult>
	<ETag>"ee8de918d05640145b18f70f4c3aa602"</ETag>
	<CRC64>16749565679157681890</CRC64>
	<LastModified>2020-04-10T18:22:58Z</LastModified>
</CopyObjectResult>
```

#### Example 9. Specifying the version ID of source object

#### Request

```plaintext
PUT /exampleobject HTTP/1.1
Host: destinationbucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Sat, 11 Apr 2020 17:51:35 GMT
x-cos-copy-source: sourcebucket-1250000001.cos.ap-shanghai.myqcloud.com/example.jpg?versionId=MTg0NDUxNTc0NDYyMjQ2MzUzMjQ
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586627495;1586634695&q-key-time=1586627495;1586634695&q-header-list=content-length;date;host;x-cos-copy-source&q-url-param-list=&q-signature=da80bd079b2c1fdb0dd961dea8568ee8d998****
Connection: close
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 219
Connection: close
Date: Sat, 11 Apr 2020 17:51:35 GMT
Server: tencent-cos
x-cos-copy-source-version-id: MTg0NDUxNTc0NDYyMjQ2MzUzMjQ
x-cos-request-id: NWU5MjAzYTdfMWZjMDJhMDlfNTE4N18zNGU2****

<?xml version="1.0" encoding="UTF-8"?>
<CopyObjectResult>
	<ETag>"ee8de918d05640145b18f70f4c3aa602"</ETag>
	<CRC64>16749565679157681890</CRC64>
	<LastModified>2020-04-11T17:51:35Z</LastModified>
</CopyObjectResult>
```

#### Example 10. Copying an object to a versioning-enabled bucket

#### Request

```plaintext
PUT /exampleobject HTTP/1.1
Host: destinationbucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Sat, 11 Apr 2020 17:51:56 GMT
x-cos-copy-source: sourcebucket-1250000001.cos.ap-shanghai.myqcloud.com/example.jpg
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586627516;1586634716&q-key-time=1586627516;1586634716&q-header-list=content-length;date;host;x-cos-copy-source&q-url-param-list=&q-signature=2c79d63b6078ace6fc9430fb6533b9a9ade1****
Connection: close
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 272
Connection: close
Date: Sat, 11 Apr 2020 17:51:56 GMT
Server: tencent-cos
x-cos-request-id: NWU5MjAzYmNfNjRiMDJhMDlfOTE3N18yYWI4****

<?xml version="1.0" encoding="UTF-8"?>
<CopyObjectResult>
	<ETag>"22e024392de860289f0baa7d6cf8a549"</ETag>
	<CRC64>11596229263574363878</CRC64>
	<LastModified>2020-04-11T17:51:56Z</LastModified>
	<VersionId>MTg0NDUxNTc0NDYxOTI4MzU0MDI</VersionId>
</CopyObjectResult>
```

