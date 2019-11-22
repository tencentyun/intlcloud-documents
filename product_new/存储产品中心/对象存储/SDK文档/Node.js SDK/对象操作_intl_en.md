## Overview

This document provides an overview of APIs related to simple object operations, multipart upload, and other operations, corresponding SDK sample code, and usage examples.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ---------------------------------------- |
| [GET Bucket（List Object）](https://intl.cloud.tencent.com/document/product/436/30614) | Querying object list | Queries some or all objects in a bucket |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Simply uploading an object | Uploads an object to a bucket |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | Uploading an Object Using a Form | Uploads an object using a form request |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |
| [OPTIONS Object](https://intl.cloud.tencent.com/document/product/436/8288) | Pre-requesting cross-origin configuration | Uses a pre-request to confirm whether a real cross-origin request can be sent |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object | Copies an object to the destination path (object key) |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes the specified object in a bucket |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes objects in a bucket in batches |

**Multipart upload operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying a multipart upload | Queries the information of a multipart upload in progress |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload task |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads object parts |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries uploaded parts in the specified multipart upload operation |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of the entire file |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload operation and deletes the uploaded parts |

**Other operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Retrieves an archived object for access |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting object ACL | Sets the ACL for the specified object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying object ACL | Queries the ACL of an object |

## Simple Operations

### Querying Object List

#### Feature Description

This API is used to query some or all objects in a bucket.

#### Samples

Sample 1. List all files in directory a.

```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',     /* Required */
    Prefix: 'a/',           /* Optional */
}, function(err, data) {
    console.log(err || data.Contents);
});
```

Return value format:

```json
{
    "Name": "examplebucket-1250000000",
    "Prefix": "",
    "Marker": "a/",
    "MaxKeys": "1000",
    "Delimiter": "",
    "IsTruncated": "false",
    "Contents": [{
        "Key": "a/3mb.zip",
        "LastModified": "2018-10-18T07:08:03.000Z",
        "ETag": "\"05a9a30179f3db7b63136f30aa6aacae-3\"",
        "Size": "3145728",
        "Owner": {
            "ID": "1250000000",
            "DisplayName": "1250000000"
        },
        "StorageClass": "STANDARD"
    }],
    "statusCode": 200,
    "headers": {}
}
```

Sample 2. List files in directory a with no deep traversal.

```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Prefix: 'a/',              /* Optional */
    Delimiter: '/',            /* Optional */
}, function(err, data) {
    console.log(err || data.CommonPrefix);
});
```

Return value format:

```json
{
    "Name": "examplebucket-1250000000",
    "Prefix": "a/",
    "Marker": "",
    "MaxKeys": "1000",
    "Delimiter": "/",
    "IsTruncated": "false",
    "CommonPrefixes": [{
        "Prefix": "a/1/"
    }],
    "Contents": [{
        "Key": "a/3mb.zip",
        "LastModified": "2018-10-18T07:08:03.000Z",
        "ETag": "\"05a9a30179f3db7b63136f30aa6aacae-3\"",
        "Size": "3145728",
        "Owner": {
            "ID": "1250000000",
            "DisplayName": "1250000000"
        },
        "StorageClass": "STANDARD"
    }],
    "statusCode": 200,
    "headers": {}
}
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Prefix | Prefix match, used to specify the prefix address of the file returned | String | No |
| Delimiter | The delimiter is a separator symbol which is generally `/`. If there is a prefix, the identical paths between prefix and delimiter are grouped into one class and defined as a common prefix, and then all common prefixes are listed. If there is no prefix, it starts at the beginning of the path | String | No |
| Marker | By default, entries are listed in UTF-8 binary order, and the entry list starts at marker | String | No |
| MaxKeys | Maximum number of entries returned at a time. Default value: 1,000 | String | No |
| EncodingType | Specifies the encoding method of the return value; value range: url | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ---------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - headers | Header information returned by the request | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| CommonPrefixes | The identical paths between prefix and delimiter are grouped into one class and defined as a common prefix | ObjectArray |
| - - Prefix | A single common prefix | String |
| - - Name | Describes bucket information | String |
| - Prefix | Prefix match, used to specify the prefix address of the file returned | String |
| - Marker | By default, entries are listed in UTF-8 binary order, and the entry list starts at marker | String |
| - MaxKeys | Maximum number of results returned in one response | String |
| - IsTruncated | Whether response entries are truncated; string type; value range: 'true', 'false' | String |
| - NextMarker | If the returned entries are truncated, then NextMarker is the starting point of the next entry | String |
| - Encoding-Type | Encoding method of the return value, which is effective for Delimiter, Marker, Prefix, NextMarker, and Key | String |
| - Contents | Metadata | ObjectArray |
| - - ETag | MD5 checksum of the file, <br>such as `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and end** | String |
| - - Size | Describes the file size in bytes | String |
| - - Key | Object name | String |
| - - LastModified | Describes the last modified time of the object, such as 2017-06-23T12:33:27.000Z | String |
| - - Owner | Bucket owner information | Object |
| - ID | Bucket AppID | String |
| - StorageClass | Object storage class; enumerated values: STANDARD, STANDARD_IA, ARCHIVE | String |

### Simply Uploading an Object

#### Feature Description

This API is used to upload an object to a bucket. The requester of this operation should have write permission to the bucket.

> 
> 1. Key (file name) cannot end in `/`; otherwise, it will be recognized as a folder.
2. The total number of policies associated with the ACL, Policy, and CAM of a bucket under one single root account (i.e., under the same APPID) can be up to 1,000. The number of object ACL rules is not limited. If you do not need access control for the object, do not set it during the upload, so that the object will inherit the permission of the bucket.
> 3. After the object is uploaded, you can use the same key to generate a pre-signed link. (For a download operation, specify the method as GET. For detailed API descriptions, see below.) This link can be shared for download. However, please note that if your file is private-read, then the pre-signed link is only valid for a certain period of time.

#### Use Cases

Simple upload is suitable for uploading small files.

```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
    StorageClass: 'STANDARD',
    Body: fs.createReadStream('./picture.jpg'), // Upload the file object
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

Upload Buffer as the file content:

```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
    Body: Buffer.from('hello!'), /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

Upload a string as the file content:

```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
    Body: 'hello!',
}, function(err, data) {
    console.log(err || data);
});
```

Create a directory:

```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'a/',              /* Required */
    Body: '',
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | An object key (object name) is a unique ID of an object in the bucket. For more information, see [Object Key Description](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| CacheControl | Cache policy as defined in RFC 2616, which will be stored as the object's metadata | String | No |
| ContentDisposition | File name as defined in RFC 2616, which will be stored as the object's metadata | String | No |
| ContentEncoding | Encoding format as defined in RFC 2616, which will be stored as the object's metadata | String | No |
| ContentLength | HTTP request length in bytes as defined in RFC 2616 | String | No |
| ContentType | Content type (MIME) as defined in RFC 2616, which will be stored as the object's metadata | String | No |
| Expect | If `Expect: 100-continue` is used, the request content will be sent only after confirmation from the server is received | String | No |
| Expires | File expiration time as defined in RFC 2616, which will be stored as the object's metadata | String | No |
| ACL | Defines the ACL attribute of the object. Value range: private, public-read. Default value: private | String | No |
| GrantRead | Grants the grantee the read permission in the format of x-cos-grant-read: id="[OwnerUin]" | String | No |
| GrantFullControl | Grants the grantee full permission in the format of x-cos-grant-full-control: id="[OwnerUin]" | String | No |
| StorageClass | Sets the storage class of the object. Enumerated values: STANDARD, STANDARD_IA, ARCHIVE. Default value: STANDARD | String | No |
| x-cos-meta-* | Headers that can be customized, which will be returned as the object metadata of up to 2 KB | String | No |
| Body | Content of the uploaded file, which can be a FileStream, string, or Buffer | Stream/Buffer/String | Yes |
| onProgress | Progress callback function. Attributes of the progress callback response object (progressData) are as follows | Function | No |
| - progressData.loaded | Size of the file part that has been downloaded in bytes | Number | No |
| - progressData.total | Size of the entire file in bytes | Number | No |
| - progressData.speed | File download speed in bytes/s | Number | No |
| - progressData.percent | Percentage of file download progress in decimal form; for example, 0.5 means 50% downloaded | Number | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - ETag | Returns the MD5 checksum of the file. The value of ETag can be used to check whether the object gets corrupted during upload, <br>such as `"09cba091df696af91549de27b8e7d0f6"`. **Note: There should be double quotation marks at the beginning and end of the ETag value string here** | String |

### Uploading an Object Using a Form

The SDK for Node.js SDK does not provide a method corresponding to the POST Object API. If you need to use this API, see "Scheme B: Upload using a form" in [Web Upload Practices](https://intl.cloud.tencent.com/document/product/436/9067).

### Querying Object Metadata

#### Feature Description

This API is used to query object metadata.

#### Use Cases

```js
cos.headObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',               /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| --------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | An object key (object name) is a unique ID of an object in the bucket. For more information, see [Object Key Description](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| IfModifiedSince | If the object is modified after the specified time, the corresponding object metadata will be returned; otherwise, 304 will be returned | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, and 304. If no modification is made after the specified time, 304 will be returned | Number |
| - headers | Header information returned by the request | Object |
| - x-cos-object-type | Indicates whether the object can be appended to an upload operation. Enumerated values: normal, appendable | String |
| x-cos-storage-class | Storage class of the object. Enumerated values: STANDARD, STANDARD_IA, ARCHIVE | String |
| - x-cos-meta-* | User-defined metadata | String |
| - NotModified | Whether the object is not modified after the specified time | Boolean |

### Downloading an Object

This API (GET Object) API is used to get the content (in string format) of the specified file in a bucket.

#### Use Cases

```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
}, function(err, data) {
    console.log(err || data.Body);
});
```

Specify Range to get the file content:

```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
    Range: 'bytes=1-3',        /* Optional */
}, function(err, data) {
    console.log(err || data.Body);
});
```

Download the file to the specified path:

```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
    Output: './picture.jpg',
}, function(err, data) {
    console.log(err || data.Body);
});
```

Download the file to the specified write file stream:

```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
    Output: fs.createWriteStream('./picture.jpg'),
}, function(err, data) {
    console.log(err || data.Body);
});
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| -------------------------- | ------------------------------------------------------------ | ------------------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | An object key (object name) is a unique ID of an object in the bucket. For more information, see [Object Key Description](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| Output | An output file path or write stream. If this parameter is not passed in, the full content will be written to the data of the callback function | String/WriteStream | No |
| ResponseContentType | Sets the Content-Type parameter in the response header | String | No |
| ResponseContentLanguage | Sets the Content-Language parameter in the response header | String | No |
| ResponseExpires | Sets the Content-Expires parameter in the response header | String | No |
| ResponseCacheControl | Sets the Cache-Control parameter in the response header | String | No |
| ResponseContentDisposition | Sets the Content-Disposition parameter in the response header | String | No |
| ResponseContentEncoding | Sets the Content-Encoding parameter in the response header | String | No |
| Range | Byte range of the object. The range value must be in the format of bytes=first-last, where both first and last are offsets starting from 0. For example, bytes=0-9 means that you want to copy the first 10 bytes of data of the source object. If this parameter is not specified, the entire object will be read | String | No |
| IfModifiedSince | If the object is modified after the specified time, the corresponding object metadata will be returned; otherwise, 304 will be returned | String | No |
| IfModifiedSince | The file content will be returned only if the file is modified before or at the specified time; otherwise, 412 (precondition failed) will be returned | String | No |
| IfMatch | The file will be returned only if ETag matches the specified content; otherwise, 412 (precondition failed) will be returned | String | No |
| IfNoneMatch | The file will be returned only if ETag does not match the specified content; otherwise, 304 (not modified) will be returned | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 304, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - x-cos-object-type | Indicates whether the object can be appended to an upload operation. Enumerated values: normal, appendable | String |
| x-cos-storage-class | Storage class of the object. Enumerated values: STANDARD, STANDARD_IA. <br>**Note: If this header is not returned, the file storage class is STANDARD (standard storage)** | String |
| - x-cos-meta-* | User-defined metadata | String |
| - NotModified | This attribute will be returned if the request carries IfModifiedSince. It will be true if the file has not been modified; otherwise, false | Boolean |
| - Body | Returned file content, which is in string format by default | String |

### Pre-requesting Cross-origin Configuration

#### Feature Description

This API (OPTIONS Object) is used to implement a pre-request for an cross-origin object access configuration, i.e., an OPTIONS request carrying the specific source origin, HTTP method, and header information is sent to COS for it to determine whether a real cross-origin resource sharing (CORS) request can be made. If no CORS configuration exists, 403 Forbidden will be returned for the request. **You can enable the CORS support of a bucket using the PUT Bucket cors API.**

#### Use Cases

```js
cos.optionsObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
    Origin: 'https://www.qq.com',      /* Required */
    AccessControlRequestMethod: 'PUT', /* Required */
    AccessControlRequestHeaders: 'origin,accept,content-type' /* Optional */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | An object key (object name) is a unique ID of an object in the bucket. For more information, see [Object Key Description](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| Origin | Origin domain name of the simulated cross-origin access request | String | Yes |
| AccessControlRequestMethod | HTTP method of the simulated cross-origin access request | String | Yes |
| AccessControlRequestHeaders | Headers of the simulated cross-origin access request | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ---------------------------- | ------------------------------------------------------------ | ------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - headers | Header information returned by the request | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - AccessControlAllowOrigin | Origin domain names of the simulated cross-origin access request separated by commas, such as `*`. This header will not be returned if the origin is not allowed | String |
| - AccessControlAllowMethods | HTTP methods of the simulated cross-origin access request separated by commas, such as PUT, GET, POST, DELETE, and HEAD. This header will not be returned if the request method is not allowed | String |
| - AccessControlAllowHeaders | Headers of the simulated cross-origin access request separated by commas, such as accept, content-type, origin, and authorization. This request header will not be returned if no simulated headers are allowed | String |
| - AccessControlExposeHeaders | Headers that can be returned by CORS, separated by commas, such as ETag | String |
| - AccessControlMaxAge | Sets the validity period of the result of the OPTIONS request, such as 3600 | String  |
| - OptionsForbidden | Whether the OPTIONS request is forbidden, which is true if the returned HTTP status code is 403 | Boolean |

### Copying an Object

#### Feature Description

This API (PUT Object - Copy) is used to copy a file from the source path to the destination path. It is recommended for files of 1 MB to 5 GB in size. For files over 5 GB, use the Upload - Copy API for multipart copy. Meta attributes and ACLs of the file can be modified during the copy process. You can use this API to copy a file, modify its attributes (the source file attributes are the same as the destination file attributes), move it, or rename it (copy it first and then call the deleting API separately).

#### Use Cases

```js
cos.putObjectCopy({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'ap-beijing',                                  /* Required */
    Key: 'picture.jpg',                                            /* Required */
    CopySource: 'test-1250000000.cos.ap-guangzhou.myqcloud.com/2.jpg', /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | An object key (object name) is a unique ID of an object in the bucket. For more information, see [Object Key Description](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| CopySource | Source file URL path. A previous version can be specified using the versionid sub-resource | String | Yes |
| ACL | Defines the ACL attribute of the object. Value range: private, public-read. Default value: private | String | No |
| GrantRead | Grants the grantee the read permission in the format of id="[OwnerUin]" | String | No |
| GrantFullControl | Grants the grantee full permission in the format of id="[OwnerUin]" | String | No |
| MetadataDirective | Whether to copy the metadata. Enumerated values: Copy, Replaced. Default value: Copy. If the flag is Copy, the user metadata in the header is ignored and the copy is performed directly; if the flag is Replaced, the metadata is modified based on the header information. **If the destination path is the same as the source path (i.e., when you want to modify the metadata), the flag has to be Replaced** | String | No |
| CopySourceIfModifiedSince | If the object is modified after the specified time, the operation is performed; otherwise, 412 is returned. **This parameter can be used together with CopySourceIfNoneMatch. If it is used together with other conditions, a conflict is returned** | String | No |
| CopySourceIfUnmodifiedSince | If the object is not modified after the specified time, the operation is performed; otherwise, 412 is returned. **This parameter can be used together with CopySourceIfMatch. If it is used together with other conditions, a conflict is returned** | String | No |
| CopySourceIfMatch | If the Etag of the object is the same as the specified one, the operation is performed; otherwise, 412 is returned. **This parameter can be used together with CopySourceIfUnmodifiedSince. If it is used together with other conditions, a conflict is returned** | String | No |
| CopySourceIfNoneMatch | If the Etag of the object is different from the specified one, the operation is performed; otherwise, 412 is returned. **This parameter can be used together with CopySourceIfModifiedSince. If it is used together with other conditions, a conflict is returned** | string | No |
| StorageClass | Storage class; enumerated values: Standard, Standard_IA. Default value: Standard | String | No |
| x-cos-meta-* | Other custom file headers | String | No |
| CacheControl | Specifies the commands that all caching mechanisms must obey throughout the entire request/response chain | String | No |
| ContentDisposition | An extension of the MIME protocol. The MIME protocol instructs the MIME user agent on how to display the attached files | String | No |
| ContentEncoding | A pair of header fields used in HTTP to negotiate the "encoding format of body transmission" | String | No |
| ContentType | HTTP request content type (MIME) as defined in RFC 2616, such as text/plain | String | No |
| Expect | Requested specific server behavior | String | No |
| Expires | Expiration date and time of the response | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - ETag | MD5 checksum of the file, such as `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and end** | String |
| - LastModified | Describes the last modified time of the object, such as 2017-06-23T12:33:27.000Z | String |

### Deleting a Single Object

#### Feature Description

This API is used to delete the specified object in a bucket. The requester of this operation should have write permission to the bucket.

#### Use Cases

```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg'                            /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | An object key (object name) is a unique ID of an object in the bucket. For more information, see [Object Key Description](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 204, 403, and 404. **If the deletion is successful or the file does not exist, 204 or 200 will be returned; if the specified bucket is not found, 404 will be returned** | Number |
| - headers | Header information returned by the request | Object |

### Deleting Multiple Objects

#### Feature Description

This API is used to delete objects in a bucket in batches. It can delete up to 1,000 objects in a single request. For the response result, COS provides two modes: Verbose and Quiet. Verbose mode returns the deletion result for each object; while Quiet mode only returns the information of objects for which errors are reported.

#### Use Cases

Delete multiple files:

```js
cos.deleteMultipleObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Objects: [
        {Key: 'picture.jpg'},
        {Key: '2.zip'},
    ]
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ----------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Quiet | A boolean value which determines whether to enable Quiet mode. If the value is true, Quiet mode is enabled; if it is false, Verbose mode is enabled. The default value is false | Boolean | No |
| Objects | List of files to be deleted | ObjectArray | Yes |
| - Key | An object key (object name) is a unique ID of an object in the bucket. For more information, see [Object Key Description](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| - VersionId | Version ID of the object to be deleted or DeleteMarker | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 204, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 204, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - Deleted | Describes the information of successfully deleted objects in this operation | ObjectArray |
| - - Key | An object key (object name) is a unique ID of an object in the bucket. For more information, see [Object Key Description](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| - - VersionId | If the VersionId parameter is passed in, it will also be included in the return, indicating the version of the manipulated object or DeleteMarker | String |
| - - DeleteMarker | If versioning is enabled and the VersionId parameter is not present, this deletion will not actually erase the content of files; instead, only a new DeleteMarker will be added, indicating that the visible files have been deleted. Enumerated values: true, false | String |
| - - DeleteMarkerVersionId | If the returned DeleteMarker is true, the VersionId of the newly added DeleteMarker will be returned | String |
| - Error | Describes the information of objects that failed to be deleted in this operation | ObjectArray |
| - - Key | An object key (object name) is a unique ID of an object in the bucket. For more information, see [Object Key Description](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| - - Code | Error code of the deletion failure | String |
| - - Message | Error message of the deletion failure | String |

## Multipart Upload Operations

### Querying a Multipart Upload

#### Feature Description

This API (List Multiparts Uploads) is used to query the multipart uploads in progress. Up to 1,000 ones can be listed in one single operation.

#### Use Cases

Get the list of incomplete UploadIds prefixed with 1.zip. Below is an example:

```js
cos.multipartList({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Prefix: '1.zip',                        /* Optional */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Prefix | Matching prefix for object keys, which requires the return to contain only object keys with the specified prefix. Note that when a prefix query is used, the returned key will still contain the prefix | String | No |
| Delimiter | The delimiter is a separator symbol which is used to group object keys and is generally `/`. The identical paths between prefix (or the beginning if no prefix is specified) and delimiter are grouped into one class and defined as a common prefix, and then all common prefixes are listed. | String | No |
| EncodingType | Specifies the encoding method of the return value; value range: url | String | No |
| MaxUploads | Sets the maximum number of entries returned between 1 and 1,000. Default value: 1,000 | String | No |
| KeyMarker | Used together with upload-id-marker. <br> <li>If upload-id-marker is not specified, <br>&emsp;- only the multipart uploads with ObjectNames lexicographically greater than the specified key-marker will be included in the list; <br><li>otherwise, <br>&emsp;- the multipart uploads with ObjectNames lexicographically greater than the specified key-marker will be included, <br>&emsp;- and any multipart uploads with ObjectNames equal to the key-marker will also be included, provided that they have UploadIDs lexicographically greater than the specified upload-id-marker | String | No |
| UploadIdMarker | Used together with key-marker. <br><li>If key-marker is not specified, <br>&emsp;- upload-id-marker will be ignored; <br><li>otherwise, <br>&emsp;- the multipart uploads with ObjectNames lexicographically greater than the specified key-marker will be included in the list, <br>&emsp;- and any multipart uploads with ObjectNames equal to the key-marker will also be included, provided that they have UploadIDs lexicographically greater than the specified upload-id-marker | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| -------------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - Bucket | Destination bucket for the multipart upload | String |
| - Encoding-Type | Specifies the encoding method of the return value; value range: url | String |
| - KeyMarker      | The entry list starts at this key value                                      | String |
| - UploadIdMarker     | The entry list starts at this UploadId value                                      | String |
| - NextKeyMarker | If the returned entries are truncated, then NextKeyMarker is the starting point of the next entry | String |
| - NextUploadIdMarker | If the returned entries are truncated, then UploadId is the starting point of the next entry | String |
| - MaxUploads | Sets the maximum number of entries returned between 1 and 1,000 | String |
| - IsTruncated | Whether returned entries are truncated; value range: true, false | String |
| - Prefix | Matching prefix for object keys, which requires the return to contain only object keys with the specified prefix. | String |
| - Delimiter | The delimiter is a separator symbol which is used to group object keys and is generally `/`. The identical paths between prefix (or the beginning if no prefix is specified) and delimiter are grouped into one class and defined as a common prefix, and then all common prefixes are listed. | String |
| - CommonPrefixes | The identical paths between prefix and delimiter are grouped into one class and defined as a common prefix | ObjectArray |
| - - Prefix | Displays the specific Common Prefixes | String |
| - Upload | Multipart upload information set | ObjectArray |
| - - Key | Object name, i.e., object key | String |
| - - UploadId | Identifies the ID of this multipart upload | String |
| - - StorageClass | Indicates the part storage class; enumerated values: STANDARD, STANDARD_IA, ARCHIVE | String |
| - - Initiator        | Identifies the initiator of this upload                                 | Object                 |
| - - - DisplayName      | Upload initiator name                                            | String      |
| - - - ID | Upload initiator ID in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`. <br>If it is a root account, &lt;OwnerUin> and &lt;SubUin> are the same value | String |
| - - Owner | Identifies the owner of the parts | Object  |
| - - - DisplayName | Part owner name | String |
| - - - ID | Part owner ID in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`.<br>If it is a root account, &lt;OwnerUin> and &lt;SubUin> are the same value | String |
| - - Initiated | Start time of the multipart upload | String |


### Initializing a Multipart Upload

#### Feature Description

This API (Initiate Multipart Upload) is used to initialize a multipart upload. After the execution of this request, Upload ID will be returned for the subsequent Upload Part requests.

#### Use Cases

```js
cos.multipartInit({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | An object key (object name) is a unique ID of an object in the bucket. For more information, see [Object Key Description](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| CacheControl | Cache policy as defined in RFC 2616, which will be stored as the object's metadata | String | No |
| ContentDisposition | File name as defined in RFC 2616, which will be stored as the object's metadata | String | No |
| ContentEncoding | Encoding format as defined in RFC 2616, which will be stored as the object's metadata | String | No |
| ContentType | Content type (MIME) as defined in RFC 2616, which will be stored as the object's metadata | String | No |
| Expires | File expiration time as defined in RFC 2616, which will be stored as the object's metadata | String | No |
| ACL | Defines the ACL attribute of the object. Value range: private, public-read. Default value: private | String | No |
| GrantRead | Grants the grantee the read permission in the format of id="[OwnerUin]" | String | No |
| GrantFullControl | Grants the grantee full permission in the format of id="[OwnerUin]" | String | No |
| StorageClass | Sets the storage class of the object. Enumerated values: STANDARD, STANDARD_IA, ARCHIVE. Default value: STANDARD | String | No |
| x-cos-meta-* | Headers that can be customized, which will be returned as the object metadata of up to 2 KB | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| Bucket | Destination bucket for the multipart upload | String |
| Key | An object key (object name) is a unique ID of an object in the bucket. For more information, see [Object Key Description](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| UploadId | ID used in subsequent uploads | String |

### Uploading Parts

#### Feature Description

This API (Upload Part) is used to upload parts after a multipart upload is initialized. It can upload 1-10,000 parts of 1 MB to 5 GB in size.
When the Initiate Multipart Upload API is used to initialize a multipart upload, an uploadId will be obtained, which not only uniquely identifies the data but also identifies the data position in the entire file. Each time you request the Upload Part API, you need to pass in the partNumber (which is the part number) and uploadId parameters. Out-of-order uploading is supported.
When the uploadId and partNumber of a newly uploaded part are the same as those of a previously uploaded part, the former will overwrite the latter. A 404 NoSuchUpload error will be returned if the uploadId does not exist.

#### Use Cases

```js
cos.multipartUpload({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',       /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------------- | ------------------------------------------------------------ | ---------------- | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | An object key (object name) is a unique ID of an object in the bucket. For more information, see [Object Key Description](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| ContentLength | HTTP request length in bytes as defined in RFC 2616 | String | Yes |
| PartNumber | Part number | String | Yes |
| UploadId | Upload task number | String | Yes |
| Body | Content of the uploaded file part, which can be a string, File object, or Blob object | String\File\Blob | Yes |
| Expect | If `Expect: 100-continue` is used, the request content will be sent only after confirmation from the server is received | String | No |
| ContentMD5 | Base64-encoded 128-bit content MD5 checksum as defined in RFC 1864. This header is used to check whether the file content has changed | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

### Copying Parts

#### Feature Description

This API (Upload Part - Copy) is used to copy the parts of an object from the source path to the destination path.
> 
>
> 1. If the destination object and the source object are in different regions, and the part size of the destination object will exceed 5 GB, you need to use multipart upload or multipart copy API to copy the object.
> 2. To upload an object in parts, you must first initialize the multipart upload. A unique descriptor (upload ID) will be returned in the response of multipart upload initialization, which needs to be carried in the multipart upload request.

#### Use Cases

```js
cos.uploadPartCopy({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',       /* Required */
    CopySource: 'destination-bucket-1250000000.cos.ap-guangzhou.myqcloud.com/picture-1.jpg', /* Required */
    UploadId: '1521389146c60e7e198202e4e6670c5c78ea5d1c60ad62f1862f47294ec0fb8c6b7f3528a2', /* Required */
    PartNumber: '1', /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | An object key (object name) is a unique ID of an object in the bucket. For more information, see [Object Key Description](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| CopySource | Source object URL path. A previous version can be specified using the URL parameter `?versionId=\<versionId>` | String | Yes |
| partNumber | Part number during multipart copy | String | Yes |
| uploadId | To upload a file in parts, you must first initialize the multipart upload. A unique descriptor (upload ID) will be returned in the response of multipart upload initialization, which needs to be carried in the multipart upload request | String | Yes |
| CopySourceRange | Byte range of the source object. The range value must be in the format of bytes=first-last, where both first and last are offsets starting from 0. For example, bytes=0-9 means that you want to copy the first 10 bytes of data of the source object. If this parameter is not specified, the entire object will be copied | String | No |
| CopySourceIfMatch | If the Etag of the object is the same as the specified one, the operation is performed; otherwise, 412 is returned. This parameter can be used together with x-cos-copy-source-If-Unmodified-Since. If it is used together with other conditions, a conflict is returned | String | No |
| CopySourceIfNoneMatch | If the Etag of the object is different from the specified one, the operation is performed; otherwise, 412 is returned. This parameter can be used together with x-cos-copy-source-If-Modified-Since. If it is used together with other conditions, a conflict is returned | string | No |
| CopySourceIfUnmodifiedSince | If the object is not modified after the specified time, the operation is performed; otherwise, 412 is returned. This parameter can be used together with x-cos-copy-source-If-Match. If it is used together with other conditions, a conflict is returned | String | No |
| CopySourceIfModifiedSince | If the object is modified after the specified time, the operation is performed; otherwise, 412 is returned. This parameter can be used together with x-cos-copy-source-If-None-Match. If it is used together with other conditions, a conflict is returned | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - ETag | MD5 checksum of the file, such as `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and end** | String |
| - LastModified | Returns the last modified time of the object in GMT time | String |


### Querying Uploaded Parts

#### Feature Description

This API (List Parts) is used to query the uploaded parts in the specified multipart upload, i.e., listing all successfully uploaded parts in the multipart upload with the specified UploadId.

#### Use Cases

```js
cos.multipartListPart({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
    UploadId: '1521389146c60e7e198202e4e6670c5c78ea5d1c60ad62f1862f47294ec0fb8c6b7f3528a2',                      /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ---------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | An object key (object name) is a unique ID of an object in the bucket. For more information, see [Object Key Description](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| UploadId | ID of this multipart upload; when the Initiate Multipart Upload API is used to initialize a multipart upload, an uploadId will be obtained, which not only uniquely identifies the data but also identifies the data position in the entire file | String | Yes |
| EncodingType | Specifies the encoding method of the return value | String | No |
| MaxParts | Maximum number of entries returned at a time. Default value: 1,000 | String | No |
| PartNumberMarker | By default, entries are listed in UTF-8 binary order, and the entry list starts at marker | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ---------------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - Bucket | Destination bucket for the multipart upload | String |
| - Encoding-type | Specifies the encoding method of the return value | String |
| - Key | An object key (object name) is a unique ID of an object in the bucket. For more information, see [Object Key Description](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| - UploadId | Identifies the ID of this multipart upload | String |
| - Initiator        | Identifies the initiator of this upload                                 | Object                 |
| - - DisplayName      | Upload initiator name                                            | String      |
| - - ID | Upload initiator ID in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` <br>If it is a root account, &lt;OwnerUin> and &lt;SubUin> are the same value | String |
| - Owner | Identifies the owner of the parts | Object  |
| - - DisplayName      | Bucket owner name                                            | String      |
| - - ID | Bucket owner ID, which is typically a UIN | String |
| - StorageClass | Indicates the part storage class; enumerated values: Standard, Standard_IA, Archive | String |
| PartNumberMarker | By default, entries are listed in UTF-8 binary order, and the entry list starts at marker | String |
| - NextPartNumberMarker | If the returned entries are truncated, then NextMarker is the starting point of the next entry | String |
| - MaxParts | Maximum number of entries returned at a time | String |
| - IsTruncated | Whether returned entries are truncated; value range: true, false | String |
| - Part | Array | Part information list | ObjectArray |
| - - PartNumber | Part number | String |
| - - LastModified | Part's last modified time | String |
| - - ETag | MD5 checksum of the part | String |
| - - Size | Part size in bytes | String |

### Completing a Multipart Upload

#### Feature Description

This API (Complete Multipart Upload) is used to complete the entire multipart upload. After all parts are uploaded using the Upload Parts API, this API must be called to complete the multipart upload of the entire file. When using this API, you must specify the PartNumber and ETag of each part in the request body to verify the accuracy of parts.
As the parts need to be merged after they are uploaded, and the merge takes several minutes, when the merge starts, COS will immediately return status code 200 and periodically return space information during the merge process to keep the connection active until the merge is completed. After that, COS will return the content of the merged parts in the body.

- If the uploaded part size is below 1 MB, 400 EntityTooSmall will be returned when this API is called.
- If the uploaded part numbers are not continuous, 400 InvalidPart will be returned when this API is called.
- If the part information entries in the request body are not sorted by number in ascending order, 400 InvalidPartOrder will be returned when this API is called.
- If the UploadId does not exist, 404 NoSuchUpload will be returned when this API is called.

#### Use Cases

```js
cos.multipartComplete({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: '1.zip',              /* Required */
    UploadId: '1521389146c60e7e198202e4e6670c5c78ea5d1c60ad62f1862f472941c0fb8c6b7f3528a2', /* Required */
    Parts: [
        {PartNumber: '1', ETag: '"0cce40bdbaf2fa0ff204c20fc965dd3f"'},
    ]
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ----------- | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | An object key (object name) is a unique ID of an object in the bucket. For more information, see [Object Key Description](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| UploadId | Upload task number | String | Yes |
| Parts | Information list of the parts in this multipart upload | ObjectArray | Yes |
| - PartNumber | Part number | String | Yes |
| - ETag | MD5 checksum of each file part, <br>such as `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and end** | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - Location | Public network access domain name for the created object  | String |
| - Bucket | Destination bucket for the multipart upload | String |
| - Key | An object key (object name) is a unique ID of an object in the bucket. For more information, see [Object Key Description](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| - ETag | Unique ID of the merged file in the format of "uuid-<part quantity>", <br>such as `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`. **Note that double quotation marks are required at the beginning and end** | String |

### Aborting a Multipart Upload

#### Feature Description

This API (Abort Multipart Upload) is used to abort a multipart upload operation and delete the uploaded parts. When you call this API, if there is a request that is uploading a part using the Upload Parts API, the request will fail. If the UploadId does not exist, 404 NoSuchUpload will be returned.

>  It is recommended that you either complete or abort the multipart upload in a timely manner, as the parts that have been uploaded but not completed will take up storage space and incur storage fees.

#### Use Cases

```js
cos.multipartAbort({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: '1.zip',                           /* Required */
    UploadId: '1521389146c60e7e198202e4e6670c5c78ea5d1c60ad62f1862f47294ec0fb8c6b7f3528a2'                       /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | An object key (object name) is a unique ID of an object in the bucket. For more information, see [Object Key Description](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| UploadId | ID of this multipart upload; when the Initiate Multipart Upload API is used to initialize a multipart upload, an uploadId will be obtained, which not only uniquely identifies the data but also identifies the data position in the entire file | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

## Other Operations

### Restoring an Archived Object

#### Feature Description

This API is used to retrieve an archived object for access.

#### Use Cases

```js
cos.restoreObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',
    RestoreRequest: {
        Days: 1,
        CASJobParameters: {
            Tier: 'Expedited'
        }
    },
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------------------ | ------------------------------------------------------------ | ------- | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | An object key (object name) is a unique ID of an object in the bucket. For more information, see [Object Key Description](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| RestoreRequest | Container used for data restoration | Object | Yes |
| - Days | Sets expiration time of the temporary copy | Object | Yes |
| - CASJobParameters | Container of the archive storage parameters | Object | Yes |
| - - Tire | For data restoration, Tier can be specified as one of the three modes supported by CAS: Standard (standard mode where a restoration task can be completed in 3-5 hours), Expedited (expedited mode where a restoration task can be completed in 15 minutes), and Bulk (bulk mode where a restoration task can be completed in 5 - 12 hours) | Integer | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

### Setting Object ACL

#### Feature Description

This API is used to set the ACL for the specified object in a bucket.

>  The total number of policies associated with the ACL, Policy, and CAM of a bucket under one single root account (i.e., under the same APPID) can be up to 1,000. The number of object ACL rules is not limited. If you do not need access control for the object, do not set it, so that the object will inherit the permission of the bucket.

#### Use Cases

```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
    ACL: 'public-read',        /* Optional */
}, function(err, data) {
    console.log(err || data);
});
```

Grant a user read/write permission to a file:

```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
    GrantFullControl: 'id="100000000001"' // 100000000001 is the uin of the root account
}, function(err, data) {
    console.log(err || data);
});
```

Modify bucket permission with AccessControlPolicy:

```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
    AccessControlPolicy: {
        "Owner": { // There must be an owner in AccessControlPolicy
            "ID": 'qcs::cam::uin/100000000001:uin/100000000001' // 100000000001 is the QQ account number of the user owning the bucket
        },
        "Grants": [{
            "Grantee": {
                "ID": "qcs::cam::uin/100000000011:uin/100000000011", // 100000000011 is a QQ account number
            },
            "Permission": "WRITE"
        }]
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | An object key (object name) is a unique ID of an object in the bucket. For more information, see [Object Key Description](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| ACL | Defines the ACL attribute of the object. Value range: private, public-read, default. Default value: private. If default is passed in, the file permission is cleared and restored to the inherited permission | String | No |
| GrantRead | Grants the grantee the read permission in the format of id="[OwnerUin]" | String | No |
| GrantFullControl | Grants the grantee full permission in the format of id="[OwnerUin]" | String | No |
| AccessControlPolicy | ACL of the object in JSON format | Object | No |
| - Owner | Identifies the resource owner | Object | No |
| - - ID | Bucket owner ID in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` <br>If it is a root account, &lt;OwnerUin> and &lt;SubUin> are the same value | String | No |
| - - DisplayName | Object owner name | String | No |
| - Grants | Information list of grantee and permission | ObjectArray | No |
| - - Permission | Specifies the permission granted to the grantee. Enumerated values: READ, WRITE, READ_ACP, WRITE_ACP, FULL_CONTROL | String | No |
| - - Grantee | Describes the information of the grantee. The type can be RootAccount or Subaccount. If the type is RootAccount, the ID specifies a root account; if the type is Subaccount, the ID specifies a sub-account | Object | No |
| - - - DisplayName | Username | String | No |
| - - - ID | User ID in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` <br>If it is a root account, &lt;OwnerUin> and &lt;SubUin> are the same value | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 204, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

### Querying Object ACL

#### Feature Description

This API is used to query the ACL of an object.

#### Use Cases

```js
cos.getObjectAcl({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | An object key (object name) is a unique ID of an object in the bucket. For more information, see [Object Key Description](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ----------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - ACL | Object's ACL attributes; enumerated values: private, public-read, default | Object |
| - Owner | Identifies the resource owner | Object |
| - - ID | Object owner ID in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>If it is a root account, &lt;OwnerUin> and &lt;SubUin> are the same value | String |
| - - DisplayName | Object owner name | String |
| - Grants | Information list of grantee and permission | ObjectArray |
| - - Permission | Specifies the permission granted to the grantee. Enumerated values: READ, READ_ACP, WRITE_ACP, FULL_CONTROL | String |
| - - Grantee | Describes the information of the grantee. The type can be RootAccount or Subaccount. If the type is RootAccount, the ID specifies a root account; if the type is Subaccount, the ID specifies a sub-account | Object |
| - - - DisplayName | Username | String |
| - - - ID | User ID in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>If it is a root account, &lt;OwnerUin> and &lt;SubUin> are the same value | String |

## Advanced API (Recommended)

Methods of this type encapsulate the native methods above to implement the complete process of multipart upload/copy and support concurrent multipart upload/copy as well as resumption, cancellation, pausing, and restart of upload tasks.

### Uploading an Object in Parts

#### Feature Description

This API (Slice Upload File) is used to upload a large files in parts.

#### Use Cases

```js
cos.sliceUploadFile({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: '1.zip',              /* Required */
    FilePath: filePath,                /* Required */
    TaskReady: function(taskId) {                   /* Optional */
        console.log(taskId);
    },
    onHashProgress: function (progressData) {       /* Optional */
        console.log(JSON.stringify(progressData));
    },
    onProgress: function (progressData) {           /* Optional */
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | An object key (object name) is a unique ID of an object in the bucket. For more information, see [Object Key Description](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| FilePath | Path to the uploaded file | String | Yes |
| SliceSize | Part size | String | No |
| AsyncLimit | Part concurrences | String | No |
| StorageClass | Object storage class; enumerated value: STANDARD, STANDARD_IA | String | No |
| TaskReady | When an upload task is created, the callback function returns a taskId, which uniquely identifies the task and can be used to cancel (cancelTask), pause (pauseTask), or restart (restartTask) the task | Function | No |
| - taskId | Upload task number | String | No |
| onHashProgress | The progress callback function of file MD5 value calculation. The callback parameter is the progress object progressData | Function | No |
| - progressData.loaded | Size of the file part that has been verified in bytes | Number | No |
| - progressData.total | Size of the entire file in bytes | Number | No |
| - progressData.speed | File verification speed in bytes/s | Number | No |
| - progressData.percent | Percentage of file verification progress in decimal form; for example, 0.5 means 50% downloaded | Number | No |
| onProgress | The progress callback function of file upload. The callback parameter is the progress object progressData | Function | No |
| - progressData.loaded | Size of the file part that has been uploaded in bytes | Number | No |
| - progressData.total | Size of the entire file in bytes | Number | No |
| - progressData.speed | File upload speed in bytes/s | Number | No |
| - progressData.percent | Percentage of file upload progress in decimal form; for example, 0.5 means 50% downloaded | Number | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - Location | Public network access domain name for the created object  | String |
| - Bucket | Destination bucket for the multipart upload | String |
| - Key | An object key (object name) is a unique ID of an object in the bucket. For more information, see [Object Key Description](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| - ETag | Unique ID of the merged file in the format of "uuid-<part quantity>", <br>such as `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`. **Note that double quotation marks are required at the beginning and end** | String |

### Copying an Object

#### Feature Description

This API (Slice Copy File) is used to copy a file from the source path to the destination path through multipart copy. Meta attributes and ACLs of the object can be modified during the copy process. You can use this API to move, rename, and copy a file or modify its attributes.

#### Method Prototype

Call the Slice Copy File operation:

```js
cos.sliceCopyFile({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'ap-beijing',                                  /* Required */
    Key: '1.zip',                                            /* Required */
    CopySource: 'destination-bucket-1250000000.cos.ap-guangzhou.myqcloud.com/2.zip', /* Required */
    onProgress:function (progressData) {                     /* Optional */
        console.log(JSON.stringify(progressData));
    }
},function (err,data) {
    console.log(err || data);
});
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | An object key (object name) is a unique ID of an object in the bucket. For more information, see [Object Key Description](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| CopySource | Source file URL path. A previous version can be specified using the versionid sub-resource | String | Yes |
| ChunkSize | Part size in the multipart copy in bytes. Default value: 1,048,576 (1 MB) | Number | No |
| SliceSize | Part size in the multipart copy. Default value: 5 GB | Number | No |
| onProgress | The progress callback function of file upload. The callback parameter is the progress object progressData | Function | No |
| - progressData.loaded | Size of the file part that has been uploaded in bytes | Number | No |
| - progressData.total | Size of the entire file in bytes | Number | No |
| - progressData.speed | File upload speed in bytes/s | Number | No |
| - progressData.percent | Percentage of file upload progress in decimal form; for example, 0.5 means 50% downloaded | Number | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - Location | Public network access domain name for the created object  | String |
| - Bucket | Destination bucket for the multipart upload | String |
| - Key | An object key (object name) is a unique ID of an object in the bucket. For more information, see [Object Key Description](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| - ETag | MD5 checksum of the merged file, <br>such as `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and end** | String |

### Batch Upload

#### Feature Description

Method 1:
You can directly call putObject and sliceUploadFile to implement batch uploads. You can control the number of file concurrences by instantiating the FileParallelLimit parameter, which is 3 by default.

Method 2:
You can call cos.uploadFiles to implement batch uploads. The SliceSize method parameter can be used to control the file. Below are instructions of the uploadFiles method.

#### Method Prototype

Call the uploadFiles operation:

```js
cos.uploadFiles({
    files: [{
        Bucket: 'examplebucket-1250000000',
        Region: 'ap-beijing',
        Key: 'picture.jpg',
        FilePath: filePath1,
    }, {
        Bucket: 'examplebucket-1250000000',
        Region: 'ap-beijing',
        Key: '2.jpg',
        FilePath: filePath2,
    }],
    SliceSize: 1024 * 1024,
    onProgress: function (info) {
        var percent = parseInt(info.percent * 10000) / 100;
        var speed = parseInt(info.speed / 1024 / 1024 * 100) / 100;
        console.log('progress:' + percent + '%; speed:' + speed + 'Mb/s;');
    },
    onFileFinish: function (err, data, options) {
        console.log(options.Key + 'uploaded' + (err ? 'failed' : 'completed'));
    },
}, function (err, data) {
    console.log(err || data);
});
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | ------ | ---- |
| files | File list, where each item is a parameter object passed to putObject and sliceUploadFile | Object | Yes |
| SliceSize | Specifies the minimum file size in bytes for which multipart upload will be used. If the size of a file is equal to or smaller than this value, the file will be uploaded using putObject; otherwise, it will be uploaded using sliceUploadFile | Number | Yes |
| onProgress | Upload progress calculated by aggregating the progress of all tasks | String | Yes |
| - progressData.loaded | Size of the file part that has been uploaded in bytes | Number | No |
| - progressData.total | Size of the entire file in bytes | Number | No |
| - progressData.speed | File upload speed in bytes/s | Number | No |
| - progressData.percent | Percentage of file upload progress in decimal form; for example, 0.5 means 50% downloaded | Number | No |
| onFileFinish | The completion or error callback of each file | String | Yes |
| - err | Upload error message | Object | No |
| - data | File completion information | Object | No |
| - options | Parameter information of the completed file | Object | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - files | error or data of each file | ObjectArray |
| - - err | Upload error message | Object |
| - - data | File completion information | Object |
| - options | Parameter information of the completed file | Object |

### Upload Queue

The SDK for JavaScript retains queues of upload tasks initiated by putObject and sliceUploadFile, which can be used in the following ways:

1. cos.getTaskList can get the task list.
2. cos.pauseTask, cos.restartTask, and cos.cancelTask can operate the task.
3. cos.on('list-update', callback); can listen to the list and progress changes.

For a complete queue use case, see [Queue Demo](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/demo/queue).

#### Canceling an Upload Task

This API is used to cancel an upload task based on the taskId.

**Use cases**

```js
var taskId = 'xxxxx';                   /* Required */
cos.cancelTask(taskId);
```

**Parameter description**

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | File upload task number. When the sliceUploadFile method is called, its TaskReady callback will return the taskId of the upload task | String | Yes |

#### Pausing an Upload Task

This API is used to pause an upload task based on the taskId.

**Use cases**

```js
var taskId = 'xxxxx';                   /* Required */
cos.pauseTask(taskId);
```

**Parameter description**

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | File upload task number. When the sliceUploadFile method is called, its TaskReady callback will return the taskId of the upload task | String | Yes |

#### Restarting an Upload Task

This API is used to restart an upload task based on the taskId that has been manually paused (by calling the pauseTask API) or stopped due to an upload error.

**Use cases**

```js
var taskId = 'xxxxx';                   /* Required */
cos.restartTask(taskId);
```

**Parameter description**

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | File upload task number. When the sliceUploadFile method is called, its TaskReady callback will return the taskId of the upload task | String | Yes |
