## Overview

This API is used to download an object in a COS bucket to a local file system. To call this API, you need to have permission to read the object, or the object is set to `public-read` (i.e., everyone can read it).

> !
>- If the `response-*` parameter is used in a request, anonymous access will not be supported and the request must carry a signature.
>- If you have [set origin-pull](https://intl.cloud.tencent.com/document/product/436/31508) in the COS console but haven’t enabled **sync origin-pull**, when COS pulls data from the configured origin server, `GET Object` will return 302 and redirect to the origin server address. If this address is not trusted, when you use the SDK or call the API, it is strongly recommended that COS verify the address on the backend before requesting it, rather than directly returning 302. Otherwise, security risks such as server-side request forgery (SSRF) (e.g., pulling from a private network address) may occur.
>

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=GetObject&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                API Explorer makes it easy to make online API calls, verify signatures, generate SDK code, search for APIs, etc. You can also use it to query the content of each request as well as its response.
            </div>
        </div>
    </div>
</div>


#### Versioning

With versioning enabled, you can specify the `versionId` request parameter to get a specific version of an object. If the version ID you specify corresponds to a delete marker, HTTP status code 404 (Not Found) will be returned. If no version ID is specified, the latest version will be returned.

#### Archive storage classes

If this API is used to get an **ARCHIVE or DEEP ARCHIVE** object, and the object has not been restored using [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) or the restored copy has been deleted after expiration, the request will return HTTP status code 403 (Forbidden) and include an error message in the response body. The error code `InvalidObjectState` indicates that you cannot use this API to get the object in its current state unless you restore it first.

## Request

#### Sample request

```shell
GET /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? 
> - In `Host: <BucketName-APPID>.cos.<Region>.myqcloud.com`, <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).
> 

#### Request parameters

| Parameter | Description | Type | Required |
| ---------------------------- | ------------------------------------------------------------ | ------ | -------- |
| response-cache-control | Sets the value of the `Cache-Control` header in the response | string | No |
| response-content-disposition | Sets the value of the `Content-Disposition` header in the response                    | string | No       |
| response-content-encoding | Sets the value of the `Content-Encoding` header in the response | string | No |
| response-content-language | Sets the value of the `Content-Language` header in the response | string | No |
| response-content-type | Sets the value of the `Content-Type` header in the response | string | No |
| response-expires | Sets the value of the `Expires` header in the response | string | No |
| versionId | Specifies the version ID of the object (if versioning is enabled). If this parameter is not specified, the object of the latest version will be downloaded. | string | No |

#### Request headers

In addition to common request headers, this API also supports the following request headers. For more information about common request headers, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

| Header  | Description | Type | Required |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------- | -------- |
| Range | Byte range as defined in RFC 2616. The value must be in the format of `bytes=first-last` ("first" and "last" are offset relative to 0) and only one range can be set.<br>For example, `bytes=0-9` indicates to download the first 10 bytes of the object and `bytes=5-9` the 6th to 10th bytes. HTTP status code 206 (Partial Content) and the `Content-Range` response header will be returned.<br>If the value of "first" is smaller than the object size, HTTP status code 416 (Requested Range Not Satisfiable) will be returned. If this parameter is not set, the whole object will be downloaded. | string | No |
| If-Modified-Since | If the object is modified after the specified time, the object will be returned; otherwise, HTTP status code 304 (Not Modified) will be returned. | string | No |
| If-Unmodified-Since | If the object is not modified after the specified time, the object will be returned; otherwise, HTTP status code 412 (Precondition Failed) will be returned. | string | No |
| If-Match | If the `ETag` of the object is the same as the specified value, the object will be returned; otherwise, HTTP status code 412 (Precondition Failed) will be returned. | string | No |
| If-None-Match | If the `ETag` of the object is different from the specified value, the object will be returned; otherwise, HTTP status code 304 (Not Modified) will be returned. | string | No |
| x-cos-traffic-limit | Limits the speed (in bit/s) for the current download for traffic control. Valid range: 819200-838860800 (i.e., 100 KB/s−100 MB/s). If the speed exceeds the limit, a 400 error will be returned. | integer | No |

**Server-side encryption headers**

If server-side encryption is used for the specified object and the encryption method is SSE-C, you will need to specify the headers related to server-side encryption to decrypt the object. For more information, see [Server-side Encryption Headers](https://intl.cloud.tencent.com/document/product/436/7728#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Request body

This API does not have a request body.

## Response

#### Response headers

In addition to common response headers, this API also returns the following response headers. For more information about common response headers, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

| Header  | Description | Type |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------ |
| Cache-Control | Cache directives as defined in RFC 2616, which will be returned only if it is contained in the object metadata or if it is specified in the request parameter | string |
| Content-Disposition                                         | Filename as defined in RFC 2616, which will be returned only if it is contained in the object metadata or if it is specified in the request parameter | string  |
| Content-Encoding                                            | Encoding format as defined in RFC 2616, which will be returned only if it is contained in the object metadata or if it is specified in the request parameter | string  |
| Content-Range                                                | Byte range of the returned content as defined in RFC 2616, which will be returned only if it is specified in the request | string |
| Expires                                                    | Cache expiration time as defined in RFC 2616, which will be returned only if it is contained in the object metadata or if it is specified in the request parameter | string  |
| x-cos-meta-\* | Contains user-defined metadata and header suffixes | string |
| x-cos-storage-class | Object storage class. For the enumerated values, such as `INTELLIGENT_TIERING`, `STANDARD_IA`, `ARCHIVE`, and `DEEP_ARCHIVE`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). Note that this header will be returned only if the object’s storage class is not STANDARD. | enum |
|  x-cos-storage-tier | Specifies the access tier of INTELLIGENT TIERING objects. Valid values: `FREQUENT`, `INFREQUENT` |  enum  |

**Versioning-related headers**

If the target object is from a versioning-enabled bucket, the following response header will be returned:

| Header | Description | Type |
| ---------------- | ------------- | ------ |
| x-cos-version-id | Object version ID | string |

**Server-side encryption headers**

If server-side encryption is used for the specified object, this API will return the server-side encryption headers. For more information, see [Server-side Encryption Headers](https://intl.cloud.tencent.com/document/product/436/7729#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Response body

The response body of this API request is the object (file) content.

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Sample

#### Sample 1: simple use case (with versioning disabled)

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

#### Sample 2: specifying response headers through request parameters

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

#### Sample 3: specifying search criteria through the request headers with HTTP status code 304 (Not Modified) returned

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

#### Sample 4: specifying search criteria through the request header with HTTP status code 412 (Precondition Failed) returned

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

#### Sample 5: using server-side encryption SSE-COS

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

#### Sample 6: using server-side encryption SSE-KMS

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

#### Sample 7: using server-side encryption SSE-C

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

#### Sample 8: downloading an object of the latest version (with versioning enabled)

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

#### Sample 9: downloading an object of a specific version (with versioning enabled)

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

#### Sample 10: specifying the Range request header to download partial content

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

#### Sample 11: downloading an ARCHIVE object that has not been restored

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

