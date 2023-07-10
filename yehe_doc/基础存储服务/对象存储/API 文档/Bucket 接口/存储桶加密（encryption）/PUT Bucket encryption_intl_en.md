## Feature Description

This API is used to set the default encryption configuration for a bucket.

To call this API, you must have the `PutBucketEncryption` permission. By default, the bucket owner has permission to use this API and can grant such permission to other users.

## Request

**Sample request**

```sh
PUT /?encryption HTTP 1.1
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

You can configure the default encryption in the request body using the XML markup language. The configuration mainly includes the encryption item.

The following request body sets SSE-COS as the default encryption:

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

| Node | Parent Node | Description | Type | Required |
| ---------------------------------- | ---------------------------------- | -------------------------------------- | --------- | -------- |
| ServerSideEncryptionConfiguration | None | Default encryption configurations | Container | Yes |
| Rule | ServerSideEncryptionConfiguration | Default server-side encryption rule | Container | Yes |
| ApplyServerSideEncryptionByDefault | ServerSideEncryptionConfiguration.Rule                              | Default configuration for server-side encryption | Container | Yes |
| SSEAlgorithm                       | ServerSideEncryptionConfiguration.Rule.<br>ApplyServerSideEncryptionByDefault | Valid values: `AES256` (SSE-COS mode with AES256 algorithm), `KMS` (SSE-KMS mode) | String    | Yes       |
|KMSMasterKeyID                       | ServerSideEncryptionConfiguration.Rule.<br>ApplyServerSideEncryptionByDefault | Customer master key (CMK) of KMS if `SSEAlgorithm` is set to `KMS`. If this field is not specified, the default CMK created by COS will be used. For more information, see SSE-KMS Encryption.  | String    | Yes       |

## Response

**Response headers**

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

**Response body**

The response body is empty.

**Error Code**

This API returns common error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

**Request**

The following example sets SSE-COS as the default encryption for the `examplebucket-1250000000` bucket.

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
