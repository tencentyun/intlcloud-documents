## Description
This API is used to upload an object to COS in parts. It supports up to 10,000 parts of 1 MB to 5 GB each in size, and the last part can be less than 1 MB.

### Notes
1. To upload an object in parts, first you need to use the `Initiate Multipart Upload` API to initialize a multipart upload. After the initialization, an `uploadId` will be returned, which uniquely identifies this upload.
2. Every time you request the `Upload Part` API, you need to pass in `partNumber`, the part number, and `uploadId`. You can upload multiple parts out of order.
3. When the `uploadId` and `partNumber` of a new part are the same as those of a previously uploaded part, the old part will be overwritten by the new one. A 404 error, `NoSuchUpload`, will be returned if the `uploadId` does not exist.

## Request
### Sample Request

```shell
PUT /<ObjectKey>?partNumber=PartNumber&uploadId=UploadId HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Length: Size
Authorization: Auth String

[Object]
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information)

### Request Headers

#### Common Headers
The implementation of this operation uses common request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special Headers
**Required Headers**
The implementation of this operation uses the following required request headers:

| Name | Description | Type | Required |
| :------------- | :---------------------------- | :----- | :--- |
| Content-Length | HTTP request length in bytes as defined in RFC 2616 | String | Yes |

**Recommended Headers**
It is recommended to use the following request headers for the implementation of this operation:

| Name | Description | Type | Required |
| :---------- | :--------------------------------------- | :----- | :--- |
| Expect | HTTP request length in bytes as defined in RFC 2616 | String | No |
| Content-MD5 | Base64-encoded 128-bit MD5 checksum as defined in RFC 1864. This header is used to verify whether the file content has changed | String | No |

#### Request Parameters
The parameters are described in details below:

| Parameter Name | Description | Type | Required |
| :--------- | :--------------------------------------- | :----- | :--- |
| partNumber  | A number which identifies this multipart upload                                       | String | Yes  |
| uploadId | ID of this multipart upload. <br>When the `Initiate Multipart Upload` API is used to initialize a multipart upload, an `uploadId` will be returned. The ID uniquely identifies the data of the part and its position in the entire file | String | Yes |

### Request Body
The request body of this request is the data content of the part.

## Response

### Response Headers
#### Common Response Headers 
This response contains common response headers. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Special Response Headers
This response may return the following response headers:

| Name | Description | Type |
| ---------------------------- | ---------------------------------------- | ------ |
| x-cos-server-side-encryption | If it is specified to use server-side encryption when the file is uploaded, this response header will be returned. Enumerated value: AES256 | String |
|x-cos-storage-class| Object storage class. COS will return this response header for all objects but those in the `STANDARD` storage class. Enumerated values: `STANDARD_IA`, `ARCHIVE`| String |

### Response Body
The response body of this request is empty.

### Error Codes
The implementation of this operation does not return special error messages. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Example

### Request
```shell
PUT /exampleobject?partNumber=1&uploadId=1484727270323ddb949d528c629235314a9ead80f0ba5d993a3d76b460e6a9cceb9633b08e HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed，18 Jan 2017 16:17:03 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484727403;32557623403&q-key-time=1484727403;32557623403&q-header-list=host&q-url-param-list=partNumber;uploadId&q-signature=bfc54518ca8fc31b3ea287f1ed2a0dd8c8e88a1d
Content-Length: 10485760

[Object]
```

### Response
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Wed，18 Jan 2017 16:17:03 GMT
Etag: "e1e5b4965bc7d30880ed6d226f78a5390f1c09fc"
Server: tencent-cos
x-cos-request-id: NTg3ZjI0NzlfOWIxZjRlXzZmNGJfMWYy
```
