## Description
This API (Upload Part - Copy) is used to copy the parts of an object from the source path to the destination path. You can use x-cos-copy-source to specify the source object and use x-cos-copy-source-range to specify the byte range (allowed part size: 1 MB - 5 GB).

>!
>- If the destination object and the source object are in different regions, and the part size of the destination object will exceed 5 GB, you need to use multipart upload or multipart copy API to copy the object.
>- To upload an object in parts, you must first initialize the multipart upload. A unique descriptor (upload ID) will be returned in the response of multipart upload initialization, which needs to be carried in the multipart upload request.

### Version
If versioning is enabled for the bucket, x-cos-copy-source identifies the current version of the object being copied. If the current version is a delete marker and no version is specified for x-cos-copy-source, then COS will consider that the object has been deleted and return a 404 error. If you specify a versionId in x-cos-copy-sourceand and the versionId is a delete marker, COS will return an HTTP 400 error as the delete marker is not allowed as the version of x-cos-copy-source.

## Request
### Sample Request

```http
PUT /examplebucket?partNumber=PartNumber&uploadId=UploadId  HTTP/1.1
Host: <Bucketname-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
x-cos-copy-source: <Bucketname>-<APPID>.cos.<Region>.myqcloud.com/filepath
x-cos-copy-source-range: bytes=first-last
x-cos-copy-source-if-match: etag
x-cos-copy-source-if-none-match : etag
x-cos-copy-source-if-unmodified-since: time_stamp
x-cos-copy-source-if-modified-since: time_stamp
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).


### Request Headers

#### Common Headers
The implementation of this request operation uses a common request header. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special Headers

**Required headers**

The implementation of this request operation uses the following required request headers:

| Name | Description | Type | Required |
| ----------- | ----------- | ------------- | ---- |
| x-cos-copy-source     | Source object URL path. A previous version can be specified using the versionid sub-resource | String | Yes |


**Recommended headers**

The implementation of this request operation uses the following recommended request headers:

| Name | Description | Type | Required |
| ---------------- | ---------- | ------ | -------- |
| x-cos-copy-source-range | Byte range of the source object. The range value must be in the format of bytes=first-last, where both first and last are offsets starting from 0. <br>For example, bytes=0-9 means that you want to copy the first 10 bytes of data of the source object. If this parameter is not specified, the entire object will be copied | String | No |
| x-cos-copy-source-If-Modified-Since | If the object is modified after the specified time, the operation will be performed; otherwise, 412 will be returned. <br>This parameter can be used together with x-cos-copy-source-If-None-Match. If it is used together with other conditions, a conflict will be returned | String | No |
| x-cos-copy-source-If-Unmodified-Since | If the object is not modified after the specified time, the operation will be performed; otherwise, 412 will be returned. <br>This parameter can be used together with x-cos-copy-source-If-Match. If it is used together with other conditions, a conflict will be returned | String | No |
| x-cos-copy-source-If-Match | If the Etag of the object is the same as the specified one, the operation will be performed; otherwise, 412 will be returned. <br>This parameter can be used together with x-cos-copy-source-If-Unmodified-Since. If it is used together with other conditions, a conflict will be returned | String | No |
| x-cos-copy-source-If-None-Match | If the Etag of the object is different from the specified one, the operation will be performed; otherwise, 412 will be returned. <br>This parameter can be used together with x-cos-copy-source-If-Modified-Since. If it is used together with other conditions, a conflict will be returned | string | No |

### Request Parameter

 Name | Description | Type | Required
---|---|---|---
partNumber| Part number during the multipart copy |String| Yes
uploadId| To upload a file in parts, you must first initialize the multipart upload. A unique descriptor (upload ID) will be returned in the response of multipart upload initialization, which needs to be carried in the multipart upload request |String| Yes

### Request Body
The request body of this request is empty.

## Response

### Response Headers
#### Common Response Headers 
This response contains a common response header. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Special Response Headers

Name | Description | Type
---|---|---
x-cos-copy-source-version-id| Version of the copied source object if versioning is enabled for the source bucket |String
x-cos-server-side-encryption | If the object is stored with COS-managed server-side encryption, the response will contain the values of this header and the encryption algorithm used (AES256) | String

### Response Body
The return of this response body is **application/xml** data. Below is a sample containing all the node data:

```shell
<?xml version="1.0" encoding="UTF-8" ?>
<CopyPartResult>
   <ETag>"ba82b57cfdfda8bd17ad4e5879ebb4fe"</ETag>
   <LastModified>2017-09-04T04:45:45</LastModified>
</CopyPartResult>
```

Detailed data is as shown below:

| Name | Description | Type |
| ---------- | ------------------- | ------ |
| CopyPartResult | Returns the copy result information | String |
| ETag             | Returns the MD5 checksum of the object. The value of ETag can be used to check whether the object content has changed | String |
| LastModified | Returns the last modified time of the object in GMT time | String |

## Samples
### Request

```HTTP
PUT /exampleobject?partNumber=1&uploadId=1505706248ca8373f8a5cd52cb129f4bcf85e11dc8833df34f4f5bcc456c99c42cd1ffa2f9 HTTP/1.1
User-Agent: curl/7.19.7 (x86_64-redhat-linux-gnu) libcurl/7.19.7 NSS/3.13.1.0 zlib/1.2.3 libidn/1.18 libssh2/1.2.2
Accept: */*
x-cos-copy-source:examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/exampleobject1
x-cos-copy-source-range: bytes=10-100
Host: examplebucket-1250000000.cos.ap-shanghai.myqcloud.com
Authorization:q-sign-algorithm=sha1&q-ak=AKIDDNMEycgLRPI2axw9xa2Hhx87wZ3MqQCn&q-sign-time=1507530223;1508530223&q-key-time=1507530223;1508530223&q-header-list=&q-url-param-list=&q-signature=d02640c0821c49293e5c289fa07290e6b2f05cb2
```

### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 133 
Connection: keep-alive 
Date: Mon, 04 Sep 2017 04:45:45 GMT
Server: tencent-cos
x-cos-request-id: NTlkYjFjYWJfMjQ4OGY3MGFfNGIzZV9k

<CopyPartResult>
   <ETag>"ba82b57cfdfda8bd17ad4e5879ebb4fe"</ETag>
   <LastModified>2017-09-04T04:45:45</LastModified>
</CopyPartResult>
```
