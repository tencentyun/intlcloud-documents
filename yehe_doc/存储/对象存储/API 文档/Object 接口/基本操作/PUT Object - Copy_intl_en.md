## Feature description

This API is used to create a copy of an object that already exists in COS, i.e., copying an object from the source path (object key) to the destination path (object key). The recommended object size is from 1 MB to 5 GB. For objects over 5 GB, refer to [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287).

You can specify how metadata is processed during the copy process. By default, the metadata will be copied to the destination object. You can also choose not to copy the metadata of the source object, and instead can specify new metadata in the API request. However, unless the storage type, access control list (ACL), and server-side encryption (SSE) are explicitly specified in the request, then, regardless of the processing method, the storage type of the destination object will remain as standard, the ACL of the destination bucket will be inherited by default, and SSE will not be used.

You can use this API to move, rename, and copy object metadata and create copies.

To request this API, you need to have read permission for the object that you want to copy, or the object must have public read permission enabled (i.e., everyone has read permission for the object), and you must have write permission for the destination bucket.

> 
>
> - An error may be returned when COS receives the copy request or is copying the object. If an error occurs before copying begins, a standard error response will be returned. If an error occurs during copying, `HTTP 200 OK` will be returned with the error as the response body, meaning that the `HTTP 200 OK` response can include both success and error information. When using this API, pay attention to the content of the response body to determine whether the copy request was successful and process the result accordingly.
> - The `MAZ_STANDARD` storage class only supports replication into the exact same class rather than standard storage, low frequency, or archive storage classes.

#### Versioning

- If versioning is enabled on the bucket where the source object resides, the latest version of the source object is copied by default. You can specify the versionId parameter in the `x-cos-copy-source` request header to copy a specified version.
- If versioning is enabled on the destination bucket, COS will automatically generate a unique version ID for the destination object.

## Request

#### Sample request

