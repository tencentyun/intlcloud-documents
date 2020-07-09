## Description
This API is used to copy a part from an existing object as a source path to a destination path. You specify the data source using `x-cos-copy-source` and a byte range (allowable part size between 1 MB to 5 GB) using `x-cos-copy-source-range` in your request.

>!
>- Before using this API, first initiate a multipart upload using the [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) API and specify the destination path.
>- If the destination object and the source object are in different regions, and the part size of the destination object will exceed 5 GB, you will need to use multipart upload or multipart copy API to copy the object.
>- To upload an object in parts, you must first initialize a multipart upload. A unique descriptor (upload ID) will be returned in response to the initiate request, and must be included in your upload part request.

#### Versioning
If versioning is enabled for the bucket, `x-cos-copy-source` identifies the current version of the object to be copied. If the current version is a delete marker and no version is specified in `x-cos-copy-source`, COS will consider the object as deleted and return a 404 error. If you specify a delete marker as `versionId` in the `x-cos-copy-source`, COS will return an HTTP 400 error as it is not allowed to use a delete marker as versionId in `x-cos-copy-source`.

## Request
#### Sample request

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

>?Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).


#### Request headers

#### Common headers
The implementation of this operation uses common request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special headers

**Required headers**

The implementation of this operation uses the following required request headers:

| Name | Description | Type | Required |
| ----------- | ----------- | ------------- | ---- |
| x-cos-copy-source     | URL path to the source object. A version can be specified using the `versionId` subresource | String | Yes |


**Recommended headers**

The implementation of this operation uses the following recommended request headers:

| Name | Description | Type | Required |
| ---------------- | ---------- | ------ | -------- |
| x-cos-copy-source-range | Byte range of the source object. The range value must be in the format of `bytes=first-last`, where both `first` and `last` are zero-based byte offsets.<br>For example, `bytes=0-9` means that you want to copy the first 10 bytes of data of the source object. If this parameter is not specified, the entire object will be copied | String | No |
| x-cos-copy-source-If-Modified-Since | If the object is modified after the specified time, the operation will be performed; otherwise, `412` will be returned.<br>This header can be used together with `x-cos-copy-source-If-None-Match`. If it is used together with other conditions, a conflict will be returned | String | No |
| x-cos-copy-source-If-Unmodified-Since | If the object is not modified after the specified time, the operation will be performed; otherwise, `412` will be returned.<br>This header can be used together with `x-cos-copy-source-If-Match`. If it is used together with other conditions, a conflict will be returned | String | No |
| x-cos-copy-source-If-Match | If the Etag of the object is the same as the specified one, the operation will be performed; otherwise, `412` will be returned.<br>This header can be used together with `x-cos-copy-source-If-Unmodified-Since`. If it is used together with other conditions, a conflict will be returned | String | No |
| x-cos-copy-source-If-None-Match | If the Etag of the object is different from the specified one, the operation will be performed; otherwise, `412` will be returned.<br>This header can be used together with `x-cos-copy-source-If-Modified-Since`. If it is used together with other conditions, a conflict will be returned | String | No |

#### Request parameters

 Name | Description | Type | Required
---|---|---|---
partNumber| Number of the part being copied |String| Yes
uploadId| A unique descriptor (upload ID) that is returned in response to the initiate multipart upload request required for uploading a file in parts, and must be included in your upload part request |String| Yes

#### Request body
The request body of this request is empty.

## Response

#### Response headers
#### Common response headers 
This response contains common response headers. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Special response headers

| Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Type | 
|---|---|---|
|x-cos-copy-source-version-id| Version ID of the copied source object if versioning is enabled for the source bucket |String|
|x-cos-server-side-encryption | If the object is stored with COS-managed server-side encryption, the response will contain this header and the value of the encryption algorithm used (AES256) | String|

#### Response body
This response body returns **application/xml** data. The following example contains all the node data:

```shell
<?xml version="1.0" encoding="UTF-8" ?>
<CopyPartResult>
   <ETag>"ba82b57cfdfda8bd17ad4e5879ebb4fe"</ETag>
   <LastModified>2017-09-04T04:45:45</LastModified>
</CopyPartResult>
```

The nodes are described in details below:

| Name | Description | Type |
| ---------- | ------------------- | ------ |
| CopyPartResult | Returns the result of the copy | String |
| ETag             | Returns the MD5 checksum of the object. The value of `ETag` can be used to check whether the object content has changed during transit | String |
| LastModified | Returns the last modified time of the object in GMT time | String |

#### Error codes

This API returns uniform error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples
#### Request

```HTTP
PUT /exampleobject?partNumber=1&uploadId=1505706248ca8373f8a5cd52cb129f4bcf85e11dc8833df34f4f5bcc456c99c42cd1ffa2f9 HTTP/1.1
User-Agent: curl/7.19.7 (x86_64-redhat-linux-gnu) libcurl/7.19.7 NSS/3.13.1.0 zlib/1.2.3 libidn/1.18 libssh2/1.2.2
Accept: */*
x-cos-copy-source:examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/exampleobject1
x-cos-copy-source-range: bytes=10-100
Host: examplebucket-1250000000.cos.ap-shanghai.myqcloud.com
Authorization:q-sign-algorithm=sha1&q-ak=AKIDDNMEycgLRPI2axw9xa2Hhx87wZ3M****&q-sign-time=1507530223;1508530223&q-key-time=1507530223;1508530223&q-header-list=&q-url-param-list=&q-signature=d02640c0821c49293e5c289fa07290e6b2f0****
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 133 
Connection: keep-alive 
Date: Mon, 04 Sep 2017 04:45:45 GMT
Server: tencent-cos
x-cos-request-id: NTlkYjFjYWJfMjQ4OGY3MGFfNGIz****

<CopyPartResult>
   <ETag>"ba82b57cfdfda8bd17ad4e5879ebb4fe"</ETag>
   <LastModified>2017-09-04T04:45:45</LastModified>
</CopyPartResult>
```
