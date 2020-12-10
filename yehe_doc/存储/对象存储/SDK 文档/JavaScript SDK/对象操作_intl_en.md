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
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload job |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading a part | Uploads a part in a multipart upload |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying parts | Queries uploaded parts in a specified multipart upload |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of an entire object |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload operation | Aborts a multipart upload operation and deletes the uploaded parts |

**Other operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an ARCHIVED object | Restores an ARCHIVED object for access |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting object ACL | Sets the ACL of a specified object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying object ACL | Queries the ACL of an object |

## Simple Operations

### Querying an object list

#### API description

Queries some or all objects in a bucket.

#### Use case

Sample 1. List all files in directory `a`.

[//]: # (.cssg-snippet-get-bucket)
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

[//]: # (.cssg-snippet-get-bucket-with-delimiter)
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
| ------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name, formatted as `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Prefix | Matching prefix for object keys. It limits the response to object keys that begin with the specified prefix. | String | No |
| Delimiter | A separating symbol that is used to group object keys. It is usually `/`. The identical paths between `Prefix` or, if no `Prefix` is specified, the beginning, and the first `Delimiter` are grouped and defined as a common prefix. All common prefixes will be listed | String | No |
| Marker | Indicates where the object key listing begins. Entries are listed starting from the key after the `Marker` in UTF-8 lexicographical order by default | String | No |
| MaxKeys | Maximum number of entries returned at a time. The default value is 1000 | String | No |
| encoding-type | Encoding type of the returned value. Valid value: `url`, meaning that the returned object keys are URL-encoded (percent-encoded) values. For example, "Tencent Cloud" will be encoded as `%E8%85%BE%E8%AE%AF%E4%BA%91`. | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ----------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty | Object |
| - headers | Headers returned by the request | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - Name | Bucket name, formatted as `BucketName-APPID` (e.g., `examplebucket-1250000000`) | String |
| - Prefix | Matching prefix for object keys. Object key entries will be returned in UTF-8 lexicographical order starting from the first object key after the prefix | String |
| - Marker | By default, entries are listed in UTF-8 binary order starting from the entry after the `Marker` | String |
| - MaxKeys | Maximum number of entries returned in a single request | String |
| - Delimiter | Delimiter | String |
| - IsTruncated | Specifies whether returned entries are truncated. Valid values: `true`, `false` | String |
| - NextMarker | If returned entries are truncated, `NextMarker` marks where the next entry should begin | String |
| - CommonPrefixes | The identical paths between a specified prefix and the delimiter are grouped and defined as a common prefix | ObjectArray |
| - - Prefix | A single common prefix | String |
| - EncodingType | Encoding type of the returned values. It is applicable to `Delimiter`, `Marker`, `Prefix`, `NextMarker`, and `Key` | String |
| - Contents | An array of object metadata | ObjectArray |
| - - Key | Object key, namely the object name | String |
| - - ETag | MD5 checksum of the file<br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end of ETag** | String |
| - - Size | Object size, in bytes | String |
| - - LastModified  | Time when the object was last modified, in ISO8601 format (e.g., 2019-05-24T10:56:40Z) | String |
| - - Owner | Information of the object owner | Object |
| - - - ID | Complete ID of the object owner, formatted as `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`<br>Example: `qcs::cam::uin/100000000001:uin/100000000001`, where `100000000001` is the UIN | String |
| - - - DisplayName | Name of the object owner | String |
| - - StorageClass |Storage class of the object. Enumerated values: `STANDARD`, `STANDARD_IA` and `ARCHIVE`. For more information, please see [Storage Classes Overview](https://intl.cloud.tencent.com/document/product/436/30925) | String |

### Uploading an object using simple upload

#### API description

This API (PUT Object) is used to upload an object to a bucket. To call this API, you need to have write permissions for the bucket.

> !
> 1. The Key (filename) cannot end with `/`; otherwise, it will be identified as a folder.
> 2. The total number of bucket ACL rules under a single root account (i.e., under the same `APPID`) cannot exceed 1,000. There is no upper limit on the number of object ACL rules. If you do not need access control for an object, you can choose not to configure an ACL for the object during upload, and the object will inherit the permissions of its bucket by default.
> 3. After an object is uploaded, you can use the same key to generate a pre-signed URL, which can be shared with others for download. However, please note that if your file is set to private-read, the pre-signed URL will be valid for only a certain period of time. To download, please specify the method to GET (see the API description below).

#### Use case

Simple upload is suitable for small files.

[//]: # (.cssg-snippet-put-object)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    StorageClass: 'STANDARD',
    Body: fileObject, // Upload the object
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

Upload strings as file content:

[//]: # (.cssg-snippet-put-object-string)
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

[//]: # (.cssg-snippet-put-object-folder)
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
| ---------------------- | ------------------------------------------------------------ | ---------------- | ---- |
| Bucket | Bucket name, formatted as `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| Body | Content of the file to upload. It can be a string, a file object, or a blob object | String\File\Blob | Yes |
| CacheControl | Cache policy as defined in RFC 2616. It will be stored as object metadata | String | No |
| ContentDisposition | Filename as defined in RFC 2616. It will be stored as object metadata | String | No |
| ContentEncoding | Encoding format as defined in RFC 2616. It will be stored as object metadata | String | No |
| ContentLength | HTTP request length (in bytes) as defined in RFC 2616 | String | No |
| ContentType | Content type (MIME) as defined in RFC 2616. It will be stored as object metadata | String | No |
| Expires | Expiration time as defined in RFC 2616. It will be stored as object metadata | String | No |
| Expect  | If `Expect: 100-continue` is set, the requested content can only be sent after the server’s confirmation is received. | String | No   |
| ACL   | Defines the access control list (ACL) attribute of the object. For the enumerated values such as `default`, `private`, and `public-read`, please see the Preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). <br>**Note:** If you do not need access control for the object, set `default` for this parameter or simply leave it empty, and the object will inherit the permissions of the bucket | String | No |
| GrantRead | Grants a user read access in the format: `id="[OwnerUin]"`. You can use a comma (,) to separate multiple users. <br><li>Authorizing a sub-account: `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>Authorizing a root account: `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantReadAcp | Grants a user read access to the object’s ACL in the format: `id="[OwnerUin]"`. You can use a comma (,) to separate multiple users. <br><li>Authorizing a sub-account: `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br><li>Authorizing a root account: `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantWriteAcp | Grants a user write access to the object’s ACL in the format: `id="[OwnerUin]"`. You can use a comma (,) to separate multiple users. <br><li>Authorizing a sub-account: `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`br><li>Authorizing a root account: `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantFullControl | Grants a user full access in the format: `id="[OwnerUin]"`. You can use a comma (,) to separate multiple users. <br><li>Authorizing a sub-account: `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>Authorizing a root account: `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| StorageClass | Sets the storage class for an object. Enumerated values: `STANDARD` (default), `STANDARD_IA`, `ARCHIVE` | String | No |
| x-cos-meta-* | Customizable header. It will be stored as object metadata. Maximum size: 2 KB | String | No |
| UploadAddMetaMd5       | During the upload, sets `x-cos-meta-md5` as the object’s MD5 value in the object metadata. It is a 32-bit lowercase string (e.g., `4d00d79b6733c9cc066584a02ed03410`) | String           | No   |
| onTaskReady   | Callback function when an upload task is created. The callback returns a `taskId`, which uniquely identifies the task and can be used to cancel (cancelTask), pause (pauseTask), or restart (restartTask) the task | Function | No |
| - taskId    | Upload task number   | String    | No  |
| onProgress | Progress callback function. Attributes of the progress callback response object (`progressData`) are as follows | Function | No |
| - progressData.loaded | Size of the uploaded file part, in bytes | Number | No |
| - progressData.total    | Total file size, in bytes                      | Number    | No   |
| - progressData.speed  | File upload speed, in bytes/s  | Number | No   |
| - progressData.percent | A decimal representing the file upload progress (e.g, 0.5 indicates 50% has been uploaded) | Number | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Returns data when the request is successful. If the request fails, this parameter is left empty | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| - ETag | MD5 checksum of the file. The value of `ETag` can be used to check whether the object was corrupted during the upload. <br>For example, `"09cba091df696af91549de27b8e7d0f6"`. **Note that double quotation marks are required at the beginning and the end of the `ETag`** | String |
| - Location   | The location where the uploaded file can be accessed   | String |
| - VersionId       | Version ID for versioning-enabled buckets. For buckets which have never had versioning enabled, this parameter is not returned | String  |

### Uploading an object using an HTML form

The SDK for JS does not provide a method for the `POST Object` API. If you need to use this API, please see "Solution B: Upload with Form" in [Practice of Direct Transfer for Web End](https://intl.cloud.tencent.com/document/product/436/9067).

### Querying object metadata

#### API description

This API is used to query the metadata of an object.

#### Use case

[//]: # (.cssg-snippet-head-object)
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
| --------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name, formatted as `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | ObjectKey (object name) is a unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| IfModifiedSince | Returns object metadata if the object is modified after the specified time; otherwise, 304 is returned | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200` and `304`. If no modification is made after the specified time, `304` will be returned | Number |
| - headers | Headers returned by the request | Object |
| - x-cos-object-type | Indicates whether an object is appendable. Enumerated values: `normal`, `appendable`. The default value `normal` is not displayed in the return | String |
| - x-cos-storage-class | Storage class of the object. Enumerated values: `STANDARD` (default), `STANDARD_IA`, `ARCHIVE`. `STANDARD` is not displayed in the return | String |
| - x-cos-meta-* | User-defined metadata | String |
| - NotModified | Indicates whether an object is unmodified after the specified time | Boolean |
| - ETag | MD5 checksum of the file. The value of `ETag` can be used to check whether the object was corrupted during the upload. <br>For example, `"09cba091df696af91549de27b8e7d0f6"`. **Note that double quotation marks are required at the beginning and the end of `ETag`** | String |
| - VersionId       | Version ID for versioning-enabled buckets. For buckets which have never had versioning enabled, this parameter is not returned  | String  |

### Downloading an object

> !This API is used to read object content. To download a file using your browser, you should first get a download URL through the `cos.getObjectUrl` method. For more information, please see [Pre-signed URLs](https://intl.cloud.tencent.com/document/product/436/31540).

#### Feature description 

This API (GET Object) is used to get the content, in string format, of a specified file in a bucket.

#### Use case

[//]: # (.cssg-snippet-get-object)
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

[//]: # (.cssg-snippet-get-object-range)
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
| -------------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket | Bucket name, formatted as `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| ResponseContentType | Sets the `Content-Type` parameter in the response headers | String | No |
| ResponseContentLanguage | Sets the `Content-Language` parameter in the response headers | String | No |
| ResponseExpires | Sets the `Content-Expires` parameter in the response headers | String | No |
| ResponseCacheControl | Sets the `Cache-Control` parameter in the response headers | String | No |
| ResponseContentDisposition | Sets the `Content-Disposition` parameter in the response headers | String | No |
| ResponseContentEncoding | Sets the `Content-Encoding` parameter in the response headers | String | No |
| Range | Byte range of the object as defined in RFC 2616. The range value must be in the format of `bytes=first-last`, where both `first` and `last` are offsets starting from 0. For example, `bytes=0-9` means that you want to download the first 10 bytes of data of the source object. If this parameter is not specified, the entire object will be downloaded | String | No |
| IfModifiedSince    | If the object is modified after the specified time, the object will be returned; otherwise, HTTP status code `304` (Not Modified) will be returned | String | No |
| IfUnmodifiedSince    | If the object is not modified after the specified time, the object will be returned; otherwise, HTTP status 412 (Precondition Failed) will be returned | String | No |
| IfMatch | The object will be returned only if ETag matches the specified value; otherwise, 412 (precondition failed) will be returned | String | No |
| IfNoneMatch | The object will be returned only if ETag does not match the specified value; otherwise, 304 (not modified) will be returned | String | No |
| VersionId | Specifies the version ID of the object to download | String | No |
| onProgress | Progress callback function. Attributes of the progress callback response object (`progressData`) are as follows | Function | No |
| - progressData.loaded | Size of the file part that has been downloaded, in bytes | Number | No |
| - progressData.total | Size of the entire object, in bytes | Number | No |
| - progressData.speed | Object download speed, in bytes/s | Number | No |
| - progressData.percent | A decimal representing the object download progress (e.g., 0.5 indicates 50% has been downloaded) | Number | No |

#### Callback function description

```
function(err, data) { ... }

```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Parameter Description | Type | 
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------- |
| err | A returned request error (network error or service error). If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `304`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| - CacheControl  | Cache directives as defined in RFC 2616. It will be returned only if it is contained in the object metadata or if it is specified in the request parameter | string |
| - ContentDisposition                                         | File name as defined in RFC 2616. It will be returned only if it is contained in the object metadata or if it is specified in the request parameter | String  |
| - ContentEncoding    | Encoding format as defined in RFC 2616. It will be returned only if it is contained in the object metadata or if it is specified in the request parameter | String  |
| - Expires   | Cache expiration time as defined in RFC 2616. It will be returned only if it is contained in the object metadata or if it is specified in the request parameter | String  |
| - x-cos-storage-class | Storage class of the object. Enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE` <br>**Note: If this header is not returned, the storage class is automatically set to `STANDARD`** | String |
| - x-cos-meta-*                                               | User defined metadata                                           | String  |
| - NotModified      | It will be returned if the request contains `IfModifiedSince`. If the file has been modified, `false` will be returned. If not, `true` will be returned | Boolean |
| - ETag | MD5 checksum of the file. The value of `ETag` can be used to check whether the object was corrupted during the upload. <br>For example, `"09cba091df696af91549de27b8e7d0f6"`. **Note that double quotation marks are required at the beginning and the end of ETag** | String |
| - VersionId       | Version ID for versioning-enabled buckets. For buckets which have never had versioning enabled, this parameter is not returned  | String  |
| - Body                | Returned file content. The String format is used by default       | String  |

### Configuring a pre-flight request for cross-origin access

#### Feature description

This API (OPTIONS Object) is used to send a pre–flight request for the cross-origin access configuration of an object. Before making a real cross-origin resource sharing (CORS) request, you can send an OPTIONS request that includes the source, HTTP method, and headers to COS for it to determine whether a real cross-origin request can be sent. If there is no CORS configuration, the HTTP `403 Forbidden` status code will be returned. **You can enable CORS for a bucket using the `PUT Bucket cors` API**.

#### Use case

[//]: # (.cssg-snippet-option-object)
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
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name, formatted as `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| Origin | Origin endpoint of the simulated cross-origin access request | String | Yes |
| AccessControlRequestMethod | HTTP method of the simulated cross-origin access request | String | Yes |
| AccessControlRequestHeaders | Headers of the simulated cross-origin access request | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Parameter Description | Type | 
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------- |
| err | A returned request error (network error or service error). If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty | Object |
| - headers | Headers returned by the request | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - AccessControlAllowOrigin | Origin endpoint of the simulated cross-origin access request (separated by commas). This header will not be returned if the origins are not allowed. Example: `*` | String |
| - AccessControlAllowMethods | HTTP methods of the simulated cross-origin access request (separated by commas), such as PUT, GET, POST, DELETE, and HEAD. This header will not be returned if the request method is not allowed | String |
| - AccessControlAllowHeaders | Headers of the simulated cross-origin access request (separated by commas), such as `accept`, `content-type`, `origin`, and `authorization`. This request header will not be returned if any of the simulated headers are not allowed | String |
| - AccessControlExposeHeaders | Response headers supported by CORS, such as `ETag`. The headers are separated by commas | String |
| - AccessControlMaxAge | The validity duration of results returned by the OPTIONS request, e.g. `3600` | String  |
| - OptionsForbidden | Indicates whether the `OPTIONS` request is forbidden. It is `true` if HTTP status code `403` is returned | Boolean |

### Copying an object

#### Feature description

This API (PUT Object - Copy) is used to create a copy of an existing COS object, that is, an object is copied from the source path (object key) to the destination path (object key). During the replication, object metadata and access control lists (ACLs) can be modified.
Users can use this API to create a copy, modify object metadata (the source object and destination file have the same attributes), and move or rename the object (first copy the object, and then call the delete API separately).

> !We recommend that you use this API to download an object of 1 MB-5 GB. For objects greater than 5 GB, please use the advanced replication API [Slice Copy File](#.E5.A4.8D.E5.88.B6.E5.AF.B9.E8.B1.A12).

#### Use case

[//]: # (.cssg-snippet-copy-object)
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
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name, formatted as `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| CopySource | URL path to the source object. A history version can be specified by using the URL parameter `?versionId=<versionId>` | String | Yes |
| ACL    | Defines the access control list (ACL) attribute of the object. For the enumerated values such as `default`, `private`, and `public-read`, please see the Preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). <br>**Note:** If you do not need access control for the object, set `default` for this parameter or simply leave it blank, and the object will inherit the permissions of the bucket | String | No |
| GrantRead | Grants a user read access in the format: `id="[OwnerUin]"`. You can use a comma (,) to separate multiple users. <br><li>Authorizing a sub-account: `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>Authorizing a root account: `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantWrite        | Grants the user write permission in the format: `id="[OwnerUin]"`.<br>You can use a comma (,) to separate multiple users.<br><li>Authorizing a sub-account: `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>Authorizing a root account: `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantFullControl | Grants the user full permission in the format: `id="[OwnerUin]"`. You can use a comma (,) to separate multiple users. <br><li>Authorize a sub-account: `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>Authorizing a root account: `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| MetadataDirective | Indicates whether to copy the metadata. Enumerated values: `Copy` (default), `Replaced`. If set to `Copy`, the user metadata in the corresponding header will be ignored and the copy operation will be performed; if set to `Replaced`, the metadata will be replaced by the information in the corresponding header. **If the destination path is the same as the source path, meaning you want to modify the metadata, this parameter must be set to `Replaced`** | String | No |
| CopySourceIfModifiedSince | If the object is modified after the specified time, the operation will be performed; otherwise, the HTTP `412` status code will be returned. **This parameter can be used together with `CopySourceIfNoneMatch`. If it is used together with other conditions, a conflict will be returned** | String | No |
| CopySourceIfUnmodifiedSince | If the object is not modified after the specified time, the operation will be performed; otherwise, an HTTP `412` status code will be returned. **This parameter can be used together with `CopySourceIfMatch`. If it is used together with other conditions, a conflict will be returned** | String | No |
| CopySourceIfMatch | If `Etag` of the object is the same as the specified one, the operation will be performed; otherwise, the HTTP `412` status code will be returned. **This parameter can be used together with `CopySourceIfUnmodifiedSince`. If it is used together with other conditions, a conflict will be returned** | String | No |
| CopySourceIfNoneMatch | If `Etag` of the object is different from the specified one, the operation will be performed; otherwise, `412` will be returned. **This parameter can be used together with `CopySourceIfModifiedSince`. If it is used together with other conditions, a conflict will be returned** | string | No |
| StorageClass | Sets the object storage class. Enumerated values: `STANDARD` (default), `STANDARD_IA`, `ARCHIVE`. | String | No |
| x-cos-meta-* | Other user-defined file headers | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this parameter is left empty | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| - ETag | MD5 checksum of the file, such as `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end of ETag** | String |
| - LastModified | Describes the time the object was last modified, such as `2017-06-23T12:33:27.000Z` | String |
| - VersionId       | Returns the version ID for versioning-enabled buckets. For buckets which have never had versioning enabled, this parameter is not returned  | String  |

### Deleting a single object

#### Feature description

This API (DELETE Object) is used to delete an object from a COS bucket. To make this request, you need to have write permissions for the bucket.

#### Use case

[//]: # (.cssg-snippet-delete-object)
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
| --------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name, formatted as `BucketName-APPID`. | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| VersionId | Version ID of the object or delete marker to delete | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `204`, `403`, and `404`. **If the deletion is successful or the file does not exist, the HTTP `204` or `200` status code will be returned; if the specified bucket is not found, the HTTP `404` status code will be returned** | Number |
| - headers | Headers returned by the request | Object |

### Deleting multiple objects

#### Feature description

This API (DELETE Multiple Objects) is used to delete multiple objects from a bucket in a single request, which allows a maximum number of 1,000 objects. There are two response modes for you to choose from: `Verbose` and `Quiet`. The Verbose mode returns information on the deletion of each object, whereas the Quiet mode only returns information on the objects for which errors were reported.

#### Use case

Deleting multiple files:

[//]: # (.cssg-snippet-delete-multi-object)
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
| ----------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket | Bucket name, formatted as `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Quiet | A boolean value that determines whether to use the `Quiet` mode. If set to `true`, the `Quiet` mode will be used; if set to `false` (default), the `Verbose` mode will be used. | Boolean | No |
| Objects | A list of files to delete | ObjectArray | Yes |
| - Key | Object key (object name), a unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| - VersionId | Version ID of the object or delete marker to delete | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Parameter Description                                                     | Type |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ----------- |
| err | A returned request error (network error or service error). If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `204`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `204`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| - Deleted | Lists objects deleted successfully | ObjectArray |
| - - Key | Object key (object name), a unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| - - VersionId | If  `VersionId` takes a value, it will also be included in the response, indicating the version of the object or the `DeleteMarker` | String |
| - - DeleteMarker | If versioning is enabled and the `VersionId` parameter is not specified, the delete operation will not actually delete the file; instead, it will only add a new delete marker, indicating that the visible file has been deleted. Enumerated values: `true`, `false` | String |
| - - DeleteMarkerVersionId | Returns the VersionId of the newly added delete marker if `DeleteMarker` is `true`  | String |
| - Error | Lists objects whose deletion failed | ObjectArray |
| - - Key | Object key (object name), a unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| - - Code                                                     | Deletion failure error codes                                             | String      |
| - - Message                                                  | Deletion failure error messages                                      | String      |

## Multipart Operations

### Querying multipart uploads

#### Feature description 

This API (List Multipart Uploads) is used to query ongoing multipart uploads. A single request operation can list up to 1,000 multipart uploads.

#### Use case

The sample below obtains a list of UploadIds prefixed with `exampleobject` for which the multiple upload was incomplete:

[//]: # (.cssg-snippet-list-multi-upload)
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
| -------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name, formatted as `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Prefix | Matching prefix for object keys. It limits the response to object keys that begin with the specified prefix. Note that when you make a query with the specified prefix, the returned keys will still contain `Prefix` | String | No |
| Delimiter | A separating symbol that is used to group object keys. It is usually `/`. The identical paths between `Prefix` or, if no `Prefix` is specified, the beginning and the first `delimiter` are grouped and defined as a common prefix. All common prefixes will be listed | String | No |
| EncodingType | Encoding type of the return value. Valid value: `url` | String | No |
| MaxUploads | The maximum number of entries returned. Value range: 1-1000. Default value: 1000 | String | No |
| KeyMarker | Used together with `upload-id-marker`. <br><li>If `upload-id-marker` is not specified: <br>&emsp;- only multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed. <br><li>If `upload-id-marker` is specified: <br>&emsp;- multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed; <br>&emsp;- and multipart uploads whose `ObjectName` is equal to the `key-marker` will also be listed, provided that their `UploadID` is greater than the specified `upload-id-marker` | String | No |
| UploadIdMarker | Used together with `key-marker`. <br><li>If `key-marker` is not specified: <br>&emsp;- `upload-id-marker` will be ignored. <br><li>If `key-marker` is specified: <br>&emsp;- multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed; <br>&emsp;- and multipart uploads whose `ObjectName` is equal to the `key-marker` will also be listed, provided that their `UploadID` is greater than the specified `upload-id-marker` | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Type |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this parameter is left empty | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| - Bucket | Destination bucket for the multipart upload | String |
| - Encoding-Type | The encoding type of the returned value. Valid value: `url`  | String |
| - KeyMarker | Marks the key after which the entry listing starts  | String |
| - UploadIdMarker | Marks the `UploadId` after which the entry listing starts | String |
| - NextKeyMarker | If the returned list is truncated, the `NextKeyMarker` returned will be the starting point of the subsequent list | String |
|-  NextUploadIdMarker |  If the returned list is truncated, the `UploadId` returned will be the starting point of the subsequent list | String |
| - MaxUploads                                                 | The maximum number of returned entries. Value range: 1-1000     | String   |
| - IsTruncated   |  Indicates whether returned objects are truncated. Valid value: `true`, `false` | String|
|  - Prefix  | Limits the response to keys that begin with the specified prefix | String | 
| - Delimiter | A separating symbol that is used to group object keys. It is usually `/`. The identical paths between `Prefix` or, if no `Prefix` is specified, the beginning and the first `delimiter` are grouped and defined as a common prefix. All common prefixes will be listed | String |
| - CommonPrefixs  | The identical paths between `Prefix` and `Delimiter` are grouped and defined as a common prefix | ObjectArray |
| - - Prefix | Displays specific common prefixes | String |
| - Upload                                                     | A collection of multipart upload information                                  | ObjectArray |
| - - Key   | Object key, namely the object name | String      |
| - - UploadId           | ID of the current multipart upload     | String     |
| - - StorageClass | Storage class of the part. Enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE` | String | 
| - - Initiator                        | Initiator of the current multipart upload                                    | Object      |
| - - - DisplayName | Name of the upload initiator | String |
|- - - ID | ID of the upload initiator, formatted as `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String |
| - - Owner                 | Owner of the parts                                    | Object      |
| - - - DisplayName | Name of the parts’ owner | String |
| - - - ID | Parts owner ID, formatted as `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`.<br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String |
| - - Initiated                               | Start time of the multipart upload                                        | String      |

### Initializing a multipart upload

#### Feature description 

This API (Initiate Multipart Upload) is used to initialize a multipart upload operation. After a successful operation, an upload ID will be returned which can be used in the subsequent `Upload Part` requests.

#### Use case

[//]: # (.cssg-snippet-init-multi-upload)
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
| ------------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name, formatted as `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| CacheControl | Cache policy as defined in RFC 2616. It will be stored as object metadata | String | No |
| Content-Disposition | Filename as defined in RFC 2616. It will be stored as object metadata | String | No |
| Content-Encoding | Encoding format as defined in RFC 2616. It will be stored as object metadata | String | No |
| ContentType | Content type (MIME) as defined in RFC 2616. It will be stored as object metadata | String | No |
| Expires | Cache expiration time as defined in RFC 2616. It will be stored as object metadata | String | No |
| ACL    | Defines the access control list (ACL) attribute of the object. For the enumerated values such as `default`, `private`, and `public-read`, please see the Preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). <br>**Note:** If you do not need access control for the object, set `default` for this parameter or simply leave it blank, and the object will inherit the permissions of the bucket | String | No |
| GrantRead | Grants a user read access in the format: `id="[OwnerUin]"`. You can use a comma (,) to separate multiple users. <br><li>Authorizing a sub-account: `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>Authorizing a root account: `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantFullControl | Grants a user full access in the format: `id="[OwnerUin]"`. You can use a comma (,) to separate multiple users. <br><li>Authorizing a sub-account: `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li> Authorizing a root account: `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| StorageClass | Sets the storage class for an object. Enumerated values: `STANDARD` (default), `STANDARD_IA`, `ARCHIVE`. | String | No |
| x-cos-meta-* | Customizable headers, It will be returned as object metadata of up to 2 KB | String | No |
| UploadAddMetaMd5       | During the upload, sets `x-cos-meta-md5` as the object’s MD5 value in the object metadata. It is a 32-bit lowercase string (e.g., `4d00d79b6733c9cc066584a02ed03410`) | String | No   |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty | Object |
| Bucket     | Name of the destination bucket for the multipart upload, which is formed by connecting a user-defined string and the system-generated APPID with a hyphen, such as `examplebucket-1250000000` | string |
| Key | Object key (object name), a unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| UploadId | ID that can be used in subsequent uploads | String |

### Uploading a part

#### Feature description 

This API (Upload Part) is used to upload a part after a multipart upload is initialized. It can upload up to 10,000 parts of 1 MB to 5 GB.
<li>You can obtain an `uploadId` when you use the API `Initiate Multipart Upload` to initiate a multipart upload. This ID uniquely identifies the data of the part and its position in the entire file.</li>
<li>Every time you request the `Upload Part` API, you need to pass in `partNumber`, the part number, and `uploadId`. You can upload multiple parts out of order.</li>
<li>When the `uploadId` and `partNumber` of a new part are the same as those of a previously uploaded part, the old part will be overwritten by the new one. The 404 error, `NoSuchUpload`, will be returned if the `uploadId` does not exist.</li>

#### Use case

[//]: # (.cssg-snippet-upload-part)
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
| ------------- | ------------------------------------------------------------ | ---------------- | ---- |
| Bucket | Bucket name, formatted as `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| ContentLength | HTTP request length (in bytes) as defined in RFC 2616 | String | Yes |
| PartNumber | Part number | String | Yes |
| UploadId | The number of this multipart upload task | String | Yes |
| Body | Content of the file part to upload. It can be a string, a File object, or a Blob object | String\File\Blob | Yes |
| Expect | If `Expect: 100-continue` is set, the requested content can only be sent after the server’s confirmation is received | String | No |
| ContentMD5 | Base64-encoded 128-bit content MD5 checksum as defined in RFC 1864. This header is used to check whether there have been changes to the file content | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Returns data when the request is successful. If the request fails, this parameter is left empty | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |

### Copying Parts

#### Feature description

This API (Upload Part - Copy) is used to copy the parts of an object from the source path to the destination path.

> !To upload an object in parts, you must first initialize the multipart upload. A unique descriptor (upload ID) will be returned in the response of the multipart upload initialization, which needs to be carried in the multipart upload request.

#### Use case

[//]: # (.cssg-snippet-upload-part-copy)
```js
cos.uploadPartCopy({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    CopySource: 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject', /*Required*/
    UploadId: 'exampleUploadId', /*Required*/
    PartNumber: '1', /*Required*/
}, function(err, data) {
    console.log(err || data);
    if (data) {
      eTag = data.ETag;
    }
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name, formatted as `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| CopySource | URL path to the source object. A past object version can be specified with the URL parameter `?versionId=&lt;versionId>` | String | Yes |
| PartNumber | Part number | String | Yes |
| uploadId | To upload an object in parts, you must first initialize the multipart upload. The response of the multipart upload initialization will return a unique descriptor, an upload ID, which needs to be carried in the multipart upload request | String | Yes |
| CopySourceRange | Byte range of the source object. The range value must be in the format of `bytes=first-last`, where both `first` and `last` are offsets starting from 0. For example, `bytes=0-9` means that you want to copy the first 10 bytes of data of the source object. If this parameter is not specified, the entire object will be copied | String | No |
| CopySourceIfMatch | If `Etag` of the object is the same as the specified one, the operation will be performed; otherwise, `412` will be returned. This parameter can be used together with `x-cos-copy-source-If-Unmodified-Since`. If it is used together with other conditions, a conflict will be returned | String | No |
| CopySourceIfNoneMatch | If `Etag` of the object is different from the specified one, the operation will be performed; otherwise, `412` will be returned. This parameter can be used together with `x-cos-copy-source-If-Modified-Since`. If it is used together with other conditions, a conflict will be returned | string | No |
| CopySourceIfUnmodifiedSince | If the object is not modified after the specified time, the operation will be performed; otherwise, `412` will be returned. This parameter can be used together with `x-cos-copy-source-If-Match`. If it is used together with other conditions, a conflict will be returned | String | No |
| CopySourceIfModifiedSince | If the object is modified after the specified time, the operation will be performed; otherwise, `412` will be returned. This parameter can be used together with `x-cos-copy-source-If-None-Match`. If it is used together with other conditions, a conflict will be returned | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this parameter is left empty | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| - ETag | MD5 checksum of the file, such as `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end of ETag** | String |
| - LastModified | Time when the object was last modified, in GMT format | String |

### Querying uploaded parts

#### Feature description

This API (List Parts) is used to query the uploaded parts of a specified multipart upload operation, i.e., listing all successfully uploaded parts of a multipart upload corresponding to a particular `uploadId`.

#### Use case

[//]: # (.cssg-snippet-list-parts)
```js
cos.multipartListPart({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    UploadId: 'exampleUploadId', /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ---------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name, formatted as `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| UploadId | ID of the multipart upload. When the `Initiate Multipart Upload` API is used to initialize a multipart upload operation, an `uploadId` will be returned. This ID uniquely identifies the data of the part and its position in the entire file | String | Yes |
| EncodingType | Encoding type of the returned value | String | No |
| MaxParts | Maximum number of entries returned at a time. Default value: `1000` | String | No |
| PartNumberMarker | By default, entries are listed in UTF-8 binary order starting from the marker | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Paramater Description | Type |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ----------- |
| err | A returned request error (network error or service error). If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this parameter is left empty | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| - Bucket | Destination bucket for the multipart upload | String |
| EncodingType | Encoding type of the returned value | String |
| - Key | Object key (object name), a unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| - UploadId     | ID of the current multipart upload                                    | String   |
| - Initiator | Initiator of the current multipart upload   | Object  |
| - - DisplayName | Name of the upload initiator | String |
| - - ID | ID of the upload initiator, formatted as `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`. <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String |
| - Owner     | Owner of the parts   | Object  |
| - - DisplayName                                              | Bucket owner username | String      |
| - - ID                      | Bucket owner ID, generally the user’s UIN                            | String      |
| StorageClass        | Indicates the storage class of the parts; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE` | string    |
| PartNumberMarker      | By default, entries are listed in UTF-8 binary order starting from `marker`  | string    |
| NextPartNumberMarker  | If the returned list is truncated, the `NextMarker` returned will be the starting point of the subsequent list   | string    |
| - MaxUploads                                                 | The maximum number of entries returned in a single request                 | String      |
| - IsTruncated   |  Indicates whether returned objects are truncated. Valid value: `true` or `false` | String|
| - Part                                  | Parts information list                                                 | ObjectArray |
| - - PartNumber                                               | Part number                                                    | String      |
| - - LastModified                 | Time when the part was last modified             | String      |
| - - ETag     | MD5 checksum of the part    | String      |
| - - Size          | Part size, in bytes                                            | String      |

### Completing Multipart Upload

#### Feature description

This API (Complete Multipart Upload) is used to complete a multipart upload operation. After all parts are uploaded via the `Upload Part` API, you need to call this API to complete the multipart upload. When using this API, you need to specify the `PartNumber` and `ETag` of each part in the request body for the part information to be verified.
As the uploaded parts need to be merged and the merge takes several minutes, when the merge starts, COS will immediately return status code `200` and periodically return space information during the merge process to keep the connection active until the merge is completed. After that, COS will return the content of the merged parts in the body.

- If any uploaded part is less than 1 MB in size, `400 EntityTooSmall` will be returned when this API is called.
- If the uploaded part numbers are not continuous, `400 InvalidPart` will be returned when this API is called.
- If the part information entries in the request body are not sorted in ascending order, `400 InvalidPartOrder` will be returned when this API is called.
- If the `uploadId` does not exist, `404 NoSuchUpload` will be returned when this API is called.

> !We recommend you either complete or abort a multipart upload as early as possible, as the uploaded parts of an incomplete multipart upload will consume storage capacity and incur storage fees.

#### Use case

[//]: # (.cssg-snippet-complete-multi-upload)
```js
cos.multipartComplete({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    UploadId: 'exampleUploadId', /*Required*/
    Parts: [
        {PartNumber: '1', ETag: 'exampleETag'},
    ]
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ----------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| UploadId | Upload task number | String | Yes |
| Parts | List of information on the parts of a particular multipart upload | ObjectArray | Yes |
| - PartNumber | Part number | String | Yes |
| - ETag | MD5 checksum of each part. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end** | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Returns data when the request is successful. If the request fails, this parameter is left empty | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| - Location   | The location where the uploaded file can be accessed  | String |
| - Bucket | Destination bucket for the multipart upload | String |
|  - Key  | Object key (object name), a unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| - ETag | Unique ID of the merged file, formatted as `"uuid-<part quantity>"`. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`. **Note that double quotation marks are required at the beginning and the end** | String |

### Aborting a multipart upload operation

#### Feature description 

This API (Abort Multipart Upload) is used to abort a multipart upload operation and delete the uploaded parts. If you call this API and there is an `Upload Part` request that is using the multipart upload, the request will fail. If the `uploadId` does not exist, `404 NoSuchUpload` will be returned.

> !We recommend you either complete or abort a multipart upload as early as possible, as the uploaded parts of an incomplete multipart upload will consume storage capacity and incur storage fees.

#### Use case

[//]: # (.cssg-snippet-abort-multi-upload)
```js
cos.multipartAbort({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    UploadId: 'exampleUploadId' /*Required*/
}, function(err, data) {
    console.log(err || data);
});

```

#### Parameter description

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name, formatted as `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| UploadId | ID of the multipart upload. When the `Initiate Multipart Upload` API is used to initialize a multipart upload operation, an `uploadId` will be returned. This ID uniquely identifies the data of the part and its position in the entire file | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Returns data when the request is successful. If the request fails, this parameter is left empty | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |

##Other Operations

### Restoring an ARCHIVED object

#### Feature description

This API (POST Object restore) is used to restore an object archived by COS. The restored readable object is temporary. You can configure it to stay readable and set the time for it to be deleted. You can use the `Days` parameter to specify when the temporary object should expire. If the object expires and you have not initiated any operation to copy the object or extend its validity period before the expiration date, the temporary object will be automatically deleted. A temporary object is only a copy of the source archived object and the source object will continue to exist throughout this period.

#### Use case

[//]: # (.cssg-snippet-restore-object)
```js
cos.restoreObject({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject',
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

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name, formatted as `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| RestoreRequest | Container for data restoration | Object | Yes |
| - Days | Sets the expiration time of a temporary copy | Number | Yes |
| - CASJobParameters | Container of the Cloud Archive Storage job parameters | Object | Yes |
| - - Tier | This parameter can be specified as one of the three data restoration modes supported by COS: `Standard` (completes a restoration job in 3-5 hours), `Expedited` (completes a restoration job in 15 minutes), and `Bulk` (completes multiple restoration jobs in 5-12 hours). | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Returns data when the request is successful. If the request fails, this parameter is left empty | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |

### Setting object ACL

#### Feature description

This API (PUT Object acl) is used to set the access control list (ACL) of an object in a specific bucket.

> !The total number of policies associated with bucket ACL, Policy, and CAM under a single root account (i.e., under the same `APPID`) cannot exceed 1,000. There is no upper limit on the number of object ACL rules. If you do not need access control for an object, do not make any configuration, and the object will inherit the permissions of its bucket.

#### Use case

[//]: # (.cssg-snippet-put-object-acl)
```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    ACL: 'public-read', /*Optional*/
}, function(err, data) {
    console.log(err || data);
});
```

Grant a user all permissions to an object:

[//]: # (.cssg-snippet-put-object-acl-user)
```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    GrantFullControl: 'id="100000000001"' // 100000000001 is the UIN of the root account
}, function(err, data) {
    console.log(err || data);
});
```

Grant an object write permissions via `AccessControlPolicy`:

[//]: # (.cssg-snippet-put-object-acl-acp)
```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    AccessControlPolicy: {
        "Owner": { // `Owner` is required in `AccessControlPolicy`
            "ID": 'qcs::cam::uin/100000000001:uin/100000000001' // 100000000001 is the QQ account number of the user owning the bucket
        },
        "Grants": [{
            "Grantee": {
                "ID": "qcs::cam::uin/100000000011:uin/100000000011", // 100000000011 is the QQ account number
            },
            "Permission": "WRITE"
        }]
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket | Bucket name, formatted as `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| ACL    | Defines the access control list (ACL) attribute of the object. For the enumerated values such as `default`, `private`, and `public-read`, please see the Preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). <br>**Note:** If you do not need access control for the object, set `default` for this parameter or simply leave it blank, and the object will inherit the permissions of the bucket | String | No |
| GrantRead | Grants the user read permission in the format: `id="[OwnerUin]"`. You can use a comma (,) to separate multiple users.<br><li>Authorizing a sub-account: `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>Authorizing a root account: `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantFullControl | Grants the user full permission in the format: `id="[OwnerUin]"`. You can use a comma (,) to separate multiple users.<br><li>Authorizing a sub-account: `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>Authorizing a root account: `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| AccessControlPolicy | Sets an object's access control list (ACL) attributes | Object | No |
| - Owner | Information of the object owner | Object | No |
| - - - ID | ID of the object owner, formatted as `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String | No |
| - - DisplayName | Object owner name | String |
| - Grants | List of information on the grantee and permissions | ObjectArray | No |
| - - Permission | Specifies the permission granted to the authorized user. Enumerated values: `READ`, `WRITE`, `READ_ACP`, `WRITE_ACP`, `FULL_CONTROL` | String | No |
| - - Grantee         | Authorized user’s information     | Object      | No   |
| - - - DisplayName | Grantee Name | String | No |
| - - - ID | ID of the authorized user, formatted as `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |

### Querying object ACL

#### Feature description 

The API (GET Object acl) is used to query the ACL of an object. Only the owner of the bucket has permission to use this API.

#### Use case

[//]: # (.cssg-snippet-get-object-acl)
```js
cos.getObjectAcl({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name, formatted as `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ----------------- | ------------------------------------------------------------ | ----------- |
| err | A returned request error (network error or service error). If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| - ACL  | Defines the access control list (ACL) attribute of the object. For the enumerated values such as `default`, `private`, and `public-read`, see the Preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). <br>**Note:** If you do not need access control for the object, set `default` for this parameter or simply leave it blank, and the object will inherit the permissions of the bucket | String | No |
| - Owner | Owner of the resource | Object |
| - - ID | ID of the object owner, formatted as `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String |
| - - DisplayName | Object owner name | String |
| - Grants | List of information on the authorized user and granted permissions | ObjectArray |
| - - Permission | Specifies the permission granted to the authorized user. Enumerated values: `READ`, `WRITE`, `READ_ACP`, `WRITE_ACP`, `FULL_CONTROL` | String | No |
| - - Grantee | Authorized user’s information | Object |
| - - - DisplayName | User Name | String |
| - - - ID | Id of the user, formatted as `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String |

## Advanced APIs (Recommended)

The following methods encapsulate the native methods mentioned above. They can implement the complete process of multipart upload/copy and support concurrent multipart upload/copy, checkpoint restart as well as canceling, pausing, and restarting upload tasks.

### Uploading an object in parts

#### Feature description 

This API (Slice Upload File) is used to upload large files in parts.

>?
>- If the browser is not closed, you can suspend, restart, or cancel the upload job as needed.
>- After refreshing the browser, if you upload the same object to the same bucket, the object content will be verified based on `UploadId`. The upload will proceed after the verification.

#### Use case

[//]: # (.cssg-snippet-transfer-upload-file)
```js
cos.sliceUploadFile({
    Bucket: 'examplebucket-1250000000',                               /* Required */
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
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description  | Type  | Required |
| ------------------------------------------------------------ | ------------------------------------------------------------ | --------- | ---- |
| Bucket | Bucket name, formatted as `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| Body | Content of the file part to be uploaded, which can be a File object, or a Blob object | File\Blob | Yes |
| SliceSize                                                    | Part size                                                    | String    | No   |
| AsyncLimit | Concurrent number of parts being uploaded | String | No |
| StorageClass | Object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE` | String | No |
| UploadAddMetaMd5 | During the upload, sets `x-cos-meta-md5` as the object’s MD5 value in the object metadata. It is a 32-bit lowercase string (e.g., `4d00d79b6733c9cc066584a02ed03410`) | String | No |
| onTaskReady | Callback function when an upload task is created. The callback returns a `taskId`, which uniquely identifies the task and can be used to cancel (cancelTask), pause (pauseTask), or restart (restartTask) the task | Function | No |
| - taskId                                                     | Upload task number                                              | String    | No  |
| onHashProgress | Progress callback function for file MD5 value computation. The callback parameter is the progress object `progressData` | Function | No |
| - progressData.loaded | Size of the verified file part, in bytes | Number | No |
| - progressData.total                                         | Total file size, in bytes                      | Number    | No   |
| - progressData.speed                                         | File verification speed, in bytes/s                 | Number    | No   |
| - progressData.percent | A decimal representing the file verification progress. For example, 0.5 indicates 50% has been verified | Number | No |
| onProgress | File upload progress callback function. The callback parameter is the object in progress `progressData` | Function | No |
| - progressData.loaded | Size of the uploaded file part, in bytes | Number | No |
| - progressData.total                                         | Total file size, in bytes                      | Number    | No   |
| - progressData.speed                                         | File upload speed, in bytes/s                 | Number    | No   |
| - progressData.percent | A decimal representing the file upload progress. For example, 0.5 indicates 50% has been uploaded | Number | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Returns data when the request is successful. If the request fails, this parameter is left empty | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| - Location   | The location where the uploaded file can be accessed   | String |
| - Bucket | Destination bucket for the multipart upload | String |
| - Key | Object key (object name), a unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| - ETag | Unique ID of the merged file, formatted as  `"uuid-<part quantity>"`. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`. **Note that double quotation marks are required at the beginning and the end** | String |
| - VersionId | The version ID will be returned for buckets that have enabled versioning. If the bucket has never enabled versioning, no value will be returned | String |

### Copying object

#### Feature description

This API (Slice Copy File) is used to copy a file from a source path to a destination path through multipart copy. Object metadata and ACL can be modified during the copy process. You can call this API to move, rename, and copy a file, and modify the file attributes.

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
| Bucket | Bucket name, formatted as `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| CopySource | URL path to the source object. A past object version can be specified with the URL parameter `?versionId=\<versionId>` | String | Yes |
| ChunkSize | Size of each part in the multipart copy (in bytes). Default value: 1048576 (1 MB) | Number | No |
| SliceSize | Indicates the file size threshold (in bytes) for a multipart replication operation. Default value: 5 GB. If a file is smaller than or equal to 5 GB, it will be uploaded using `putObjectCopy`; otherwise, `sliceCopyFile` will be used. | Number | No |
| onProgress | File upload progress callback function. The callback parameter is the object in progress `progressData` | Function | No |
| - progressData.loaded | Size of the uploaded file part, in bytes | Number | No |
| - progressData.total                                         | Total file size, in bytes                      | Number    | No   |
| - progressData.speed                                         | File upload speed, in bytes/s                 | Number    | No   |
| - progressData.percent | A decimal representing the file upload progress. For example, 0.5 indicates 50% has been uploaded | Number | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Returns data when the request is successful. If the request fails, this parameter is left empty | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| - Location   | The location where the uploaded file can be accessed  | String |
| - Bucket | Destination bucket for the multipart upload | String |
| - Key | Object key (object name), a unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| - ETag | MD5 checksum of the merged file. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end** | String |
| - VersionId  | Uploads an object in a version control-enabled bucket returns the version ID of the object. This parameter is not returned if the bucket has never been enabled | String |

### Batch upload

#### Feature description

Method 1:
You can call `putObject` and `sliceUploadFile` multiple times to implement batch uploads. You can instantiate the `FileParallelLimit` parameter to limit how many files can be uploaded at the same time, which is 3 by default.

Method 2:
You can call `cos.uploadFiles` to implement batch uploads. The `SliceSize` method parameter can be used to manage the files. Below are instructions on using the `uploadFiles` method.

#### Method prototype

Call `uploadFiles`:

[//]: # (.cssg-snippet-transfer-batch-upload-objects)
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
}, function (err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | --------- | ---- |
| files | File list, where each item is a parameter object to be passed to `putObject` and `sliceUploadFile` | Object | Yes |
| Bucket | Bucket name, formatted as `BucketName-APPID` | String | Yes |
| - Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| - Key | Object key (object name), a unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| - Body | Content of the file part to upload, which can be a File object, or a Blob object | File\Blob | Yes |
| SliceSize | Specifies the minimum file size (in bytes) for which multipart upload will be used. If the file size is equal to or less than this value, the file will be uploaded using `putObject`; otherwise, it will be uploaded using `sliceUploadFile` | Number | Yes |
| onProgress | Overall upload progress for all jobs | String | Yes |
| - progressData.loaded | Size of the uploaded file part, in bytes | Number | No |
| - progressData.total   | Total file size, in bytes | Number    | No   |
| - progressData.speed  | File upload speed, in bytes/s                 | Number | No   |
| - progressData.percent | A decimal representing the file upload progress. For example, 0.5 indicates 50% has been uploaded | Number | No |
| onFileFinish | Callback for the error or the completion of each file | String | Yes |
| - err | Error message for the upload | Object | No |
| - data | Completion information for the file upload | Object | No |
| - options | Parameter information about the files that have been uploaded | Object | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ----------- |
| err | Object returned when a request error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty | Object |
| - files | error or data for each file | ObjectArray |
| - - err | Upload error message | Object |
| - - data | File upload completion information | Object |
| - - options | Parameter information on the files that have been uploaded | Object |

### Uploading Queue

The SDK for JavaScript records all the upload tasks initiated with `putObject` and `sliceUploadFile` in an upload queue. You can use the queue in the following ways:

1. Use `cos.getTaskList` to get the task list.
2. Use `cos.pauseTask`, `cos.restartTask`, and `cos.cancelTask` to perform operations on upload tasks.
3. Use `cos.on('list-update', callback);` to monitor changes in the list and the upload progress.

For a complete example of queue usage, see the [demo](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/demo/queue).

#### Canceling an upload task

This API is used to cancel an upload task with `taskId`.

**Sample**

[//]: # (.cssg-snippet-transfer-upload-cancel)
```js
var taskId = 'xxxxx';                   /* Required */
cos.cancelTask(taskId);
```

**Parameter description**

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | ID of an upload task. When `sliceUploadFile` is called, `TaskReady` in the callback will return the `taskId` of the upload task | String | Yes |

#### Pausing an upload task

This API suspends an upload task by `taskId`.

**Use case**

[//]: # (.cssg-snippet-transfer-upload-pause)
```js
var taskId = 'xxxxx';                   /* Required */
cos.pauseTask(taskId);
```

**Parameters**

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | ID of an upload task. When `sliceUploadFile` is called, `TaskReady` in the callback will return the `taskId` of the upload task | String | Yes |

#### Restarting an upload task

This API is used to restart an upload task with `taskId`. You can restart tasks that have been manually suspended through the `pauseTask` API, or those automatically suspended due to an upload error.

**Use case**

[//]: # (.cssg-snippet-transfer-upload-resume)
```js
var taskId = 'xxxxx';                   /* Required */
cos.restartTask(taskId);
```

**Parameters**

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | ID of an upload task. When `sliceUploadFile` is called, `TaskReady` in the callback will return the `taskId` of the upload task | String | Yes |
