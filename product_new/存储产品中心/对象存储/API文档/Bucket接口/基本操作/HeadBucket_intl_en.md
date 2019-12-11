## Description

This API is used to check whether a bucket exists and whether you have the permission to access it. Possible scenarios include:
- If the bucket exists and you have the permission to read it, HTTP status code 200 will be returned.
- If you do not have the permission to read the bucket, HTTP status code 403 will be returned.
- If the bucket does not exist, HTTP status code 404 will be returned.

## Request

#### Sample Request

```shell
HEAD / HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

#### Request Parameters

This API does not use any request parameter.

#### Request Headers

This API only uses common request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request Body

This API does not have a request body.

## Response

#### Response Headers

In addition to common response headers, this API returns the following response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

| Name | Description | Type |
| --- | --- | --- |
| x-cos-bucket-region | Bucket region such as `ap-beijing`, `ap-hongkong`, and `eu-frankfurt`. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | Enum |

#### Response Body

The response body of this API is empty.

#### Error Codes

There is no special error message for this API. For all error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Example

#### Request

```shell
HEAD / HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Tue, 28 May 2019 03:16:12 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1559013372;1559020572&q-key-time=1559013372;1559020572&q-header-list=date;host&q-url-param-list=&q-signature=9085930afacf1e8a0ade2697b69353b27901****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: close
Date: Tue, 28 May 2019 03:16:12 GMT
Server: tencent-cos
x-cos-bucket-region: ap-beijing
x-cos-request-id: NWNlY2E3ZmNfZjhjMDBiMDlfMTBjOWRfZDcz****
```
