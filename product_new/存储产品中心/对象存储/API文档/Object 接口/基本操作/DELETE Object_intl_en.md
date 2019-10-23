## Description

This API (DELETE Object) is used to delete a file (object) in a COS bucket. The requester of this operation should have write permission to the bucket.

### Detail Analysis

- Deleting a non-existing object in a DELETE Object request will still be considered a success, but `204 No Content` will be returned.
- To use the DELETE Object API, you should have write permission to the object.

## Request

### Sample Request
```shell
DELETE /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Length: length
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

### Request Headers

#### Common Headers

The implementation of this request operation uses a common request header. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special Headers

This request operation has no special request headers.


### Request Body

The request body of this request is empty.

## Response

### Response Headers
#### Common Response Headers 

This response uses a common response header. For more information on the common response header, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Special Response Headers

This request operation has no special response headers.

### Response Body

The response body of this request is empty.

### Error Analysis

Some frequent special errors that may occur with this request are listed below:

| Error Code | HTTP Status Code | Description |
|--|--|--|
| NoSuchBucket |404 Not Found| The bucket does not exist |

For more common error codes in COS or the complete list of errors, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
## Samples

### Request
```shell
DELETE /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 23 Oct 2016 21:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484213409;32557109409&q-key-time=1484213409;32557109409&q-header-list=host&q-url-param-list=&q-signature=1c24fe260ffe79b8603f932c4e916a6cbb0af44a
```

### Response
```shell
HTTP /1.1 204 No Content
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Wed, 23 Oct 2016 21:32:00 GMT
Server: tencent-cos
x-cos-request-id: NTg3NzRjYTRfYmRjMzVfMzFhOF82MmM3Yg==
```
