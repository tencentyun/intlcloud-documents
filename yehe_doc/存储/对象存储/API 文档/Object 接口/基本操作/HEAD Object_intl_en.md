## Feature

This API is used to determine whether the specified object exists and whether you have the permission to access it. You can use this API to get the object metadata if you can access it. To make this request, you need to have Read access to the object or the object allows Public Read.

#### Versioning

With versioning enabled, you can specify the `versionId` request parameter to get the metadata of a specific version of the object. If the version ID you specify corresponds to a delete marker, HTTP status code 404 (Not Found) will be returned. If no version ID is specified, the metadata of the latest version will be returned.

## Request

#### Sample Request

```shell
HEAD /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://cloud.tencent.com/document/product/436/7778) for details).

#### Request Parameters

| Name | Description | Type | Required |
| --- | --- | --- | --- |
| versionId | Specifies the version ID of the object if versioning is enabled; if this parameter is not specified, the latest version will be queried | string | No |

#### Request Header

In addition to common request headers, this API also supports the following request headers. For more information on common request headers, see [Common Request Headers](https://cloud.tencent.com/document/product/436/7728).

| Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Type | Required |
| --- | --- | --- | --- |
| If-Modified-Since | If the object is modified after the specified time, HTTP status code 200 (OK) will be returned; otherwise, HTTP status code 304 (Not Modified) will be returned | string | No |
| If-Unmodified-Since | If the object is not modified after the specified time, HTTP status code 200 (OK) will be returned; otherwise, HTTP status code 412 (Precondition Failed) will be returned | string | No |
| If-Match | If the `ETag` of the object is the same as the specified value, HTTP status code 200 (OK) will be returned; otherwise, HTTP status code 412 (Precondition Failed) will be returned | string | No |
| If-None-Match | If the `ETag` of the object is different from the specified value, HTTP status code 200 (OK) will be returned; otherwise, HTTP status code 304 (Not Modified) will be returned | string | No |

**Server-side Encryption Headers**

If server-side encryption is used for the specified object and the encryption method is SSE-C, you will need to specify the headers related to server-side encryption to decrypt the object. For more information, see [Server-side Encryption Headers](https://intl.cloud.tencent.com/document/product/436/7728#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Request Body

This API does not have a request body.

## Response

#### Response Headers

In addition to common response headers, this API also returns the following response headers. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

| Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Type |
| --- | --- | --- |
| Cache-Control | Cache directives as defined in RFC 2616, which will be returned only if it is contained in the object metadata | string |
| Content-Disposition | Filename as defined in RFC 2616, which will be returned only if it is contained in the object metadata | string |
| Content-Encoding | Encoding format as defined in RFC 2616, which will be returned only if it is contained in the object metadata | string |
| Expires | Cache expiration time as defined in RFC 2616, which will be returned only if it is contained in the object metadata | string |
| x-cos-meta-\* | Header suffix and information of the user-defined metadata | string |
| x-cos-storage-class | Object storage class, such as `STANDARD_IA` and `ARCHIVE`. For enumerated values, see [Storage Class](https://intl.cloud.tencent.com/document/product/436/30925). This header will be returned only if the storage class of the object is not `STANDARD` | Enum |

#### Archived Object-related Headers

If the storage class of the object is `ARCHIVE` and `POST Object restore` has been used to restore it, the following response headers will be returned:

| Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Type |
| --- | --- | --- |
| x-cos-restore | Indicates the status of the restoration process:<br><li>If the restoration is ongoing, the value of the response header will be `ongoing-request="true"`<li>If the object has already been restored, the response header will include the time when COS will delete the temporary copy, e.g. `ongoing-request="false", expiry-date="Tue, 19 Nov 2019 16:00:00 GMT"` | string
| x-cos-restore-status | This parameter will be returned if the restoration is ongoing, indicating what restoration mode is used and when the restoration is requested, e.g. `tier="bulk"; request-date="Mon, 18 Nov 2019 09:34:50 GMT"`. For more information on restoration modes, see [POST Object restore](https://cloud.tencent.com/document/product/436/12633#.E8.AF.B7.E6.B1.82) | string

**Versioning-related Headers**

If the target object is from a bucket where versioning is enabled, the following response headers will be returned:

| Name | Description | Type |
| --- | --- | --- |
| x-cos-version-id | Object version ID | string |

**Server-side Encryption Headers**

If server-side encryption is used for the specified object, this API will return the server-side encryption headers. For more information, see [Server-side Encryption Headers](https://intl.cloud.tencent.com/document/product/436/7729#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Response Body

The response body of this API is empty.

#### Error Codes

There are no special error messages for this API. For all error messages, see [Error Codes](https://cloud.tencent.com/document/product/436/7730).

## Examples

#### Example 1. Simple example (versioning not enabled)

#### Request

```shell
HEAD /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 09 Aug 2019 10:21:01 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1565346061;1565353261&q-key-time=1565346061;1565353261&q-header-list=date;host&q-url-param-list=&q-signature=82f401cf54cd6ad0331d1c0b8c827bf8f2f9****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 13
Connection: close
Date: Fri, 09 Aug 2019 10:21:01 GMT
ETag: "b62e10bcab55a88240bd9c436cffdcf9"
Last-Modified: Fri, 09 Aug 2019 10:20:56 GMT
Server: tencent-cos
x-cos-request-id: NWQ0ZDQ5MGRfNmRjMDJhMDlfOThjMl8xNzE2****
```

#### Example 2. Using server-side encryption SSE-COS

#### Request

```shell
HEAD /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 03 Jan 2020 03:15:45 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1578021345;1578028545&q-key-time=1578021345;1578028545&q-header-list=date;host&q-url-param-list=&q-signature=fce853999e9887979144772897191918f222****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 13
Connection: close
Date: Fri, 03 Jan 2020 03:15:45 GMT
ETag: "b62e10bcab55a88240bd9c436cffdcf9"
Last-Modified: Fri, 03 Jan 2020 03:15:38 GMT
Server: tencent-cos
x-cos-request-id: NWUwZWIxZTFfNTZiODJhMDlfMWI3ZDVfMTE4****
x-cos-server-side-encryption: AES256
```

#### Example 3. Using server-side encryption SSE-KMS

#### Request

```shell
HEAD /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 03 Jan 2020 03:15:52 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1578021352;1578028552&q-key-time=1578021352;1578028552&q-header-list=date;host&q-url-param-list=&q-signature=85c65724701a653ec6f539b01497ca77b112****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 13
Connection: close
Date: Fri, 03 Jan 2020 03:15:52 GMT
ETag: "e5177e1f7894ababc290c23851e6b2a7"
Last-Modified: Fri, 03 Jan 2020 03:15:46 GMT
Server: tencent-cos
x-cos-request-id: NWUwZWIxZThfNjRiODJhMDlfMTU1NjFfMTFk****
x-cos-server-side-encryption: cos/kms
x-cos-server-side-encryption-cos-kms-key-id: 48ba38aa-26c5-11ea-855c-52540085****
```

#### Example 4. Using server-side encryption SSE-C

#### Request

```shell
HEAD /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 03 Jan 2020 03:19:12 GMT
x-cos-server-side-encryption-customer-algorithm: AES256
x-cos-server-side-encryption-customer-key: MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=
x-cos-server-side-encryption-customer-key-MD5: U5L61r7jcwdNvT7frmUG8g==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1578021552;1578028752&q-key-time=1578021552;1578028752&q-header-list=date;host;x-cos-server-side-encryption-customer-algorithm;x-cos-server-side-encryption-customer-key;x-cos-server-side-encryption-customer-key-md5&q-url-param-list=&q-signature=9fd7bb651ba253f522a544d75f4acaeff1d9****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 13
Connection: close
Date: Fri, 03 Jan 2020 03:19:12 GMT
ETag: "492b458ec33eaf0a824e7dd1bdd403b3"
Last-Modified: Fri, 03 Jan 2020 03:19:06 GMT
Server: tencent-cos
x-cos-request-id: NWUwZWIyYjBfNjFjODJhMDlfMTFjNTdfMjFi****
x-cos-server-side-encryption-customer-algorithm: AES256
x-cos-server-side-encryption-customer-key-MD5: U5L61r7jcwdNvT7frmUG8g==
```

#### Example 5. Requesting the latest version of the object (with versioning enabled)

#### Request

```shell
HEAD /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 03 Jan 2020 03:16:19 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1578021379;1578028579&q-key-time=1578021379;1578028579&q-header-list=date;host&q-url-param-list=&q-signature=7efe66664752371b87d36eb117206009d85a****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 15
Connection: close
Date: Fri, 03 Jan 2020 03:16:19 GMT
ETag: "60c7644eb1ae8918a7fe7e13a352712c"
Last-Modified: Fri, 03 Jan 2020 03:16:13 GMT
Server: tencent-cos
x-cos-request-id: NWUwZWIyMDNfZThiOTJhMDlfMTMwNjZfMTQ0****
x-cos-version-id: MTg0NDUxNjYwNTIzMzU4NjY5MDk
```

#### Example 6. Requesting a specific version of the object (with versioning enabled)

#### Request

```shell
HEAD /exampleobject?versionId=MTg0NDUxNjYwNTIxNTA5MDIyMDg HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 03 Jan 2020 03:19:25 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1578021565;1578028765&q-key-time=1578021565;1578028765&q-header-list=date;host&q-url-param-list=versionid&q-signature=91b0fe614247694bb7611a69f05c4aad0f16****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 13
Connection: close
Date: Fri, 03 Jan 2020 03:19:25 GMT
ETag: "b62e10bcab55a88240bd9c436cffdcf9"
Last-Modified: Fri, 03 Jan 2020 03:19:18 GMT
Server: tencent-cos
x-cos-request-id: NWUwZWIyYmNfMzJiMDJhMDlfN2YzOF8zOWRl****
x-cos-version-id: MTg0NDUxNjYwNTIxNTA5MDIyMDg
```

#### Example 7. Requesting an archived object that is being restored

#### Request

```shell
HEAD /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 27 Dec 2019 08:19:35 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1577434775;1577441975&q-key-time=1577434775;1577441975&q-header-list=date;host&q-url-param-list=&q-signature=72408a09a5fc00d77d389559a0cfa5c98e31****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 13
Connection: close
Date: Fri, 27 Dec 2019 08:19:35 GMT
ETag: "b62e10bcab55a88240bd9c436cffdcf9"
Last-Modified: Fri, 27 Dec 2019 08:19:23 GMT
Server: tencent-cos
x-cos-request-id: NWUwNWJlOTdfN2VjODJhMDlfOGI1N18yYjYz****
x-cos-restore: ongoing-request="true"
x-cos-restore-status: tier="expedited"; request-date="Fri, 27 Dec 2019 08:19:29 GMT"
x-cos-storage-class: ARCHIVE
```

#### Example 8. Requesting an archived object which has been restored

#### Request

```shell
HEAD /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 02 Jan 2020 18:09:51 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1577988591;1577995791&q-key-time=1577988591;1577995791&q-header-list=date;host&q-url-param-list=&q-signature=ff23b3a44945f019916450add646e963c29b****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 13
Connection: close
Date: Thu, 02 Jan 2020 18:09:51 GMT
ETag: "b62e10bcab55a88240bd9c436cffdcf9"
Last-Modified: Thu, 02 Jan 2020 18:09:40 GMT
Server: tencent-cos
x-cos-request-id: NWUwZTMxZWZfZWZiOTJhMDlfMTE1ZDhfMTI1****
x-cos-restore: ongoing-request="false", expiry-date="Sat, 04 Jan 2020 16:00:00 GMT"
x-cos-storage-class: ARCHIVE
```
