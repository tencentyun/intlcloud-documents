## Overview

This document provides an overview of APIs and SDK sample codes related to simple operations, multipart operations, and other object operations.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ---------------------------------------- |
| [GET Bucket（List Object）](https://intl.cloud.tencent.com/document/product/436/7734) | Querying an object list | Queries some or all objects in a bucket |
| [PUT Object](https://cloud.tencent.com/document/product/436/7749) | Uploading on object using simple upload | Uploads an object to a bucket |
| [POST Object](https://cloud.tencent.com/document/product/436/14690) | Uploading an object using a form | Uploads an object using a form request |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |
| [OPTIONS Object](https://cloud.tencent.com/document/product/436/8288) | Configuring pre-flight requests for cross-origin access | Sends a pre-flight request to check whether a real cross-origin access request can be sent |
| [PUT Object - Copy](https://cloud.tencent.com/document/product/436/10881) | Setting object replication | Copies a file to the destination path |
| [DELETE Object](https://cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes a specified object from a bucket |
| [DELETE Multiple Objects](https://cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket in a single request |

**Multipart operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries in-progress multipart uploads |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload task |
| [Upload Part](https://cloud.tencent.com/document/product/436/7750) | Uploading a part | Uploads a file in multiple parts |
| [Upload Part - Copy](https://cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part |
| [List Parts](https://cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries the uploaded parts of a specified multipart upload operation |
| [Complete Multipart Upload](https://cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of the entire file |
| [Abort Multipart Upload](https://cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload operation and deletes the uploaded parts |

**Other operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------------- |
| [POST Object restore](https://cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access |
| [PUT Object acl](https://cloud.tencent.com/document/product/436/7748) | Setting object ACL | Sets the ACL of a specified object in a bucket |
| [GET Object acl](https://cloud.tencent.com/document/product/436/7744) | Querying object ACL | Queries the ACL of an object |

## Simple operations

### Querying an object list

## Feature description

This API is used to query some or all objects in a bucket.

### Use case

Sample 1. List all the files in directory `a`.

[//]: # (.cssg-snippet-get-bucket)
```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Prefix: 'a/', /*Optional*/
},function (err,data) {
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
        'Owner': {
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

[//]: # (.cssg-snippet-get-bucket-prefix)
```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Prefix: 'a/', /*Optional*/
    Delimiter: '/',            /* Optional */
},function (err,data) {
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
        'Owner': {
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
| ------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Regions and Access Domain Names] (https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| - Prefix | Matching prefix for object keys, which sets that the response only contains object keys with the specified prefix. | String | No |
| Delimiter | A delimiter is a separating symbol used to group object keys. It is usually `/`. The identical paths between `Prefix` or, if no `Prefix` is specified, the beginning and the first `delimiter` are grouped and defined as a common prefix. All common prefixes will be listed. | String | No |
| Marker | Starting object key tag. `MaxKeys` entries are listed starting from the `Marker`, the default order is UTF-8 lexicographical order | String | No |
| MaxKeys | Maximum number of entries returned at a time; the default value is 1,000 | String | No |
| encoding-type | Specifies the encoding type of the returned value. Valid value: `url`, meaning that the returned object keys are URL-encoded (percent-encoded) values. For example, "Tencent Cloud" will be encoded as `Tencent%20Cloud`. | String | No |

### Callback function description

```
},function (err,data) {
```

| Parameter Name | Description | Type |
| ----------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this is null | Object |
| - headers | Header information returned by the request | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| Name | ListBucketResult | Bucket name in the format: `<BucketName-APPID>`, such as `examplebucket-1250000000` | string |
| - Prefix | Matching prefix for object keys, returns the object key entries after this tag (not included) in UTF-8 lexicographical order | String |
| - Marker | By default, entries are listed in UTF-8 binary order starting from `Marker` | String |
| - MaxKeys | Maximum number of results returned in one response | String |
| - Delimiter | Delimiter | String |
| - IsTruncated | Indicates whether the returned request entries are truncated. Valid values: `true`, `false` | String |
| - NextMarker | If the returned entries are truncated, then NextMarker is the starting point of the next entry | String |
| - CommonPrefixes | The identical paths between `Prefix` and `Delimiter` are grouped and defined as a common prefix | ObjectArray |
| - - Prefix | A single common prefix | String |
| - Encoding-Type | Encoding type of the returned values, which is applicable to `Delimiter`, `Marker`, `Prefix`, `NextMarker`, and `Key` | String |
| - Contents | Metadata | ObjectArray |
| - - Key | Object key, i.e., object name | String |
| - - ETag | MD5 checksum of the file, such as `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end** | String |
| - - Size | Part size in bytes | String |
| - - LastModified  | Returns the time the object was last modified in ISO8601 format, such as 2019-05-24T10: 56: 40Z | String |
| - - Owner | Object owner information | Object |
| - - - ID | Complete ID of object owner, format: `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`, such as `qcs::cam::uin/100000000001:uin/100000000001`，where 100000000001 is uin | String |
| - - - DisplayName | Part owner name | String |
| x-cos-storage-class | Object storage class, such as `STANDARD_IA` and `ARCHIVE`. Default value: `STANDARD`. For enumerated values, see [Storage Class](https://intl.cloud.tencent.com/document/product/436/30925) | String |

### Uploading an object using simple upload

## Feature description

This API is used to upload an object to a bucket. To make this request, you need to have write permission for the bucket.

>
> 1. Key (file name) cannot end in `/`; otherwise, it will be recognized as a folder.
> 2. The total number of policies associated with bucket ACL, Policy, and CAM under a single root account (i.e., under the same APPID) cannot exceed 1,000. There is no upper limit on the number of object ACL rules. If you do not need access control for an object, do not make the configuration when uploading it; the object will inherit the permissions of its bucket by default.
> 3. After an object is uploaded, you can use the same key to generate a pre-signed link, which can be shared with others for download. However, please note that if your file is set to private-read, the pre-signed link will only be valid for a certain period of time. To download, please specify the method as `GET`. For API details, see below.

### Use case

Simple upload is suitable for uploading small files.

[//]: # (.cssg-snippet-put-object)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    StorageClass: 'STANDARD',
    Body: fileObject, // Upload file object
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
},function (err,data) {
    console.log(err || data);
});
```

Upload strings as file content:

[//]: # (.cssg-snippet-put-object-string)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    Body: 'hello!',
},function (err,data) {
    console.log(err || data);
});
```

Create a directory:

[//]: # (.cssg-snippet-put-object-folder)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'a/', /*Required*/
    Body: '',
},function (err,data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | ---------------- | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Regions and Access Domain Names] (https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name) is the unique identifier of an object in a bucket, see [Object Overview] (https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| Body | Content of the file part to be uploaded, which can be a string, a file object, or a blob object | String\File\Blob | Yes |
| CacheControl | Cache policy as defined in RFC 2616, which will be stored as object metadata | String | No |
| ContentDisposition | Filename as defined in RFC 2616, which will be stored as object metadata | String | No |
| ContentEncoding | Encoding format as defined in RFC 2616, which will be stored as object metadata | String | No |
| ContentLength | HTTP request length in bytes as defined in RFC 2616 | String | No |
| ContentType | Content type (MIME) as defined in RFC 2616, which will be stored as object metadata | String | No |
| Expires | Expiration time as defined in RFC 2616, which will be stored as object metadata | String | No |
| Expect | If `Expect: 100-continue` is used, the request content will be sent only after confirmation from the server is received | String | No |
| ACL   | Defines the access control list (ACL) attribute of the object. For the enumerated values such as `default`, `private`, and `public-read`, see the Preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). <br>**Note:** If you do not need access control for the object, set `default` for this parameter or simply leave it blank, and the object will inherit the permissions of the bucket | String | No |
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

### Callback function description

```
},function (err,data) {
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - ETag | Returns the MD5 checksum of the file. The value of `ETag` can be used to check whether the object was corrupted during the upload. <br>For example, `"09cba091df696af91549de27b8e7d0f6"`. **Note that double quotation marks are required at the beginning and the end** | String |
| - Location | Creates an object's access domain name for external networks | String |
| - VersionId       | The version ID will be returned for buckets that have enabled versioning. If the bucket has never enabled versioning, no value will be returned | String  |

### Uploading an object using a form

The SDK for JS does not provide a method for the `POST Object` API. If you need to use this API, see "Solution B: Upload with Form" in [Practice of Direct Transfer for Web End](https://intl.cloud.tencent.com/document/product/436/9067).

### Querying object metadata

## Feature description

This API is used to query object metadata.

### Use case

[//]: # (.cssg-snippet-head-object)
```js
cos.headObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
},function (err,data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| --------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Regions and Access Domain Names] (https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name) is the unique identifier of an object in a bucket, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| IfModifiedSince | Returns the object metadata if the object is modified after the specified time | String | No |

### Callback function description

```
},function (err,data) {
```

| Parameter Name | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200` and `304`. If no modification is made after the specified time, 304 will be returned | Number |
| - headers | Header information returned by the request | Object |
| - x-cos-object-type | Indicates whether an object can be appended to an upload operation. Enumerated values: `normal`, `appendable` | String |
| - x-cos-storage-class | Object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE` | String |
| - x-cos-meta-* | User-defined metadata | String |
| - NotModified | Whether an object is unmodified after the specified time | Boolean |
| - ETag | Returns the MD5 checksum of the file. The value of `ETag` can be used to check whether the object was corrupted during the upload. <br>For example, `"09cba091df696af91549de27b8e7d0f6"`. **Note that double quotation marks are required at the beginning and the end** | String |
| - VersionId       | The version ID will be returned for buckets that have enabled versioning. If the bucket has never enabled versioning, no value will be returned | String  |

### Downloading an object

> This API is used to read object content. If you need to launch a browser to download the file, you can get the URL through `cos.getObjectUrl` and then start a download in the browser. For more information, see [Pre-signed URL](https://intl.cloud.tencent.com/document/product/436/30598).

## Feature description

This API is used to get the content, in string format, of a specified file in a bucket.

### Use case

[//]: # (.cssg-snippet-get-object)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
},function (err,data) {
    console.log(err || data.Body);
});
```

Get file content with `Range` specified:

[//]: # (.cssg-snippet-get-object-range)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    Range: 'bytes=1-3', /*Optional*/
},function (err,data) {
    console.log(err || data.Body);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| -------------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Regions and Access Domain Names] (https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name) is the unique identifier of an object in a bucket, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| ResponseContentType | Sets the `Content-Type` parameter in the response headers | String | No |
| ResponseContentLanguage | Sets the `Content-Language` parameter in the response headers | String | No |
| ResponseExpires | Sets the `Content-Expires` parameter in the response headers | String | No |
| ResponseCacheControl | Sets the `Cache-Control` parameter in the response headers | String | No |
| ResponseContentDisposition | Sets the `Content-Disposition` parameter in the response headers | String | No |
| ResponseContentEncoding | Sets the `Content-Encoding` parameter in the response headers | String | No |
| Range | Byte range of the object as defined in RFC 2616. The range value must be in the format of `bytes=first-last`, where both `first` and `last` are offsets starting from 0. For example, `bytes=0-9` means that you want to download the first 10 bytes of data of the source object. If this parameter is not specified, the entire object will be downloaded | String | No |
| IfModifiedSince    | If the object is modified after the specified time, the object will be returned; otherwise, HTTP status code 304 (Not Modified) will be returned | String | No |
| IfUnmodifiedSince    | If the object is not modified after the specified time, the object will be returned; otherwise, HTTP status 412 (Precondition Failed) will be returned | String | No |
| IfMatch | The object will be returned only if ETag matches the specified value; otherwise, 412 (precondition failed) will be returned | String | No |
| IfNoneMatch | The object will be returned only if ETag does not match the specified value; otherwise, 304 (not modified) will be returned | String | No |
| VersionId | Specifies the version ID of the object to be downloaded | String | No |
| onProgress | Progress callback function. Attributes of the progress callback response object, `progressData`, are as follows | Function | No |
| - progressData.loaded | Size of the downloaded file part in bytes | Number | No |
| - progressData.total | Size of the entire object in bytes | Number | No |
| - progressData.speed | Object download speed; unit: bytes/s | Number | No |
| - progressData.percent | A decimal representing the object download progress. For example, 0.5 means 50% has been downloaded | Number | No |

### Callback function description

```
},function (err,data) {

```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Parameter Description | Type | 
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `304`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - CacheControl  | Cache directives as defined in RFC 2616, which will be returned only if it is contained in the object metadata or if it is specified in the request parameter | string |
| - ContentDisposition                                         | File name as defined in RFC 2616, which will be returned only if it is contained in the object metadata or if it is specified in the request parameter | String  |
| - ContentEncoding                                            | Encoding format as defined in RFC 2616, which will be returned only if it is contained in the object metadata or if it is specified in the request parameter | String  |
| - Expires                                                    | Cache expiration time as defined in RFC 2616, which will be returned only if it is contained in the object metadata or if it is specified in the request parameter | String  |
| x-cos-storage-class | Storage class of the object. Enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE` <br>**Note: If this header is not returned, it means the file storage class is `STANDARD` (standard storage)** | String |
| - x-cos-meta-*                                               | User defined metadata                                           | String  |
| - NotModified      | If the request has IfModifiedSince, then the attributes of IfModifiedSince will be returned. If the file has been modified, `false` will be returned. If not, `true` will be returned | Boolean |
| - ETag | Returns the MD5 checksum of the file. The value of `ETag` can be used to check whether the object was corrupted during the upload. <br>For example, `"09cba091df696af91549de27b8e7d0f6"`. **Note that double quotation marks are required at the beginning and the end** | String |
| - VersionId       | The version ID will be returned for buckets that have enabled versioning. If the bucket has never enabled versioning, no value will be returned | String  |
| - Body                | Returned file content. Uses the String format by default.        | String  |

### Configuring pre-flight fequests for  cross-origin access

## Feature description

This API is used to implement a pre–flight request for cross-origin object access. Before making a real cross-origin resource sharing (CORS) request, you can send an `OPTIONS` request carrying the specific source origin, HTTP method, and header information to COS for it to determine whether a real request can be sent. If there is no CORS configuration, `403 Forbidden` will be returned. **You can enable CORS for a bucket using the `PUT Bucket cors` API**.

### Use case

[//]: # (.cssg-snippet-option-object)
```js
cos.optionsObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    Origin: 'https://www.qq.com', /*Required*/
    AccessControlRequestMethod: 'PUT', /*Required*/
    AccessControlRequestHeaders: 'origin,accept,content-type' /*Optional*/
},function (err,data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Regions and Access Domain Names] (https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name) is the unique identifier of an object in a bucket, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| Origin | Source origin of the simulated cross-origin access request | String | Yes |
| AccessControlRequestMethod | HTTP method of the simulated cross-origin access request | String | Yes |
| AccessControlRequestHeaders | Headers of the simulated cross-origin access request | String | No |

### Callback function description

```
},function (err,data) {
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Parameter Description | Type | 
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this is null | Object |
| - headers | Header information returned by the request | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - AccessControlAllowOrigin | Source origins of the simulated cross-origin access request separated by commas. This header will not be returned if the origins are not allowed. Example: `*` | String |
| - AccessControlAllowMethods | HTTP methods of the simulated cross-origin access request separated by commas, such as PUT, GET, POST, DELETE, and HEAD. This header will not be returned if the request method is not allowed | String |
| - AccessControlAllowHeaders | Headers of the simulated cross-origin access request separated by commas, such as `accept`, `content-type`, `origin`, and `authorization`. This request header will not be returned if any of the simulated headers are not allowed | String |
| - AccessControlExposeHeaders | Response headers supported by CORS, such as `ETag`. The headers are separated by commas | String |
| accessControlMaxAge | long | The validity period of the results obtained by `OPTIONS` | String  |
| - OptionsForbidden | Whether the `OPTIONS` request is forbidden, which will be `true` if the returned HTTP status code is `403` | Boolean |

### Setting object replication

## Feature description

This API is used to create a copy of an existing COS object, that is, an object is copied from the source path (object key) to the destination path (object key). During replication, object metadata and access control lists (ACLs) can be modified.
Users can use this API to create a copy, modify object meta attributes (the source object and destination file have the same attributes), move or rename the object (copy first, and then call the delete API separately).

> We recommend an object size between 1MB-5GB. For objects greater than 5GB, please use the advanced APIs to copy the object [Slice Copy File] (#. E5.A4.8D.E5.88.B6.E5.AF.B9.E8.B1.A12) .

### Use case

[//]: # (.cssg-snippet-copy-object)
```js
cos.putObjectCopy({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    CopySource: 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject', /*Required*/
},function (err,data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Regions and Access Domain Names] (https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key                 | Object key (object name) is the unique identifier of an object in a bucket, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) for details | String      | Yes  |
| CopySource | URL path to the source object. A past version can be specified with the URL parameter ?versionId=&lt;versionId> | String | Yes |
| ACL    | Defines the access control list (ACL) attribute of the object. For the enumerated values such as `default`, `private`, and `public-read`, see the Preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). <br>**Note:** If you do not need access control for the object, set `default` for this parameter or simply leave it blank, and the object will inherit the permissions of the bucket | String | No |
| GrantRead | Grants a user read access in the format: `id="[OwnerUin]"`. You can use a comma (,) to separate multiple users. <br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantWrite        | Grants a user write access in the format: id="[OwnerUin]".<br>You can use a comma (,) to separate multiple users.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantFullControl | Grants a user full access in the format: `id="[OwnerUin]"`. You can use a comma (,) to separate multiple users. <br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| MetadataDirective | Indicates whether to copy metadata. Enumerated values: `Copy`, `Replaced`. Default value: `Copy`. If its value is `Copy`, the user metadata in the corresponding header will be ignored and the copy will be performed; if its value is `Replaced`, the metadata will be replaced by the information in the corresponding header. **If the destination path is the same as the source path, which means you want to modify the metadata, you must specify this parameter as `Replaced`** | String | No |
| CopySourceIfModifiedSince | If the object is modified after the specified time, the operation will be performed; otherwise, `412` will be returned. **This parameter can be used together with `CopySourceIfNoneMatch`. If it is used together with other conditions, a conflict will be returned** | String | No |
| CopySourceIfUnmodifiedSince | If the object is not modified after the specified time, the operation will be performed; otherwise, `412` will be returned. **This parameter can be used together with `CopySourceIfMatch`. If it is used together with other conditions, a conflict will be returned** | String | No |
| CopySourceIfMatch | If the `Etag` of the object is the same as the specified one, the operation will be performed; otherwise, `412` will be returned. **This parameter can be used together with `CopySourceIfUnmodifiedSince`. If it is used together with other conditions, a conflict will be returned** | String | No |
| CopySourceIfNoneMatch | If the `Etag` of the object is different from the specified one, the operation will be performed; otherwise, `412` will be returned. **This parameter can be used together with `CopySourceIfModifiedSince`. If it is used together with other conditions, a conflict will be returned** | string | No |
| StorageClass | Sets the object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String | No |
| x-cos-meta-* | Other user-defined file headers | String | No |

### Callback function description

```
},function (err,data) {
```

| Parameter Name | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - ETag | MD5 checksum of the file, such as `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end** | String |
| - LastModified | Returns the time the object was last modified, such as `2017-06-23T12:33:27.000Z` | String |
| - VersionId       | The version ID will be returned for buckets that have enabled versioning. If the bucket has never enabled versioning, no value will be returned | String  |

### Deleting a single object

## Feature description

This API is used to delete an object from a COS bucket. To make this request, you need to have write permission for the bucket.

### Use case

[//]: # (.cssg-snippet-delete-object)
```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject' /*Required*/
},function (err,data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Regions and Access Domain Names] (https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name) is the unique identifier of an object in a bucket, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| - VersionId | Version ID of the object or delete marker to be deleted | String | No |

### Callback function description

```
},function (err,data) {
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404`. **If the deletion is successful or the file does not exist, 204 or 200 will be returned; if the specified bucket is not found, 404 will be returned** | Number |
| - headers | Header information returned by the request | Object |

### Deleting multiple objects

## Feature description

This API is used to delete multiple objects from a bucket in a single request. You can delete up to 1,000 objects in a single request. For the response, there are two modes for you to choose from: `Verbose` and `Quiet`. Verbose mode returns the information on the deletion of each object, whereas Quiet mode only returns the information on objects for which errors were reported.

### Use case

Deleting multiple files:

[//]: # (.cssg-snippet-delete-multi-object)
```js
cos.deleteMultipleObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Objects: [
        {Key: 'exampleobject'},
        {Key: 'exampleobject2'},
    ]
},function (err,data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ----------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Regions and Access Domain Names] (https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Quiet | A boolean value which determines whether to use Quiet mode. If the value is `true`, Quiet mode will be used; if it is `false`, Verbose mode will be used. Default value: `false` | Boolean | No |
| Objects | List of files to be deleted | ObjectArray | Yes |
| Key | Object key (object name) is the unique identifier of an object in a bucket, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| - VersionId | Version ID of the object or the delete marker to be deleted | String | No |

### Callback function description

```
},function (err,data) {
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Parameter Description                                                     | Type |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `204`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `204`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - Deleted | List of object information indicating successful deletion | ObjectArray |
| Key | Object key (object name) is the unique identifier of an object in a bucket, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) for details | String |
| - - VersionId | If the `VersionId` parameter is passed in, it will also be included in the response, indicating the version of the object or delete marker | String |
| - - DeleteMarker | If versioning is enabled and the `VersionId` parameter is not specified, the deletion will not actually erase the content of the file; instead, it will only add a new delete marker, indicating that the visible file has been deleted. Enumerated values: `true`, `false` | String |
| - - DeleteMarkerVersionId | If the value of the returned `DeleteMarker` is `true`, this parameter will be returned, representing the `VersionId` of the newly added delete marker | String |
| - Error | List of object information indicating deletion failure | ObjectArray |
| Key | Object key (object name) is the unique identifier of an object in a bucket, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) for details | String |
| - - Code                                                     | Deletion failure error codes                                             | String      |
| - - Message                                                  | Deletion failure error messages                                      | String      |

## Multipart operations

### Querying a multipart upload

## Feature description

This API is used to query ongoing multipart uploads. A single request operation can list up to 1,000 multipart uploads.

### Use case

Get the list of unfinshed `UploadIds` prefixed with `exampleobject`, for example:

[//]: # (.cssg-snippet-list-multi-upload)
```js
cos.multipartList({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Prefix: 'exampleobject', /*Optional*/
},function (err,data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Regions and Access Domain Names] (https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Prefix | Matching prefix for object keys, which sets that the response only contains object keys with the specified prefix. Note that when you make a query with the specified prefix, the returned keys will still contain `Prefix` | String | No |
| Delimiter | A delimiter is a separating symbol used to group object keys. It is usually `/`. The identical paths between `Prefix` or, if no `Prefix` is specified, the beginning and the first `delimiter` are grouped and defined as a common prefix. All common prefixes will be listed. | String | No |
| EncodingType | Specifies the encoding method of the return value; value range: url | String | No |
| MaxUploads | Sets the maximum number of entries returned; value range: 1-1,000. Default value: 1,000 | String | No |
| KeyMarker | Used together with `upload-id-marker`. <br> <li>If `upload-id-marker` is not specified: <br>&emsp;- only the multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed. <br><li>If `upload-id-marker` is specified: <br>&emsp;- the multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed; <br>&emsp;- and the multipart uploads whose `ObjectName` is equal to the `key-marker` will also be listed, provided that their `UploadID` is greater than the specified `upload-id-marker` | String | No |
| UploadIdMarker | Used together with `key-marker`. <br><li>If `key-marker` is not specified: <br>&emsp;- `upload-id-marker` will be ignored. <br><li>If `key-marker` is specified: <br>&emsp;- the multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed; <br>&emsp;- and the multipart uploads whose `ObjectName` is equal to the `key-marker` will also be listed, provided that their `UploadID` is greater than the specified `upload-id-marker` | String | No |

### Callback function description

```
},function (err,data) {
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Parameter Description | Type |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - Bucket | Destination bucket for the multipart upload | String |
| EncodingType | Specifies the encoding type of the returned value. Valid value: url  | String |
| - KeyMarker | The key value where the entry list starts | String |
| - UploadIdMarker | The `UploadId` value where the entry list starts | String |
| - NextKeyMarker | If the returned list is truncated, the `NextKeyMarker` returned will be the starting point of the subsequent list | String |
|-  NextUploadIdMarker |  If the returned list is truncated, the `UploadId` returned will be the starting point of the subsequent list | String |
| - MaxUploads                                                 | The maximum number of returned entries. Valid value range: 1 - 1000                  | String      |
| IsTruncated   |  Indicates whether the returned object is truncated. Valid value: `true` or `false` | String|
| prefix | Matching prefix for object keys, which sets that the response only contains object keys with the specified prefix | String | 
| Delimiter | A delimiter is a separating symbol used to group object keys. It is usually `/`. The identical paths between `Prefix` or, if no `Prefix` is specified, the beginning and the first `delimiter` are grouped and defined as a common prefix. All common prefixes will be listed. | String | No |
| - CommonPrefixs                                              | The identical paths between `Prefix` and `Delimiter` are grouped and defined as a common prefix | ObjectArray |
| - - Prefix | Displays specific common prefixes | String |
| - Upload                                                     | Multipart upload information collection                                    | ObjectArray |
| - - Key                                                      | Name of the object, i.e. Object Key                                         | String      |
| - - UploadId           | ID of the current multipart upload                                    | String      |
| StorageClass | Object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE` | String | No |
| - - Initiator                        | Initiator of the current multipart upload                                    | Object      |
| - - DisplayName | Name of the upload initiator | String |
| - - - ID | ID of the upload initiator in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`. <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String |
| - - Owner                 | Owner of the parts                                    | Object      |
| - - DisplayName | Parts owner name | String |
| - - - ID | Parts owner ID in the format: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`.<br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String |
| - - Initiated                               | Multipart upload start time                                           | String      |

### Initializing a multipart upload

## Feature description

This API is used to initialize a multipart upload operation. After a successful operation, an upload ID will be returned which can be used in the subsequent `Upload Part` requests.

### Use case

[//]: # (.cssg-snippet-init-multi-upload)
```js
cos.multipartInit({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    UploadId: 'exampleUploadId',
    Body: fileObject
},function (err,data) {
    console.log(err || data);
    if (data) {
      uploadId = data.UploadId;
    }
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Regions and Access Domain Names] (https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name) is the unique identifier of an object in a bucket, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| CacheControl | Cache policy as defined in RFC 2616, which will be stored as object metadata | String | No |
| Content-Disposition | Filename as defined in RFC 2616, which will be stored as object metadata | String | No |
| Content-Encoding | Encoding format as defined in RFC 2616, which will be stored as object metadata | String | No |
| ContentType | Content type (MIME) as defined in RFC 2616, which will be stored as object metadata | String | No |
| Expires | Cache expiration time as defined in RFC 2616, which will be stored as object metadata | String | No |
| ACL    | Defines the access control list (ACL) attribute of the object. For the enumerated values such as `default`, `private`, and `public-read`, see the Preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). <br>**Note:** If you do not need access control for the object, set `default` for this parameter or simply leave it blank, and the object will inherit the permissions of the bucket | String | No |
| GrantRead | Grants a user read access in the format: `id="[OwnerUin]"`. You can use a comma (,) to separate multiple users. <br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantFullControl | Grants a user full access in the format: `id="[OwnerUin]"`. You can use a comma (,) to separate multiple users. <br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| StorageClass | Sets the object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String | No |
| x-cos-meta-* | Headers that can be defined by users, which will be returned as object metadata; maximum size: 2 KB | String | No |
| UploadAddMetaMd5       | Sets x-cos-meta-md5 as the object’s MD5 value in the object’s metadata during upload in the format of a 32-bit lowercase string. For example:  `4d00d79b6733c9cc066584a02ed03410` | String           | No   |

### Callback function description

```
},function (err,data) {
```

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| data | Object returned when the request is successful. If the request fails, this is null | Object |
| Bucket              | Name of the destination bucket for the multipart upload, which is formed by connecting a user-defined string and the system-generated APPID with a hyphen, such as `examplebucket-1250000000` | string |
| Key | Object key (object name) is the unique identifier of an object in a bucket, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) for details | String |
| UploadId | ID that can be used in subsequent uploads | String |

### Uploading parts

## Feature description

This API is used to upload parts after a multipart upload is initialized. It can upload up to 10,000 parts of 1 MB to 5 GB each in size.
<li>You can obtain an uploadId when you use the API `Initiate Multipart Upload` to initiate a multipart upload. This ID uniquely identifies the data of the part and its position in the entire file.</li>
<li>Every time you request the `Upload Part` API, you need to pass in `partNumber`, the part number, and `uploadId`. You can upload multiple parts out of order.</li>
<li>When the `uploadId` and `partNumber` of a new part are the same as those of a previously uploaded part, the old part will be overwritten by the new one. A 404 error, `NoSuchUpload`, will be returned if the `uploadId` does not exist.</li>

### Use case

[//]: # (.cssg-snippet-upload-part)
```js
cos.multipartUpload({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    UploadId: 'exampleUploadId',
    PartNumber: '1',
    Body: fileObject
},function (err,data) {
    console.log(err || data);
    if (data) {
      eTag = data.ETag;
    }
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------------- | ------------------------------------------------------------ | ---------------- | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Regions and Access Domain Names] (https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name) is the unique identifier of an object in a bucket, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| ContentLength | HTTP request length in bytes as defined in RFC 2616 | String | Yes |
| PartNumber | Part number | String | Yes |
| UploadId | The number of this multipart upload task | String | Yes |
| Body | Content of the file part to be uploaded, which can be a string, a File object, or a Blob object | String\File\Blob | Yes |
| Expect | If `Expect: 100-continue` is used, the request content will be sent only after confirmation from the server is received | String | No |
| ContentMD5 | Base64-encoded 128-bit content MD5 checksum as defined in RFC 1864. This header is used to check whether there have been changes to the file content | String | No |

### Callback function description

```
},function (err,data) {
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |

### Copying parts

## Feature description

This API is used to copy the parts of an object from the source path to the destination path.

> To upload an object in parts, you must first initialize the multipart upload. A unique descriptor (upload ID) will be returned in the response of the multipart upload initialization, which needs to be carried in the multipart upload request.

### Use case

[//]: # (.cssg-snippet-upload-part-copy)
```js
cos.uploadPartCopy({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    CopySource: 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject', /*Required*/
    UploadId: 'exampleUploadId', /*Required*/
    PartNumber: '1', /*Required*/
},function (err,data) {
    console.log(err || data);
    if (data) {
      eTag = data.ETag;
    }
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Regions and Access Domain Names] (https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name) is the unique identifier of an object in a bucket, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| CopySource | URL path to the source object. A past version can be specified with the URL parameter ?versionId=\<versionId> | String | Yes |
| PartNumber | Part number | String | Yes |
| uploadId | To upload an object in parts, you must first initialize the multipart upload. The response of the multipart upload initialization will return a unique descriptor, an upload ID, which needs to be carried in the multipart upload request | String | Yes |
| CopySourceRange | Byte range of the source object. The range value must be in the format of `bytes=first-last`, where both `first` and `last` are offsets starting from 0. For example, `bytes=0-9` means that you want to copy the first 10 bytes of data of the source object. If this parameter is not specified, the entire object will be copied | String | No |
| CopySourceIfMatch | If the `Etag` of the object is the same as the specified one, the operation will be performed; otherwise, `412` will be returned. This parameter can be used together with `x-cos-copy-source-If-Unmodified-Since`. If it is used together with other conditions, a conflict will be returned | String | No |
| CopySourceIfNoneMatch | If the `Etag` of the object is different from the specified one, the operation will be performed; otherwise, `412` will be returned. This parameter can be used together with `x-cos-copy-source-If-Modified-Since`. If it is used together with other conditions, a conflict will be returned | string | No |
| CopySourceIfUnmodifiedSince | If the object is not modified after the specified time, the operation will be performed; otherwise, `412` will be returned. This parameter can be used together with `x-cos-copy-source-If-Match`. If it is used together with other conditions, a conflict will be returned | String | No |
| CopySourceIfModifiedSince | If the object is modified after the specified time, the operation will be performed; otherwise, `412` will be returned. This parameter can be used together with `x-cos-copy-source-If-None-Match`. If it is used together with other conditions, a conflict will be returned | String | No |

### Callback function description

```
},function (err,data) {
```

| Parameter Name | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - ETag | MD5 checksum of the file, such as `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end** | String |
| - LastModified | Returns the time the object was last modified in GMT format | String |

### Querying uploaded parts

## Feature description

This API is used to query the uploaded parts of a specified multipart upload operation, i.e., listing all successfully uploaded parts of a multipart upload corresponding to a particular `uploadId`.

### Use case

[//]: # (.cssg-snippet-list-parts)
```js
cos.multipartListPart({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    UploadId: 'exampleUploadId', /*Required*/
},function (err,data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ---------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Regions and Access Domain Names] (https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name) is the unique identifier of an object in a bucket, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| UploadId | ID of the multipart upload. When the `Initiate Multipart Upload` API is used to initialize a multipart upload operation, an `uploadId` will be returned. This ID uniquely identifies the data of the part and its position in the entire file | String | Yes |
| EncodingType | Specifies the encoding type of the returned value | String | No |
| MaxParts | Maximum number of entries returned at a time. Default value: 1,000 | String | No |
| PartNumberMarker | By default, entries are listed in UTF-8 binary order starting from the marker | String | No |

### Callback Function Description

```
},function (err,data) {
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Paramater Description | Type |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - Bucket | Destination bucket for the multipart upload | String |
| EncodingType | Specifies the encoding type of the returned value | String |
| Key | Object key (object name) is the unique identifier of an object in a bucket, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) for details | String |
| - - UploadId           | ID of the current multipart upload                                    | String      |
| - - Initiator                        | Initiator of the current multipart upload                                    | Object      |
| - - DisplayName | Name of the upload initiator | String |
| - - - ID | ID of the upload initiator in the format: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`. <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String |
| - - Owner                 | Owner of the parts                                    | Object      |
| - - DisplayName                                              | Bucket owner username | String      |
| - - ID                      | Bucket owner ID, generally the user’s UIN                            | String      |
| StorageClass        | Indicates the storage class of the parts; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE` | string    |
| PartNumberMarker      | By default, entries are listed in UTF-8 binary order starting from `marker`  | string    |
| NextPartNumberMarker  | If the returned list is truncated, the `NextMarker` returned will be the starting point of the subsequent list   | string    |
| - MaxUploads                                                 | The maximum number of entries returned in a single request                 | String      |
| IsTruncated   |  Indicates whether the returned object is truncated. Valid value: `true` or `false` | String|
| - Part                                  | Parts information list                                                 | ObjectArray |
| - - PartNumber                                               | Part number                                                    | String      |
| - - LastModified                 | Last modified time of the part                                           | String      |
| - - ETag                                 | MD5 algorithm checksum of the part                                          | String      |
| - - Size          | Part size in bytes                                            | String      |

### Completing a multipart upload

## Feature description

This API is used to complete a multipart upload operation. After all parts are uploaded via the `Upload Part` API, you need to call this API to complete the multipart upload. When using this API, you need to specify the `PartNumber` and `ETag` of each part in the request body for the part information to be verified.
As the parts need to be merged after they are uploaded, and the merge takes several minutes, when the merge starts, COS will immediately return status code 200 and periodically return space information during the merge process to keep the connection active until the merge is completed. After that, COS will return the content of the merged parts in the body.

- If any uploaded part is less than 1 MB in size, `400 EntityTooSmall` will be returned when this API is called.
- If the numbers of the uploaded parts are not continuous, `400 InvalidPart` will be returned when this API is called.
- If the part information entries in the request body are not sorted by number in ascending order, `400 InvalidPartOrder` will be returned when this API is called.
- If the `uploadId` does not exist, `404 NoSuchUpload` will be returned when this API is called.

>We recommend you either complete or abort a multipart upload as early as possible, as the uploaded parts of an incomplete multipart upload will take up storage capacity and incur storage fees.

### Use case

[//]: # (.cssg-snippet-complete-multi-upload)
```js
cos.multipartComplete({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    UploadId: 'exampleUploadId', /*Required*/
    Parts: [
        {PartNumber: '1', ETag: 'exampleETag'},
    ]
},function (err,data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ----------- | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Regions and Access Domain Names] (https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name) is the unique identifier of an object in a bucket, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| UploadId | Upload task number | String | Yes |
| Parts | List of information on the parts of a particular multipart upload | ObjectArray | Yes |
| - PartNumber | Part number | String | Yes |
| - ETag | MD5 checksum of each part. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end** | String | Yes |

### Callback function description

```
},function (err,data) {
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - Location | Creates an object's access domain name for external networks | String |
| - Bucket | Destination bucket for the multipart upload | String |
| Key | Object key (object name) is the unique identifier of an object in a bucket, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) for details | String |
| - ETag | Unique ID of the merged file in the format: `"uuid-<part quantity>"`. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`. **Note that double quotation marks are required at the beginning and the end** | String |

### Aborting a multipart upload

## Feature description

This API is used to abort a multipart upload operation and delete the uploaded parts. If you call this API and there is an `Upload Part` request that is using the multipart upload, the request will fail. If the `uploadId` does not exist, `404 NoSuchUpload` will be returned.

>We recommend you either complete or abort a multipart upload as early as possible, as the uploaded parts of an incomplete multipart upload will take up storage capacity and incur storage fees.

### Use case

[//]: # (.cssg-snippet-abort-multi-upload)
```js
cos.multipartAbort({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    UploadId: 'exampleUploadId' /*Required*/
},function (err,data) {
    console.log(err || data);
});

```

#### Parameter description

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Regions and Access Domain Names] (https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name) is the unique identifier of an object in a bucket, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| UploadId | ID of the multipart upload. When the `Initiate Multipart Upload` API is used to initialize a multipart upload operation, an `uploadId` will be returned. This ID uniquely identifies the data of the part and its position in the entire file | Yes |

### Callback function description

```
},function (err,data) {
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |

**Other operations**

### Restoring an archived object

## Feature description

This API is used to restore an object archived by COS. The restored readable object is temporary. You can configure it to stay readable and set the time for it to be deleted. You can use the `Days` parameter to specify when the temporary object should expire. If the object expires and you have not initiated any operation to copy the object or extend its validity period before the expiration date, the temporary object will be automatically deleted. A temporary object is only a copy of the source archived object and the source object will continue to exist throughout this period.

### Use case

[//]: # (.cssg-snippet-restore-object)
```js
cos.restoreObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject',
    RestoreRequest: {
        Days: 1,
        CASJobParameters: {
            Tier: 'Expedited'
        }
    },
},function (err,data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Regions and Access Domain Names] (https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name) is the unique identifier of an object in a bucket, see [Object Overview] (https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| RestoreRequest | Container for data restoration | Object | Yes |
| - Days | Sets the expiration time of a temporary copy | Number | Yes |
| - CASJobParameters | Container of the Cloud Archive Storage job parameters | Object | Yes |
| - - Tier | This parameter can be specified as one of three data restoration modes supported by CAS: `Standard`, which completes a restoration job in 3-5 hours; `Expedited`, which completes a restoration job in 15 minutes; and `Bulk`, which completes batch restoration jobs in 5-12 hours. | String | Yes |

### Callback function description

```
},function (err,data) {
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |

### Setting object ACL

## Feature description

This API is used to set the access control list (ACL) of an object in a specified bucket.

> The total number of policies associated with bucket ACL, Policy, and CAM under a single root account (i.e., under the same APPID) cannot exceed 1,000. There is no upper limit on the number of object ACL rules. If you do not need access control for an object, do not make any configuration, and the object will inherit the permissions of its bucket.

### Use case

[//]: # (.cssg-snippet-put-object-acl)
```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    ACL: 'public-read', /*Optional*/
},function (err,data) {
    console.log(err || data);
});
```

Grant a user all permissions to an object:

[//]: # (.cssg-snippet-put-object-acl-user)
```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    GrantFullControl: 'id="100000000001"' // 100000000001 is the UIN of the root account
},function (err,data) {
    console.log(err || data);
});
```

Grant an object write permissions via AccessControlPolicy:

[//]: # (.cssg-snippet-put-object-acl-acp)
```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    AccessControlPolicy={
        "Owner": { // `Owner` is required in `AccessControlPolicy`
            "ID": 'qcs::cam::uin/100000000001:uin/100000000001' // 100000000001 is the QQ account number of the user owning the bucket
        },
        "Grants": [{
            'Grantee': {
                "ID": "qcs::cam::uin/100000000011:uin/100000000011", // 100000000011 is the QQ account number
            },
            "Permission": "WRITE"
        }]
    }
},function (err,data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Regions and Access Domain Names] (https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key                 | Object key (object name) is the unique identifier of an object in a bucket, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) for details | String      | Yes  |
| ACL    | Defines the access control list (ACL) attribute of the object. For the enumerated values such as `default`, `private`, and `public-read`, see the Preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). <br>**Note:** If you do not need access control for the object, set `default` for this parameter or simply leave it blank, and the object will inherit the permissions of the bucket | String | No |
| GrantRead | Grants a user read access in the format: `id="[OwnerUin]"`. You can use a comma (,) to separate multiple users. <br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantFullControl | Grants a user full access in the format: `id="[OwnerUin]"`. You can use a comma (,) to separate multiple users. <br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| AccessControlPolicy | Sets an object's access control list (ACL) attributes information | Object | No |
| - Owner | Object owner information | Object | No |
| - - - ID | Object owner ID in the format: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String | No |
| - - - DisplayName | Object owner name | String |
| - Grants | List of information on the authorized user and granted permissions | ObjectArray | No |
| - - Permission | Specifies the permission granted to the authorized user. Enumerated values: READ, WRITE, READ_ACP, WRITE_ACP, FULL_CONTROL | String |
| - - Grantee         | Authorized user’s information     | Object      | No   |
| - - - DisplayName | Grantee Name | String | No |
| - - - ID | ID of the authorized user in the format: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String | No |

### Callback function description

```
},function (err,data) {
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `204`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |

### Querying object ACL

## Feature description

The API is used to query the ACL of an object. Only the owner of the bucket has the permission to use this API.

### Use case

[//]: # (.cssg-snippet-get-object-acl)
```js
cos.getObjectAcl({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
},function (err,data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Regions and Access Domain Names] (https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name) is the unique identifier of an object in a bucket, see [Object Overview] (https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |

### Callback function description

```
},function (err,data) {
```

| Parameter Name | Description | Type |
| ----------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - ACL  | Defines the access control list (ACL) attribute of the object. For the enumerated values such as `default`, `private`, and `public-read`, see the Preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). <br>**Note:** If you do not need access control for the object, set `default` for this parameter or simply leave it blank, and the object will inherit the permissions of the bucket | String | No |
| - Owner | Identifies owner of the resource | Object |
| - - - ID | Object owner ID in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String |
| - - DisplayName | Object owner name | String |
| - Grants | List of information on the authorized user and granted permissions | ObjectArray |
| - - Permission | Specifies the permission granted to the authorized user. Enumerated values: `READ`, `WRITE`, `READ_ACP`, `WRITE_ACP`, `FULL_CONTROL` | String | No |
| - - Grantee | Authorized user’s information | Object |
| - - - DisplayName | User Name | String |
| - - - ID | User ID in the format: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String |

## Advanced APIs (recommended)

The following methods encapsulate the native methods mentioned above. They can implement the complete process of multipart upload/copy and support concurrent multipart upload/copy, checkpoint restart as well as cancelling, pausing, and restarting upload tasks.

### Uploading an object in parts

## Feature description

This API is used to upload large files in parts.

### Use case

[//]: # (.cssg-snippet-transfer-upload-object)
```js
cos.sliceUploadFile({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    Body: fileObject,               /*Required*/
    TaskReady: function(taskId) { /*Optional*/
        console.log(taskId);
    },
    onHashProgress: function (progressData) { /* Optional */
        console.log(JSON.stringify(progressData));
    },
    onProgress: function (progressData) { /* Optional */
        console.log(JSON.stringify(progressData));
    }
},function (err,data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Parameter Description | Type |
| ------------------------------------------------------------ | ------------------------------------------------------------ | --------- | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Regions and Access Domain Names] (https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name) is the unique identifier of an object in a bucket, see [Object Overview] (https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| Body | Content of the file part to be uploaded, which can be a File object, or a Blob object | File\Blob | Yes |
| SliceSize                                                    | Part size                                                    | String    | No   |
| AsyncLimit | Concurrent number of parts being uploaded | String | No |
| StorageClass | Object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE` | String | No |
| UploadAddMetaMd5       | Sets x-cos-meta-md5 as the object’s MD5 value in the object’s metadata during upload in the format of a 32-bit lowercase string. For example:  `4d00d79b6733c9cc066584a02ed03410` | String           | No   |
| TaskReady | Callback function when an upload task is created. The callback returns a `taskId`, which uniquely identifies the task and can be used to cancel (cancelTask), pause (pauseTask), or restart (restartTask) the task | Function | No |
| - taskId                                                     | Upload task number                                              | String    | No  |
| onHashProgress | Progress callback function for file MD5 value calculation. The callback parameter is the progress object `progressData` | Function | No |
| - progressData.loaded | Size of the verified file part in bytes | Number | No |
| - progressData.total                                         | Total file size in bytes                      | Number    | No   |
| - progressData.speed                                         | File verification speed in bytes/s                 | Number    | No   |
| - progressData.percent | A decimal representing the file verification progress. For example, 0.5 means 50% has been verified | Number | No |
| onProgress | File upload progress callback function. The callback parameter is the object in progress `progressData` | Function | No |
| - progressData.loaded | Size of the uploaded file part in bytes | Number | No |
| - progressData.total                                         | Total file size in bytes                      | Number    | No   |
| - progressData.speed                                         | File upload speed in bytes/s                 | Number    | No   |
| - progressData.percent | A decimal representing the file upload progress; for example, 0.5 means 50% has been uploaded | Number | No |

### Callback function description

```
},function (err,data) {
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - Location | Creates an object's access domain name for external networks | String |
| - Bucket | Destination bucket for the multipart upload | String |
| Key | Object key (object name) is the unique identifier of an object in a bucket, see [Object Overview] (https://intl.cloud.tencent.com/document/product/436/13324) for details | String |
| - ETag | Unique ID of the merged file in the format: `"uuid-<part quantity>"`. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`. **Note that double quotation marks are required at the beginning and the end** | String |
| - VersionId | The version ID will be returned for buckets that have enabled versioning. If the bucket has never enabled versioning, no value will be returned | String |

### Replicating objects

## Feature description

This API is used to copy a file from the source path to the destination path through multipart copy. The object metadata and ACL can be modified during the copy process. You can use this API to move, rename, and copy a file or modify its attributes.

#### Method prototype

Call Slice Copy File:

[//]: # (.cssg-snippet-transfer-copy-object)
```js
cos.sliceCopyFile({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    CopySource: 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject', /*Required*/
    onProgress:function (progressData) { /*Optional*/
        console.log(JSON.stringify(progressData));
    }
},function (err,data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Regions and Access Domain Names] (https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name) is the unique identifier of an object in a bucket, see [Object Overview] (https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| CopySource | URL path to the source object. A past version can be specified with the URL parameter ?versionId=&lt;versionId> | String | Yes |
| ChunkSize | Size of the parts in the multipart copy; unit: byte. Default value: 1,048,576 (1 MB) | Number | No |
| SliceSize | Specifies the minimum file size in bytes for which multipart copy will be used; the default value is 5G. If the file size is equal to or less than this value, the file will be uploaded using `putObjectCopy`, otherwise it will be uploaded using `sliceCopyFile` | Number | No | | Number | No |
| onProgress | File upload progress callback function. The callback parameter is the object in progress `progressData` | Function | No |
| - progressData.loaded | Size of the uploaded file part in bytes | Number | No |
| - progressData.total                                         | Total file size in bytes                      | Number    | No   |
| - progressData.speed                                         | File upload speed in bytes/s                 | Number    | No   |
| - progressData.percent | A decimal representing the file upload progress; for example, 0.5 means 50% has been uploaded | Number | No |

### Callback function description

```
},function (err,data) {
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - Location | Creates an object's access domain name for external networks | String |
| - Bucket | Destination bucket for the multipart upload | String |
| Key | Object key (object name) is the unique identifier of an object in a bucket, see [Object Overview] (https://intl.cloud.tencent.com/document/product/436/13324) for details | String |
| - ETag | MD5 checksum of the merged file. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end** | String |
| - VersionId  | The version ID will be returned for buckets that have enabled versioning. If the bucket has never enabled versioning, no value will be returned | String |

**Batch upload**

## Feature description

Method 1:
You can call `putObject` and `sliceUploadFile` multiple times to implement batch uploads. You can instantiate the `FileParallelLimit` parameter to limit how many files can be uploaded at the same time, which is 3 by default.

Method 2:
You can call `cos.uploadFiles` to implement batch uploads. The `SliceSize` method parameter can be used to manage the files. Below are instructions on using the `uploadFiles` method.

#### Method prototype

Call the `uploadFiles` operation:

[//]: # (.cssg-snippet-batch-upload-objects)
```js
cos.uploadFiles({
    files: [{
        Bucket: 'examplebucket-1250000000', // Format：BucketName-APPID
        Region: 'COS_REGION',     /* Bucket region. Required */
        Key: 'exampleobject',
        Body: fileObject1,
    }, {
        Bucket: 'examplebucket-1250000000', // Format：BucketName-APPID
        Region: 'COS_REGION',     /* Bucket region. Required */
        Key: 'exampleobject2',
        Body: fileObject2,
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
},function (err,data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | --------- | ---- |
| files | File list, where each item is a parameter object to be passed to `putObject` and `sliceUploadFile` | Object | Yes |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Regions and Access Domain Names] (https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name) is the unique identifier of an object in a bucket, see [Object Overview] (https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| Body | Content of the file part to be uploaded, which can be a File object, or a Blob object | File\Blob | Yes |
| SliceSize | Specifies the minimum file size in bytes for which multipart upload will be used. If the file size is equal to or less than this value, the file will be uploaded using `putObject`; otherwise, it will be uploaded using `sliceUploadFile` | Number | Yes |
| onProgress | Upload progress calculated by averaging out the progress of all tasks | String | Yes |
| - progressData.loaded | Size of the uploaded file part in bytes | Number | No |
| - progressData.total                                         | Total file size in bytes                      | Number    | No   |
| - progressData.speed                                         | File upload speed in bytes/s                 | Number    | No   |
| - progressData.percent | A decimal representing the file upload progress; for example, 0.5 means 50% has been uploaded | Number | No |
| onFileFinish | The completion or error callback for each file | String | Yes |
| - err | Upload error message | Object | No |
| - data | File upload completion information | Object | No |
| - options | Parameter information on the files that have been uploaded | Object | No |

### Callback function description

```
},function (err,data) {
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this is null | Object |
| - files | error or data for each file | ObjectArray |
| - - err | Upload error message | Object |
| - - data | File upload completion information | Object |
| - - options | Parameter information on the files that have been uploaded | Object |

### Upload queue

The SDK for JavaScript records all the upload tasks initiated with `putObject` and `sliceUploadFile` in an upload queue. You can use the queue in the following ways:

1. Use `cos.getTaskList` to get the task list.
2. Use `cos.pauseTask`, `cos.restartTask`, and `cos.cancelTask` to perform operations on upload tasks.
3. Use `cos.on('list-update', callback);` to monitor changes in the list and the upload progress.

For a complete sample of how to use the upload queue, see [Queue Demo](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/demo/queue).

#### Canceling an upload task

This API is used to cancel an upload task by `taskId`.

**Use case**

```js
var taskId = 'xxxxx';                   /* Required */
cos.cancelTask(taskId);
```

**Parameter description**

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | ID of an upload task. When `sliceUploadFile` is called, `TaskReady` in the callback will return the `taskId` of the upload task | String | Yes |

#### Pausing an upload task

This API is used to pause an upload task by `taskId`.

**Use case**

```js
var taskId = 'xxxxx';                   /* Required */
cos.pauseTask(taskId);
```

**Parameter description**

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | ID of an upload task. When `sliceUploadFile` is called, `TaskReady` in the callback will return the `taskId` of the upload task | String | Yes |

#### Restarting an upload task

This API is used to restart an upload task by `taskId`. It can restart tasks that have been manually paused with the `pauseTask` API or have been stopped due to an upload error.

**Use case**

```js
var taskId = 'xxxxx';                   /* Required */
cos.restartTask(taskId);
```

**Parameter description**

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | ID of an upload task. When `sliceUploadFile` is called, `TaskReady` in the callback will return the `taskId` of the upload task | String | Yes |
