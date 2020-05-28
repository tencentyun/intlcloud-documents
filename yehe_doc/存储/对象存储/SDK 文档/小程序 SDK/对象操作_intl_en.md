## Overview

This document provides an overview of APIs and SDK code samples related to simple operations and other operations on objects.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ---------------------------------------- |
| [GET Bucket (List Object)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying an object list | Queries all or a subnet of objects in a bucket |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploads an object using simple upload | Uploads an object to a bucket |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | Uploading an object using a form | Uploads an object using a form request |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object |
| [OPTIONS Object](https://intl.cloud.tencent.com/document/product/436/8288) | Pre-requesting cross-origin configuration | Uses a pre-request to confirm whether a real cross-origin request can be sent |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object | Copies an object to a destination path (object key) |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes a specified object from a bucket |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects in a single request |

**Other operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting object ACL | Sets the ACL for the specified object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying object ACL | Queries the ACL of an object |

## Simple Operations

### Querying object list

#### Feature

Queries some or all objects in a bucket.

#### Sample

Sample 1. List all the files in directory `a`.

```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000',  /* Required */
    Region: 'ap-beijing',     /* Required */
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

```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000',  /* Required */
    Region: 'ap-beijing',    /* Required */
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
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| - Prefix | Matching prefix for object keys, which sets that the response only contains object keys with the specified prefix. | String | No |
| Delimiter | A separating symbol used to group object keys. It is usually `/`. The identical paths between `Prefix` or, if no `Prefix` is specified, the beginning and the first `delimiter` are grouped and defined as a common prefix. All common prefixes will be listed. | String | No |
| Marker | Marker for the starting object key. Object key entries will be returned in UTF-8 lexicographical order starting from the first object key after the marker | String | No |
| MaxKeys | Maximum number of entries returned at a time. Default value: 1,000 | String | No |
| encoding-type | Specifies the encoding type of the returned value. Valid value: `url`, which means that the returned object keys are URL-encoded (percent-encoded) values. For example, "Tencent Cloud" will be encoded as `Tencent%20Cloud`. | String | No |

### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ----------------- | ------------------------------------------------------------ | ----------- |
| err | A returned request error (network error or service error). If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null. | Object |
| - headers | Header information returned by the request | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - Name | Bucket name in the format of `<BucketName-APPID>`, such as `examplebucket-1250000000` | String |
| - Prefix | The object key prefix for match. Object key entries will be returned in UTF-8 lexicographical order starting from the first object key after the prefix | String |
| - Marker | Marker for the starting object key. Object key entries will be returned in UTF-8 lexicographical order starting from the first object key after the marker | String |
| - MaxKeys | Maximum number of results returned in one response | String |
| - Delimiter | Delimiter | String |
| - IsTruncated | Whether the returned request entries are truncated. Valid values: `true`, `false` | String |
| - NextMarker | If the returned entries are truncated, then NextMarker is the starting point of the next entry | String |
| - CommonPrefixes | The identical paths between `Prefix` and `Delimiter` are grouped and defined as a common prefix | ObjectArray |
| - - Prefix | A single common prefix | String |
| - EncodingType | Encoding method of the return value, which is effective for Delimiter, Marker, Prefix, NextMarker, and Key | String |
| - Contents | Metadata | ObjectArray |
| - - Key | Object name, i.e., object key | String |
| - - ETag | MD5 checksum of the file, such as `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end** | String |
| - - Size | Part size in bytes | String |
| - - LastModified  | The last modified time of the object, in ISO8601 format, such as 2019-05-24T10:56:40Z | String |
| - - Owner | Object owner information | Object |
| - - - ID | Complete ID of object owner. Format: `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`, such as `qcs::cam::uin/100000000001:uin/100000000001`，where 100000000001 is uin | String |
| - - - DisplayName | Part owner name | String |
| - - StorageClass | Object storage class. Enumerated values: `STANDARD`, `STANDARD_IA` and `ARCHIVE`. For more information, see [Storage Class](https://intl.cloud.tencent.com/document/product/436/30925) | String |

### Uploading an object usng simple upload

#### Feature

This API (PUT Object) is used to upload an object to a bucket. To make this request, you need to have write permission for the bucket.

>
> 1. The Key (file name) cannot end with `/`; otherwise, it will be identified as a folder.
> 2. The total number of policies associated with bucket ACL, Policy, and CAM under a single root account (i.e., under the same APPID) cannot exceed 1,000. There is no upper limit on the number of object ACL rules. If you do not need access control for an object, do not make the configuration when uploading it, and the object will inherit the permissions of its bucket.
> 3. After an object is uploaded, you can use the same key to generate a pre-signed link, which can be shared with others for download. However, please note that if your file is set to private-read, the pre-signed link will only be valid for a certain period of time. To download, please specify the method as `GET`. For API details, see below.

#### Sample

Upload a string as the file content:

```js
cos.putObject({
    Bucket: 'examplebucket-1250000000',  /* Required */
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
    Bucket: 'examplebucket-1250000000',  /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'a/', /*Required*/
    Body: '',
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | An object key (object name) is a unique ID of an object in the bucket. For more information, see [Object Key Description](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| Body | Text content of the created file, which can be a string | String | Yes |
| CacheControl | Cache policy as defined in RFC 2616, which will be stored in the object metadata | String | No |
| ContentDisposition | Filename as defined in RFC 2616, which will be stored in the object metadata | String | No |
| ContentEncoding | Encoding format as defined in RFC 2616, which will be stored in the object metadata | String | No |
| ContentLength | HTTP request length in bytes as defined in RFC 2616 | String | No |
| ContentType | Content type (MIME) as defined in RFC 2616, which will be stored in the object metadata | String | No |
| Expires | Expiration time as defined in RFC 2616, which will be stored in the object metadata | String | No |
| Expect | If `Expect: 100-continue` is used, the request content will be sent only after confirmation from the server is received | String | No |
| ACL   | Defines the access control list (ACL) attribute of the object. For the enumerated values such as `default`, `private`, and `public-read`, see the Preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). <br>**Note:** If you do not need access control for the object, set `default` for this parameter or simply leave it blank, and the object will inherit the permissions of the bucket | String | No |
| GrantRead | Grants the user read access in the format of `id="[OwnerUin]"`. You can use comma (,) to separate multiple users. <br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantReadAcp | Grants the user read access to the object’s ACL in the format of `id="[OwnerUin]"`. You can use comma (,) to separate multiple users.<br/><li>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br><li>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantWriteAcp | Grants the user write access to the object’s ACL in the format of `id="[OwnerUin]"`. You can use comma (,) to separate multiple users.<br><li>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br><li>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantFullControl | Grants the user full access in the format of `id="[OwnerUin]"`. You can use comma (,) to separate multiple users.<br><li>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br><li>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| StorageClass | Sets the object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String | No |
| x-cos-meta-* | Headers that can be defined by users, which will be returned as the object metadata; maximum size: 2 KB | String | No |
| TaskReady | Callback function when an upload task is created. The callback returns a `taskId`, which uniquely identifies the task and can be used to cancel (cancelTask), pause (pauseTask), or restart (restartTask) the task | Function | No |
| - taskId                                                     | Upload task number                                              | String    | No  |
| onProgress | Progress callback function. Attributes of the progress callback response object, `progressData`, are as follows | Function | No |
| - progressData.loaded | Size of the file part that has been uploaded; unit: byte | Number | No |
| - progressData.total                                         | Total file size in bytes                      | Number    | No   |
| - progressData.speed                                         | File upload speed in bytes/s                 | Number    | No   |
| - progressData.percent | Percentage of file upload progress in decimal form; for example, 0.5 means 50% downloaded | Number | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | A returned request error (network error or service error). If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request succeeds. If the request fails, this is null. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - ETag | Returns the MD5 checksum of the file. The value of `ETag` can be used to check whether the object gets corrupted during the upload. <br>For example, `"09cba091df696af91549de27b8e7d0f6"`. **Note: Double quotation marks are required at the beginning and the end of the `ETag` value string here** | String |
| - Location | Creates an object's access domain name for external network | String |
| - VersionId       | The version ID will be returned for buckets that have enabled versioning. If the bucket has never enabled versioning, no value will be returned | String  |

### Uploading an object using a form

This API (POST Object) is used to upload a file (object) selected by the user through wx.chooseImage to a specified bucket. To make this request, you need to have the permission to write to the bucket.

#### Sample

Upload a file using simple upload

```js
cos.postObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: filename,
    FilePath: tmpFilePath, // tmpFilePath obtained when you select the file through wx.chooseImage
    onProgress: function (info) {
        console.log(JSON.stringify(info));
    }
}, function (err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | An object key (object name) is a unique ID of an object in the bucket. For more information, see [Object Key Description](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| ContentLength | HTTP request length in bytes as defined in RFC 2616 | String | Yes |
| CacheControl | Cache policy as defined in RFC 2616, which will be stored in the object metadata | String | No |
| ContentDisposition | Filename as defined in RFC 2616, which will be stored in the object metadata | String | No |
| ContentEncoding | Encoding format as defined in RFC 2616, which will be stored in the object metadata | String | No |
| ContentType | Content type (MIME) as defined in RFC 2616, which will be stored in the object metadata | String | No |
| Expires | Expiration time as defined in RFC 2616, which will be stored in the object metadata | String | No |
| Expect | If `Expect: 100-continue` is used, the request content will be sent only after confirmation from the server is received | String | No |
| ACL    | Defines the access control list (ACL) attribute of the object. For the enumerated values such as `default`, `private`, and `public-read`, see the Preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). <br>**Note:** If you do not need access control for the object, set `default` for this parameter or simply leave it blank, and the object will inherit the permissions of the bucket | String | No |
| StorageClass | Sets the object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String | No |
| x-cos-meta-* | Headers that can be defined by users, which will be returned as the object metadata; maximum size: 2 KB | String | No |
| FilePath | Temporary file path to the file to be uploaded, which can be obtained by selecting the file through wx.chooseImage | String | Yes |
| onProgress | Progress callback function. The first parameter in a callback is the `progressData` object | Function | No |
| - progressData.loaded | Size of the file part that has been downloaded in bytes | Number | No |
| - progressData.total                                         | Total file size in bytes                      | Number    | No   |
| - progressData.speed | File download speed in bytes/s | Number | No |
| - progressData.percent | Percentage of file download progress in decimal form; for example, 0.5 means 50% downloaded | Number | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | A returned request error (network error or service error). If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request succeeds. If the request fails, this is null. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - ETag | Returns the MD5 checksum of the object. The value of `ETag` can be used to check whether the object gets corrupted during the upload. <br>**Note: double quotation marks are required at the beginning and the end of the `ETag` value string here, such as `"09cba091df696af91549de27b8e7d0f6"`** | String |
| - Location | Creates an object's access domain name for external network | String |
| - VersionId | The version ID of the returned object in a versioning-enabled bucket | String |

### Querying object metadata

#### Feature

Queries the metadata of an object.

#### Sample

```js
cos.headObject({
    Bucket: 'examplebucket-1250000000',  /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',               /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| --------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | An object key (object name) which uniquely identifies an object in the bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| IfModifiedSince | Returns the metadata on the object if the object is modified after the specified time | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Parameter Description | Type |
| --------------------- | ------------------------------------------------------------ | ------- |
| err | A returned request error (network error or service error). If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request succeeds. If the request fails, this is null. | Object |
| - statusCode | HTTP status code returned by the request, such as 200 and 304. If no modification is made after the specified time, 304 will be returned | Number |
| - headers | Header information returned by the request | Object |
| - x-cos-object-type | Indicates whether an object can be appended to an upload operation. Enumerated values: `normal`, `appendable` | String |
| - x-cos-storage-class | Object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: STANDARD, which is not displayed in the response | String |
| - x-cos-meta-* | User-defined metadata | String |
| - NotModified | Whether an object is unmodified after the specified time | Boolean |
| - ETag | Returns the MD5 checksum of the file. The value of `ETag` can be used to check whether the object gets corrupted during the upload. <br>For example, `"09cba091df696af91549de27b8e7d0f6"`. **Note: Double quotation marks are required at the beginning and the end of the `ETag` value string here** | String |
| - VersionId       | The version ID will be returned for buckets that have enabled versioning. If the bucket has never enabled versioning, no value will be returned | String  |

### Downloading an object

This API (GET Object) is used to get the content, in string format, of a specified file in a bucket.

#### Sample

```js
cos.getObject({
    Bucket: 'examplebucket-1250000000',  /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
}, function(err, data) {
    console.log(err || data.Body);
});
```

Get file content with `Range` specified:

```js
cos.getObject({
    Bucket: 'examplebucket-1250000000',  /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
    Range: 'bytes=1-3', /*Optional*/
}, function(err, data) {
    console.log(err || data.Body);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| -------------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | An object key (object name) which uniquely identifies an object in the bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| ResponseContentType | Sets the `Content-Type` parameter in the response headers | String | No |
| ResponseContentLanguage | Sets the `Content-Language` parameter in the response headers | String | No |
| ResponseExpires | Sets the `Content-Expires` parameter in the response headers | String | No |
| ResponseCacheControl | Sets the `Cache-Control` parameter in the response headers | String | No |
| ResponseContentDisposition | Sets the `Content-Disposition` parameter in the response headers | String | No |
| ResponseContentEncoding | Sets the `Content-Encoding` parameter in the response headers | String | No |
| Range | Byte range of the object as defined in RFC 2616. The range value must be in the format of bytes=first-last, where both first and last are offsets starting from 0. For example, bytes=0-9 means that you want to download the first 10 bytes of data of the source object. If this parameter is not specified, the entire object will be downloaded | String | No |
| IfModifiedSince | Returns the metadata on the object if the object is modified after the specified time; otherwise, returns a 304 (not modified) error| String | No |
| IfUnmodifiedSince    | If the object is not modified after the specified time, the object will be returned; otherwise, HTTP status 412 (Precondition Failed) will be returned | String | No |
| IfMatch | The file will be returned only if ETag matches the specified content; otherwise, 412 (precondition failed) will be returned | String | No |
| IfNoneMatch | The file will be returned only if ETag does not match the specified content; otherwise, 304 (not modified) will be returned | String | No |
| VersionId | Specifies the version ID of the object to be downloaded | String | No |
| onProgress | Progress callback function. Attributes of the progress callback response object, `progressData`, are as follows | Function | No |
| - progressData.loaded | Size of the file part that has been downloaded; unit: byte | Number | No |
| - progressData.total | Size of the entire object in bytes | Number | No |
| - progressData.speed | Object download speed; unit: bytes/s | Number | No |
| - progressData.percent | A decimal representing the file download progress. For example, 0.5 means 50% has been downloaded | Number | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Parameter Description | Type |
| --------------------- | ------------------------------------------------------------ | ------- |
| err | A returned request error (network error or service error). If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request succeeds. If the request fails, this is null. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| Cache-Control | Cache directives as defined in RFC 2616, which will be returned only if it is contained in the object metadata or specified through the request parameter | string |
| Content-Disposition | Filename as defined in RFC 2616, which will be returned only if it is contained in the object metadata or specified through the request parameter | string |
| Content-Encoding | Encoding format as defined in RFC 2616, which will be returned only if it is contained in the object metadata or specified through the request parameter | string |
| Expires | Cache expiration time as defined in RFC 2616, which will be returned only if it is contained in the object metadata or specified through the request parameter | string |
| - x-cos-storage-class | Storage class of the object. Enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE` <br>**Note: if this header is not returned, it means the file storage class is `STANDARD` (standard storage)** | String |
| - x-cos-meta-* | User-defined metadata | String |
| - NotModified      | If the request has IfModifiedSince, then the attributes of IfModifiedSince will be returned. If the file has been modified, `false` will be returned. If not, `true` will be returned | Boolean |
| - ETag | Returns the MD5 checksum of the file. The value of `ETag` can be used to check whether the object gets corrupted during the upload. <br>For example, `"09cba091df696af91549de27b8e7d0f6"`. **Note: Double quotation marks are required at the beginning and the end of the `ETag` value string here** | String |
| - VersionId       | The version ID will be returned for buckets that have enabled versioning. If the bucket has never enabled versioning, no value will be returned | String  |
| - Body                | Returned file content. Uses the String format by default.        | String  |

### Configuring pre-flight requests for cross-origin access

#### Feature

This API (OPTIONS Object) is used to implement a pre–flight request for cross-origin object access configuration. Before making a real cross-origin resource sharing (CORS) request, you can send an `OPTIONS` request carrying the specific source origin, HTTP method, and header information to COS for it to determine whether a real request can be sent. If there is no CORS configuration, `403 Forbidden` will be returned. **You can enable CORS for a bucket using the `PUT Bucket cors` API**.

#### Sample

```js
cos.optionsObject({
    Bucket: 'examplebucket-1250000000',  /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
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
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | An object key (object name) which uniquely identifies an object in the bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| Origin | Source origin of the simulated cross-origin access request | String | Yes |
| AccessControlRequestMethod | HTTP method of the simulated cross-origin access request | String | Yes |
| AccessControlRequestHeaders | Headers of the simulated cross-origin access request | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Parameter Description | Type |
| ---------------------------- | ------------------------------------------------------------ | ------- |
| err | A returned request error (network error or service error). If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request succeeds. If the request fails, this is null. | Object |
| - headers | Header information returned by the request | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - AccessControlAllowOrigin | Source origins of the simulated cross-origin access request separated by commas. This header will not be returned if the origins are not allowed. Example: `*` | String |
| - AccessControlAllowMethods | HTTP methods of the simulated cross-origin access request separated by commas, such as PUT, GET, POST, DELETE, and HEAD. This header will not be returned if the request method is not allowed | String |
| - AccessControlAllowHeaders | Headers of the simulated cross-origin access request separated by commas, such as accept, content-type, origin, and authorization. This request header will not be returned if any of the simulated headers is not allowed | String |
| - AccessControlExposeHeaders | Response headers supported by CORS, such as `ETag`. The headers are separated by commas | String |
| - AccessControlMaxAge | Sets the validity period of the `OPTIONS` request result, such as `3600` | String  |
| - OptionsForbidden | Whether the `OPTIONS` request is forbidden, which will be `true` if the returned HTTP status code is `403` | Boolean |

### Replicating objects

#### Feature

This API (PUT Object-Copy) is used to create a copy of an existing COS object, that is, an object is copied from the source path (object key) to the destination path (object key). During replication, object metadata and access control lists (ACLs) can be modified.
Users can use this API to create a copy, modify object meta attributes (source object and destination file have the same attributes), move or rename the object (copy first, and then call the delete API separately).

> We recommend an object size between 1MB-5GB. For objects greater than 5GB, please use the advanced APIs to copy the object [Slice Copy File] (#. E5.A4.8D.E5.88.B6.E5.AF.B9.E8.B1.A12) .



#### Sample

```js
cos.putObjectCopy({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'ap-beijing',                                  /* Required */
    Key: 'picture.jpg',                                            /* Required */
    CopySource: 'test-1250000000.cos.ap-guangzhou.myqcloud.com/2.jpg', /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | An object key (object name) which uniquely identifies an object in the bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| CopySource | URL path to the source object. A historical version can be specified with the URL parameter ?versionId=&lt;versionId> | String | Yes |
| ACL    | Defines the access control list (ACL) attribute of the object. For the enumerated values such as `default`, `private`, and `public-read`, see the Preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). <br>**Note:** If you do not need access control for the object, set `default` for this parameter or simply leave it blank, and the object will inherit the permissions of the bucket | String | No |
| GrantRead | Grants the user read access in the format of `id="[OwnerUin]"`. You can use comma (,) to separate multiple users. <br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantWrite        | Grants the user write access in the format of id="[OwnerUin]".<br>Use a comma (,) to separate multiple users.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantFullControl | Grants the user full access in the format of `id="[OwnerUin]"`. You can use comma (,) to separate multiple users. <br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| MetadataDirective | Whether to copy the metadata. Enumerated values: `Copy`, `Replaced`. Default value: `Copy`. If its value is `Copy`, the user metadata in the corresponding header will be ignored and the copy will be performed; if its value is `Replaced`, the metadata will be replaced by the information in the corresponding header. **If the destination path is the same as the source path, which means you want to modify the metadata, you must specify this parameter as `Replaced`** | String | No |
| CopySourceIfModifiedSince | If the object is modified after the specified time, the operation will be performed; otherwise, `412` will be returned. **This parameter can be used together with `CopySourceIfNoneMatch`. If it is used together with other conditions, a conflict will be returned** | String | No |
| CopySourceIfUnmodifiedSince | If the object is not modified after the specified time, the operation will be performed; otherwise, `412` will be returned. **This parameter can be used together with `CopySourceIfMatch`. If it is used together with other conditions, a conflict will be returned** | String | No |
| CopySourceIfMatch | If the `Etag` of the object is the same as the specified one, the operation will be performed; otherwise, `412` will be returned. **This parameter can be used together with `CopySourceIfUnmodifiedSince`. If it is used together with other conditions, a conflict will be returned** | String | No |
| CopySourceIfNoneMatch | If the `Etag` of the object is different from the specified one, the operation will be performed; otherwise, `412` will be returned. **This parameter can be used together with `CopySourceIfModifiedSince`. If it is used together with other conditions, a conflict will be returned** | string | No |
| StorageClass | Sets the object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String | No |
| x-cos-meta-* | Other user-defined file headers | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| err | A returned request error (network error or service error). If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request succeeds. If the request fails, this is null. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - ETag | MD5 checksum of the file, such as `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end** | String |
| - LastModified | Describes the last modified time of the object, such as `2017-06-23T12:33:27.000Z` | String |
| - VersionId       | The version ID will be returned for buckets that have enabled versioning. If the bucket has never enabled versioning, no value will be returned | String  |

### Deleting a single object

#### Feature

This API (Delete Object) is used to delete an object from a COS bucket. To make this request, you need to have write permission for the bucket.

#### Sample

```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000',  /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg'                            /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | An object key (object name) which uniquely identifies an object in the bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| - VersionId | Version ID of the object or the delete marker to be deleted | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | A returned request error (network error or service error). If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request succeeds. If the request fails, this is null. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 204, 403, and 404. **If the deletion is successful or the file does not exist, 204 or 200 will be returned; if the specified bucket is not found, 404 will be returned** | Number |
| - headers | Header information returned by the request | Object |

### Deleting multiple objects

#### Feature

This API (DELETE Multiple Objects) is used to delete multiple objects in a single request. You can delete up to 1,000 objects in a single request. For the response, there are two modes for you to choose from: Verbose and Quiet. Verbose mode returns the information on the deletion of each object, whereas Quiet mode only returns the information on objects for which errors are reported.

#### Sample

Deleting multiple files:

```js
cos.deleteMultipleObject({
    Bucket: 'examplebucket-1250000000',  /* Required */
    Region: 'ap-beijing',    /* Required */
    Objects: [
        {Key: 'picture.jpg'},
        {Key: '2.zip'},
    ]
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ----------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Quiet | A boolean value which determines whether to use the Quiet mode. If the value is `true`, the Quiet mode will be used; if it is `false`, the Verbose mode will be used. Default value: `false` | Boolean | No |
| Objects | List of files to be deleted | ObjectArray | Yes |
| - Key | An object key (object name) which uniquely identifies an object in the bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| - VersionId | Version ID of the object or the delete marker to be deleted | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------------------- | ------------------------------------------------------------ | ----------- |
| err | A returned request error (network error or service error). If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request succeeds. If the request fails, this is null. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - Deleted | List of object information indicating successful deletion | ObjectArray |
| - - Key | An object key (object name) which uniquely identifies an object in the bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| - - VersionId | If the `VersionId` parameter is passed in, it will also be included in the response, indicating the version of the operated object or delete marker | String |
| - - DeleteMarker | If versioning is enabled and the `VersionId` parameter is not specified, the deletion will not actually erase the content of a file; instead, it will only add a new delete marker, indicating that the visible file has been deleted. Enumerated values: `true`, `false` | String |
| - - DeleteMarkerVersionId | If the value of the returned `DeleteMarker` is `true`, this parameter will be returned, representing the `VersionId` of the newly added delete marker | String |
| - Error | List of object information indicating deletion failure | ObjectArray |
| - - Key | An object key (object name) which uniquely identifies an object in the bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| - - Code                                                     | Deletion failure error codes                                             | String      |
| - - Message                                                  | Deletion failure error messages                                      | String      |

**Other Operations**

### Restoring an archived object

#### Feature

This API (POST Object restore) is used to restore an object archived by COS. The restored readable object is temporary, and you can make configuration to keep it readable and set the time when you want it to be deleted. You can use the `Days` parameter to specify the expiration time of the temporary object. If the object expires and you have not initiated any operation to copy the object or extend its validity period before the expiration, the temporary object will be automatically deleted. A temporary object is only a copy of the source archived object and the source object will exist throughout the period.

#### Sample

```js
cos.restoreObject({
    Bucket: 'examplebucket-1250000000',  /* Required */
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

#### Parameter description

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Type | Required|
| ------------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | An object key (object name) which uniquely identifies an object in the bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| RestoreRequest | Container for data restoration | Object | Yes |
| - Days | Sets the expiration time of a temporary copy | Number | Yes |
| - CASJobParameters | Container of the Cloud Archive Storage job parameters | Object | Yes |
| - - Tier | This parameter can be specified as one of the three data restoration modes supported by COS: `Standard`, which completes a restoration job in 3-5 hours; `Expedited`, which completes a restoration job in 15 minutes; and `Bulk`, which completes multiple restoration jobs in 5-12 hours. | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | A returned request error (network error or service error). If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request succeeds. If the request fails, this is null. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

### Setting object ACL

#### Feature

This API (PUT Object acl) is used to set the access control list (ACL) of an object in a specific bucket.

> The total number of policies associated with bucket ACL, Policy, and CAM under a single root account (i.e., under the same APPID) cannot exceed 1,000. There is no upper limit on the number of object ACL rules. If you do not need access control for an object, do not make any configuration, and the object will inherit the permissions of its bucket.

#### Sample

```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000',  /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
    ACL: 'public-read', /*Optional*/
}, function(err, data) {
    console.log(err || data);
});
```

Grant a user all permissions to an object:

```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000',  /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
    GrantFullControl: 'id="100000000001"' // 100000000001 is the UIN of the root account
}, function(err, data) {
    console.log(err || data);
});
```

Grant an object write permissions via AccessControlPolicy:

```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000',  /* Required */
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

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | An object key (object name) which uniquely identifies an object in the bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| ACL    | Defines the access control list (ACL) attribute of the object. For the enumerated values such as `default`, `private`, and `public-read`, see the Preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). <br>**Note:** If you do not need access control for the object, set `default` for this parameter or simply leave it blank, and the object will inherit the permissions of the bucket | String | No |
| GrantRead | Grants the user read access in the format of `id="[OwnerUin]"`. You can use comma (,) to separate multiple users.<br><li>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br><li>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantFullControl | Grants the user full access in the format of `id="[OwnerUin]"`. You can use comma (,) to separate multiple users.<br><li>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br><li>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| AccessControlPolicy | Sets an object's access control list (ACL) attributes information | Object | No |
| - Owner | Object owner information | Object | No |
| - - - ID | Object owner ID in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String | No |
| - - - DisplayName | Object owner name | String |
| - Grants | List of information on the authorized user and granted permissions | ObjectArray | No |
| - - Permission | Specifies the permission granted to the grantee. Enumerated values: READ, WRITE, READ_ACP, WRITE_ACP, FULL_CONTROL | String | No |
| - - Grantee         | Information of the authorized user     | Object      | No   |
| - - - DisplayName | Grantee Name | String | No |
| - - - ID | User ID in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value. | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | A returned request error (network error or service error). If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request succeeds. If the request fails, this is null. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

### Querying object ACL

#### Feature

This API is used to get the access permissions on a specified object in a specified bucket. Only the bucket owner has the permission to perform this operation.

#### Sample

```js
cos.getObjectAcl({
    Bucket: 'examplebucket-1250000000',  /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | An object key (object name) which uniquely identifies an object in the bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ----------------- | ------------------------------------------------------------ | ----------- |
| err | A returned request error (network error or service error). If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - ACL | Defines the access control list (ACL) attributes of the object. For the enumerated values such as `private` and `public-read`, see the “Preset ACL for buckets” section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: `private` | String |
| - Owner | Identifies owner of the resource | Object |
| - - - ID | Object owner ID in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String |
| - - DisplayName | Object owner name | String |
| - Grants | List of information on the authorized user and granted permissions | ObjectArray |
| - - Permission | Specifies the permission granted to the grantee. Enumerated values: `READ`, `WRITE`, `READ_ACP`, `WRITE_ACP`, `FULL_CONTROL` | String | No |
| - - Grantee | Grantee Information | Object |
| - - - DisplayName | User Name | String |
| - - - ID | User ID in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String |

## Advanced APIs (recommended)

The following methods encapsulate the native methods mentioned above. They can implement the complete process of multipart replication and support concurrent multipart replications, checkpoint restart as well as cancelling, pausing, and restarting replication tasks.

### Replicating objects

#### Feature

This API (Slice Copy File) is used to copy a file from a source path to a destination path through multipart copy. Object metadata and ACL can be modified during the copy process. You can use this API to move, rename, and copy a file or modify its attributes.

#### Method prototype

Call Slice Copy File:

```js
cos.sliceCopyFile({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'ap-beijing',                                  /* Required */
    Key: '1.zip',                                            /* Required */
    CopySource: 'test-1250000000.cos.ap-guangzhou.myqcloud.com/2.zip', /* Required */
    onProgress:function (progressData) { /*Optional*/
        console.log(JSON.stringify(progressData));
    }
},function (err,data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Type | Required|
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | An object key (object name) is a unique ID of an object in the bucket. For more information, see [Object Key Description](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| CopySource | URL path to the source object. A historical version can be specified with the URL parameter ?versionId=\<versionId> | String | Yes |
| ChunkSize | Size of the parts in the multipart copy; unit: byte. Default value: 1,048,576 (1 MB) | Number | No |
| SliceSize | Indicates the file size threshold in byte for multipart replication. Default value: 5 G. If a file is smaller than or equal to 5 G, it will be uploaded using putObjectCopy; otherwise, sliceCopyFile will be used. | Number | No |
| onProgress | File upload progress callback function. The callback parameter is the object in progress `progressData` | Function | No |
| - progressData.loaded | Size of the file part that has been uploaded; unit: byte | Number | No |
| - progressData.total                                         | Total file size in bytes                      | Number    | No   |
| - progressData.speed                                         | File upload speed in bytes/s                 | Number    | No   |
| - progressData.percent | Percentage of file upload progress in decimal form; for example, 0.5 means 50% uploaded | Number | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - Location | Creates an object's access domain name for external network | String |
| - Bucket | Destination bucket for the multipart upload | String |
| - Key | An object key (object name) which uniquely identifies an object in the bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| - ETag | MD5 checksum of the merged file. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end** | String |
| - VersionId  | Uploads an object in a version control-enabled bucket returns the version ID of the object. This parameter is not returned if the bucket has never been enabled | String |

### Upload queue

The SDK for Wechat Mini Program records all the putObject upload tasks in a queue, whose related operations are as follows:

1. Use cos.getTaskList to get the task list.
2. Use cos.pauseTask, cos.restartTask, and cos.cancelTask to perform operations on upload tasks.
3. Use cos.on('list-update', callback); to monitor changes in the list and the upload progress.

For a complete example of queue usage, see [demo-queue](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/demo/queue).

#### Canceling an upload task

Cancels an upload task by `taskId`.

**Sample**

```js
var taskId = 'xxxxx';                   /* Required */
cos.cancelTask(taskId);
```

**Parameter description**

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | ID of an upload task. When `putObject` is called, `TaskReady` in the callback will return the `taskId` of the upload task. | String | Yes |

#### Suspending an upload task

Suspends an upload task by `taskId`.

**Sample**

```js
var taskId = 'xxxxx';                   /* Required */
cos.pauseTask(taskId);
```

**Parameter description**

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | ID of an upload task. When `putObject` is called, `TaskReady` in the callback will return the `taskId` of the upload task. | String | Yes |

#### Restarting an upload task

Restarts an upload task by `taskId`. You can restart tasks that have been manually suspended from the `pauseTask` API, or automatically suspended due to an upload error.

**Sample**

```js
var taskId = 'xxxxx';                   /* Required */
cos.restartTask(taskId);
```

**Parameter description**

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | ID of an upload task. When `putObject` is called, `TaskReady` in the callback will return the `taskId` of the upload task. | String | Yes |
