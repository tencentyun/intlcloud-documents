## Feature

This API (PUT Object - Copy) is used to create a copy of an object already exists in COS, i.e., copying an object from the source path (object key) to the destination path (object key). The recommended object size is from 1 MB to 5 GB. For objects over 5 GB, refer to [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287).

You can specify how metadata is processed during the copy process. By default, the metadata will be copied to the destination object. You can also choose not to copy the metadata information of the source object, and specify new metadata information in this API request. However, unless the storage type, access control list (ACL), and server-side encryption (SSE) are explicitly specified in this request, the destination object remains standard storage regardless of the processing method, the ACL of the destination bucket is inherited by default, and SSE will not be used.

You can use this API to move, rename, and copy the object metadata and create copies.

The requester of this API needs to have read permission to the copied object, or the copied object allows read permission (public read) to everyone, and write permission to the destination bucket.

>- An error may be returned when COS receives the copy request or is copying the object. If an error occurs before copying begins, a standard error response will be returned. If an error occurs during copying, `HTTP 200 OK` will be returned with the error as the response body, meaning that the `HTTP 200 OK` response includes both success and error. When using this API, pay attention to the content of the response body to determine whether the copy request is successful and process the result accordingly.

#### Versioning

- If versioning is enabled on the bucket where the source object resides, the latest version of the source object is copied by default. You can specify the versionId parameter in the x-cos-copy-source request header to copy the specified version.
- If versioning is enabled on the destination bucket, COS will automatically generate a unique version ID for the destination object.

## Request

#### Sample Request

