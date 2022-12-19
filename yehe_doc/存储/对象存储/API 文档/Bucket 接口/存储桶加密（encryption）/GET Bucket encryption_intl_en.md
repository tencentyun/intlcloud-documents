## Feature Description

This API is used to query the default encryption configuration of a specified bucket.

To call this API, you need to have the `GetBucketEncryption` permission. By default, the bucket owner has permission to call this API and can grant this permission to other users.

## Request

**Sample request**

```sh
GET /?encryption HTTP 1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? 
> - Host: &lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com, where &lt;BucketName-APPID> is the bucket name followed by the `APPID`, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and &lt;Region> is a COS region (see [Regions and Access Endpoints](https://www.tencentcloud.com/document/product/436/6224)).
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
                <SSEAlgorithm>AES256|KMS</SSEAlgorithm>
                <KMSMasterKeyID>String</KMSMasterKeyID>
            </ApplyServerSideEncryptionByDefault>
      </Rule>
</ServerSideEncryptionConfiguration>
```


The nodes are described as follows:

| Element | Parent Node | Description | Type |
| ---------------------------------- | ---------------------------------- | ------------------------------------------------------------ | --------- |
| ServerSideEncryptionConfiguration | None | Contains the default encryption configuration parameters | Container |
| Rule | ServerSideEncryptionConfiguration | Default server-side encryption configuration rule | Container |
| ApplyServerSideEncryptionByDefault | ServerSideEncryptionConfiguration.Rule                              | Default configuration of server-side encryption | Container |
| SSEAlgorithm                       | ServerSideEncryptionConfiguration.Rule.<br>ApplyServerSideEncryptionByDefault | Valid values: `AES256` (SSE-COS mode with AES256 algorithm), `KMS` (SSE-KMS mode)  | String    |
|KMSMasterKeyID                       | ServerSideEncryptionConfiguration.Rule.<br>ApplyServerSideEncryptionByDefault | Customer master key (CMK) of KMS if `SSEAlgorithm` is set to `KMS`. If this field is not specified, the default CMK created by COS will be used. For more information, see SSE-KMS Encryption.  | String    | Yes       |

**Error Code**

This API returns common error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

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

