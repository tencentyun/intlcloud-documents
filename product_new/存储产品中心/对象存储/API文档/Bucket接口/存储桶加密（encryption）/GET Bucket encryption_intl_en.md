## Description

This API (GET Bucket encryption) is used to query the default encryption configuration of the specified bucket.

To call this API, you must have the `GetBucketEncryption` permission. By default, the bucket owner has direct permission to use this API and can grant such permission to other users.

## Request

**Sample request**

```sh
GET /?encryption HTTP 1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

**Request parameters**

This API does not use any request parameter.

**Request headers**

This API only uses common request headers. For more information, please see [Common Request Headers](https://cloud.tencent.com/document/product/436/7728).

**Request body**

This API does not have a request body.

## Response

**Response headers**

This API only returns common response headers. For more information, please see [Common Response Headers](https://cloud.tencent.com/document/product/436/7729).

**Response body**

The following response elements will be returned:

| Element Name | Parent Node | Description | Type |
| ---------------------------------- | ---------------------------------- | ------------------------------------------------------------ | --------- |
| ServerSideEncryptionConfiguration | None | This contains the default encryption configuration parameters | Container |
| Rules | ServerSideEncryptionConfiguration | Default server-side encryption configuration rule | Container |
| ApplyServerSideEncryptionByDefault | Rules | Default configuration information of server-side encryption | Container |
| SSEAlgorithm | ApplyServerSideEncryptionByDefault | Server-side encryption algorithm to be used. Enumerated value: AES256 | String |

**Error codes**

There are no special error messages for this API. For all error messages, please see [Error Codes](https://cloud.tencent.com/document/product/436/7730).

## Use Cases

**Request**

```sh
GET /?encryption HTTP 1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Mon, 17 Jun 2019 08:37:35 GMT
Authorization: signatureValue
```

**Response**

```sh
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: xxxx
Date: Mon, 17 Jun 2019 08:37:36 GMT
Server: tencent-cos
x-cos-request-id: NWQwNzUxNTBfMzdiMDJhMDlfOWM0Nl85NDFk****

<?xml version = "1.0" encoding = "UTF-8">
<ServerSideEncryptionConfiguration>
   <Rule>
      <ApplySideEncryptionConfiguration>
         <SSEAlgorithm>AES256</SSEAlgorithm>
      </ApplySideEncryptionConfiguration>
   </Rule>
</ServerSideEncryptionConfiguration>
```
