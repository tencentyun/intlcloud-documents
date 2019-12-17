## Overview

This document provides an overview of APIs and SDK code samples related to simple operations, multipart upload operations, and other operations on objects.

**Simple Operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ---------------------------------------- |
| [GET Bucket（List Object）](https://intl.cloud.tencent.com/document/product/436/30614) | Querying object list | Queries some or all objects in a bucket |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object using simple upload | Uploads an object to a bucket |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | Uploading an object using a form | Uploads an object using a form request |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |
| [OPTIONS Object](https://intl.cloud.tencent.com/document/product/436/8288) | Pre-requesting cross-origin access configuration | Sends a pre-request to check whether a real cross-origin access request can be sent |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object | Copies an object to a destination path (object key) |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes a specified object from a bucket |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects in a single request |

**Multipart Upload Operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries the information on ongoing multipart uploads |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload task |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads object parts |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries uploaded parts in a specified multipart upload operation |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of the entire file |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload operation and deletes the uploaded parts |

**Other Operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting object ACL | Sets the ACL for a specified object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying object ACL | Queries the ACL of an object |

## Simple Operations

### Querying Object List

#### Feature Description

This API (GET Bucket (List Object)) is used to query some or all objects in a bucket.

#### Samples

Sample 1. List all the files in directory `a`.

```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',     /* Required */
    Prefix: 'a/',           /* Optional */
}, function(err, data) {
    console.log(err || data.Contents);
});
```

Response:

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

Sample 2. List the files in directory `a` without deep traversal.

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

Response:

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

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Prefix | Prefix to be matched, which specifies the prefix address of the files to be returned | String | No |
| Delimiter | A delimiter is a separating symbol which is usually `/`. The identical paths between `Prefix` or, if no `Prefix` is specified, the beginning and the first `delimiter` are grouped and defined as a common prefix. All common prefixes will be listed. | String | No |
| Marker | By default, entries are listed in UTF-8 binary order starting from `Marker` | String | No |
| MaxKeys | Maximum number of entries returned at a time. Default value: 1,000 | String | No |
| EncodingType | Specifies the encoding type of the returned values; valid value: `url` | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ---------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - headers | Header information returned by the request | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - CommonPrefixes | The identical paths between `Prefix` and `Delimiter` are grouped and defined as a common prefix | ObjectArray |
| - - Prefix | A single common prefix | String |
| - - Name | Describes bucket information | String |
| - Prefix | Prefix to be matched, which specifies the prefix address of the files to be returned | String |
| - Marker | By default, entries are listed in UTF-8 binary order starting from `Marker` | String |
| - MaxKeys | Maximum number of results returned in one response | String |
| - IsTruncated | Whether the returned list is truncated; a string. Valid values: `true`, `false` | String |
| - NextMarker | If the returned list is truncated, the `NextMarker` returned will be the starting point of the subsequent list | String |
| - Encoding-Type | Encoding type of the returned values, which is applicable to `Delimiter`, `Marker`, `Prefix`, `NextMarker`, and `Key` | String |
| - Contents | Metadata | ObjectArray |
| - - ETag | MD5 checksum of the file. <br>For example, `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end** | String |
| - - Size | Describes file size in bytes | String |
| - - Key | Object name | String |
| - - LastModified | Describes the last modified time of an object, such as `2017-06-23T12:33:27.000Z` | String |
| - - Owner | Bucket owner information | Object |
| - ID | Bucket APPID | String |
| - StorageClass | Object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE` | String |

### Uploading an Object Using Simple Upload

#### Feature Description

This API (PUT Object) is used to upload an object to a bucket. To make this request, you need to have the permission to write to the bucket.

> 
> 1. An object key (file name) cannot end with `/`; otherwise, the file will be recognized as a folder.
2. The total number of policies associated with bucket ACL, Policy, and CAM under a single root account (i.e., under the same APPID) cannot exceed 1,000. There is no upper limit on the number of object ACL rules. If you do not need access control for an object, do not make the configuration when uploading it, and the object will inherit the permissions of its bucket.
> 3. After an object is uploaded, you can use the same key to generate a pre-signed link, which can be shared with others for download. However, please note that if your file is set to private-read, the pre-signed link will only be valid for a certain period of time. To download, please specify the method as `GET`. For API details, see below.

#### Sample

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

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| CacheControl | Cache policy as defined in RFC 2616, which will be stored in the object metadata | String | No |
| ContentDisposition | Filename as defined in RFC 2616, which will be stored in the object metadata | String | No |
| ContentEncoding | Encoding format as defined in RFC 2616, which will be stored in the object metadata | String | No |
| ContentLength | HTTP request length in bytes as defined in RFC 2616 | String | No |
| ContentType | Content type (MIME) as defined in RFC 2616, which will be stored in the object metadata | String | No |
| Expect | If `Expect: 100-continue` is used, the request content will be sent only after the confirmation from the server is received | String | No |
| Expires | Expiration time as defined in RFC 2616, which will be stored in the object metadata | String | No |
| ACL | Defines the ACL attribute of the object. Valid values: `private`, `public-read`. Default value: `private` | String | No |
| GrantRead | Grants the grantee Read access in the format of `x-cos-grant-read: id="[OwnerUin]"` | String | No |
| GrantFullControl | Grants the grantee full permission in the format of `x-cos-grant-full-control: id="[OwnerUin]"` | String | No |
| StorageClass | Sets the object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String | No |
| x-cos-meta-* | Headers that can be defined by users, which will be returned as the object metadata; maximum size: 2 KB | String | No |
| Body | Content of the file to be uploaded, which can be a FileStream, string, or Buffer | Stream/Buffer/String | Yes |
| onProgress | Progress callback function. Attributes of the progress callback response object, `progressData`, are as follows | Function | No |
| - progressData.loaded | Size of the file part that has been downloaded; unit: byte | Number | No |
| - progressData.total | Size of the entire file; unit: byte | Number | No |
| - progressData.speed | File download speed; unit: bytes/s | Number | No |
| - progressData.percent | A decimal representing the file download progress. For example, 0.5 means 50% has been downloaded | Number | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - ETag | Returns the MD5 checksum of the file. The value of `ETag` can be used to check whether the object gets corrupted during the upload. <br>For example, `"09cba091df696af91549de27b8e7d0f6"`. **Note: Double quotation marks are required at the beginning and the end of the `ETag` value string here** | String |

### Uploading an Object Using a Form

The SDK for Node.js does not provide a method for the `POST Object` API. If you need to use this API, see "Solution B: Upload with Form" in [Practice of Direct Transfer for Web End](https://intl.cloud.tencent.com/document/product/436/9067).

### Querying Object Metadata

#### Feature Description

This API (HEAD Object) is used to query object metadata.

#### Sample

```js
cos.headObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',               /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| --------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| IfModifiedSince | If the object is modified after the specified time, the corresponding object metadata will be returned; otherwise, `304` will be returned | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------- |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200` and `304`. If no modification is made after the specified time, `304` will be returned | Number |
| - headers | Header information returned by the request | Object |
| - x-cos-object-type | Indicates whether an object can be appended to an upload operation. Enumerated values: `normal`, `appendable` | String |
| - x-cos-storage-class | Object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE` | String |
| - x-cos-meta-* | User-defined metadata | String |
| - NotModified | Whether an object is unmodified after the specified time | Boolean |

### Downloading an Object

This API (GET Object) is used to get the content, in string format, of a specified file in a bucket.

#### Sample

```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
}, function(err, data) {
    console.log(err || data.Body);
});
```

Get file content with `Range` specified:

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

Download the file to a specified path:

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

Download the file to a specified write file stream:

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

#### Parameter Description

| Parameter Name | Description | Type | Required |
| -------------------------- | ------------------------------------------------------------ | ------------------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| Output | An output file path or a write stream. If this parameter is not passed in, the full content will be written to `data` in the callback function | String/WriteStream | No |
| ResponseContentType | Sets the `Content-Type` parameter in the response headers | String | No |
| ResponseContentLanguage | Sets the `Content-Language` parameter in the response headers | String | No |
| ResponseExpires | Sets the `Content-Expires` parameter in the response headers | String | No |
| ResponseCacheControl | Sets the `Cache-Control` parameter in the response headers | String | No |
| ResponseContentDisposition | Sets the `Content-Disposition` parameter in the response headers | String | No |
| ResponseContentEncoding | Sets the `Content-Encoding` parameter in the response headers | String | No |
| Range | Byte range of the object. The range value must be in the format of `bytes=first-last`, where both `first` and `last` are offsets starting from 0. For example, `bytes=0-9` means that you want to copy the first 10 bytes of data of the source object. If this parameter is not specified, the entire object will be read | String | No |
| IfModifiedSince | If the object is modified after the specified time, the corresponding object metadata will be returned; otherwise, `304` will be returned | String | No |
| IfModifiedSince | The file content will be returned only if the file is modified before or at the specified time; otherwise, `412` (precondition failed) will be returned | String | No |
| IfMatch | The file will be returned only if `ETag` matches the specified content; otherwise, `412` (precondition failed) will be returned | String | No |
| IfNoneMatch | The file will be returned only if `ETag` does not match the specified content; otherwise, `304` (not modified) will be returned | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------- |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `304`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - x-cos-object-type | Indicates whether an object can be appended to an upload operation. Enumerated values: `normal`, `appendable` | String |
| x-cos-storage-class | Storage class of the object. Enumerated values: `STANDARD`, `STANDARD_IA`. <br>**Note: If this header is not returned, it means the file storage class is `STANDARD` (standard storage)** | String |
| - x-cos-meta-* | User-defined metadata | String |
| - NotModified | This attribute will be returned if the request carries `IfModifiedSince`. If the file has not been modified, `true` will be returned; otherwise, `false` will be returned | Boolean |
| - Body | Returned file content, which is in string format by default | String |

### Pre-requesting Cross-origin Configuration

#### Feature Description

This API (OPTIONS Object) is used to implement a pre-request for cross-origin object access configuration. Before making a real cross-origin resource sharing (CORS) request, you can send an `OPTIONS` request carrying the specific source origin, HTTP method, and header information to COS for it to determine whether a real request can be sent. If there is no CORS configuration, `403 Forbidden` will be returned. **You can enable CORS for a bucket using the `PUT Bucket cors` API**.

#### Sample

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

#### Parameter Description

| Parameter Name | Description | Type | Required |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| Origin | Source origin of the simulated cross-origin access request | String | Yes |
| AccessControlRequestMethod | HTTP method of the simulated cross-origin access request | String | Yes |
| AccessControlRequestHeaders | Headers of the simulated cross-origin access request | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ---------------------------- | ------------------------------------------------------------ | ------- |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - headers | Header information returned by the request | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - AccessControlAllowOrigin | Source origins of the simulated cross-origin access request separated by commas. This header will not be returned if the origins are not allowed. Example: `*` | String |
| - AccessControlAllowMethods | HTTP methods of the simulated cross-origin access request separated by commas, such as PUT, GET, POST, DELETE, and HEAD. This header will not be returned if the request methods are not allowed | String |
| - AccessControlAllowHeaders | Headers of the simulated cross-origin access request separated by commas, such as accept, content-type, origin, and authorization. This request header will not be returned if any of the simulated headers is not allowed | String |
| - AccessControlExposeHeaders | Response headers supported by CORS, such as `ETag`. The headers are separated by commas | String |
| - AccessControlMaxAge | Sets the validity period of the `OPTIONS` request result, such as `3600` | String  |
| - OptionsForbidden | Whether the `OPTIONS` request is forbidden, which will be `true` if the returned HTTP status code is `403` | Boolean |

### Copying an Object

#### Feature Description

This API (PUT Object - Copy) is used to copy a file from the source path to the destination path. The recommended file size is from 1 MB to 5 GB. For files over 5 GB, please use the multipart upload API (Upload - Copy). The metadata and ACL of the file can be modified during the copy process. You can use this API to copy a file, modify its attributes (the source file attributes are the same as the destination file attributes), move it, or rename it (copy it first and then call the DELETE API separately).

#### Sample

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

#### Parameter Description

| Parameter Name | Description | Type | Required |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| CopySource | URL path to the source file. A historical version can be specified using the `versionId` subresource | String | Yes |
| ACL | Defines the ACL attribute of the object. Valid values: `private`, `public-read`. Default value: `private` | String | No |
| GrantRead | Grants the grantee Read access in the format of `id="[OwnerUin]"` | String | No |
| GrantFullControl | Grants the grantee full permission in the format of `id="[OwnerUin]"` | String | No |
| MetadataDirective | Whether to copy the metadata. Enumerated values: `Copy`, `Replaced`. Default value: `Copy`. If its value is `Copy`, the user metadata in the corresponding header will be ignored and the copy will be performed; if its value is `Replaced`, the metadata will be replaced by the information in the corresponding header. **If the destination path is the same as the source path, which means you want to modify the metadata, you must specify this parameter as `Replaced`** | String | No |
| CopySourceIfModifiedSince | If the object is modified after the specified time, the operation will be performed; otherwise, `412` will be returned. **This parameter can be used together with `CopySourceIfNoneMatch`. If it is used together with other conditions, a conflict will be returned** | String | No |
| CopySourceIfUnmodifiedSince | If the object is not modified after the specified time, the operation will be performed; otherwise, `412` will be returned. **This parameter can be used together with `CopySourceIfMatch`. If it is used together with other conditions, a conflict will be returned** | String | No |
| CopySourceIfMatch | If the `Etag` of the object is the same as the specified one, the operation will be performed; otherwise, `412` will be returned. **This parameter can be used together with `CopySourceIfUnmodifiedSince`. If it is used together with other conditions, a conflict will be returned** | String | No |
| CopySourceIfNoneMatch | If the `Etag` of the object is different from the specified one, the operation will be performed; otherwise, `412` will be returned. **This parameter can be used together with `CopySourceIfModifiedSince`. If it is used together with other conditions, a conflict will be returned** | string | No |
| StorageClass | Storage class; enumerated values: `Standard`, `Standard_IA`. Default value: `Standard` | String | No |
| x-cos-meta-* | Other user-defined file headers | String | No |
| CacheControl | Specifies the commands that all caching mechanisms must obey throughout the entire request/response chain | String | No |
| ContentDisposition | An extension of the MIME protocol. The MIME protocol instructs the MIME user agent on how to display the attached files | String | No |
| ContentEncoding | A pair of header fields used in HTTP which specifies the encoding format of the body | String | No |
| ContentType | HTTP request content type (MIME) as defined in RFC 2616, such as `text/plain` | String | No |
| Expect | Requested specific server behavior | String | No |
| Expires | Expiration date and time of the response | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - ETag | MD5 checksum of the file, such as `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end** | String |
| - LastModified | Describes the last modified time of the object, such as `2017-06-23T12:33:27.000Z` | String |

### Deleting a Single Object

#### Feature Description

This API (DELETE Object) is used to delete a specified object in a bucket. To make this request, you need to have the permission to write to the bucket.

#### Sample

```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg'                            /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `204`, `403`, and `404`. **If the deletion is successful or the file does not exist, `204` or `200` will be returned; if the specified bucket is not found, `404` will be returned** | Number |
| - headers | Header information returned by the request | Object |

### Deleting Multiple Objects

#### Feature Description

This API (DELETE Multiple Objects) is used to delete multiple objects in a single request. You can delete up to 1,000 objects in a single request. For the response, there are two modes for you to choose from: Verbose and Quiet. Verbose mode returns the information on the deletion of each object, whereas Quiet mode only returns the information on objects for which errors are reported.

#### Sample

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

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ----------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Quiet | A boolean value which determines whether to use the Quiet mode. If the value is `true`, the Quiet mode will be used; if it is `false`, the Verbose mode will be used. Default value: `false` | Boolean | No |
| Objects | List of files to be deleted | ObjectArray | Yes |
| - Key | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| - VersionId | Version ID of the object or the delete marker to be deleted | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `204`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `204`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - Deleted | Describes information on the objects successfully deleted in this operation | ObjectArray |
| - - Key | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| - - VersionId | If the `VersionId` parameter is passed in, it will also be included in the response, indicating the version of the operated object or delete marker | String |
| - - DeleteMarker | If versioning is enabled and the `VersionId` parameter is not specified, the deletion will not actually erase the content of a file; instead, it will only add a new delete marker, indicating that the visible file has been deleted. Enumerated values: `true`, `false` | String |
| - - DeleteMarkerVersionId | If the value of the returned `DeleteMarker` is `true`, this parameter will be returned, representing the `VersionId` of the newly added delete marker | String |
| - Error | Describes information on the objects that have not been deleted in this operation | ObjectArray |
| - - Key | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| - - Code | Error code of the deletion failure | String |
| - - Message | Error message of the deletion failure | String |

## Multipart Upload Operations

### Querying a Multipart Upload

#### Feature Description

This API (List Multiparts Uploads) is used to query the ongoing multipart uploads. A single request operation can list up to 1,000 multipart uploads.

#### Sample

Get the list of incomplete multipart uploads whose `UploadId` is prefixed with `1.zip`:

```js
cos.multipartList({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Prefix: '1.zip',                        /* Optional */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Prefix | Matching prefix for object keys, which sets that the response only contains object keys with the specified prefix. Note that when you make a query with the prefix specified, the returned keys will still contain `Prefix` | String | No |
| Delimiter | A delimiter is a separating symbol used to group object keys. It is usually `/`. The identical paths between `Prefix` or, if no `Prefix` is specified, the beginning and the first `delimiter` are grouped and defined as a common prefix. All common prefixes will be listed. | String | No |
| EncodingType | Specifies the encoding type of the returned values; valid value: `url` | String | No |
| MaxUploads | Sets the maximum number of entries returned; value range: 1-1,000. Default value: 1,000 | String | No |
| KeyMarker | Used together with `upload-id-marker`. <br> <li>If `upload-id-marker` is not specified: <br>&emsp;- only the multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed. <br><li>If `upload-id-marker` is specified: <br>&emsp;- the multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed; <br>&emsp;- and the multipart uploads whose `ObjectName` is equal to the `key-marker` will also be listed, provided that their `UploadID` is greater than the specified `upload-id-marker` | String | No |
| UploadIdMarker | Used together with `key-marker`. <br><li>If `key-marker` is not specified: <br>&emsp;- `upload-id-marker` will be ignored. <br><li>If `key-marker` is specified: <br>&emsp;- the multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed; <br>&emsp;- and the multipart uploads whose `ObjectName` is equal to the `key-marker` will also be listed, provided that their `UploadID` is greater than the specified `upload-id-marker` | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| -------------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - Bucket | Destination bucket for the multipart upload | String |
| - Encoding-Type | Specifies the encoding type of the returned values; valid value: `url` | String |
| - KeyMarker      | The key value where the entry list starts                                      | String |
| - UploadIdMarker     | The `UploadId` value where the entry list starts                                      | String |
| - NextKeyMarker | If the returned list is truncated, the `NextKeyMarker` returned will be the starting point of the subsequent list | String |
| - NextUploadIdMarker | If the returned list is truncated, the `UploadId` returned will be the starting point of the subsequent list | String |
| - MaxUploads | Sets the maximum number of entries returned; value range: 1-1,000 | String |
| - IsTruncated | Whether the returned list is truncated; valid values: `true`, `false` | String |
| - Prefix | Matching prefix for object keys, which sets that the response only contains object keys with the specified prefix. | String |
| - Delimiter | A delimiter is a separating symbol used to group object keys. It is usually `/`. The identical paths between `Prefix` or, if no `Prefix` is specified, the beginning and the first `delimiter` are grouped and defined as a common prefix. All common prefixes will be listed. | String |
| - CommonPrefixes | The identical paths between `prefix` and `delimiter` are grouped and defined as a common prefix | ObjectArray |
| - - Prefix | Displays specific common prefixes | String |
| - Upload | Set of information on multipart uploads | ObjectArray |
| - - Key | Object name, i.e., object key | String |
| - - UploadId | Identifies the ID of this multipart upload | String |
| - - StorageClass | Indicates part storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE` | String |
| - - Initiator        | Information on the initiator of this upload                                 | Object                 |
| - - - DisplayName      | Name of the upload initiator                                            | String      |
| - - - ID | ID of the upload initiator in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`. <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String |
| - - Owner | Information on the owner of the parts | Object  |
| - - - DisplayName | Part owner name | String |
| - - - ID | Part owner ID in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`.<br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String |
| - - Initiated | Starting time of the multipart upload | String |


### Initializing a Multipart Upload

#### Feature Description

This API (Initiate Multipart Upload) is used to initialize a multipart upload. After a successful operation, an upload ID will be returned which can be used in the subsequent `Upload Part` requests.

#### Sample

```js
cos.multipartInit({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| CacheControl | Cache policy as defined in RFC 2616, which will be stored in the object metadata | String | No |
| ContentDisposition | Filename as defined in RFC 2616, which will be stored in the object metadata | String | No |
| ContentEncoding | Encoding format as defined in RFC 2616, which will be stored in the object metadata | String | No |
| ContentType | Content type (MIME) as defined in RFC 2616, which will be stored in the object metadata | String | No |
| Expires | Expiration time as defined in RFC 2616, which will be stored in the object metadata | String | No |
| ACL | Defines the ACL attribute of the object. Valid values: `private`, `public-read`. Default value: `private` | String | No |
| GrantRead | Grants the grantee Read access in the format of `id="[OwnerUin]"` | String | No |
| GrantFullControl | Grants the grantee full permission in the format of `id="[OwnerUin]"` | String | No |
| StorageClass | Sets the object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String | No |
| x-cos-meta-* | Headers that can be defined by users, which will be returned as the object metadata; maximum size: 2 KB | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| Bucket | Destination bucket for the multipart upload | String |
| Key | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| UploadId | ID that can be used in subsequent uploads | String |

### Uploading Parts

#### Feature Description

This API (Upload Part) is used to upload parts after a multipart upload is initialized. It can upload up to 10,000 parts of 1 MB to 5 GB each in size.
When the `Initiate Multipart Upload` API is used to initialize a multipart upload, an `uploadId` will be returned. The ID uniquely identifies the data of the part and its position in the entire file. Every time you request the `Upload Part` API, you need to pass in `partNumber`, the part number, and `uploadId`. You can upload multiple parts out of order.
When the `uploadId` and `partNumber` of a new part are the same as those of a previously uploaded part, the old part will be overwritten by the new one. A 404 error, `NoSuchUpload`, will be returned if the `uploadId` does not exist.

#### Sample

```js
cos.multipartUpload({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',       /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------------- | ------------------------------------------------------------ | ---------------- | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| ContentLength | HTTP request length in bytes as defined in RFC 2616 | String | Yes |
| PartNumber | Part number | String | Yes |
| UploadId | Upload task number | String | Yes |
| Body | Content of the file part to be uploaded, which can be a string, a File object, or a Blob object | String\File\Blob | Yes |
| Expect | If `Expect: 100-continue` is used, the request content will be sent only after the confirmation from the server is received | String | No |
| ContentMD5 | Base64-encoded 128-bit content MD5 checksum as defined in RFC 1864. This header is used to check whether the file content has changed | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |

### Copying Parts

#### Feature Description

This API (Upload Part - Copy) is used to copy the parts of an object from a source path to a destination path.
> 
>
> 1. If the destination object and the source object are in different regions, and the part size of the destination object will exceed 5 GB, you will need to use the API for object copying or object multipart upload to copy the object.
> 2. To upload an object in parts, you must first initialize the multipart upload. The response of the multipart upload initialization will return a unique descriptor, an upload ID, which needs to be carried in the multipart upload request.

#### Sample

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

#### Parameter Description

| Parameter Name | Description | Type | Required |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| CopySource | URL path to the source object. A historical version can be specified with the URL parameter ?versionId=\<versionId> | String | Yes |
| partNumber | Number of the part to be copied | String | Yes |
| uploadId | To upload an object in parts, you must first initialize the multipart upload. The response of the multipart upload initialization will return a unique descriptor, an upload ID, which needs to be carried in the multipart upload request | String | Yes |
| CopySourceRange | Byte range of the source object. The range value must be in the format of `bytes=first-last`, where both `first` and `last` are offsets starting from 0. For example, `bytes=0-9` means that you want to copy the first 10 bytes of data of the source object. If this parameter is not specified, the entire object will be copied | String | No |
| CopySourceIfMatch | If the `Etag` of the object is the same as the specified one, the operation will be performed; otherwise, `412` will be returned. This parameter can be used together with `x-cos-copy-source-If-Unmodified-Since`. If it is used together with other conditions, a conflict will be returned | String | No |
| CopySourceIfNoneMatch | If the `Etag` of the object is different from the specified one, the operation will be performed; otherwise, `412` will be returned. This parameter can be used together with `x-cos-copy-source-If-Modified-Since`. If it is used together with other conditions, a conflict will be returned | string | No |
| CopySourceIfUnmodifiedSince | If the object is not modified after the specified time, the operation will be performed; otherwise, `412` will be returned. This parameter can be used together with `x-cos-copy-source-If-Match`. If it is used together with other conditions, a conflict will be returned | String | No |
| CopySourceIfModifiedSince | If the object is modified after the specified time, the operation will be performed; otherwise, `412` will be returned. This parameter can be used together with `x-cos-copy-source-If-None-Match`. If it is used together with other conditions, a conflict will be returned | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - ETag | MD5 checksum of the file, such as `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end** | String |
| - LastModified | Returns the last modified time of the object in GMT time | String |


### Querying Uploaded Parts

#### Feature Description

This API (List Parts) is used to query the uploaded parts in a specified multipart upload, i.e., listing all the successfully uploaded parts in the multipart upload with the specified `UploadId`.

#### Sample

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

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ---------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| UploadId | ID of this multipart upload. When the `Initiate Multipart Upload` API is used to initialize a multipart upload, an `uploadId` will be returned. The ID uniquely identifies the data of the part and its position in the entire file | String | Yes |
| EncodingType | Specifies the encoding type of the returned value | String | No |
| MaxParts | Maximum number of entries returned at a time. Default value: 1,000 | String | No |
| PartNumberMarker | By default, entries are listed in UTF-8 binary order starting from the marker | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ---------------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - Bucket | Destination bucket for the multipart upload | String |
| - Encoding-type | Specifies the encoding type of the returned value | String |
| - Key | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| - UploadId | Identifies the ID of this multipart upload | String |
| - Initiator        | Identifies the initiator of this upload                                 | Object                 |
| - - DisplayName      | Name of the upload initiator                                            | String      |
| - - ID | ID of the upload initiator in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String |
| - Owner | Information on the owner of the parts | Object  |
| - - DisplayName      | Bucket owner name                                            | String      |
| - - ID | Bucket owner ID, which is typically a UIN | String |
| - StorageClass | Indicates part storage class; enumerated values: `Standard`, `Standard_IA`, `Archive` | String |
| PartNumberMarker | By default, entries are listed in UTF-8 binary order starting from the marker | String |
| - NextPartNumberMarker | If the returned list is truncated, the `NextMarker` returned will be the starting point of the subsequent list | String |
| - MaxParts | Maximum number of entries returned at a time | String |
| - IsTruncated | Whether the returned list is truncated; valid values: `true`, `false` | String |
| - Part | Array | Part information list | ObjectArray |
| - - PartNumber | Part number | String |
| - - LastModified | Last modified time of a part | String |
| - - ETag | MD5 checksum of a part | String |
| - - Size | Part size in bytes | String |

### Completing a Multipart Upload

#### Feature Description

This API (Complete Multipart Upload) is used to complete a multipart upload. After all parts are uploaded via the `Upload Part` API, you need to call this API to complete the multipart upload. When using this API, you need to specify the `PartNumber` and `ETag` of each part in the request body for the part information to be verified.
As the parts need to be merged after they are uploaded, and the merge takes several minutes, COS will immediately return status code `200` when the merge starts, and periodically return spaces during the merge to keep the connection active until the merge is complete. After that, COS will return the content of the merged object in the response body.

- If any uploaded part is below 1 MB in size, `400 EntityTooSmall` will be returned when this API is called.
- If the numbers of the uploaded parts are not continuous, `400 InvalidPart` will be returned when this API is called.
- If the part information entries in the request body are not sorted by number in ascending order, `400 InvalidPartOrder` will be returned when this API is called.
- If the `UploadId` does not exist, `404 NoSuchUpload` will be returned when this API is called.

#### Sample

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

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ----------- | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| UploadId | Upload task number | String | Yes |
| Parts | List of information on the parts in this multipart upload | ObjectArray | Yes |
| - PartNumber | Part number | String | Yes |
| - ETag | MD5 checksum of each part. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end** | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - Location | Domain name of the created object for public network access | String |
| - Bucket | Destination bucket for the multipart upload | String |
| - Key | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| - ETag | Unique ID of the merged file in the format of `"uuid-<part quantity>"`. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`. **Note that double quotation marks are required at the beginning and the end** | String |

### Aborting a Multipart Upload

#### Feature Description

This API (Abort Multipart Upload) is used to abort a multipart upload and delete the uploaded parts. If you call this API and there is an `Upload Part` request that is using the multipart upload, the request will fail. If the `uploadId` does not exist, `404 NoSuchUpload` will be returned.

>  It is recommended to either complete or abort a multipart upload as early as possible, as the uploaded parts of an incomplete multipart upload will take up storage capacity and incur storage fees.

#### Sample

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

#### Parameter Description

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| UploadId | ID of this multipart upload. When the `Initiate Multipart Upload` API is used to initialize a multipart upload, an `uploadId` will be returned. The ID uniquely identifies the data of the part and its position in the entire file | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |

## Other Operations

### Restoring an Archived Object

#### Feature Description

This API (POST Object restore) is used to restore an archived object for access.

#### Sample

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

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------------------ | ------------------------------------------------------------ | ------- | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| RestoreRequest | Container used for data restoration | Object | Yes |
| - Days | Sets the expiration time of the temporary copy | Object | Yes |
| - CASJobParameters | Container of the Cloud Archive Storage job parameters | Object | Yes |
| - - Tier | This parameter can be specified as one of the three data restoration modes supported by CAS: `Standard`, standard mode where a restoration job can be completed in 3-5 hours; `Expedited`, expedited mode where a restoration job can be completed in 15 minutes; and `Bulk`, batch mode where a restoration job can be completed in 5-12 hours | Integer | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |

### Setting Object ACL

#### Feature Description

This API (PUT Object acl) is used to set the ACL for an object.

>  The total number of policies associated with bucket ACL, Policy, and CAM under a single root account (i.e., under the same APPID) cannot exceed 1,000. There is no upper limit on the number of object ACL rules. If you do not need access control for an object, do not make the configuration, and the object will inherit the permissions of its bucket.

#### Sample

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

Grant a user Read/Write access to a file:

```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
    GrantFullControl: 'id="100000000001"' // 100000000001 is the UIN of the root account
}, function(err, data) {
    console.log(err || data);
});
```

Modify bucket permission with `AccessControlPolicy`:

```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
    AccessControlPolicy: {
        "Owner": { // `Owner` is required in `AccessControlPolicy`
            "ID": 'qcs::cam::uin/100000000001:uin/100000000001' // 100000000001 is the UIN of the bucket owner
        },
        "Grants": [{
            "Grantee": {
                "ID": "qcs::cam::uin/100000000011:uin/100000000011", // 100000000011 is UIN
            },
            "Permission": "WRITE"
        }]
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| ACL | Defines the ACL attribute of the object. Valid values: `private`, `public-read`, `default`. Default value: `private`. If `default` is passed in, the file permissions will be cleared and restored to the inherited permissions | String | No |
| GrantRead | Grants the grantee Read access in the format of `id="[OwnerUin]"` | String | No |
| GrantFullControl | Grants the grantee full permission in the format of `id="[OwnerUin]"` | String | No |
| AccessControlPolicy | Object ACL in JSON format | Object | No |
| - Owner | Identifies the resource owner | Object | No |
| - - ID | Object owner ID in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String | No |
| - - DisplayName | Object owner name | String | No |
| - Grants | List of information on the grantee and permissions | ObjectArray | No |
| - - Permission | Specifies the permission granted to the grantee. Enumerated values: `READ`, `WRITE`, `READ_ACP`, `WRITE_ACP`, `FULL_CONTROL` | String | No |
| - - Grantee | Describes the information on the grantee. The type can be RootAccount or Subaccount. If the type is RootAccount, the ID specifies a root account; if the type is Subaccount, the ID specifies a sub-account | Object | No |
| - - - DisplayName | Username | String | No |
| - - - ID | User ID in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `204`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |

### Querying Object ACL

#### Feature Description

This API (GET Object acl) is used to query the ACL of an object.

#### Sample

```js
cos.getObjectAcl({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ----------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - ACL | Object's ACL attributes; enumerated values: `private`, `public-read`, `default` | Object |
| - Owner | Identifies the resource owner | Object |
| - - ID | Object owner ID in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String |
| - - DisplayName | Object owner name | String |
| - Grants | List of information on the grantee and permissions | ObjectArray |
| - - Permission | Specifies the permission granted to the grantee. Enumerated values: `READ`, `READ_ACP`, `WRITE_ACP`, `FULL_CONTROL` | String |
| - - Grantee | Describes the information on the grantee. The type can be RootAccount or Subaccount. If the type is RootAccount, the ID specifies a root account; if the type is Subaccount, the ID specifies a sub-account | Object |
| - - - DisplayName | Username | String |
| - - - ID | User ID in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String |

## Advanced APIs (Recommended)

The following methods encapsulate the native methods mentioned above. They can implement the complete process of multipart upload/copy and support concurrent multipart upload/copy, checkpoint restart as well as cancelling, pausing, and restarting upload tasks.

### Uploading an Object in Parts

#### Feature Description

This API (Slice Upload File) is used to upload a large files in parts.

#### Sample

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

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| FilePath | Path to the file to be uploaded | String | Yes |
| SliceSize | Part size | String | No |
| AsyncLimit | Concurrent number of parts being uploaded | String | No |
| StorageClass | Object storage class; enumerated value: `STANDARD`, `STANDARD_IA` | String | No |
| TaskReady | Callback function when an upload task is created. The callback returns a `taskId`, which uniquely identifies the task and can be used to cancel (cancelTask), pause (pauseTask), or restart (restartTask) the task | Function | No |
| - taskId | Upload task number | String | No |
| onHashProgress | Progress callback function for file MD5 value calculation. The callback parameter is the progress object `progressData` | Function | No |
| - progressData.loaded | Size of the file part that has been verified; unit: byte | Number | No |
| - progressData.total | Size of the entire file; unit: byte | Number | No |
| - progressData.speed | File verification speed; unit: bytes/s | Number | No |
| - progressData.percent | A decimal representing the file verification progress; for example, 0.5 means 50% verified | Number | No |
| onProgress | Progress callback function for file upload. The callback parameter is the progress object `progressData` | Function | No |
| - progressData.loaded | Size of the file part that has been uploaded; unit: byte | Number | No |
| - progressData.total | Size of the entire file; unit: byte | Number | No |
| - progressData.speed | File upload speed; unit: bytes/s | Number | No |
| - progressData.percent | A decimal representing the file upload progress. For example, 0.5 means 50% uploaded | Number | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - Location | Domain name of the created object for public network access | String |
| - Bucket | Destination bucket for the multipart upload | String |
| - Key | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| - ETag | Unique ID of the merged file in the format of `"uuid-<part quantity>"`. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`. **Note that double quotation marks are required at the beginning and the end** | String |

### Copying an Object

#### Feature Description

This API (Slice Copy File) is used to copy a file from a source path to a destination path through multipart copy. Object metadata and ACL can be modified during the copy process. You can use this API to move, rename, and copy a file or modify its attributes.

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

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| CopySource | URL path to the source file. A historical version can be specified using the `versionId` subresource | String | Yes |
| ChunkSize | Size of the parts in the multipart copy; unit: byte. Default value: 1,048,576 (1 MB) | Number | No |
| SliceSize | Size of the file to be copied. Default value: 5 GB | Number | No |
| onProgress | Progress callback function for file upload. The callback parameter is the progress object `progressData` | Function | No |
| - progressData.loaded | Size of the file part that has been uploaded; unit: byte | Number | No |
| - progressData.total | Size of the entire file; unit: byte | Number | No |
| - progressData.speed | File upload speed; unit: bytes/s | Number | No |
| - progressData.percent | A decimal representing the file upload progress. For example, 0.5 means 50% uploaded | Number | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - Location | Domain name of the created object for public network access | String |
| - Bucket | Destination bucket for the multipart upload | String |
| - Key | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| - ETag | MD5 checksum of the merged file. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end** | String |

### Batch Upload

#### Feature Description

Method 1:
You can call `putObject` and `sliceUploadFile` multiple times to implement batch uploads. You can instantiate `FileParallelLimit` parameter to limit how many files can be uploaded at the same time, which is 3 by default.

Method 2:
You can call `cos.uploadFiles` to implement batch uploads. The `SliceSize` method parameter can be used to manage the files. Below are instructions on the `uploadFiles` method.

#### Method Prototype

Call the `uploadFiles` operation:

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
        console.log(options.Key + 'upload' + (err ? 'failed' : 'completed'));
    },
}, function (err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | ------ | ---- |
| files | File list, where each item is a parameter object to be passed to `putObject` and `sliceUploadFile` | Object | Yes |
| SliceSize | Specifies the minimum file size in bytes for which multipart upload will be used. If the size of a file is equal to or smaller than this value, the file will be uploaded using `putObject`; otherwise, it will be uploaded using `sliceUploadFile` | Number | Yes |
| onProgress | Upload progress calculated by averaging out the progress of all tasks | String | Yes |
| - progressData.loaded | Size of the file part that has been uploaded; unit: byte | Number | No |
| - progressData.total | Size of the entire file; unit: byte | Number | No |
| - progressData.speed | File upload speed; unit: bytes/s | Number | No |
| - progressData.percent | A decimal representing the file upload progress. For example, 0.5 means 50% uploaded | Number | No |
| onFileFinish | The completion or error callback for each file | String | Yes |
| - err | Upload error message | Object | No |
| - data | File upload completion information | Object | No |
| - options | Parameter information on the files that have been uploaded | Object | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - files | error or data for each file | ObjectArray |
| - - err | Upload error message | Object |
| - - data | File upload completion information | Object |
| - - options | Parameter information on the files that have been uploaded | Object |

### Upload Queue

The SDK for JavaScript recorded all the upload tasks initiated with `putObject` and `sliceUploadFile` in an upload queue. You can use the queue in the following ways:

1. Use cos.getTaskList to get the task list.
2. Use cos.pauseTask, cos.restartTask, and cos.cancelTask to perform operations on upload tasks.
3. Use cos.on('list-update', callback); to monitor changes in the list and the upload progress.

For a complete example of queue usage, see [demo-queue](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/demo/queue).

#### Canceling an Upload Task

This API is used to cancel an upload task by `taskId`.

**Sample**

```js
var taskId = 'xxxxx';                   /* Required */
cos.cancelTask(taskId);
```

**Parameter Description**

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | ID of an upload task. When `sliceUploadFile` is called, `TaskReady` in the callback will return the `taskId` of the upload task | String | Yes |

#### Pausing an Upload Task

This API is used to pause an upload task by `taskId`.

**Sample**

```js
var taskId = 'xxxxx';                   /* Required */
cos.pauseTask(taskId);
```

**Parameter Description**

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | ID of an upload task. When `sliceUploadFile` is called, `TaskReady` in the callback will return the `taskId` of the upload task | String | Yes |

#### Restarting an Upload Task

This API is used to restart an upload task by `taskId`. It can restart tasks that have been manually paused with the `pauseTask` API or have been stopped due to an upload error.

**Sample**

```js
var taskId = 'xxxxx';                   /* Required */
cos.restartTask(taskId);
```

**Parameter Description**

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | ID of an upload task. When `sliceUploadFile` is called, `TaskReady` in the callback will return the `taskId` of the upload task | String | Yes |
