## Description

This document describes the common request headers that may be used in API requests. The headers mentioned below will not be addressed again in related API documents.

### Request Headers

| Header Name | Description | Type | Required |
| -------------------- | ------------------------------------------------------------ | ------- | ------------------------------------------------------------ |
| Authorization | Carries the authentication information, i.e., signing information used to verify the validity of a request. <br>This header is optional for public-read objects or if the authentication information is passed in through request parameters. For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) | string | Yes. <br>This header is optional for public-read objects or if the authentication information is passed in through request parameters |
| Content-Length | HTTP request length in bytes as defined in RFC 2616 | integer | No. <br>This header is required for `PUT` and `POST` requests (except for `PUT Object` requests where the `Transfer-Encoding` request header is specified) |
| Content-Type | HTTP request content type (MIME) as defined in RFC 2616. <br>For example, `application/xml`, `image/jpeg` | string | No. <br>This header is required for `PUT` and `POST` requests with a request body |
| Content-MD5 | Base64-encoded MD5 hash value of the request body content as defined in RFC 1864, such as `ZzD3iDJdrMAAb00lgLLeig==`. <br>This header is used for integrity check to verify whether the request body has changed during the transfer. <br>For `PUT` and `POST` requests with a request body (except for `POST Object` requests), we highly recommend you carry this header | string | No |
| Date | Current time in GMT format as defined in RFC 1123, such as `Wed, 29 May 2019 04:10:12 GMT` | string | No |
| Host | Requested host in the format of `<BucketName-APPID>.cos.<Region>.myqcloud.com` | string  | Yes |
| x-cos-security-token | The security token field that needs to be passed in when temporary security credentials are used. For more information, see [Temporary Security Credentials](https://intl.cloud.tencent.com/document/product/436/30613) | string | No. <br>This header is required when a temporary key is used and the authentication information is carried through `Authorization` |

## Server-side encryption headers

For APIs that support server-side encryption (SSE), the following request headers are applicable based on different encryption methods, please refer to specific API documents to determine whether SSE is applicable. Whether the following headers are required is only for scenarios where SSE is used. If you request an API that does not support or use SSE, the following headers do not need to be carried. For more information, see [Server-side Encryption Overview](https://intl.cloud.tencent.com/document/product/436/18145).

#### SSE-COS

| Header Name | Description | Type | Required |
| ---------------------------- | -------------------------------------------- | ------ | ------------------------------------------------------------ |
| x-cos-server-side-encryption | Server-side encryption algorithm, currently only AES256 is supported | string | Required when you upload or copy objects (including simple upload/copy and multipart upload/copy). This header cannot be specified when you download objects |

#### SSE-KMS

| Header Name | Description | Type | Required |
| ------------------------------------------- | ------------------------------------------------------------ | ------ | ------------------------------------------------------------ |
| x-cos-server-side-encryption | Server-side encryption algorithm, currently only AES256 is supported | string | Required when you upload or copy objects (including simple upload/copy and multipart upload/copy). This header cannot be specified when you download objects |
| x-cos-server-side-encryption-cos-kms-key-id | When x-cos-server-side-encryption value is cos/kms, it is used to specify the user master key (CMK) of KMS. If not specified, the default CMK created by COS is used. For more details, see [SSE-KMS Encryption](https://intl.cloud.tencent.com/document/product/436/18145) | string | No |
x-cos-server-side-encryption-context | When the x-cos-server-side-encryption value is cos/kms, it is used to specify the encryption context, and the value is a Base64-encoded string holding JSON with the key-value pairs for the encryption context. <br> For example, `eyJhIjoiYXNkZmEiLCJiIjoiMTIzMzIxIn0 =` | string | No |



#### SSE-C

| Header Name | Description | Type | Required |
| ----------------------------------------------- | ------------------------------------------------------------ | ------ | -------- |
| x-cos-server-side-encryption-customer-algorithm | Server-side encryption algorithm, currently only AES256 is supported | string | Yes |
| x-cos-server-side-encryption-customer-key | Base64-encoded server-side encryption key. <br>For example, `MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=` | string | Yes       |
| x-cos-server-side-encryption-customer-key-MD5  | Base64-encoded MD5 hash of the server-side encryption key. <br>For example, `U5L61r7jcwdNvT7frmUG8g==` | string | Yes       |
