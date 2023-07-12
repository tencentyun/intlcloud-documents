## Overview
This API is used to copy the parts of an object from the source path to the destination path. You can use `x-cos-copy-source` to specify the source object and use `x-cos-copy-source-range` to specify the byte range to copy (each part should be 1 MB to 5 GB).

>?The following two types of accounts can call this API:
>- Have the root account permissions.
>- Have the `GetObjecet` API permission of the source object and the `InitiateMultipartUpload`, `ListMultipartUploads`, `ListParts`, `PutObject`, `CompleteMultipartUpload`, and `AbortMultipartUpload` API permissions under the destination path.

>!
>- To call this API, you need to first call the [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) API to initialize the multipart upload and specify the destination path.
>- If the source and destination objects reside in two different regions and the part size is larger than 5 GB, use the multipart upload or multipart copy API to copy the object.
>- To upload an object in parts, you must first initialize the multipart upload. The response of the multipart upload initialization will include a unique descriptor `uploadId`, which needs to be carried in the multipart upload request.


<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer (recommended)
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=UploadPartCopy&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                Tencent Cloud API Explorer makes it easy for you to make online API calls, verify signatures, generate SDK code, and search for APIs. You can use it to query the request and response of each API call and generate sample SDK codes for the call.
            </div>
        </div>
    </div>
</div>

#### Versioning
If versioning is enabled for the bucket, `x-cos-copy-source` identifies the current version of the object to copy. If the current version is a delete marker and no version is specified in `x-cos-copy-source`, COS will consider that the object has been deleted and return a 404 error. If you specify a `versionId` in `x-cos-copy-source` and the `versionId` is a delete marker, COS will return an HTTP 400 error as delete markers cannot be set in `x-cos-copy-source`.

## Request
#### Sample request

```shell
PUT /<ObjectKey>?partNumber=PartNumber&uploadId=UploadId  HTTP/1.1
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

>? 
> - Host: <BucketName-APPID>.cos.<Region>.myqcloud.com, where <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://www.tencentcloud.com/document/product/436/6224)).
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> 


#### Request headers

#### Common request headers
This API uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Non-common request headers

**Required headers**

This API uses the following required header:

| Header | Description | Type | Required |
| ----------- | ----------- | ------------- | ---- |
| x-cos-copy-source     | URL of the source object. You can use `versionid` to specify the `versionId` of the object. | String | Yes |


**Recommended headers**

This API uses the following recommended headers:

| Header | Description | Type | Required |
| ---------------- | ---------- | ------ | -------- |
| x-cos-copy-source-range | Byte range of the source object. The range value must be in the format of `bytes=first-last`, where both `first` and `last` are offsets starting from 0. <br>For example, `bytes=0-9` means that you want to copy the first 10 bytes of data of the source object. If this parameter is not specified, the entire object will be copied. | String | No |
| x-cos-copy-source-If-Modified-Since | If the object is modified after the specified time, the operation will be performed; otherwise, 412 will be returned. <br>This parameter can be used together with `x-cos-copy-source-If-None-Match`. If it is used together with other conditions, a conflict will be returned. | String | No |
| x-cos-copy-source-If-Unmodified-Since | If the object is not modified after the specified time, the operation will be performed; otherwise, 412 will be returned. <br>This parameter can be used together with `x-cos-copy-source-If-Match`. If it is used together with other conditions, a conflict will be returned. | String | No |
| x-cos-copy-source-If-Match | If the `ETag` of the object is the same as the specified one, the operation will be performed; otherwise, 412 will be returned. <br>This parameter can be used together with `x-cos-copy-source-If-Unmodified-Since`. If it is used together with other conditions, a conflict will be returned. | String | No |
| x-cos-copy-source-If-None-Match | If the `ETag` of the object is different from the specified one, the operation will be performed; otherwise, 412 will be returned. <br>This parameter can be used together with `x-cos-copy-source-If-Modified-Since`. If it is used together with other conditions, a conflict will be returned. | string | No |

#### Request parameters

 | Parameter | Description | Type | Required |
---|---|---|---
| partNumber | Part number | String | Yes |
| uploadId | To upload an object in parts, you must first initialize the multipart upload. The response of the multipart upload initialization will carry a unique descriptor (`uploadId`), which needs to be carried in the multipart upload request. | String | Yes |

#### Request body
The request body of this request is empty.

## Response

#### Response headers
#### Common response headers 
This API uses [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Non-common response headers

|Header &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| Description | Type |
|---|---|---|
| x-cos-copy-source-version-id | Version ID of the source object to copy (if versioning is enabled for the source bucket) | String |
| x-cos-server-side-encryption | If the object is stored with COS-managed server-side encryption, the response will contain this header and the encryption algorithm used (AES256). | String |

#### Response body
The response body returns **application/xml** data. The following contains all the nodes:

```shell
<?xml version="1.0" encoding="UTF-8" ?>
<CopyPartResult>
   <ETag>"ba82b57cfdfda8bd17ad4e5879ebb4fe"</ETag>
   <LastModified>2017-09-04T04:45:45</LastModified>
</CopyPartResult>
```

The nodes are described as follows:

| Parameter | Description | Type |
| ---------- | ------------------- | ------ |
| CopyPartResult | Results of the copy | String |
| ETag | MD5 checksum of the object. `ETag` can be used to check whether the object content has changed. | String |
| LastModified | Last modified time of the object, in GMT format | String |

#### Error codes

This API returns common error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples
#### Request

```shell
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
