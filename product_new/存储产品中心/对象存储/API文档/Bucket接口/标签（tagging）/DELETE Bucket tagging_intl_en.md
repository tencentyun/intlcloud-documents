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

This API only uses common request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special Headers

This request operation does not use any special request header.

### Request Body

The request body of this request is empty.

## Response

### Response Headers

#### Common Response Headers

This API only uses common response headers. For more information on common request headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Special Response Headers

This request operation does not use any special response header.

### Response Body

The response body of this request is empty.

### Error Codes

This API uses standardized error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) .

## Example

### Request

The following request is made to delete the existing tags of the bucket `examplebucket-1250000000`. COS parses the request and deletes all the tags of the bucket.

```shell
DELETE /?tagging HTTP/1.1
User-Agent: curl/7.29.0
Accept: */*
Host: examplebucket-1250000000.cos.ap-chengdu.myqcloud.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDrbAYjEBqqdEconpFi8NPFsOjrnX4****&q-sign-time=1516361923;1517361973&q-key-time=1516361923;1517361973&q-url-param-list=tagging&q-header-list=content-md5;host&q-signature=71251feb4501494edcfbd01747fa87300375****
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
