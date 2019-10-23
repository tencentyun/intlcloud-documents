## Description

This API (GET Object) is used to download an object in a COS bucket to the local file system. This operation requires you to have permission to read the target object or the target object to be public-read.

>? If the response-* request parameter is used, this request operation does not support anonymous request and must carry a signature.

#### Versioning

If versioning is enabled, the GET operation will return the latest version of the object. To return a previous version of the object, use the versionId request parameter.

## Request

#### Sample Request

```shell
GET /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

#### Request Parameters

| Name | Description | Type | Required |
| ---------------------------- | ----------------------------------------- | ------ | -------- |
| response-cache-control | Sets the value of the Cache-Control header in the response | string | No |
| response-content-disposition | Sets the value of the Content-Disposition header in the response | string | No |
| response-content-encoding | Sets the value of the Content-Encoding header in the response | string | No |
| response-content-language | Sets the value of the Content-Language header in the response | string | No |
| response-content-type | Sets the value of the Content-Type header in the response | string | No |
| response-expires | Sets the value of the Expires header in the response | string | No |
| versionId | Specifies the version ID of the object to be downloaded | string | No |

#### Request Header

In addition to common request headers, this API also supports the following request headers. For more information on the common request header, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

| Name | Description | Type | Required |
| ------------------- | ------------------------------------------------------------ | ------ | -------- |
| Range | Byte range as defined in RFC 2616. The range value must be in the format of bytes=first-last, where both first and last are offsets starting from 0. For example, bytes=0-9 indicates to download the first 10 bytes of data of the object, and HTTP status code 206 (Partial Content) and the Content-Range response header will be returned. If this parameter is not specified, the entire object will be downloaded | String | No |
| If-Modified-Since   | If the object is modified after the specified time, the object will be returned; otherwise, HTTP status code 304 (Not Modified) will be returned | String | No |
| If-Unmodified-Since | If the object is not modified after the specified time, the object will be returned; otherwise, HTTP status 412 (Precondition Failed) will be returned | String | No |
| If-Match | If the ETag of the object is the same as the specified value, the object will be returned; otherwise, HTTP status code 412 (Precondition Failed) will be returned | string | No |
| If-None-Match | If the ETag of the object is different from the specified value, the object will be returned; otherwise, HTTP status code 304 (Not Modified) will be returned | string | No |

**Server-side encryption-related headers**

If server-side encryption is used for the specified object and the encryption method is SSE-C, the headers related to server-side encryption needs to be specified for decrypting the object. For more information. see [Server-side Encryption-specific Headers](https://intl.cloud.tencent.com/document/product/436/7728#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Request Body

This API has no request body.

## Response

#### Response Header

In addition to common response headers, this API returns the following response headers. For more information on common response header, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

| Name | Description | Type |
| ------------------- | ------------------------------------------------------------ | ------ |
| Cache-Control | Cache policy as defined in RFC 2616, which will be returned only if it is contained in the object metadata or specified through the request parameter | string |
| Content-Disposition | Filename as defined in RFC 2616, which will be returned only if it is contained in the object metadata or specified through the request parameter | string |
| Content-Encoding | Encoding format as defined in RFC 2616, which will be returned only if it is contained in the object metadata or specified through the request parameter | string |
| Content-Range | Byte range of the return content as defined in RFC 2616, which will be returned only if the `Range` request header is specified in the request | string |
| Expires | Cache expiration time as defined in RFC 2616, which will be returned only if it is contained in the object metadata or specified through the request parameter | string |
| x-cos-meta-\* | This includes the suffix and information of the user-defined metadata header | string |
| x-cos-storage-class | Object storage class, such as STANDARD_IA and ARCHIVE. For enumerated values, see [Storage Class](https://intl.cloud.tencent.com/document/product/436/30925). This header will be returned only if the object is not in STANDARD storage class | Enum |

**Versioning-related headers**

For versioned objects, the following response headers will be returned:

| Name | Description | Type |
| ---------------- | ------------- | ------ |
| x-cos-version-id | Object version ID | string |

**Server-side encryption-related headers**

If server-side encryption is used for the specified object, this API will return the server-side encryption-specific headers. For more information. see [Server-side Encryption-specific Headers](https://intl.cloud.tencent.com/document/product/436/7729#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Response Body

The response body of this API request is the object (file) content.

#### Error Codes

There are no special error messages for this API. For all error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

#### Sample 1. A Simple Sample (with Versioning Not Enabled)

#### Request

```shell
GET /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 04 Jul 2019 11:33:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1562239980;1562247180&q-key-time=1562239980;1562247180&q-header-list=date;host&q-url-param-list=&q-signature=fa5552e4c84ab474e9b66bcecbefcb5c15d9****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 13
Connection: close
Accept-Ranges: bytes
Date: Thu, 04 Jul 2019 11:33:00 GMT
ETag: "b62e10bcab55a88240bd9c436cffdcf9"
Last-Modified: Thu, 04 Jul 2019 11:32:55 GMT
Server: tencent-cos
x-cos-request-id: NWQxZGUzZWNfN2RiZTBiMDlfM2EzZF8yMGYx****

