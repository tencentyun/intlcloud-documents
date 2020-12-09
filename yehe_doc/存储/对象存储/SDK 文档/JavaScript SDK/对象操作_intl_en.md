## Overview

This document provides an overview of APIs and SDK sample codes related to simple operations, multipart operations, and other object operations.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ---------------------------------------- |
| [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying an object list | Queries some or all objects in a bucket |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object using simple upload | Uploads an object to a bucket |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | Uploading an object using an HTML form | Uploads an object using an HTML form |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |
| [OPTIONS Object](https://intl.cloud.tencent.com/document/product/436/8288) | Configuring a pre-flight request for cross-origin access | Sends a pre-flight request to confirm whether a real cross-origin access request can be sent |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object | Copies an object to the destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes a specified object from a bucket |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects in a single request |

**Multipart operations**

| API          | Operation                   | Description                                       |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries in-progress multipart uploads |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading a part | Uploads a part in a multipart upload |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Uploads a part by copying data from an existing object as the data source |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying parts | Queries uploaded parts in a specified multipart upload |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of an entire object |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload and deletes the uploaded parts |

**Other operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting object ACL | Sets the ACL of a specified object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying object ACL | Queries the ACL of an object |

## Simple Operations

### Querying an object list

#### API description

This API is used to query some or all objects in a bucket.

#### Samples

Sample 1. List all the files in directory `a`.

[//]: # ".cssg-snippet-get-bucket"
```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Prefix: 'a/', /*Optional*/
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

[//]: # ".cssg-snippet-get-bucket-with-delimiter"
```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Prefix: 'a/', /*Optional*/
    Delimiter: '/',            /* Optional */
}, function(err, data) {
    console.log(err || data.CommonPrefixes);
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

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ------ | -------- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Prefix | Limits the response to keys that begin with the specified prefix | String | No |
| Delimiter | A delimiter is a separating symbol used to group object keys. It is usually `/`. The identical paths between `Prefix` or, if no `Prefix` is specified, the beginning, and the first delimiter` are grouped and defined as a common prefix. All common prefixes will be listed | String | No |
| Marker | Indicates where the object key listing begins. Entries are listed starting from the key after the `Marker` in UTF-8 lexicographical order by default | String | No |
| MaxKeys | Specifies the maximum number of entries returned at a time; default value: 1000 | String | No |
| EncodingType | Specifies the encoding type of the returned value. Valid value: `url`, meaning that returned object keys are URL-encoded (percent-encoded). For example, "Tencent Cloud" will be encoded as `%E8%85%BE%E8%AE%AF%E4%BA%91` | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ----------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty | Object |
| - headers | Headers returned by the request | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - Name | Bucket name in the format: `BucketName-APPID`, such as `examplebucket-1250000000` | String |
| - Prefix | Limits the response to keys that begin with the specified prefix | String |
| - Marker | By default, entries are listed in UTF-8 binary order starting from the entry after the `Marker` | String |
| - MaxKeys | Maximum number of results returned for a single request | String |
| - Delimiter | Delimiter | String |
| - IsTruncated | Specifies whether returned entries are truncated. Valid values: `true`, `false` | String |
| - NextMarker | If returned entries are truncated, then `NextMarker` marks where the next listing should begin | String |
| - CommonPrefixes | The identical paths between a specified prefix and the delimiter are grouped and defined as a common prefix | ObjectArray |
| - - Prefix | A single common prefix | String |
| - EncodingType | Encoding type of the returned values, which is applicable to `Delimiter`, `Marker`, `Prefix`, `NextMarker`, and `Key` | String |
| - Contents | Lists object metadata | ObjectArray |
| - - Key | Object key, i.e., object name | String |
| - - ETag | MD5 checksum of the file,<br>such as `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end of the ETag** | String |
| - - Size | Object size in bytes | String |
| - - LastModified  | Returns the time the object was last modified in ISO8601 format, such as 2019-05-24T10:56:40Z | String |
| - - Owner | Object owner information | Object |
| - - - ID | Complete ID of the object owner in the format of `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`,<br>such as `qcs::cam::uin/100000000001:uin/100000000001`, where 100000000001 is the UIN | String |
| - - - DisplayName | Object owner name | String |
| - - StorageClass |Storage class of the object. Enumerated values: `STANDARD`, `STANDARD_IA` and `ARCHIVE`. For more information, please see [Storage Classes Overview](https://intl.cloud.tencent.com/document/product/436/30925) | String |

### Uploading an object using simple upload

#### API description

This API is used to upload an object to a bucket. To make this request, you need to have write permission for the bucket.

> !
> 1. The Key (file name) cannot end with `/`; otherwise, it will be identified as a folder.
> 2. Each root account (AAPID) can have up to 1,000 bucket ACLs and an unlimited number of object ACLs. If you do not need access control for an object, you can choose not to configure an ACL for the object during upload, and the object will inherit the permissions of its bucket by default.
> 3. After an object is uploaded, you can use the same key to generate a pre-signed URL, which can be shared with others for download. However, please note that if your file is set to private-read, the pre-signed URL will only be valid for a certain period of time.

#### Samples

Simple upload is suitable for uploading small files.

[//]: # ".cssg-snippet-put-object"
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    StorageClass: 'STANDARD',
    Body: fileObject, // Upload the file object
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

Upload strings as file content:

[//]: # ".cssg-snippet-put-object-string"
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    Body: 'hello!',
}, function(err, data) {
    console.log(err || data);
});
```

Create a directory:

[//]: # ".cssg-snippet-put-object-folder"
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'a/', /*Required*/
    Body: '',
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | ---------------- | -------- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| Body | Content of the file to be uploaded, which can be a string, a File object, or a Blob object | String\File\Blob | Yes |
| CacheControl | Cache policy as defined in RFC 2616, which will be stored as object metadata | String | No |
| ContentDisposition | Filename as defined in RFC 2616, which will be stored as object metadata | String | No |
| ContentEncoding | Encoding format as defined in RFC 2616, which will be stored as object metadata | String | No |
| ContentLength | HTTP request length in bytes as defined in RFC 2616 | String | No |
| ContentType | Content type (MIME) as defined in RFC 2616, which will be stored as object metadata | String | No |
| Expires | Expiration time as defined in RFC 2616, which will be stored as object metadata | String | No |
| Expect | If `Expect: 100-continue` is used, the request content will be sent only after confirmation from the server is received | String | No |
| ACL   | Defines the access control list (ACL) attribute of the object. For the enumerated values such as `default`, `private`, and `public-read`, please see the Preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). <br>**Note:** if you do not need access control for the object, set `default` for this parameter or simply leave it blank, and the object will inherit the permissions of the bucket | String | No |
| GrantRead | Grants a user read access in the format: `id="[OwnerUin]"`. You can use a comma (,) to separate multiple users. <br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantReadAcp | Grants a user read access to the object’s ACL in the format: `id="[OwnerUin]"`. You can use a comma (,) to separate multiple users. <br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantWriteAcp | Grants a user write access to the object’s ACL in the format: `id="[OwnerUin]"`. You can use a comma (,) to separate multiple users. <br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantFullControl | Grants a user full access in the format: `id="[OwnerUin]"`. You can use a comma (,) to separate multiple users. <br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| StorageClass | Sets the object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String | No |
| x-cos-meta-* | Headers that can be defined by users, which will be stored as object metadata; maximum size: 2 KB | String | No |
| UploadAddMetaMd5       | Sets x-cos-meta-md5 as the object’s MD5 value in the object’s metadata during upload in the format of a 32-bit lowercase string. For example:  `4d00d79b6733c9cc066584a02ed03410` | String           | No   |
| TaskReady | Callback function when an upload task is created. The callback returns a `taskId`, which uniquely identifies the task and can be used to cancel (cancelTask), pause (pauseTask), or restart (restartTask) the task | Function | No |
| - taskId                                                     | Upload task number                                              | String    | No  |
| onProgress | Progress callback function. Attributes of the progress callback response object, `progressData`, are as follows | Function | No |
| - progressData.loaded | Size of the uploaded file part in bytes | Number | No |
| - progressData.total                                         | Total file size in bytes                      | Number    | No   |
| - progressData.speed                                         | File upload speed in bytes/s                 | Number    | No   |
| - progressData.percent | A decimal representing the file upload progress; for example, 0.5 means 50% has been uploaded | Number | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Returns data when the request is successful. If the request fails, this parameter is left empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - ETag | Returns the MD5 checksum of the file. The value of `ETag` can be used to check whether the object was corrupted during upload. <br>For example, `"09cba091df696af91549de27b8e7d0f6"`. **Note: double quotation marks are required at the beginning and the end of the `ETag` value string** | String |
| - Location   | The location where the uploaded file can be accessed                                        | String |
| - VersionId       | Returns the version ID for versioning-enabled buckets. For buckets which have never had versioning enabled, this parameter is not returned | String  |

### Uploading an object using an HTML form

The SDK for JS does not provide a method for the `POST Object` API. If you need to use this API, please see "Solution B: Upload with Form" in [Practice of Direct Transfer for Web End](https://intl.cloud.tencent.com/document/product/436/9067).

### Querying object metadata

#### API description

This API is used to query the metadata of an object.

#### Samples

[//]: # ".cssg-snippet-head-object"
```js
cos.headObject({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| --------------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| IfModifiedSince | Returns object metadata if the object is modified after the specified time; otherwise, 304 is returned | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200` and `304`. If no modification is made after the specified time, 304 will be returned | Number |
| - headers | Headers returned by the request | Object |
| - x-cos-object-type | Indicates whether an object is appendable. Enumerated values: `normal`, `appendable`. The default value `normal` is not displayed if returned | String |
| - x-cos-storage-class | Storage class of the object. Enumerated values: `STANDARD` (default), `STANDARD_IA`, `ARCHIVE`. `STANDARD` is not displayed if returned | String |
| - x-cos-meta-* | User-defined metadata | String |
| - NotModified | Indicates whether an object is unmodified after the specified time | Boolean |
| - ETag | Returns the MD5 checksum of the file to check whether the object was corrupted during the upload.<br>For example, `"09cba091df696af91549de27b8e7d0f6"`. **Note that double quotation marks are required at the beginning and the end of the ETag** | String |
| - VersionId       | Returns the version ID for versioning-enabled buckets. For buckets which have never had versioning enabled, this parameter is not returned  | String  |

### Downloading an object

> !This API is used to read object content. To download a file using your browser, you should first get a download URL through the `cos.getObjectUrl` method. For more information, please see [Pre-signed URLs](https://intl.cloud.tencent.com/document/product/436/31540).

#### API description

This API is used to get the content, in string format, of a specified file in a bucket.

#### Samples

[//]: # ".cssg-snippet-get-object"
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
}, function(err, data) {
    console.log(err || data.Body);
});
```

Get file content with `Range` specified:

[//]: # ".cssg-snippet-get-object-range"
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    Range: 'bytes=1-3', /*Optional*/
}, function(err, data) {
    console.log(err || data.Body);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| -------------------------- | ------------------------------------------------------------ | -------- | -------- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| ResponseContentType | Sets the `Content-Type` parameter in the response headers | String | No |
| ResponseContentLanguage | Sets the `Content-Language` parameter in the response headers | String | No |
| ResponseExpires | Sets the `Content-Expires` parameter in the response headers | String | No |
| ResponseCacheControl | Sets the `Cache-Control` parameter in the response headers | String | No |
| ResponseContentDisposition | Sets the `Content-Disposition` parameter in the response headers | String | No |
| ResponseContentEncoding | Sets the `Content-Encoding` parameter in the response headers | String | No |
| Range | Byte range of the object as defined in RFC 2616. The range value must be in the format of `bytes=first-last`, where both `first` and `last` are offsets starting from 0. For example, `bytes=0-9` means that you want to download the first 10 bytes of data of the source object. If this parameter is not specified, the entire object will be downloaded | String | No |
| IfModifiedSince    | If the object is modified after the specified time, the object will be returned; otherwise, HTTP status code 304 (Not Modified) will be returned | String | No |
| IfUnmodifiedSince    | If the object is not modified after the specified time, the object will be returned; otherwise, HTTP status 412 (precondition failed) will be returned | String | No |
| IfMatch | The object will be returned only if ETag matches the specified value; otherwise, 412 (precondition failed) will be returned | String | No |
| IfNoneMatch | The object will be returned only if ETag does not match the specified value; otherwise, 304 (not modified) will be returned | String | No |
| VersionId | Specifies the version ID of the object to be downloaded | String | No |
| onProgress | Progress callback function. Attributes of the progress callback response object, `progressData`, are as follows | Function | No |
| - progressData.loaded | Size of the file part that has been downloaded; unit: byte | Number | No |
| - progressData.total | Size of the entire object in bytes | Number | No |
| - progressData.speed | Object download speed; unit: bytes/s | Number | No |
| - progressData.percent | A decimal representing the object download progress. For example, 0.5 means 50% has been downloaded | Number | No |

#### Callback function description

```
function(err, data) { ... }

```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Parameter Description | Type | 
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------- |
| err | A returned request error (network error or service error). If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | Returns an HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Returns headers | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `304`, `403`, and `404` | Number |
| - headers | Returns headers | Object |
| - CacheControl  | Cache directives as defined in RFC 2616, which will be returned only if it is contained in the object metadata or if it is specified in the request parameter | string |
| - ContentDisposition                                         | File name as defined in RFC 2616, which will be returned only if it is contained in the object metadata or if it is specified in the request parameter | String  |
| - ContentEncoding                                            | Encoding format as defined in RFC 2616, which will be returned only if it is contained in the object metadata or if it is specified in the request parameter | String  |
| - Expires                                                    | Cache expiration time as defined in RFC 2616, which will be returned only if it is contained in the object metadata or if it is specified in the request parameter | String  |
| - x-cos-storage-class | Storage class of the object. Enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE` <br>**Note: If this header is not returned, the storage class is automatically set to `STANDARD`** | String |
| - x-cos-meta-*                                               | User defined metadata                                           | String  |
| - NotModified      | If the request has IfModifiedSince, then the attributes of IfModifiedSince will be returned. If the file has been modified, `false` will be returned. If not, `true` will be returned | Boolean |
| - ETag | Returns the MD5 checksum of the file. The value of `ETag` can be used to check whether the object was corrupted during the upload. <br>For example, `"09cba091df696af91549de27b8e7d0f6"`. **Note that double quotation marks are required at the beginning and the end of the ETag** | String |
| - VersionId       | Returns the version ID for versioning-enabled buckets. For buckets which have never had versioning enabled, this parameter is not returned  | String  |
| - Body                | Returned file content. Uses the String format by default.        | String  |

### Configuring a pre-flight request for cross-origin access

#### API description

This API (OPTIONS Object) is used to send a pre–flight request for the cross-origin access configuration of an object. Before making a real cross-origin resource sharing (CORS) request, you can send an OPTIONS request that includes the source, HTTP method, and headers to COS for it to determine whether a real request can be sent. If there is no CORS configuration, an HTTP `403 Forbidden` status code will be returned. **You can enable CORS for a bucket using the `PUT Bucket cors` API**.

#### Samples

[//]: # ".cssg-snippet-option-object"
```js
cos.optionsObject({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    Origin: 'https://www.qq.com', /*Required*/
    AccessControlRequestMethod: 'PUT', /*Required*/
    AccessControlRequestHeaders: 'origin,accept,content-type' /*Optional*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| --------------------------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| Origin | Origin domain name of the simulated cross-origin access request | String | Yes |
| AccessControlRequestMethod | HTTP method of the simulated cross-origin access request | String | Yes |
| AccessControlRequestHeaders | Headers of the simulated cross-origin access request | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Parameter Description | Type | 
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------- |
| err | A returned request error (network error or service error). If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | Returns an HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Returns headers | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty | Object |
| - headers | Returns headers | Object |
| - statusCode | Returns an HTTP status code, such as `200`, `403`, and `404` | Number |
| - AccessControlAllowOrigin | Source origins of the simulated cross-origin access request separated by commas. This header will not be returned if the origins are not allowed. Example: `*` | String |
| - AccessControlAllowMethods | HTTP methods of the simulated cross-origin access request separated by commas, such as PUT, GET, POST, DELETE, and HEAD. This header will not be returned if the request method is not allowed | String |
| - AccessControlAllowHeaders | Headers of the simulated cross-origin access request separated by commas, such as `accept`, `content-type`, `origin`, and `authorization`. This request header will not be returned if any of the simulated headers are not allowed | String |
| - AccessControlExposeHeaders | Response headers supported by CORS, such as `ETag`. The headers are separated by commas | String |
| - AccessControlMaxAge | The validity duration of results returned by the OPTIONS request, e.g. `3600` | String  |
| - OptionsForbidden | Indicates whether the `OPTIONS` request is forbidden. It is `true` if HTTP status code 403 is returned | Boolean |

### Copying an object

#### API description

This API is used to create a copy of an existing COS object, that is, an object is copied from the source path (object key) to the destination path (object key). During replication, object metadata and access control lists (ACLs) can be modified.
Users can use this API to create a copy, modify object metadata (the source object and destination file have the same attributes), and move or rename the object (first copy the object, and then call the delete API separately).

> !We recommend that you use this API to download an object of 1 MB-5 GB. For objects greater than 5 GB, please use the advanced replication API [Slice Copy File](#.E5.A4.8D.E5.88.B6.E5.AF.B9.E8.B1.A12).

#### Samples

[//]: # ".cssg-snippet-copy-object"
```js
cos.putObjectCopy({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    CopySource: 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject', /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| --------------------------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| CopySource | URL path to the source object. A historical version can be specified using the URL parameter `?versionId=&lt;versionId>` | String | Yes |
| ACL    | Defines the access control list (ACL) attribute of the object. For the enumerated values such as `default`, `private`, and `public-read`, please see the Preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). <br>**Note:** If you do not need access control for the object, set `default` for this parameter or simply leave it blank, and the object will inherit the permissions of the bucket | String | No |
| GrantRead | Grants a user read access in the format: `id="[OwnerUin]"`. You can use a comma (,) to separate multiple users. <br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantWrite        | Grants the user write permission in the format: `id="[OwnerUin]"`.<br>You can use a comma (,) to separate multiple users.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantFullControl | Grants the user full permission in the format: `id="[OwnerUin]"`. You can use a comma (,) to separate multiple users. <br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| MetadataDirective | Indicates whether to copy the metadata. Enumerated values: `Copy`, `Replaced`. Default value: `Copy`. If you specify this parameter as `Copy`, the user metadata in the corresponding header will be ignored and the copy operation will be performed; if you specify this parameter as `Replaced`, the metadata will be replaced by the information in the corresponding header. **If the destination path is the same as the source path, which means you want to modify the metadata, you must specify this parameter as `Replaced`** | String | No |
| CopySourceIfModifiedSince | If the object is modified after the specified time, the operation will be performed; otherwise, an HTTP `412` status code will be returned. **This parameter can be used together with `CopySourceIfNoneMatch`. If it is used together with other conditions, a conflict will be returned** | String | No |
| CopySourceIfUnmodifiedSince | If the object is not modified after the specified time, the operation will be performed; otherwise, an HTTP `412` status code will be returned. **This parameter can be used together with `CopySourceIfMatch`. If it is used together with other conditions, a conflict will be returned** | String | No |
| CopySourceIfMatch | If the ETag of the object is the same as the specified one, the operation will be performed; otherwise, an HTTP `412` status code will be returned. **This parameter can be used together with `CopySourceIfUnmodifiedSince`. If it is used together with other conditions, a conflict will be returned** | String | No |
| CopySourceIfNoneMatch | If the ETag of the object is different from the specified one, the operation will be performed; otherwise, `412` will be returned. **This parameter can be used together with `CopySourceIfModifiedSince`. If it is used together with other conditions, a conflict will be returned** | string | No |
| StorageClass | Sets the object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String | No |
| x-cos-meta-* | Other user-defined file headers | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this parameter is left empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| - ETag | MD5 checksum of the file, such as `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end of the ETag** | String |
| - LastModified | Describes the time the object was last modified, such as `2017-06-23T12:33:27.000Z` | String |
| - VersionId       | Returns the version ID for versioning-enabled buckets. For buckets which have never had versioning enabled, this parameter is not returned  | String  |

### Deleting a single object

#### API description

This API is used to delete an object from a COS bucket. To make this request, you need to have write permission for the bucket.

#### Samples

[//]: # ".cssg-snippet-delete-object"
```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject' /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| VersionId | Version ID of the object or delete marker to be deleted | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Returns data when the request is successful. If the request fails, this parameter is left empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `204`, `403`, and `404`. **If the deletion is successful or the file does not exist, an HTTP `204` or `200` status code will be returned; if the specified bucket is not found, an HTTP `404` status code will be returned** | Number |
| - headers | Returns headers | Object |

### Deleting multiple objects

#### API description

This API is used to delete multiple objects from a bucket in a single request, which allows a maximum number of 1,000 objects. There are two response modes for you to choose from: `Verbose` and `Quiet`. The Verbose mode returns information on the deletion of each object, whereas the Quiet mode only returns information on the objects for which errors were reported.

#### Samples

Deleting multiple files:

[//]: # ".cssg-snippet-delete-multi-object"
```js
cos.deleteMultipleObject({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Objects: [
        {Key: 'exampleobject'},
        {Key: 'exampleobject2'},
    ]
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ----------- | ------------------------------------------------------------ | ----------- | -------- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Quiet | A Boolean value which determines whether to use the `Quiet` mode. If the value is `true`, the `Quiet` mode will be used; if it is `false`, the `Verbose` mode will be used. Default value: `false` | Boolean | No |
| Objects | Lists files to be deleted | ObjectArray | Yes |
| - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| - VersionId | Version ID of the object or delete marker to be deleted | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Parameter Description                                                     | Type |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ----------- |
| err | A returned request error (network error or service error). If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `204`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `204`, `403`, and `404` | Number |
| - headers | Returns headers | Object |
| - Deleted | Lists objects deleted successfully | ObjectArray |
| - - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| - - VersionId | If the `VersionId` parameter is passed in, it will also be included in the response, indicating the version of the object or delete marker | String |
| - - DeleteMarker | If versioning is enabled and the `VersionId` parameter is not specified, the deletion will not actually delete the file; instead, it will only add a new delete marker, indicating that the visible file has been deleted. Enumerated values: `true`, `false` | String |
| - - DeleteMarkerVersionId | Returns the VersionId of the newly added delete marker if `DeleteMarker` is `true`  | String |
| - Error | Lists objects whose deletion failed | ObjectArray |
| - - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| - - Code                                                     | Deletion failure error codes                                             | String      |
| - - Message                                                  | Deletion failure error messages                                      | String      |

## Multipart Operations

### Querying multipart uploads

#### API description

This API is used to query ongoing multipart uploads. A single request operation can list up to 1,000 multipart uploads.

#### Samples

The sample below gets a list of UploadIds prefixed with `exampleobject` for which the multiple upload was incomplete:

[//]: # ".cssg-snippet-list-multi-upload"
```js
cos.multipartList({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Prefix: 'exampleobject', /*Optional*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Prefix | Limits the response to keys that begin with the specified prefix. Note that when you make a query with the specified prefix, the returned keys will still contain `Prefix` | String | No |
| Delimiter | A delimiter is a separating symbol used to group object keys. It is usually `/`. The identical paths between `Prefix` or, if no `Prefix` is specified, the beginning and the first `delimiter` are grouped and defined as a common prefix. All common prefixes will be listed | String | No |
| EncodingType | Specifies the encoding method of the return value; valid value: url | String | No |
| MaxUploads | Sets the maximum number of entries returned. Value range: 1-1000; default value: 1000 | String | No |
| KeyMarker | Used together with `upload-id-marker`. <br><li>If `upload-id-marker` is not specified: <br>&emsp;- only the multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed. <br><li>If `upload-id-marker` is specified: <br>&emsp;- the multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed; <br>&emsp;- and the multipart uploads whose `ObjectName` is equal to the `key-marker` will also be listed, provided that their `UploadID` is greater than the specified `upload-id-marker` | String | No |
| UploadIdMarker | Used together with `key-marker`. <br><li>If `key-marker` is not specified: <br>&emsp;- `upload-id-marker` will be ignored. <br><li>If `key-marker` is specified: <br>&emsp;- the multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed; <br>&emsp;- and the multipart uploads whose `ObjectName` is equal to the `key-marker` will also be listed, provided that their `UploadID` is greater than the specified `upload-id-marker` | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Type |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | Returns an HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this parameter is left empty | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Returns headers | Object |
| - Bucket | Destination bucket for the multipart upload | String |
| - Encoding-Type | Specifies the encoding type of the returned value. Valid value: url  | String |
| - KeyMarker | Marks the key after which the entry listing starts  | String |
| - UploadIdMarker | Marks the UploadId after which the entry listing starts | String |
| - NextKeyMarker | If the returned list is truncated, the `NextKeyMarker` returned will be the starting point of the subsequent list | String |
|-  NextUploadIdMarker |  If the returned list is truncated, the `UploadId` returned will be the starting point of the subsequent list | String |
| - MaxUploads                                                 | The maximum number of returned entries. Valid value range: 1 - 1000                  | String      |
| - IsTruncated   |  Indicates whether returned objects are truncated. Valid value: `true` or `false` | String|
|  - Prefix  | Limits the response to keys that begin with the specified prefix | String | 
| - Delimiter | A delimiter is a separating symbol used to group object keys. It is usually `/`. The identical paths between `Prefix` or, if no `Prefix` is specified, the beginning and the first `delimiter` are grouped and defined as a common prefix. All common prefixes will be listed | String |
| - CommonPrefixs                                              | The identical paths between `Prefix` and `Delimiter` are grouped and defined as a common prefix | ObjectArray |
| - - Prefix | Displays specific common prefixes | String |
| - Upload                                                     | A collection of multipart upload information                                  | ObjectArray |
| - - Key                                                      | Name of the object, i.e. object key                                         | String      |
| - - UploadId           | ID of the current multipart upload                                    | String      |
| - - StorageClass | Storage class of the part; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE` | String | 
| - - Initiator                        | Initiator of the current multipart upload                                    | Object      |
| - - - DisplayName | Name of the upload initiator | String |
|- - - ID | ID of the upload initiator in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String |
| - - Owner                 | Owner of the parts                                    | Object      |
| - - - DisplayName | Name of the parts’ owner | String |
| - - - ID | Parts owner ID in the format: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`.<br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String |
| - - Initiated                               | Start time of the multipart upload                                        | String      |

### Initializing a multipart upload

#### API description

This API is used to initialize a multipart upload operation. After a successful operation, an upload ID will be returned which can be used in the subsequent `Upload Part` requests.

#### Samples

[//]: # ".cssg-snippet-init-multi-upload"
```js
cos.multipartInit({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    UploadId: 'exampleUploadId',
    Body: fileObject
}, function(err, data) {
    console.log(err || data);
    if (data) {
      uploadId = data.UploadId;
    }
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------------------ | ------------------------------------------------------------ | ------ | -------- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| CacheControl | Cache policy as defined in RFC 2616, which will be stored as object metadata | String | No |
| ContentDisposition | Filename as defined in RFC 2616, which will be stored as object metadata | String | No |
| ContentEncoding | Encoding format as defined in RFC 2616, which will be stored as object metadata | String | No |
| ContentType | Content type (MIME) as defined in RFC 2616, which will be stored as object metadata | String | No |
| Expires | Cache expiration time as defined in RFC 2616, which will be stored as object metadata | String | No |
| ACL    | Defines the access control list (ACL) attribute of the object. For the enumerated values such as `default`, `private`, and `public-read`, please see the “Preset ACL” section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). <br>**Note:** If you do not need access control for the object, set `default` for this parameter or simply leave it blank, and the object will inherit the permissions of the bucket | String | No |
| GrantRead | Grants a user read access in the format: `id="[OwnerUin]"`. You can use a comma (,) to separate multiple users. <br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantFullControl | Grants a user full access in the format: `id="[OwnerUin]"`. You can use a comma (,) to separate multiple users. <br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| StorageClass | Sets the object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String | No |
| x-cos-meta-* | Headers that can be defined by users, which will be returned as object metadata; maximum size: 2 KB | String | No |
| UploadAddMetaMd5       | Sets x-cos-meta-md5 as the object’s MD5 value in the object’s metadata during upload in the format of a 32-bit lowercase string. For example:  `4d00d79b6733c9cc066584a02ed03410` | String           | No   |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty | Object |
| Bucket              | Name of the destination bucket for the multipart upload, which is formed by connecting a user-defined string and the system-generated APPID with a hyphen, such as `examplebucket-1250000000` | string |
| Key | Object key (object name), a unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| UploadId | ID that can be used in subsequent uploads | String |

### Uploading a part

#### API description

This API is used to upload a part after a multipart upload is initialized. It can upload up to 10,000 parts of 1 MB to 5 GB for a multiple upload.
<li>You can obtain an uploadId when you use the API `Initiate Multipart Upload` to initiate a multipart upload. This ID uniquely identifies the data of the part and its position in the entire file.</li>
<li>Every time you request the `Upload Part` API, you need to pass in `partNumber`, the part number, and `uploadId`. You can upload multiple parts out of order.</li>
<li>When the `uploadId` and `partNumber` of a new part are the same as those of a previously uploaded part, the old part will be overwritten by the new one. A 404 error, `NoSuchUpload`, will be returned if the `uploadId` does not exist.</li>

#### Samples

[//]: # ".cssg-snippet-upload-part"
```js
cos.multipartUpload({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    UploadId: 'exampleUploadId',
    PartNumber: '1',
    Body: fileObject
}, function(err, data) {
    console.log(err || data);
    if (data) {
      eTag = data.ETag;
    }
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |