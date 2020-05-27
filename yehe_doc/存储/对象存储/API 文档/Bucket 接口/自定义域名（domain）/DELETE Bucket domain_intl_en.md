## Feature

This API (DELETE Bucket domain) is used to delete the custom domain name configuration on a bucket.

> 
>
>By default, the root account owns the permissions to delete the custom domain name of a bucket. For a sub-account to do so, the root account should grant it the access to the `DeleteBucketDomain` API in the [CAM Console](https://console.cloud.tencent.com/cam/overview).
> - Please note that this API deletes all custom domain names bound to the specified bucket. To delete only part of them, you can get all the custom domain names by calling the `GET Bucket Domain` API, and then rewrite the part not to be deleted by calling the `PUT Bucket Domain` API.

## Request

#### Request samples

```plaintext
DELETE /?domain HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

#### Request parameters

This API does not use any request parameter.

#### Request headers

This API only uses common request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

This API does not have a request body.

## Response

#### Response headers

This API only returns a common response header. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body of this API is empty.

#### Error codes

This API returns uniform error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Use Cases

#### Request

```plaintext
DELETE /?domain HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 29 Apr 2020 09:10:59 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1588151459;1588158659&q-key-time=1588151459;1588158659&q-header-list=date;host&q-url-param-list=domain&q-signature=813ddfaa3de3882f4b5ed2e0683e8a5f09e4****
Connection: close
```

#### Response

```plaintext
HTTP/1.1 204 No Content
Connection: close
Date: Wed, 29 Apr 2020 09:11:00 GMT
Server: tencent-cos
x-cos-request-id: NWVhOTQ0YTNfYWZjOTJhMDlfMWNhYTBfOTEw****
x-cos-trace-id: OGVmYzZiMmQzYjA2OWNhODk0NTRkMTBiOWVmMDAxODczNTBmNjMwZmQ0MTZkMjg0NjlkNTYyNmY4ZTRkZTk0NzJmZTI0ZmJhYTZmZjYyNmU5ZGNlZDI5YjkyODkwYjNhZjFjMTVmYjUyNmEyY2VjMjAzMGI5NWM5ZmZlOWQyZGY=
Content-Length: 0
```