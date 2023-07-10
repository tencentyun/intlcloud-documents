## Overview

This API is used to delete the custom domains bound to a bucket.

> ! 
>
>By default, the root account has permission to delete the custom domains bound to a bucket and can go to the [CAM console](https://console.cloud.tencent.com/cam/overview) to grant such permission to a sub-account by allowing it to call the `DeleteBucketDomain` API.
> - This API deletes all custom domains bound to the bucket. To delete only some domains, call `GET Bucket Domain` to query all custom domains bound to the bucket first, and call `PUT Bucket Domain` to bind the needed domains again.

## Request

#### Sample request

```plaintext
DELETE /?domain HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? 
> - In `Host: &lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com`, &lt;BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and &lt;Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).
> 

#### Request parameters

This API has no request parameter.

#### Request headers

This API only uses common request headers. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

This API does not have a request body.

## Response

#### Response headers

This API returns only common response headers. For more information, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body of this API is empty.

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Sample

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