```shell
PUT /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
x-cos-copy-source: <SourceBucketName-SourceAPPID>.cos.<SourceRegion>.myqcloud.com/<SourceObjectKey>
Content-Length: 0
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

#### Request parameters

This API does not use any request parameters.

#### Request headers

In addition to common request headers, this API also supports the following request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

| Name | Description | Type | Required |
| ------------------------------------- | ------------------------------------------------------------ | ------ | -------- |
| x-cos-copy-source | URL of the source object, where the object key needs to be URLEncoded. The version of the source object can be specified through the versionId parameter, such as <br>`sourcebucket-1250000001.cos.ap-shanghai.myqcloud.com/example-%E8%85%BE%E8%AE%AF%E4%BA%91.jpg`<br>, or `sourcebucket-1250000001.cos.ap-shanghai.myqcloud.com/example-%E8%85%BE%E8%AE%AF%E4%BA%91.jpg?versionId=MTg0NDUxNzYzMDc0NDMzNDExOTc`. | string | Yes |
| x-cos-metadata-directive | Specifies whether to copy the metadata information of the source object. Enumerated values: `Copy`, `Replaced`, the default value is `Copy`.<br><li>If marked as `Copy`, the metadata information of the source object is copied. <li>If marked as `Replaced`, the metadata information in the request header is used as the metadata information of the destination object. <br>If the destination and source objects are the same and you want to modify the metadata, it must be marked as `Replaced`. | Enum | No |
| x-cos-copy-source-If-Modified-Since    | If the object is modified after the specified time, the copy operation will be executed, otherwise an HTTP `412` status code (Precondition Failed) is returned. | string | No |
| x-cos-copy-source-If-Unmodified-Since | If the object is not modified after the specified time, the copy operation will be executed, otherwise an HTTP `412` status code (Precondition Failed) is returned. | string | No |
| x-cos-copy-source-If-Match | If the ETag of the object is the same as the specified value, the copy operation will be exectued, otherwise an HTTP `412` status code (Precondition Failed) is returned. | string | No |
| x-cos-copy-source-If-None-Match | If the ETag of the object is not the same as the specified value, the copy operation will be executed, otherwise an HTTP `412` status code (Precondition Failed) is returned. | string | No |
| x-cos-storage-class | Storage class of the destination object, such as `STANDARD_IA` and `ARCHIVE`. Default value: `STANDARD`. For the enumerated values, see [Storage Class](https://intl.cloud.tencent.com/document/product/436/30925). | Enum | No |

**Headers related to destination object metadata**

When copying an object, you can configure the metadata information of the destination object by specifying the following request headers. In this case, the request header `x-cos-metadata-directive` must be specified as `Replaced`.

| Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Type | Required |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------ | -------- |
| Cache-Control | Cache directives as defined in RFC 2616, which will be stored in the object metadata | string | No |
| Content-Disposition | File name as defined in RFC 2616, which will be stored in the object metadata | string | No |
| Content-Encoding | Encoding format as defined in RFC 2616, which will be stored in the object metadata | string | No |
| Expires | The cache expiration time as defined in RFC 2616, which will be saved in the object metadata | string | No |
| x-cos-meta-\* | Contains user-defined metatdata and header suffixes, which will be stored in the object metadata. Maximum size: 2 KB.<br>**Note:** User-defined metadata can contain underscores (_), but the header suffixes of user-defined metadata can only contain minus signs (-), not underscores | string | No |

**ACL-related headers**

When copying an object, you can configure the access permissions of the destination object by specifying the following request headers:

| Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Type | Required |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------ | -------- |
| x-cos-acl | Defines the access control list (ACL) attribute of the object. For enumerated values such as `default`, `private`, and `public-read`, see the preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: default<br>**Note:** Currently, one ACL supports up to 1,000 entries. If you do not need access control for the object, configure this parameter as `default` or leave it blank, and the object will inherit the permissions of its bucket | Enum | No |
| x-cos-grant-read | Grants a user read permission for an object; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use a comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | string | No |
| x-cos-grant-read-acp | Grants a user read permission for the ACL of an object; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use a comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | string | No |
| x-cos-grant-write-acp | Grants a user write permission for the ACL of an object; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use a comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | string | No |
| x-cos-grant-full-control | Grants a user full permission to operate on an object; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use a comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | string | No |

**Headers related to server-side encryption (SSE) of the source object**

If the source object uses the server-side encryption method, `SSE-C`, specify the following request headers to decrypt the object:

| Name                                                        | Description                                                         | Type   | Required&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;                          |
| ----------------------------------------------------------- | ------------------------------------------------------------ | ------ | ----------------------------------- |
| x-cos-server-side-encryption-customer-algorithm | Server-side encryption algorithm; currently only AES256 is supported. | string | Required if the source object uses SSE-C. |
| x-cos-server-side-encryption-customer-key | Base64-encoded server-side encryption key. such as<code>MDEyMzQ1Njc4OUFCQ<br>0RFRjAxMjM0NTY3ODlBQkNERUY=</code> | string | Required if the source object uses SSE-C |
| x-cos-server-side-encryption-customer-key-MD5  | Base64-encoded MD5 hash of the server-side encryption key, such as<br>`U5L61r7jcwdNvT7frmUG8g==` | string | Required if the source object uses SSE-C |

**Headers related to server-side encryption (SSE) of the destination object**

Server-side encryption can be used during object copying. For more information, see [Server side encryption headers](https://intl.cloud.tencent.com/document/product/436/7728#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Request body

This API does not have a request body.

## Response

#### Response headers

In addition to common response headers, this API also returns the following response headers. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

**Versioning-related headers**

When the version ID of the source object is specified, the following response headers are returned:

| Name | Description | Type |
| ---------------------------- | --------------- | ------ |
| x-cos-copy-source-version-id | Version ID of the source object | string |

**Headers related to server-side encryption (SSE)**

If server-side encryption is used during object copying, this API will return headers used specifically for server-side encryption. For more information, see [Server side encryption headers](https://intl.cloud.tencent.com/document/product/436/7729#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Response body

A successful query returns the **application/xml** data, which includes information on the object’s copying results.

```shell
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
| CopyObjectResult | None | Saves all information about the `PUT Object-Copy` result | Container |