```shell
PUT /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
x-cos-copy-source: <SourceBucketName-SourceAPPID>.cos.<SourceRegion>.myqcloud.com/<SourceObjectKey>
Content-Length: 0
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://cloud.tencent.com/document/product/436/7778) for details).

#### Request Parameters

This API does not use any request parameter.

#### Request Header

In addition to common request headers, this API also supports the following request headers. For more information on common request headers, see [Common Request Headers](https://cloud.tencent.com/document/product/436/7728).

| Name | Description | Type | Required |
| --- | --- | --- | --- |
| x-cos-copy-source | URL of the source object, where the object key needs to pass through URLEncode. The version of the source object can be specified by the versionId parameter, for example: <br>`sourcebucket-1250000001.cos.ap-shanghai.myqcloud.com/example-%E8%85%BE%E8%AE%AF%E4%BA%91.jpg`<br>或`sourcebucket-1250000001.cos.ap-shanghai.myqcloud.com/example-%E8%85%BE%E8%AE%AF%E4%BA%91.jpg?versionId=MTg0NDUxNzYzMDc0NDMzNDExOTc` | String | Yes |
| x-cos-metadata-directive | Whether to copy the metadata information of the source object. Enumerated values: Copy, Replaced, default is Copy. <br><li>If marked as Copy, the metadata information of the source object is copied. <li>If marked as Replaced, the metadata information in the request header of this request is used as the metadata information of the destination object. <br>If the destination and source objects are the same, that is, when the user tries to modify the metadata, it must be marked as Replaced | Enum | No |
| If-Unmodified-Since | If the object is modified after the specified time, execute on the copy operation, otherwise HTTP status code 412 (Precondition Failed) is returned | String | No |
| If-Unmodified-Since | If the object is not modified after the specified time, execute on the copy operation, otherwise HTTP status code 412 (Precondition Failed) is returned | String | No |
| If-Match | If the ETag of the object is the same as the specified value, execute on the copy operation, otherwise HTTP status code 412 (Precondition Failed) is returned | String | No |
| If-Match | If the ETag of the object is not the same as the specified value, execute on the copy operation, otherwise HTTP status code 412 (Precondition Failed) is returned | String | No |
| x-cos-storage-class | Storage class of the destination object, such as `STANDARD_IA` and `ARCHIVE`. Default value: `STANDARD`. For enumerated values, see [Storage Class](https://intl.cloud.tencent.com/document/product/436/30925). | Enum | No |

**Headers related to destination object metadata**

When copying an object, you can configure the metadata information of the destination object by specifying the following request headers. In this case, the request header x-cos-metadata-directive must be specified as Replaced.

| Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Type | Required |
| --- | --- | --- | --- |
| Cache-Control | Cache directives as defined in RFC 2616, which will be stored in the object metadata | String | No |
| Content-Disposition | File name as defined in RFC 2616, which will be stored in the object metadata | String | No |
| Content-Encoding | Encoding format as defined in RFC 2616, which will be stored in the object metadata | String | No |
| Expires | Cache expiration time as defined in RFC 2616, which will be stored in the object metadata | String | No |
| x-cos-meta-\* | Header suffix and information of user-defined metadata, which will be stored in the object metadata. Maximum size: 2 KB. <br>**Note:** User-defined metadata information can contain underscores (_), but header suffixes of user-defined metadata can only contain minus signs (-), not underscores | String | No |

**ACL-related headers**

When copying an object, you can configure the access permissions of the destination object by specifying the following request headers:

| Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Type | Required |
| --- | --- | --- | --- |
| x-cos-acl | Defines the access control list (ACL) attribute of the object. For enumerated values such as `default`, `private`, and `public-read`, see preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: default <br>**Note:** Currently, one ACL supports up to 1,000 entries. If you do not need access control for the object, configure this parameter as `default` or leave it blank, and bucket permissions will be inherited by default | Enum | No |
| x-cos-grant-read | Allows grantee to read the object; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | String | No |
| x-cos-grant-read-acp | Allows grantee to read the ACL of the object; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | String | No |
| x-cos-grant-write-acp | Allows grantee to write to the ACL of the object; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | String | No |
| x-cos-grant-full-control | Grants a user full permission to operate on the object; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | String | No |

**Headers related to server-side encryption (SSE) for source object**

If the source object uses server-side encryption method SSE-C, specify the following request headers to decrypt the object:

| Name | Description | Type | Required |
| --- | --- | --- | --- |
| x-cos-server-side-encryption-customer-algorithm | Server-side encryption algorithm; currently only AES256 is supported | String | Yes |
| x-cos-server-side-encryption-customer-key | Base64-encoded server-side encryption key. <br>For example, `MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=` | string | Yes |
| x-cos-server-side-encryption-customer-key-MD5  | Base64-encoded MD5 hash of the server-side encryption key. <br>For example, `U5L61r7jcwdNvT7frmUG8g==` | string | Yes |

**Headers related to server-side encryption (SSE) for destination object**

Server-side encryption can be used during object copying. For more information, see [Server side encryption headers](https://cloud.tencent.com/document/product/436/7728#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Request Body

This API does not have a request body.

## Response

#### Response Headers

In addition to common response headers, this API also returns the following response headers. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

**Versioning-related Headers**

When the version ID of the source object is specified, the following response headers are returned:

| Name | Description | Type |
| --- | --- | --- |
| x-cos-copy-source-version-id | The version ID of Source object | String |

**Headers related to server-side encryption (SSE)**

If server-side encryption is used during object copying, this API will return headers used specifically for server-side encryption. For more information. see [Server side encryption headers](https://cloud.tencent.com/document/product/436/7729#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Response Body

A successful query returns the **application/xml** data, which includes information on the object’s copying results.

```shell
<?xml version="1.0" encoding="UTF-8" ?>
<CopyObjectResult>
	<ETag>string</ETag>
	<LastModified>date</LastModified>
	<VersionId>string</VersionId>
</CopyObjectResult>
```

The nodes are described in details below:

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
CopyObjectResult | None | Save all information about PUT Object-Copy result | Container |

**Content of container’s node CopyObjectResult:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| ETag | CopyObjectResult | Entity Tag of an object, which is an information tag that identifies the content of the object when it is created. The tag can be used to check whether the content of the object has changed. <br>For example, the header `8e0b617ca298a564c3331da28dcb50df` does not necessarily return the MD5 value of the object, but varies depending on how the object is uploaded and encrypted | String |
| LastModified | ListBucketResult.Contents | Last modified time of an object in ISO8601 format, such as `2019-05-24T10:56:40Z` | date |
VersionId | CopyObjectResult | The version ID of the object, which is returned only if the destination bucket has versioning enabled | String |

#### Error Codes

There are no special error messages for this API. For all error messages, see [Error Codes](https://cloud.tencent.com/document/product/436/7730).

## Examples

The response of this API uses Transfer-Encoding: chunked encoding by default. Note that for the convenience of reading, use cases in this document are displayed without Transfer-Encoding. During use, different languages and libraries can automatically process this encoding form. For more information, refer to language- and library-related documents.

#### Example 1. Simple example

#### Request

```shell
PUT /exampleobject HTTP/1.1
Host: destinationbucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 06 Sep 2019 03:17:42 GMT
x-cos-copy-source: sourcebucket-1250000001.cos.ap-shanghai.myqcloud.com/example-%E8%85%BE%E8%AE%AF%E4%BA%91.jpg
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1558882298;1558889498&q-key-time=1558882298;1558889498&q-header-list=content-length;date;host&q-url-param-list=&q-signature=c25fd640274a6da2318935ceebfbcfba4598****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 181
Connection: close
Date: Fri, 06 Sep 2019 03:17:43 GMT
Server: tencent-cos
x-cos-request-id: NWQ3MWNmZDdfMzdiMDJhMDlfNDA5MV9mMDU1****

