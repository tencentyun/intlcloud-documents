## Description

This API (DELETE Bucket encryption) is used to delete the default encryption configuration of the specified bucket.

To call this API, you must have the `DeleteBucketEncryption` permission. By default, the bucket owner has direct permission to use this API and can grant such permission to other users.

## Request

**Sample request**

```sh
DELETE /?encryption HTTP 1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

**Request parameters**

This API does not use any request parameter.

**Request headers**

This API only uses common request headers. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

**Request body**

The request body of this request is empty.

## Response

**Response headers**

This API only returns common response headers. For more information, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

**Response body**

The response body return of this request is empty.

**Error codes**

There are no special error messages for this API. For all error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Use Cases

**Request**

The following example shows you how to delete the default SSE-COS encryption configuration of the `examplebucket-1250000000` bucket.

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
