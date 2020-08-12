## Feature description

This API is used to download an object to the local file system. To make this request, you need to have read permission for the object, or the object must have public read permission enabled (i.e., everyone has permission to read the object).

> If the `response-*` request parameter is used, this request operation will not support anonymous requests and will have to carry a signature.

#### Versioning

With versioning enabled, you can specify the `versionId` request parameter to get a specific version of an object. If the version ID you specify corresponds to a delete marker, an HTTP `404` status code (Not Found) will be returned. If no version ID is specified, the latest version will be returned.

#### ARCHIVE storage class

If this API is used to get an **archived** object, and the object has not been restored using [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) or the restored copy has been deleted after expiration, the request will return an HTTP `403` status code (Forbidden) and include an error message in the response body. The error code will be `InvalidObjectState`, indicating that you cannot get the object in its current state with this API and you must restore it first.

## Request

#### Sample request

```shell
GET /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

#### Request parameters

| Name | Description | Type | Required |
| ---------------------------- | ------------------------------------------------------------ | ------ | -------- |
| response-cache-control | Sets the value of the `Cache-Control` header in the response | string | No |
| response-content-disposition | Sets the value of the `Content-Disposition` header in the response | string | No |
| response-content-encoding | Sets the value of the `Content-Encoding` header in the response | string | No |
| response-content-language | Sets the value of the `Content-Language` header in the response | string | No |
| response-content-type | Sets the value of the `Content-Type` header in the response | string | No |
| response-expires | Sets the value of the `Expires` header in the response | string | No |
| versionId | Specifies the version ID of the object if versioning is enabled; if this parameter is not specified, the latest version will be downloaded | string | No |

#### Request headers

In addition to common request headers, this API also supports the following request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

| Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Type | Required |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------ | -------- |
| Range  | Byte range of the object as defined in RFC 2616. You can specify only one byte range in the format of bytes=first-last, where both first and last are offsets starting from 0. For example, `bytes=0-9` downloads the first 10 bytes of data of the source object, and `bytes=5-9` downloads the 6th to 10th bytes. In these cases, HTTP 206 (Partial Content) is returned with Content-Range header.<br>If `first` exceeds the object size, HTTP error 416 (Requested Range Not Satisfiable) is returned. If this parameter is not specified, the entire object will be downloaded. | string | No      || If-Modified-Since | If the object is modified after the specified time, the object will be returned; otherwise, HTTP status code `304` (Not Modified) will be returned. | string | No |
| If-Unmodified-Since | If the object is not modified after the specified time, the object will be returned; otherwise, HTTP status code `412` (Precondition Failed) will be returned. | string | No |
| If-Match | If the `ETag` of the object is the same as the specified value, the object will be returned; otherwise, HTTP status code `412` (Precondition Failed) will be returned. | string | No |
| If-None-Match | If the `ETag` of the object is different from the specified value, the object will be returned; otherwise, HTTP status code 304 (Not Modified) will be returned. | string | No |

**Server-side Encryption Headers**

If server-side encryption is used for the specified object and the encryption method is SSE-C, you will need to specify the headers related to server-side encryption to decrypt the object. For more information, see [Server-side Encryption Headers](https://intl.cloud.tencent.com/document/product/436/7728#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Request body

This API does not have a request body.

## Response

#### Response headers

In addition to common response headers, this API also returns the following response headers. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

| Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Type |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------ |
| Cache-Control | Cache directives as defined in RFC 2616, which will be returned only if it is contained in the object metadata or if it is specified in the request parameter | string |
| Content-Disposition                                         | File name as defined in RFC 2616, which will be returned only if it is contained in the object metadata or if it is specified in the request parameter | string  |
| Content-Encoding                                            | Encoding format as defined in RFC 2616, which will be returned only if it is contained in the object metadata or if it is specified in the request parameter | string  |
| Content-Range                                                | Byte range of the returned content as defined in RFC 2616, which will be returned only if it is specified in the request | string |
| Expires                                                    | Cache expiration time as defined in RFC 2616, which will be returned only if it is contained in the object metadata or if it is specified in the request parameter | string  |
| x-cos-meta-\* | Contains user-defined metadata and header suffixes | string |
| x-cos-storage-class | Object storage class, such as `MAZ_STANDARD`, `MAZ_STANDARD_IA`, `STANDARD_IA` and `ARCHIVE`. For the enumerated values, see [Storage Class](https://intl.cloud.tencent.com/document/product/436/30925). This header will be returned only if the storage class of the object is not `STANDARD`. | Enum |

**Versioning-related Headers**

If the target object is from a bucket where versioning is enabled, the following response headers will be returned:

| Name | Description | Type |
| ---------------- | ------------- | ------ |
| x-cos-version-id | Object version ID | string |

**Server-side Encryption Headers**

If server-side encryption is used for the specified object, this API will return the server-side encryption headers. For more information, see [Server-side Encryption Headers](https://intl.cloud.tencent.com/document/product/436/7729#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Response body

The response body of this API request is the object (file) content.

#### Error codes

This API uses standardized error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) .

## Use Cases

#### Example 1. Simple example (versioning not enabled)

#### Request

```shell
GET /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 09:35:16 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586511316;1586518516&q-key-time=1586511316;1586518516&q-header-list=date;host&q-url-param-list=&q-signature=1bd1898e241fb978df336dc68aaef4c0acae****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 16
Connection: close
Accept-Ranges: bytes
Date: Fri, 10 Apr 2020 09:35:16 GMT
ETag: "ee8de918d05640145b18f70f4c3aa602"
Last-Modified: Fri, 10 Apr 2020 09:35:05 GMT
Server: tencent-cos
x-cos-hash-crc64ecma: 16749565679157681890
x-cos-request-id: NWU5MDNkZDRfZDgyNzVkNjRfN2Q5M18xOWVi****