<?xml version="1.0" encoding="UTF-8" ?>
<CopyObjectResult>
	<ETag>"5603c4d142301f2a802d68e2078ed615"</ETag>
	<LastModified>2019-09-06T03:17:47Z</LastModified>
</CopyObjectResult>
```

#### Example 2: Replacing metadata when copying

#### Request

```shell
PUT /exampleobject HTTP/1.1
Host: destinationbucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 06 Sep 2019 08:00:42 GMT
x-cos-metadata-directive: Replaced
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=example.jpg
x-cos-copy-source: sourcebucket-1250000001.cos.ap-shanghai.myqcloud.com/example-%E8%85%BE%E8%AE%AF%E4%BA%91.jpg
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1561109075;1561116275&q-key-time=1561109075;1561116275&q-header-list=content-length;content-md5;content-type;date;host;x-cos-server-side-encryption&q-url-param-list=&q-signature=3e21f7fba71e04d5c7f3aee7ff39753b240a****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 181
Connection: close
Date: Fri, 06 Sep 2019 08:00:43 GMT
Server: tencent-cos
x-cos-request-id: NWQ3MjEyMmJfNDliMDJhMDlfNzY0MF9mNjQ1****

<?xml version="1.0" encoding="UTF-8" ?>
<CopyObjectResult>
	<ETag>"5603c4d142301f2a802d68e2078ed615"</ETag>
	<LastModified>2019-09-06T08:00:19Z</LastModified>
</CopyObjectResult>
```

#### Example 3: Modifying object metadata

#### Request

```shell
PUT /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 06 Sep 2019 08:00:43 GMT
x-cos-metadata-directive: Replaced
Cache-Control: max-age=86400
Content-Type: image/jpeg
x-cos-copy-source: examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1561109075;1561116275&q-key-time=1561109075;1561116275&q-header-list=content-length;content-md5;content-type;date;host;x-cos-server-side-encryption&q-url-param-list=&q-signature=3e21f7fba71e04d5c7f3aee7ff39753b240a****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 181
Connection: close
Date: Fri, 06 Sep 2019 08:00:44 GMT
Server: tencent-cos
x-cos-request-id: NWQ3MjEyMmNfYjNjMjJhMDlfYjk4NV9mNjRk****

<?xml version="1.0" encoding="UTF-8" ?>
<CopyObjectResult>
	<ETag>"b62e10bcab55a88240bd9c436cffdcf9"</ETag>
	<LastModified>2019-09-06T08:00:49Z</LastModified>
</CopyObjectResult>
```

#### Example 4: Modifying object storage type

This example shows how to convert the object from standard storage to archived storage. This method is also suitable for the conversion between standard storage and infrequent access storage. If you want to convert the object in archived storage to other storage types, restore it first via [POST Object restore](https://cloud.tencent.com/document/product/436/12633) before using this API to request conversion of the storage type.

#### Request

```shell
PUT /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 02 Jan 2020 09:39:27 GMT
x-cos-metadata-directive: Replaced
x-cos-storage-class: ARCHIVE
x-cos-copy-source: examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1560760212;1560767412&q-key-time=1560760212;1560767412&q-header-list=content-length;date;host;x-cos-acl;x-cos-grant-read-acp;x-cos-grant-write&q-url-param-list=acl&q-signature=5b10c6ea4e6c9630c085e1f85476c76d8c4e****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 181
Connection: close
Date: Thu, 02 Jan 2020 09:39:27 GMT
Server: tencent-cos
x-cos-request-id: NWUwZGJhNGZfNDVjODJhMDlfNjk4Yl8xYzNk****

<?xml version="1.0" encoding="UTF-8" ?>
<CopyObjectResult>
	<ETag>"b62e10bcab55a88240bd9c436cffdcf9"</ETag>
	<LastModified>2020-01-02T09:37:11Z</LastModified>
