## Description

COS supports deleting tags for existing buckets. This API is used to delete existing tags of a specified bucket.

>  If you call the `DELETE Bucket tagging` API using a sub-account, please make sure that you have obtained the permission to use this API from the root account.

## Request

### Sample Request

```http
DELETE /?tagging HTTP 1.1
Host:<BucketName-APPID>.cos.<Region>.myqcloud.com
Date:date
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

### Request Headers

#### Common Headers

The implementation of this operation uses common request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special Headers

This request operation does not use any special request header.

### Request Body

The request body of this request is empty.

## Response

### Response Headers

#### Common Response Headers

This response uses common response headers. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Special Response Headers

This request operation does not use any special response header.

### Response Body

This request does not have special response body information.

### Error Codes

The following describes some frequent special errors that may occur when you make this request:

| Error Code | Description | HTTP Status Code |
| --------------------- | ---------------------------------------------------- | ------------------------------------------------------------ |
| SignatureDoesNotMatch | If the provided signature does not conform to the rule, this error code will be returned | 403 [Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3) |
| NoSuchBucket | If the bucket to which you want to add the rule does not exist, this error code will be returned | 404 [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4) |
| NoSuchTagSetError     | No bucket tag has been set for the requested bucket | 404 [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4) |

## Example

### Request

The following request is made to delete the existing tags of the bucket `examplebucket-1250000000`. COS parses the request and deletes all the tags of the bucket.

```shell
DELETE /?tagging HTTP/1.1
User-Agent: curl/7.29.0
Accept: */*
Host: examplebucket-1250000000.cos.ap-chengdu.myqcloud.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDrbAYjEBqqdEconpFi8NPFsOjrnX4LYUE&q-sign-time=1516361923;1517361973&q-key-time=1516361923;1517361973&q-url-param-list=tagging&q-header-list=content-md5;host&q-signature=71251feb4501494edcfbd01747fa873003759404
Content-Md5: LIbd5t5HLPhuNWYkP6qHcQ==
Content-Length: 127
Content-Type: application/xml
```

### Response

```shell
HTTP/1.1 204 No Content
Content-Type: application/xml
Connection: close
Date: Fri, 19 Jan 2018 11:40:22 GMT
```