**Content of container node CopyObjectResult:**

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ---------------- | ------------------------------------------------------------ | ------ |
| ETag | CopyObjectResult | ETag of the object; this is a tag that identifies the content of an object when it is created. The tag can be used to check whether the content of an object has changed.<br>For example, the header `8e0b617ca298a564c3331da28dcb50df` does not necessarily return the MD5 value of the object, but varies depending on how the object is uploaded and encrypted. | string |
| CRC64 | CopyObjectResult | CRC64 value of the object. For more information, see [CRC64 Check](https://intl.cloud.tencent.com/document/product/436/34078). | number |
| LastModified | CopyObjectResult | Last modified time of the object in ISO8601 format, such as `2019-05-24T10:56:40Z` | date |
VersionId | CopyObjectResult | The version ID of the object, which is returned only if the destination bucket has versioning enabled | string |

#### Error codes

There are no special error messages for this API. For all error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Use Cases

The response of this API uses `Transfer-Encoding: chunked` encoding by default. Note that for the convenience of reading, use cases in this document are displayed without Transfer-Encoding. During use, different languages and libraries can automatically process this encoding form. For more information, refer to language- and library-related documents.

#### Example 1. Simple example

#### Request

```shell
PUT /exampleobject HTTP/1.1
Host: destinationbucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 18:20:30 GMT
x-cos-copy-source: sourcebucket-1250000001.cos.ap-shanghai.myqcloud.com/example-%E8%85%BE%E8%AE%AF%E4%BA%91.jpg
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586542830;1586550030&q-key-time=1586542830;1586550030&q-header-list=content-length;date;host;x-cos-copy-source&q-url-param-list=&q-signature=f91b02809317616d993e14625996e416e08e****
Connection: close
```

#### Response

```shell
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

#### Example 2. Replacing metadata when copying

#### Request

```shell
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

```shell
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

```shell
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

```shell
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

#### Example 4. Modifying the object storage type

This example shows how to convert the object from standard storage to archived storage. This method is also suitable for the conversion between standard storage and infrequent access storage. If you want to convert an object in archive storage to a different storage type, you must restore it first via [POST Object restore] (https://intl.cloud.tencent.com/document/product/436/12633) before using this API to request a conversion of the storage type.

#### Request

```shell
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

```shell
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

```shell
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

```shell
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

#### Example 6. Copying an unencrypted object to a destination object encrypted with SSE-KMS

#### Request

```shell
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

```shell
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

#### Example 7. Copying object encrypted with SSE-C and replace key

#### Request

```shell
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

```shell
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

#### Example 8. Modifying an object encrypted with SSE-C to non-encrypted

#### Request

```shell
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

```shell
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

#### Example 9. Specifying the version of the source object

#### Request

```shell
PUT /exampleobject HTTP/1.1
Host: destinationbucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Sat, 11 Apr 2020 17:51:35 GMT
x-cos-copy-source: sourcebucket-1250000001.cos.ap-shanghai.myqcloud.com/example.jpg?versionId=MTg0NDUxNTc0NDYyMjQ2MzUzMjQ
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586627495;1586634695&q-key-time=1586627495;1586634695&q-header-list=content-length;date;host;x-cos-copy-source&q-url-param-list=&q-signature=da80bd079b2c1fdb0dd961dea8568ee8d998****
Connection: close
```

#### Response

```shell
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

#### Example 10. Copying object to a bucket with versioning enabled

#### Request

```shell
PUT /exampleobject HTTP/1.1
Host: destinationbucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Sat, 11 Apr 2020 17:51:56 GMT
x-cos-copy-source: sourcebucket-1250000001.cos.ap-shanghai.myqcloud.com/example.jpg
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586627516;1586634716&q-key-time=1586627516;1586634716&q-header-list=content-length;date;host;x-cos-copy-source&q-url-param-list=&q-signature=2c79d63b6078ace6fc9430fb6533b9a9ade1****
Connection: close
```

#### Response

```shell
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