</CopyObjectResult>
```

#### Example 5: Copying an unencrypted object to a destination object encrypted with SSE-COS

#### Request

```shell
PUT /exampleobject HTTP/1.1
Host: destinationbucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 06 Sep 2019 08:00:44 GMT
x-cos-server-side-encryption: AES256
x-cos-copy-source: sourcebucket-1250000001.cos.ap-shanghai.myqcloud.com/example-%E8%85%BE%E8%AE%AF%E4%BA%91.jpg
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1561109075;1561116275&q-key-time=1561109075;1561116275&q-header-list=content-length;content-md5;content-type;date;host;x-cos-server-side-encryption&q-url-param-list=&q-signature=3e21f7fba71e04d5c7f3aee7ff39753b240a****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 181
Connection: close
Date: Fri, 06 Sep 2019 08:00:45 GMT
Server: tencent-cos
x-cos-request-id: NWQ3MjEyMmNfMjNhZjJhMDlfNjUxYV9mMzE2****
x-cos-server-side-encryption: AES256

<?xml version="1.0" encoding="UTF-8" ?>
<CopyObjectResult>
	<ETag>"5603c4d142301f2a802d68e2078ed615"</ETag>
	<LastModified>2019-09-06T08:00:50Z</LastModified>
</CopyObjectResult>
```

#### Example 6: Copying an unencrypted object to a destination object encrypted with SSE-KMS

#### Request

```shell
PUT /exampleobject HTTP/1.1
Host: destinationbucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 02 Jan 2020 09:39:44 GMT
x-cos-server-side-encryption: cos/kms
x-cos-server-side-encryption-cos-kms-key-id: 48ba38aa-26c5-11ea-855c-52540085****
x-cos-server-side-encryption-context: eyJhdXRob3IiOiJmeXNudGlhbiIsImNvbXBhbnkiOiJUZW5jZW50In0=
x-cos-copy-source: sourcebucket-1250000001.cos.ap-shanghai.myqcloud.com/example-%E8%85%BE%E8%AE%AF%E4%BA%91.jpg
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1561109078;1561116278&q-key-time=1561109078;1561116278&q-header-list=content-length;content-md5;content-type;date;host;x-cos-server-side-encryption-customer-algorithm;x-cos-server-side-encryption-customer-key;x-cos-server-side-encryption-customer-key-md5&q-url-param-list=&q-signature=d04a5d70af5f08c7db4f89a91628a7eacf90****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 181
Connection: close
Date: Thu, 02 Jan 2020 09:39:45 GMT
Server: tencent-cos
x-cos-request-id: NWUwZGJhNjBfZjhjODBiMDlfMWFkN2VfMzZh****
x-cos-server-side-encryption: cos/kms
x-cos-server-side-encryption-cos-kms-key-id: 48ba38aa-26c5-11ea-855c-52540085****

<?xml version="1.0" encoding="UTF-8" ?>
<CopyObjectResult>
	<ETag>"8612144fec2e2e271856b1c49c4b408f"</ETag>
	<LastModified>2020-01-02T09:37:30Z</LastModified>
</CopyObjectResult>
```

#### Example 7: Copying object encrypted with SSE-C and replace key

#### Request

```shell
PUT /exampleobject HTTP/1.1
Host: destinationbucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 06 Sep 2019 08:03:34 GMT
x-cos-copy-source-server-side-encryption-customer-algorithm: AES256
x-cos-copy-source-server-side-encryption-customer-key: MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=
x-cos-copy-source-server-side-encryption-customer-key-MD5: U5L61r7jcwdNvT7frmUG8g==
x-cos-server-side-encryption-customer-algorithm: AES256
x-cos-server-side-encryption-customer-key: MDEyMzQ1Njc4OWFiY2RlZjAxMjM0NTY3ODlhYmNkZWY=
x-cos-server-side-encryption-customer-key-MD5: hRasmdxgYDKV3nvbahU1MA==
x-cos-copy-source: sourcebucket-1250000001.cos.ap-shanghai.myqcloud.com/example-%E8%85%BE%E8%AE%AF%E4%BA%91.jpg
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1567757014;1567764214&q-key-time=1567757014;1567764214&q-header-list=content-length;date;host;x-cos-copy-source;x-cos-copy-source-server-side-encryption-customer-algorithm;x-cos-copy-source-server-side-encryption-customer-key;x-cos-copy-source-server-side-encryption-customer-key-md5;x-cos-server-side-encryption-customer-algorithm;x-cos-server-side-encryption-customer-key;x-cos-server-side-encryption-customer-key-md5&q-url-param-list=&q-signature=5c6409efce0bd4a4bfdbc546245f98d6174e****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 181
Connection: close
Date: Fri, 06 Sep 2019 08:03:35 GMT
Server: tencent-cos
x-cos-request-id: NWQ3MjEyZDdfYjliYjBiMDlfMTc0ZjVfZmI1****
x-cos-server-side-encryption-customer-algorithm: AES256
x-cos-server-side-encryption-customer-key-MD5: hRasmdxgYDKV3nvbahU1MA==

