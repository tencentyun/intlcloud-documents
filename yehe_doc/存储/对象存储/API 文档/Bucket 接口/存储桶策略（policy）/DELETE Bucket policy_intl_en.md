## Description
This API is used to delete a permission policy of a bucket.

>!Only the bucket owner is allowed to initiate this request. If the permission policy does not exist, "204 No Content" will be returned.

## Request

#### Sample request

```shell
DELETE /?policy HTTP/1.1
Host:<BucketName-APPID>.cos.<Region>.myqcloud.com
Date: date
Authorization: Auth String
```
>?Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)

#### Request headers

This API only uses common request headers. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).


#### Request body
The request body of this request is empty.

## Response
#### Response headers

This API returns only common response headers. For more information, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).


#### Response body
The response body is empty.

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Sample

#### Request

```shell
DELETE /?policy HTTP/1.1
Host: examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Authorization:q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUj****&q-sign-time=1484814613;32557710613&q-key-time=1484814613;32557710613&q-header-list=host&q-url-param-list=policy&q-signature=57c9a3f67b786ddabd2c208641944ec7f9b0****
```

#### Response

```shell
HTTP/1.1 204 No Content
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Thu Jan 19 16:30:21 2017
Server: tencent-cos
x-cos-request-id: NTg4MDc5MWRfNDQyMDRlXzNiMDRf****
```
