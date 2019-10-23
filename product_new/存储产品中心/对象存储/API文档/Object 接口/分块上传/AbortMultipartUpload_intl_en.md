## Description
This API (Abort Multipart Upload) is used to abort a multipart upload and delete the uploaded parts. When you call this API, if there is a request that is uploading a part using the Upload Parts API, the request will fail. If the UploadId does not exist, 404 NoSuchUpload will be returned.

>  It is recommended that you either complete or abort the multipart upload in a timely manner, as the parts that have been uploaded but not completed will take up storage space and incur storage fees.

## Request

### Sample Request
```shell
DELETE /<ObjectKey>?uploadId=UploadId HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

#### Request Parameters

See the details below:

| Parameter Name | Description | Type | Required |
|---|---|---|---|
|uploadId| ID of this multipart upload. <br>When the Initiate Multipart Upload API is used to initialize a multipart upload, an uploadId will be obtained, which not only uniquely identifies the data but also identifies the data position in the entire file |String| Yes |

### Request Headers

#### Common Headers
The implementation of this request operation uses a common request header. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special Headers
This request operation has no special request headers.


### Request Body
The request body of this request is empty.

## Response

### Response Headers
#### Common Response Headers 
This response uses a common response header. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Special Response Headers
This request operation has no special response headers.


### Response Body
The response body of this request is empty.


## Samples

### Request
```shell
DELETE /exampleobject?uploadId=1484727270323ddb949d528c629235314a9ead80f0ba5d993a3d76b460e6a9cceb9633b08e HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Tue, 26 Oct 2013 21:22:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484728626;32557624626&q-key-time=1484728626;32557624626&q-header-list=host&q-url-param-list=uploadId&q-signature=2d3036b57cade4a257b48a3a5dc922779a562b18
```

### Response
```shell
HTTP/1.1 204 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Tue, 26 Oct 2013 21:22:00 GMT
Server: tencent-cos
x-cos-request-id: NTg3ZjI5MzlfOTgxZjRlXzZhYjNfMjBh
```
