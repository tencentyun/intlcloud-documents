## Description

This document describes the common request headers that will be used by APIs. The headers mentioned below will not be detailed again in specific API documents.

### Request Headers

| Header Name | Description | Type | Required |
| -------------------- | ------------------------------------------------------------ | ------- | ------------------------------------------------------------ |
| Authorization | Authentication information, such as signing information used to verify the validity of request. <br>This header is optional for public-read objects or if the authentication information is passed in through the request parameters. For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778). | string | Yes. <br>This header is optional for public-read objects or if the authentication information is passed in through the request parameters. |
| Content-Length | HTTP request length in bytes as defined in RFC 2616 | integer | No. <br>This header is required for PUT and POST requests (except PUT Object requests where the Transfer-Encoding header is specified). |
| Content-Type | HTTP request content type (MIME) as defined in RFC 2616 <br>Examples: `application/xml`, `image/jpeg` | string | No. <br>This header is required for PUT and POST requests with a request body. |
| Content-MD5 | Base64-encoded MD5 hash value of the request body content as defined in RFC 1864, such as `ZzD3iDJdrMAAb00lgLLeig==` <br>This header is used for integrity check to verify whether the request body has changed during transmission. <br>For PUT and POST requests with a request body (except POST Object requests), it is highly recommended to carry this header. | string | No |
| Date | Current time in GMT format as defined in RFC 1123, such as `Wed, 29 May 2019 04:10:12 GMT` | string | No |
| Host | Requested host in the format of `<BucketName-APPID>.cos.<Region>.myqcloud.com` | string  | Yes |
| x-cos-security-token | The security token field that needs to be passed in when temporary security credentials are used. For more information, see [Temporary Security Credentials](https://intl.cloud.tencent.com/document/product/436/30613) | string | No. <br>This header is required when a temporary key is used and the authentication information is carried through Authorization. |

## Server-side Encryption Headers

For APIs that support server-side encryption (SSE), the following request headers are applicable based on different encryption methods. Please consult the specific API documents to determine whether SSE is applicable. Whether the following headers are required is only for scenarios where SSE is used. If you request an API that does not support or use SSE, the following headers do not need to be carried. For more information, see [Server-side Encryption Overview](https://intl.cloud.tencent.com/document/product/436/18145).

#### SSE-COS

| Header Name | Description | Type | Required |
| ---------------------------- | --------------------------------- | ------ | ------------------------------------------------------------ |
| x-cos-server-side-encryption | Server-side encryption algorithm, which currently can only be AES256 | string | Required when uploading or copying objects (including simple upload/copy and multipart upload/copy). This header cannot be specified when downloading objects |

#### SSE-C

| Header Name | Description | Type | Required |
| ----------------------------------------------- | ------------------------------------------------------------ | ------ | -------- |
| x-cos-server-side-encryption-customer-algorithm | Server-side encryption algorithm, which currently can only be AES256 | string | Yes |
| x-cos-server-side-encryption-customer-key       | Base64-encoded server-side encryption key, <br>such as `MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=` | string | Yes       |
| x-cos-server-side-encryption-customer-key-MD5  | Base64-encoded MD5 hash of the server-side encryption key, <br>such as `U5L61r7jcwdNvT7frmUG8g==` | string | Yes       |
