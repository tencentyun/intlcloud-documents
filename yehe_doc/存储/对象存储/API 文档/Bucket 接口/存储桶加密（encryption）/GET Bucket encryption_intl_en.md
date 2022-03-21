## Feature Description

This API is used to query the default encryption configuration of a specified bucket.

To call this API, you need to have the `GetBucketEncryption` permission. By default, the bucket owner has permission to call this API and can grant this permission to other users.

## Request

**Request sample**

```sh
GET /?encryption HTTP 1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? 
> - In `Host: <BucketName-APPID>.cos.<Region>.myqcloud.com`, <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> 

**Request parameters**

This API has no request parameter.

**Request headers**

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

**Request Body**

This API does not have a request body.

## Response

**Response headers**

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

**Response body**

The SSE-COS-encrypted response body is follows:

```sh
<ServerSideEncryptionConfiguration>
      <Rule>
            <ApplyServerSideEncryptionByDefault>
                <SSEAlgorithm>AES256</SSEAlgorithm>
            </ApplyServerSideEncryptionByDefault>
      </Rule>
</ServerSideEncryptionConfiguration>
```


The nodes are described as follows:

| Element | Parent Node | Description | Type |
| ---------------------------------- | ---------------------------------- | ------------------------------------------------------------ | --------- |
| ServerSideEncryptionConfiguration | None | Contains the default encryption configuration parameters | Container |
| Rule | ServerSideEncryptionConfiguration | Default server-side encryption configuration rule | Container |
| ApplyServerSideEncryptionByDefault | Rule | Default configuration of server-side encryption | Container |
| SSEAlgorithm | ApplyServerSideEncryptionByDefault | Server-side encryption algorithm to be used. Enumerated value: AES256 | String |

**Error Code**

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

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
            <ApplyServerSideEncryptionByDefault>
                <SSEAlgorithm>AES256</SSEAlgorithm>
            </ApplyServerSideEncryptionByDefault>
      </Rule>
</ServerSideEncryptionConfiguration>
```
