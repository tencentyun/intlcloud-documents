## Feature Description
This API (Upload Part) is used to upload an object to COS in multiple parts. It supports at most up to 10,000 parts, each being between 1 MB to 5 GB in size. The last part can be less than 1 MB.


#### Detail analysis
1. Multipart upload needs to be initialized first with the `Initiate Multipart Upload` API. After initialization, you will obtain an `uploadId` that uniquely identifies the upload.
2. Every time you request the `Upload Part` API, you need to pass in `partNumber` (the part number) and your `uploadId`. You can upload multiple parts out of order.
3. If the `uploadId` and `partNumber` of a newly uploaded part are the same as those of a previously uploaded part, the former will overwrite the latter. A 404 error (NoSuchUpload) will be returned if the `uploadId` does not exist.

## Request

#### Sample request

```shell
PUT /<ObjectKey>partNumber=PartNumber&uploadId=UploadId HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Length: Size
Authorization: Auth String

[Object]
```

>Authorization: Auth String (for more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).


#### Request header

#### Common headers
The implementation of this request operation uses common request headers. For more information on common request headers, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special headers
**Required headers**
The following headers are required for this request operation:

| Name | Description | Type | Required |
| :------------- | :---------------------------- | :----- | :--- |
| Content-Length | HTTP request length (measured in bytes) as defined in RFC 2616 | String | Yes |

**Recommended headers**
The following headers are recommended for this request operation:

| Name | Description | Type | Required |
| :---------- | :--------------------------------------- | :----- | :--- |
| Expect | HTTP request length (measured in bytes) as defined in RFC 2616 | String | No |
| Content-MD5 | Base64-encoded MD5 hash of the request body content as defined in RFC 1864, used for performing integrity checks to verify whether the request body has changed during transfer | String | No |

#### Request parameters
The details are as follows:

| Parameter Name | Description | Type | Required |
| :--------- | :--------------------------------------- | :----- | :--- |
| partNumber | Identifies the part number of a particular multipart upload, must be greater than or equal to 1 | String | Yes |
| uploadId | Identifies the ID of a particular multipart upload. When the Initiate Multipart Upload API is used to initialize a multipart upload, an `uploadId` will be obtained. This ID not only uniquely identifies the part data, but also identifies its position in the entire file | String | Yes |


#### Request body
The request body of this request is the data content of this part.

## Response


#### Response header
#### Common response headers 
This response contains common response headers. For more information on common response headers, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Special response headers
This response may return the following response headers:

| Name | Description | Type |
| ---------------------------- | ---------------------------------------- | ------ |
| x-cos-server-side-encryption | If you specify to use server-side encryption when the file is uploaded, this response header will be returned. Enumerated value: AES256 | String |
| x-cos-storage-class | Returns an object’s storage class information. COS returns this response header for all objects except those in the Standard storage class. Enumerated values: STANDARD_IA, ARCHIVE | String |


#### Response body
The response body of this request is empty.


#### Error codes
There are no specific error messages for this request operation. For common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Use Case

#### Request
```shell
PUT /exampleobject?partNumber=1&uploadId=1484727270323ddb949d528c629235314a9ead80f0ba5d993a3d76b460e6a9cceb9633b08e HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed，18 Jan 2017 16:17:03 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUj****&q-sign-time=1484727403;32557623403&q-key-time=1484727403;32557623403&q-header-list=host&q-url-param-list=partNumber;uploadId&q-signature=bfc54518ca8fc31b3ea287f1ed2a0dd8c8e8****
Content-Length: 10485760

[Object]
```

#### Response
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