[Object Content]
```

#### Example 2. Specifying response headers through request parameters

#### Request

```shell
GET /exampleobject?response-content-type=application%2Foctet-stream&response-cache-control=max-age%3D86400&response-content-disposition=attachment%3B%20filename%3Dexample.jpg HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 09:35:17 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586511317;1586518517&q-key-time=1586511317;1586518517&q-header-list=date;host&q-url-param-list=response-cache-control;response-content-disposition;response-content-type&q-signature=4fcea9f80bc67fe475dff746eca0b9abff6a****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/octet-stream
Content-Length: 16
Connection: close
Accept-Ranges: bytes
Cache-Control: max-age=86400
Content-Disposition: attachment; filename=example.jpg
Date: Fri, 10 Apr 2020 09:35:17 GMT
ETag: "ee8de918d05640145b18f70f4c3aa602"
Last-Modified: Fri, 10 Apr 2020 09:35:05 GMT
Server: tencent-cos
x-cos-hash-crc64ecma: 16749565679157681890
x-cos-request-id: NWU5MDNkZDVfNjZjODJhMDlfMTY2MDdfMThm****

[Object Content]
```

#### Example 3. Specifying query conditions using request headers and returning a HTTP status code 304 (Not Modified)

#### Request

```shell
GET /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 29 Jul 2020 06:51:49 GMT
If-None-Match: "ee8de918d05640145b18f70f4c3aa602"
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1596005509;1596012709&q-key-time=1596005509;1596012709&q-header-list=date;host;if-none-match&q-url-param-list=&q-signature=20e39095b9f22ae1279bec2a3375b527c32d****
Connection: close
```

#### Response

```shell
HTTP/1.1 304 Not Modified
Content-Type: image/jpeg
Content-Length: 0
Connection: close
Date: Wed, 29 Jul 2020 06:51:49 GMT
ETag: "ee8de918d05640145b18f70f4c3aa602"
Server: tencent-cos
x-cos-hash-crc64ecma: 16749565679157681890
x-cos-request-id: NWYyMTFjODVfOGZiNzJhMDlfNDcxZjZfZDY2****
```

#### Example 4. Specifying query conditions using request headers and returning a HTTP status code 412 (Precondition Failed)

#### Request

```shell
GET /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 29 Jul 2020 06:51:50 GMT
If-Match: "aa488bb80185a6be87f4a7b936a80752"
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1596005510;1596012710&q-key-time=1596005510;1596012710&q-header-list=date;host;if-match&q-url-param-list=&q-signature=1437a0d094c4e0f8e26909d35b2cca83dcbf****
Connection: close
```

#### Response

```shell
HTTP/1.1 412 Precondition Failed
Content-Type: application/xml
Content-Length: 480
Connection: close
Date: Wed, 29 Jul 2020 06:51:50 GMT
Server: tencent-cos
x-cos-request-id: NWYyMTFjODZfOGRjOTJhMDlfMmIyMWVfOTJl****
<?xml version='1.0' encoding='utf-8' ?>
<Error>
	<Code>PreconditionFailed</Code>
	<Message>Precondition not match.</Message>
	<Resource>examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject</Resource>
	<RequestId>NWYyMTFjODZfOGRjOTJhMDlfMmIyMWVfOTJl****</RequestId>
	<TraceId>OGVmYzZiMmQzYjA2OWNhODk0NTRkMTBiOWVmMDAxODc0OWRkZjk0ZDM1NmI1M2E2MTRlY2MzZDhmNmI5MWI1OTdjMDczODYwZjM5YTU3ZmZmOWI5MmY4NjkxY2I3MGNiNjkyOWZiNzUxZjg5MGY2OWU4NmI0YWMwNTlhNTExYWU=</TraceId>
