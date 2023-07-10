## Description

This API (PUT Bucket encryption) is used to set the default encryption configuration for the specified bucket.

To call this API, you must have the `PutBucketEncryption` permission. By default, the bucket owner has direct permission to use this API and can grant such permission to other users.

## Request

**Sample request**

```sh
PUT /?encryption HTTP 1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

**Request Parameters**

This API does not use any request parameter.

**Request Headers**

This API only uses common request headers. For more information, see [Common Request Headers](https://cloud.tencent.com/document/product/436/7728).

**Request Body**

You can use XML in the request body to set the default encryption configuration information for a bucket. The encryption configuration information mainly contains encryption items.

Below is the request body used to set SSE-COS:

```sh
<ServerSideEncryptionConfiguration>
      <Rule>
         <ApplyServerSideEncryptionByDefault>
             <SSEAlgorithm>AES256</SSEAlgorithm>
         </ApplyServerSideEncryptionByDefault>
      </Rule>
</ServerSideEncryptionConfiguration>
```

The specific elements are as follows:

| Element Name | Parent Node | Description | Type | Required |
| ---------------------------------- | ---------------------------------- | -------------------------------------- | --------- | -------- |
| ServerSideEncryptionConfiguration | None | This contains the default encryption configuration parameters | Container | Yes |
| Rules | ServerSideEncryptionConfiguration | Default server-side encryption configuration rules | Container | Yes |
| ApplyServerSideEncryptionByDefault | Rules | Default configuration information for server-side encryption | Container | Yes |
| SSEAlgorithm | ApplyServerSideEncryptionByDefault | Server-side encryption algorithm to be used. Enumerated value: AES256 | String | Yes |

## Response

**Response Header**

This API only returns common response headers. For more information, see [Common Response Headers](https://cloud.tencent.com/document/product/436/7729).

**Response Body**

The response body return of this request is empty.

**Error Codes**

This API uses standardized error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) .

## Use Cases

**Request**

The following sample shows you how to set SSE-COS encryption configuration for the `examplebucket-1250000000` bucket.

```sh
PUT /?encryption HTTP 1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Mon, 17 Jun 2019 08:37:35 GMT
Authorization: signatureValue



<ServerSideEncryptionConfiguration>
      <Rule>
         <ApplyServerSideEncryptionByDefault>
             <SSEAlgorithm>AES256</SSEAlgorithm>
         </ApplyServerSideEncryptionByDefault>
      </Rule>
</ServerSideEncryptionConfiguration>
```

**Response**

```sh
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Date: Mon, 17 Jun 2019 08:37:36 GMT
Server: tencent-cos
x-cos-request-id: NWQwNzUxNTBfMzdiMDJhMDlfOWM0Nl85NDFk****
```