[Object Content]
```

#### Sample 2. Specifying the Response Headers Through Request Parameters

#### Request

```shell
GET /exampleobject?response-content-type=application%2Foctet-stream&response-cache-control=max-age%3D86400&response-content-disposition=attachment%3B%20filename%3Dexample.jpg HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 04 Jul 2019 11:33:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1562239980;1562247180&q-key-time=1562239980;1562247180&q-header-list=date;host&q-url-param-list=response-cache-control;response-content-disposition;response-content-type&q-signature=a079419b6f0cd4ac1bc55bcdf14b54a4a9a3****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/octet-stream
Content-Length: 13
Connection: close
Accept-Ranges: bytes
Cache-Control: max-age=86400
Content-Disposition: attachment; filename=example.jpg
Date: Thu, 04 Jul 2019 11:33:00 GMT
ETag: "b62e10bcab55a88240bd9c436cffdcf9"
Last-Modified: Thu, 04 Jul 2019 11:32:55 GMT
Server: tencent-cos
x-cos-request-id: NWQxZGUzZWNfNjI4NWQ2NF9lMWYyXzk1NjFj****

[Object Content]
```

#### Sample 3. Using Server-side Encryption SSE-COS

#### Request

```shell
GET /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 04 Jul 2019 11:33:05 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1562239985;1562247185&q-key-time=1562239985;1562247185&q-header-list=date;host&q-url-param-list=&q-signature=c2f7fbaba0ad534483078eebef3ca4a829ae****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 13
Connection: close
Accept-Ranges: bytes
Date: Thu, 04 Jul 2019 11:33:06 GMT
ETag: "b62e10bcab55a88240bd9c436cffdcf9"
Last-Modified: Thu, 04 Jul 2019 11:33:00 GMT
Server: tencent-cos
x-cos-request-id: NWQxZGUzZjJfZGQyOTVkNjRfMjU0NF80MGVj****
x-cos-server-side-encryption: AES256

[Object Content]
```

#### Sample 4. Using Server-side Encryption SSE-C

#### Request

```shell
GET /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 04 Jul 2019 11:33:11 GMT
x-cos-server-side-encryption-customer-algorithm: AES256
x-cos-server-side-encryption-customer-key: MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=
x-cos-server-side-encryption-customer-key-MD5: U5L61r7jcwdNvT7frmUG8g==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1562239991;1562247191&q-key-time=1562239991;1562247191&q-header-list=date;host;x-cos-server-side-encryption-customer-algorithm;x-cos-server-side-encryption-customer-key;x-cos-server-side-encryption-customer-key-md5&q-url-param-list=&q-signature=6e50f8adca0fb8040868ab05891abf6df2a8****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 13
Connection: close
Accept-Ranges: bytes
Date: Thu, 04 Jul 2019 11:33:11 GMT
ETag: "492b458ec33eaf0a824e7dd1bdd403b3"
Last-Modified: Thu, 04 Jul 2019 11:33:06 GMT
Server: tencent-cos
x-cos-request-id: NWQxZGUzZjdfZDkyNzVkNjRfZDA0Y185OGJj****
x-cos-server-side-encryption-customer-algorithm: AES256
x-cos-server-side-encryption-customer-key-MD5: U5L61r7jcwdNvT7frmUG8g==

[Object Content]
```

#### Sample 5. Downloading the Latest Version of the Object (with Versioning Enabled)

#### Request

```shell
GET /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 05 Jul 2019 03:30:31 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1562297431;1562304631&q-key-time=1562297431;1562304631&q-header-list=date;host&q-url-param-list=&q-signature=5bb216e0260589dc6a9986bf6caa3df18db4****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 15
Connection: close
Accept-Ranges: bytes
Date: Fri, 05 Jul 2019 03:30:31 GMT
ETag: "60c7644eb1ae8918a7fe7e13a352712c"
Last-Modified: Fri, 05 Jul 2019 03:30:26 GMT
Server: tencent-cos
x-cos-request-id: NWQxZWM0NTdfZGEyNzVkNjRfMjJhOV9hMWVk****
x-cos-version-id: MTg0NDUxODE3NzYyODMxOTg0OTg

[Object Content]
```

#### Sample 6. Downloading the Specified Version of the Object (with Versioning Enabled)

#### Request

```shell
GET /exampleobject?versionId=MTg0NDUxODE3NzYyODg0ODI2MjA HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 05 Jul 2019 03:30:31 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1562297431;1562304631&q-key-time=1562297431;1562304631&q-header-list=date;host&q-url-param-list=versionid&q-signature=3ea1162e56d0b43f7398a39b99b72bbf58ad****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 13
Connection: close
Accept-Ranges: bytes
Date: Fri, 05 Jul 2019 03:30:31 GMT
ETag: "b62e10bcab55a88240bd9c436cffdcf9"
Last-Modified: Fri, 05 Jul 2019 03:30:21 GMT
Server: tencent-cos
x-cos-request-id: NWQxZWM0NTdfOTNjMjJhMDlfZDBjNV85ZTBh****
x-cos-version-id: MTg0NDUxODE3NzYyODg0ODI2MjA

[Object Content]
```

#### Sample 7. Specifying the Range Request Header to Download Partial Content

#### Request

```shell
GET /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 09 Aug 2019 04:02:17 GMT
Range: bytes=2-4
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1565323337;1565330537&q-key-time=1565323337;1565330537&q-header-list=date;host;range&q-url-param-list=&q-signature=8b3b4427bbbe15c5cfba9c458c9b3c85d0e3****
Connection: close
```

#### Response

```shell
HTTP/1.1 206 Partial Content
Content-Type: image/jpeg
Content-Length: 3
Connection: close
Accept-Ranges: bytes
Content-Range: bytes 2-4/13
Date: Fri, 09 Aug 2019 04:02:18 GMT
ETag: "b62e10bcab55a88240bd9c436cffdcf9"
Last-Modified: Fri, 09 Aug 2019 04:02:12 GMT
Server: tencent-cos
x-cos-request-id: NWQ0Y2YwNGFfNDhiNDBiMDlfMmU2ZTFfMTc0MGVl****

[Object Content]
```