<?xml version="1.0" encoding="UTF-8" ?>
<CopyObjectResult>
	<ETag>"badc400de3047d9f3148ecb54900ba05"</ETag>
	<LastModified>2019-09-06T08:03:11Z</LastModified>
</CopyObjectResult>
```

#### Example 8: Modifying object encrypted with SSE-C to non-encrypted

#### Request

```shell
PUT /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 06 Sep 2019 08:33:32 GMT
x-cos-metadata-directive: Replaced
x-cos-copy-source-server-side-encryption-customer-algorithm: AES256
x-cos-copy-source-server-side-encryption-customer-key: MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=
x-cos-copy-source-server-side-encryption-customer-key-MD5: U5L61r7jcwdNvT7frmUG8g==
x-cos-copy-source: examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1561109078;1561116278&q-key-time=1561109078;1561116278&q-header-list=content-length;content-md5;content-type;date;host;x-cos-server-side-encryption-customer-algorithm;x-cos-server-side-encryption-customer-key;x-cos-server-side-encryption-customer-key-md5&q-url-param-list=&q-signature=d04a5d70af5f08c7db4f89a91628a7eacf90****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 181
Connection: close
Date: Fri, 06 Sep 2019 08:33:32 GMT
Server: tencent-cos
x-cos-request-id: NWQ3MjE5ZGNfMjljOTBiMDlfMjQ1OWJfZmMw****

<?xml version="1.0" encoding="UTF-8" ?>
<CopyObjectResult>
	<ETag>"b62e10bcab55a88240bd9c436cffdcf9"</ETag>
	<LastModified>2019-09-06T08:33:41Z</LastModified>
</CopyObjectResult>
```

#### Example 9: Specifying the version of the source object

#### Request

```shell
PUT /exampleobject HTTP/1.1
Host: destinationbucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 06 Sep 2019 10:37:46 GMT
x-cos-copy-source: sourcebucket-1250000001.cos.ap-shanghai.myqcloud.com/example-%E8%85%BE%E8%AE%AF%E4%BA%91.jpg?versionId=MTg0NDUxNzYzMDc0NDMzNDExOTc
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1560760213;1560767413&q-key-time=1560760213;1560767413&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=acl&q-signature=70f96b91823f3715905df125d96fe447554e****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 181
Connection: close
Date: Fri, 06 Sep 2019 10:37:47 GMT
Server: tencent-cos
x-cos-copy-source-version-id: MTg0NDUxNzYzMDc0NDMzNDExOTc
x-cos-request-id: NWQ3MjM2ZmFfZjhjMDBiMDlfOTliZF9mYmNi****

<?xml version="1.0" encoding="UTF-8" ?>
<CopyObjectResult>
	<ETag>"5603c4d142301f2a802d68e2078ed615"</ETag>
	<LastModified>2019-09-06T10:37:48Z</LastModified>
</CopyObjectResult>
```

#### Example 10: Copying object to a bucket with versioning enabled

#### Request

```shell
PUT /exampleobject HTTP/1.1
Host: destinationbucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 06 Sep 2019 10:42:45 GMT
x-cos-copy-source: sourcebucket-1250000001.cos.ap-shanghai.myqcloud.com/example-%E8%85%BE%E8%AE%AF%E4%BA%91.jpg
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1558882298;1558889498&q-key-time=1558882298;1558889498&q-header-list=content-length;date;host&q-url-param-list=&q-signature=c25fd640274a6da2318935ceebfbcfba4598****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 234
Connection: close
Date: Fri, 06 Sep 2019 10:42:46 GMT
Server: tencent-cos
x-cos-request-id: NWQ3MjM4MjVfN2RiZTBiMDlfNmI0ZF9mOTA2****

<?xml version="1.0" encoding="UTF-8" ?>
<CopyObjectResult>
	<ETag>"ee8de918d05640145b18f70f4c3aa602"</ETag>
	<LastModified>2019-09-06T10:42:50Z</LastModified>
	<VersionId>MTg0NDUxNzYzMDcxNDM2MDk2MzA</VersionId>
</CopyObjectResult>
```