</Error>
```

#### Example 5. Using server-side encryption SSE-COS

#### Request

```shell
GET /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 09:36:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586511360;1586518560&q-key-time=1586511360;1586518560&q-header-list=date;host&q-url-param-list=&q-signature=6f9ec1af1aa86abd5b484b41ae1378850ad2****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 16
Connection: close
Accept-Ranges: bytes
Date: Fri, 10 Apr 2020 09:36:00 GMT
ETag: "ee8de918d05640145b18f70f4c3aa602"
Last-Modified: Fri, 10 Apr 2020 09:35:49 GMT
Server: tencent-cos
x-cos-hash-crc64ecma: 16749565679157681890
x-cos-request-id: NWU5MDNlMDBfMzdiMDJhMDlfYTgyNl8xNjA2****
x-cos-server-side-encryption: AES256

[Object Content]
```

#### Example 6. Using server-side encryption SSE-KMS

#### Request

```shell
GET /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 09:36:11 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586511371;1586518571&q-key-time=1586511371;1586518571&q-header-list=date;host&q-url-param-list=&q-signature=bdadbe917a50feeb8dddf8c75642be172720****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 16
Connection: close
Accept-Ranges: bytes
Date: Fri, 10 Apr 2020 09:36:11 GMT
ETag: "840af7c921f4b3230049af8663145bd0"
Last-Modified: Fri, 10 Apr 2020 09:36:01 GMT
Server: tencent-cos
x-cos-hash-crc64ecma: 16749565679157681890
x-cos-request-id: NWU5MDNlMGJfZGEyNzVkNjRfZDgxY18xYTBj****
x-cos-server-side-encryption: cos/kms
x-cos-server-side-encryption-cos-kms-key-id: 48ba38aa-26c5-11ea-855c-52540085****

[Object Content]
```

#### Example 7. Using server-side encryption SSE-C

#### Request

```shell
GET /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 09:36:23 GMT
x-cos-server-side-encryption-customer-algorithm: AES256
x-cos-server-side-encryption-customer-key: MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=
x-cos-server-side-encryption-customer-key-MD5: U5L61r7jcwdNvT7frmUG8g==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586511383;1586518583&q-key-time=1586511383;1586518583&q-header-list=date;host;x-cos-server-side-encryption-customer-algorithm;x-cos-server-side-encryption-customer-key;x-cos-server-side-encryption-customer-key-md5&q-url-param-list=&q-signature=7da5c304f9439df949b6550ab23aea67a5f0****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 16
Connection: close
Accept-Ranges: bytes
Date: Fri, 10 Apr 2020 09:36:23 GMT
ETag: "582d9105f71525f3c161984bc005efb5"
Last-Modified: Fri, 10 Apr 2020 09:36:12 GMT
Server: tencent-cos
x-cos-hash-crc64ecma: 16749565679157681890
x-cos-request-id: NWU5MDNlMTdfNzBiODJhMDlfZTVmMV8xNDAy****
x-cos-server-side-encryption-customer-algorithm: AES256
x-cos-server-side-encryption-customer-key-MD5: U5L61r7jcwdNvT7frmUG8g==

