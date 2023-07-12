## Description

This document describes the common request headers that may be used in API requests. The headers mentioned below will not be addressed again in related API documents.

## Request Headers


<table>
<thead>
<tr>
<th width="15%">Header Name</th>
<th width="40%">Description</th>
<th width="10%">Type</th>
<th width="35%">Required</th>
</tr>
</thead>
<tbody><tr>
<td>Authorization</td>
<td>Contains authentication information as part of the signature that authenticates a request<br>Not required if the object is public read, or if the authentication information is passed using request parameters. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/7778">Request Signature</a>.</td>
<td>string</td>
<td>Yes<br>Optional if it is used for a public-read object, or the authentication information is passed using request parameters</td>
</tr>
<tr>
<td nowrap="nowrap">Content-Length</td>
<td>The length of the content of an HTTP request in bytes defined in RFC 2616</td>
<td>integer</td>
<td><li>Required for PUT and POST requests (excluding PUT Object requests with Transfer-Encoding specified)<br><li>Cannot be used for GET, HEAD, DELETE or OPTIONS requests</td>
</tr>
<tr>
<td>Content-Type</td>
<td>The content type (MIME) of an HTTP request as defined in RFC 2616<br>Example: <code>application/xml</code> or <code>image/jpeg</code></td>
<td>string</td>
<td><li>Required for PUT and POST requests<br><li>Cannot be used for GET, HEAD, DELETE or OPTION requests</td>
</tr>
<tr>
<td>Content-MD5</td>
<td>The Base64-encoded 16-byte MD5 hash in binary format of request body content as defined in RFC 1864. It is used as an integrity check to verify whether the request body has changed during transit. The final value should be 24 characters in length. Please write code using the correct method and parameters, for example <code>ZzD3iDJdrMAAb00lgLLeig==</code>.</td>
<td>string</td>
<td><li>Required for PUT and POST requests (except POST Object requests)<br><li>Cannot be used for GET, HEAD, DELETE or OPTION requests</td>
</tr>
<tr>
<td>Date</td>
<td>Current time in GMT as defined in RFC 1123, such as <code>Wed, 29 May 2019 04:10:12 GMT</code></td>
<td>string</td>
<td>No</td>
</tr>
<tr>
<td>Host</td>
<td>Request CVM in the format <code>&lt;BucketName-APPID&gt;.cos.&lt;Region&gt;.myqcloud.com</code></td>
<td>string</td>
<td>Yes</td>
</tr>
<tr>
<td nowrap="nowrap">x-cos-security-token</td>
<td>The security token field required when using temporary security credentials. See <a href="https://intl.cloud.tencent.com/document/product/436/30613">Temporary security credentials</a> under Creating Request Overview.</td>
<td nowrap="nowrap">string</td>
<td>No<br>Required if temporary key is used and authentication information is passed using the `Authorization` header</td>
</tr>
</tbody></table>






## Server-Side Encryption Headers

For APIs that support server-side encryption (SSE), the following request headers apply based on the different encryption methods. See API-specific documents to find whether they are applicable. These headers are required only for SSE-based scenarios, but not for cases where the request doesn’t not support SSE APIs or not use SSE. For more information, see [Server-side Encryption Overview](https://intl.cloud.tencent.com/document/product/436/18145).

#### SSE-COS

| Header Name | Description | Type | Required |
| ---------------------------- | -------------------------------------------- | ------ | ------------------------------------------------------------ |
| x-cos-server-side-encryption | Server-side encryption algorithm; set to AES256 if using SSE-COS | string | Required when you upload or copy objects (including simple upload/copy and multipart upload/copy). This header cannot be specified when you download objects. |

#### SSE-KMS

| Header Name | Description | Type | Required |
| ------------------------------------------- | ------------------------------------------------------------ | ------ | ------------------------------------------------------------ |
| x-cos-server-side-encryption | Server-side encryption algorithm; set to cos/kms if using SSE-KMS | string | Required when you upload or copy objects (including simple upload/copy and multipart upload/copy). This header cannot be specified when you download objects |
| x-cos-server-side-encryption-cos-kms-key-id | Specifies the KMS customer master key (CMK) when the `x-cos-server-side-encryption` value is cos/kms. If not specified, the default CMK created by COS is used. For more information, see [SSE-KMS Encryption](https://intl.cloud.tencent.com/document/product/436/18145#sse-kms-.E5.8A.A0.E5.AF.86) | string | No |
| x-cos-server-side-encryption-context | Specifies the encryption context when the `x-cos-server-side-encryption` value is cos/kms. This value is a Base64-encoded string holding JSON with the key-value pairs for the encryption context.<br> For example, `eyJhIjoiYXNkZmEiLCJiIjoiMTIzMzIxIn0=` | string | No |



#### SSE-C

| Header Name | Description | Type | Required |
| ----------------------------------------------- | ------------------------------------------------------------ | ------ | -------- |
| x-cos-server-side-encryption-customer-algorithm | Server-side encryption algorithm; currently only AES256 is supported | string | Yes |
| x-cos-server-side-encryption-customer-key | Base64-encoded server-side encryption key. <br>For example, `MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=` | string | Yes       |
| x-cos-server-side-encryption-customer-key-MD5   | Base64-encoded MD5 hash of the server-side encryption key. <br>For example, `U5L61r7jcwdNvT7frmUG8g==` | string | Yes       |
