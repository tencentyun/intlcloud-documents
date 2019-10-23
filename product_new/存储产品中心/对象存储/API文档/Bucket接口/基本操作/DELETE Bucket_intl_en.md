## Description

This API (DELETE Bucket) is used to delete the specified bucket. The requester of this API should have write permission to the bucket.
>! Before deleting a bucket, please make sure that all data and incomplete multipart uploads have been cleared in the bucket; otherwise, the bucket cannot be deleted.

## Request

#### Sample Request

```shell
DELETE / HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

#### Request Parameters

This API has no request parameters.

#### Request Header

This API uses only a common request header. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request Body

This API has no request body.

## Response

#### Response Header

This API only returns a common response header. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response Body

The response body of this API is empty.

#### Error Codes

The special error messages for this API are as detailed below. For all error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

Error Code | Description | HTTP Status Code
---|---|---
BucketNotEmpty| The bucket is not empty |409 Conflict
NoSuchBucket| The specified bucket does not exist |404 Not Found

## Sample

#### Request

```shell
DELETE / HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Tue, 28 May 2019 03:19:13 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1559013553;1559020753&q-key-time=1559013553;1559020753&q-header-list=date;host&q-url-param-list=&q-signature=478b1db6182db32c8ed459dfa723a9f500b2****
Connection: close
```

#### Response

```shell
HTTP/1.1 204 No Content
Content-Length: 0
Connection: close
Date: Tue, 28 May 2019 03:19:14 GMT
Server: tencent-cos
x-cos-request-id: NWNlY2E4YjFfNjljMDBiMDlfMmNiZTlfZGE0****
```