[Object Content]
```

#### Example 8. Downloading the latest version of an object (with versioning enabled)

#### Request

```shell
GET /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 12:30:02 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586521802;1586529002&q-key-time=1586521802;1586529002&q-header-list=date;host&q-url-param-list=&q-signature=51b3c33f4cfae5d7b31ad61a974db7374f39****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 26
Connection: close
Accept-Ranges: bytes
Date: Fri, 10 Apr 2020 12:30:02 GMT
ETag: "22e024392de860289f0baa7d6cf8a549"
Last-Modified: Fri, 10 Apr 2020 12:29:52 GMT
Server: tencent-cos
x-cos-hash-crc64ecma: 11596229263574363878
x-cos-request-id: NWU5MDY2Y2FfMzFiYjBiMDlfMjE2NzVfMTgz****
x-cos-version-id: MTg0NDUxNTc1NTE5MTc1NjM4MDA

[Object Content Version 2]
```

#### Example 9. Downloading a specific version of an object (with versioning enabled)

#### Request

```shell
GET /exampleobject?versionId=MTg0NDUxNTc1NjIzMTQ1MDAwODg HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 09:36:45 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586511405;1586518605&q-key-time=1586511405;1586518605&q-header-list=date;host&q-url-param-list=versionid&q-signature=31aeb69334b973ef7406300a182de0645c91****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 16
Connection: close
Accept-Ranges: bytes
Date: Fri, 10 Apr 2020 09:36:45 GMT
ETag: "ee8de918d05640145b18f70f4c3aa602"
Last-Modified: Fri, 10 Apr 2020 09:36:35 GMT
Server: tencent-cos
x-cos-hash-crc64ecma: 16749565679157681890
x-cos-request-id: NWU5MDNlMmRfNzBiODJhMDlfZTYwZl8xM2Fh****
x-cos-version-id: MTg0NDUxNTc1NjIzMTQ1MDAwODg

[Object Content]
```

#### Example 10. Downloading partial content by specifying the Range request header

#### Request

```shell
GET /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 12:32:37 GMT
Range: bytes=8-14
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586521957;1586529157&q-key-time=1586521957;1586529157&q-header-list=date;host;range&q-url-param-list=&q-signature=719273479357f4b4b4c7d4f5ceb631753101****
Connection: close
```

#### Response

```shell
HTTP/1.1 206 Partial Content
Content-Type: image/jpeg
Content-Length: 7
Connection: close
Accept-Ranges: bytes
Content-Range: bytes 8-14/16
Date: Fri, 10 Apr 2020 12:32:37 GMT
ETag: "ee8de918d05640145b18f70f4c3aa602"
Last-Modified: Fri, 10 Apr 2020 12:32:25 GMT
Server: tencent-cos
x-cos-hash-crc64ecma: 16749565679157681890
x-cos-request-id: NWU5MDY3NjVfY2VjODJhMDlfOWVlZl8xNmMy****

Content
```

#### Example 11. Downloading an archived object that has not been restored

#### Request

```shell
GET /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 26 Dec 2019 11:57:24 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1577361444;1577368644&q-key-time=1577361444;1577368644&q-header-list=date;host&q-url-param-list=&q-signature=d975dc7097b2dbffcf2ba001e6dec25dd80a****
Connection: close
```

#### Response

```shell
HTTP/1.1 403 Forbidden
Content-Type: application/xml
Content-Length: 513
Connection: close
Date: Thu, 26 Dec 2019 11:57:24 GMT
Server: tencent-cos
x-cos-request-id: NWUwNGEwMjRfZDcyNzVkNjRfNjZlM183Zjcx****
x-cos-storage-class: ARCHIVE

<?xml version='1.0' encoding='utf-8' ?>
<Error>
	<Code>InvalidObjectState</Code>
	<Message>The operation is not valid for the object storage class.</Message>
	<Resource>examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject</Resource>
	<RequestId>NWUwNGEwMjRfZDcyNzVkNjRfNjZlM183Zjcx****</RequestId>
	<TraceId>OGVmYzZiMmQzYjA2OWNhODk0NTRkMTBiOWVmMDAxODc0OWRkZjk0ZDM1NmI1M2E2MTRlY2MzZDhmNmI5MWI1OTBjNjIyOGVlZmJlNDg4NDQ1MzAzMjA2ZDg4OGQ3MDhlMjIzYjI1ZWUwODY5YjdlMTBjY2EwNTgyZWMyMjc0Mjc=</TraceId>
</Error>
```

