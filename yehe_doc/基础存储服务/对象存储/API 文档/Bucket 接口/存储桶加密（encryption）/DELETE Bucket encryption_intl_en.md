## Overview

This API is used to delete the default encryption configuration from a bucket.

To call this API, you need to have the `DeleteBucketEncryption` permission. By default, the bucket owner has permission to call this API and can grant this permission to other users.

## Request

**Sample request**

```sh
DELETE /?encryption HTTP 1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? 
> - In `Host: &lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com`, &lt;BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and &lt;Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).
> 

**Request parameters**

This API has no request parameter.

**Request headers**

This API only uses common request headers. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

**Request body**

The request body of this request is empty.

## Response

**Response header**

This API returns only common response headers. For more information, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

**Response body**

The response body of this API is empty.

**Error codes**

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Sample

**Request**

The following example deletes the default SSE-COS encryption configuration from the `examplebucket-1250000000` bucket:

```sh
DELETE /?encryption HTTP 1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Mon, 17 Jun 2019 08:37:35 GMT
Authorization: signatureValue
```

**Response**

```sh
HTTP/1.1 204 No Content
Server: tencent-cos
Date: Mon, 17 Jun 2019 08:37:36 GMT
x-cos-request-id: NWQwNzUxNTBfMzdiMDJhMDlfOWM0Nl85NDFk****
```
