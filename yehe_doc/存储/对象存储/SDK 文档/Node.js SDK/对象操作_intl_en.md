## Introduction

This document provides an overview of APIs and SDK code samples related to simple operations, multipart upload operations, and other operations on objects.

**Simple Operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ---------------------------------------- |
| [GET Bucket（List Object）](https://cloud.tencent.com/document/product/436/7734) | Querying object list | Queries some or all objects in a bucket |
| [PUT Object](https://cloud.tencent.com/document/product/436/7749) | Simply uploading an object | Uploads an object to a bucket |
| [POST Object](https://cloud.tencent.com/document/product/436/14690) | Uploading an object using a form | Uploads an object using a form request |
| [HEAD Object](https://cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |
| [GET Object](https://cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |
| [OPTIONS Object](https://cloud.tencent.com/document/product/436/8288) | Pre-requesting cross-origin configuration | Uses a pre-request to confirm whether a real cross-origin request can be sent |
| [PUT Object - Copy](https://cloud.tencent.com/document/product/436/10881) | Copying an object | Copies an object to a destination path (object key) |
| [DELETE Object](https://cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes a specified object from a bucket |
| [DELETE Multiple Objects](https://cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes objects in a bucket in batches |

**Multipart Upload Operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://cloud.tencent.com/document/product/436/7736) | Querying a multipart upload | Queries the information of a multipart upload in progress |
| [Initiate Multipart Upload](https://cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload job |
| [Upload Part](https://cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads object parts |
| [Upload Part - Copy](https://cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part |
| [List Parts](https://cloud.tencent.com/document/product/436/7747) | Queries uploaded parts | Queries the uploaded parts in the specific multipart upload operation |
| [Complete Multipart Upload](https://cloud.tencent.com/document/product/436/7742) | Completes multipart upload | Completes the multipart upload of the entire file |
| [Abort Multipart Upload](https://cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload operation and deletes the uploaded parts |

**Other Operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------------- |
| [POST Object restore](https://cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access |
| [PUT Object acl](https://cloud.tencent.com/document/product/436/7748) | Setting object ACL | Sets the ACL for the specified object in a bucket |
| [GET Object acl](https://cloud.tencent.com/document/product/436/7744) | Querying object ACL | Queries the ACL of an object |

## Simple Operations

### Querying the object list

#### Feature

This API (GET Bucket (List Object)) is used to query some or all objects in a bucket.

#### Samples

Sample 1. List all the files in directory `a`.

[//]: # (.cssg-snippet-get-bucket)
```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
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

[//]: # (.cssg-snippet-get-bucket-prefix)
```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
    Prefix: 'a/', /*Optional*/
    Delimiter: '/', /* Optional */
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
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Region and Domain Nam Access](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| - Prefix | Matching prefix for object keys, which sets that the response only contains object keys with the specified prefix. | String |
| Delimiter | A delimiter is a separating symbol used to group object keys. It is usually `/`. The identical paths between `Prefix` or, if no `Prefix` is specified, the beginning and the first `delimiter` are grouped and defined as a common prefix. All common prefixes will be listed. | String | No |
| Marker | Start object key tag. MaxKeys entries are listed starting from Marker, default order is UTF-8 lexicographical order | String | No |
| MaxKeys | Maximum number of entries returned at a time. Default value: 1,000 | String | No |
| encoding-type | Specifies the encoding type of the returned value. Valid value: `url`, which means that the returned object keys are URL-encoded (percent-encoded) values. For example, "Tencent Cloud" will be encoded as `%E8%85%BE%E8%AE%AF%E4%BA%91` | string | No |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ----------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - headers | Header information returned by the request | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| Name | ListBucketResult | Bucket name in the format of `<BucketName-APPID>`, such as `examplebucket-1250000000` | string |
| - Prefix | Object key prefix match, returns object key entries after this tag (excluding) in UTF-8 lexicographical order | String |
| - Marker | By default, entries are listed in UTF-8 binary order starting from `Marker` | String |
| - MaxKeys | Maximum number of results returned in one response | String |
| - Delimiter | Delimiter | String |
| - IsTruncated | Whether the returned request entries are truncated. Valid values: `true`, `false` | String |
| - NextMarker | If the returned entries are truncated, then NextMarker is the starting point of the next entry | String |
| - CommonPrefixes | The identical paths between `Prefix` and `Delimiter` are grouped and defined as a common prefix | ObjectArray |
| - - Prefix | A single common prefix | String |
| - Encoding-Type | Encoding type of the returned values, which is applicable to `Delimiter`, `Marker`, `Prefix`, `NextMarker`, and `Key` | String |
| - Contents | Metadata | ObjectArray |
| - - Key | Object name, i.e., object key | String |
| - - ETag | MD5 checksum of the file, such as `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end** | String |
| - - Size | Part size in bytes | String |
| - - LastModified  | Object last modified time, in ISO8601 format, such as 2019-05-24T10: 56: 40Z | String |
| - - Owner | Object owner information | Object |
| - - - ID | Complete ID of object owner, format is `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`, such as `qcs::cam::uin/100000000001:uin/100000000001`，where 100000000001 is uin | String |
| - - - DisplayName | Part owner name | String |
| x-cos-storage-class | Object storage class, such as `STANDARD_IA` and `ARCHIVE`. Default value: `STANDARD`. For enumerated values, see [Storage Class](https://intl.cloud.tencent.com/document/product/436/30925) | Enum | No |

### Uploading an object usng simple upload

#### Feature

This API (PUT Object) is used to upload an object to a specified bucket. This operation requires the requester to have WRITE permission on the bucket. For upload, the object can have a maximum of 5GB, please use [Multipart Upload](#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) or [Advanced APIs](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89) for upload if greater than 5GB .

>
> 1. An object key (file name) cannot end with `/`; otherwise, the file will be recognized as a folder.
2. The total number of policies associated with bucket ACL, Policy, and CAM under a single root account (i.e., under the same APPID) cannot exceed 1,000. There is no upper limit on the number of object ACL rules. If you do not need access control for an object, do not make the configuration when uploading it, and the object will inherit the permissions of its bucket.
> 3. After an object is uploaded, you can use the same key to generate a pre-signed link, which can be shared with others for download. However, please note that if your file is set to private-read, the pre-signed link will only be valid for a certain period of time. To download, please specify the method as `GET`. For API details, see below.

#### Samples

Simple upload is suitable for uploading small files.

[//]: # (.cssg-snippet-put-object)
```js
const filePath = "temp-file-to-upload" // Local file path
cos.putObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
    Key: 'exampleobject', /*Required*/
    StorageClass: 'STANDARD',
    Body: fs.createReadStream(filePath), // Upload file object
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

Upload Buffer as the file content:

[//]: # (.cssg-snippet-put-object-buffer)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
    Key: 'exampleobject', /*Required*/
    Body: Buffer.from('hello!'), /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

Upload strings as file content:

[//]: # (.cssg-snippet-put-object-string)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
    Key: 'exampleobject', /*Required*/
    Body: 'hello!',
}, function(err, data) {
    console.log(err || data);
});
```

Create a directory

[//]: # (.cssg-snippet-put-object-folder)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
    Key: 'a/', /*Required*/
    Body: '',
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Region and Domain Nam Access](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (Object name), the unique identifier of the object in the bucket, see [Object Overview] details(https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| Body | Content of the file to be uploaded, which can be a FileStream, string, or Buffer | Stream/Buffer/String | Yes |
| CacheControl | Cache policy as defined in RFC 2616, which will be stored in the object metadata | String | No |
| ContentDisposition | Filename as defined in RFC 2616, which will be stored in the object metadata | String | No |
| ContentEncoding | Encoding format as defined in RFC 2616, which will be stored in the object metadata | String | No |
| ContentLength | HTTP request length in bytes as defined in RFC 2616 | String | No |
| ContentType | Content type (MIME) as defined in RFC 2616, which will be stored in the object metadata | String | No |
| Expires | Expiration time as defined in RFC 2616, which will be stored in the object metadata | String | No |
| Expect | If `Expect: 100-continue` is used, the request content will be sent only after confirmation from the server is received | String | No |
| x-cos-acl | Defines the access control list (ACL) attribute of the object. For the enumerated values such as `default`, `private`, and `public-read`, see the Preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: default <br>**Note:** Currently, there can be up to 1,000 entries in one ACL. If you do not need access control for the object, set `default` for this parameter or simply leave it blank, and the object will inherit the permissions of the bucket | Enum | No |
| GrantRead | Grants the grantee Read access in the format of `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantReadAcp | Grants the grantee Read access to ACL and policies in the format of `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantWriteAcp | Grants the grantee Write access to ACL and policies in the format of `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantFullControl | Grants the grantee Read/Write access in the format of `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| StorageClass | Sets the object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String | No |
| x-cos-meta-* | Headers that can be defined by users, which will be returned as the object metadata; maximum size: 2 KB | String | No |
| TaskReady | Callback function when an upload task is created. The callback returns a `taskId`, which uniquely identifies the task and can be used to cancel (cancelTask), pause (pauseTask), or restart (restartTask) the task | Function | No |
| - taskId | Upload task number | String | No |
| onProgress | Progress callback function. Attributes of the progress callback response object, `progressData`, are as follows | Function | No |
| - progressData.loaded | Size of the file part that has been uploaded; unit: byte | Number | No |
| - progressData.total | Size of the entire file in bytes | Number | No |
| - progressData.speed | File upload speed in bytes/s | Number | No |
| - progressData.percent | Percentage of file upload progress in decimal form; for example, 0.5 means 50% downloaded | Number | No |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - ETag | Returns the MD5 checksum of the file. The value of `ETag` can be used to check whether the object gets corrupted during the upload. <br>For example, `"09cba091df696af91549de27b8e7d0f6"`. **Note: Double quotation marks are required at the beginning and the end of the `ETag` value string here** | String |
| - Location | Creates an object's access domain name for external network | String |
| - VersionId | Uploads an object in a version control-enabled bucket returns the version ID of the object. This parameter is not returned if the bucket has never been enabled | String |

### Uploading an object using a form

The SDK for Node.js does not provide a method for the `POST Object` API. If you need to use this API, see "Solution B: Upload with Form" in [Practice of Direct Transfer for Web End](https://intl.cloud.tencent.com/document/product/436/9067).

### Querying object metadata

#### Feature

This API (HEAD Object) is used to query object metadata.

#### Samples

[//]: # (.cssg-snippet-head-object)
```js
cos.headObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
    Key: 'exampleobject', /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| --------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Region and Domain Nam Access](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (Object name), the unique identifier of the object in the bucket, see [Object Overview] details(https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| IfModifiedSince | If the object is modified after the specified time, the corresponding object metadata will be returned; otherwise, 304 will be returned | String | No |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200 and 304. If no modification is made after the specified time, 304 will be returned | Number |
| - headers | Header information returned by the request | Object |
| - x-cos-object-type | Indicates whether an object can be appended to an upload operation. Enumerated values: `normal`, `appendable` | String |
| - x-cos-storage-class | Object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE` | String |
| - x-cos-meta-* | User-defined metadata | String |
| - NotModified | Whether an object is unmodified after the specified time | Boolean |
| - ETag | Returns the MD5 checksum of the file. The value of `ETag` can be used to check whether the object gets corrupted during the upload. <br>For example, `"09cba091df696af91549de27b8e7d0f6"`. **Note: Double quotation marks are required at the beginning and the end of the `ETag` value string here** | String |
| - VersionId | Uploads an object in a version control-enabled bucket returns the version ID of the object. This parameter is not returned if the bucket has never been enabled | String |

### Downloading an object

This API is used to download an object in a COS bucket to a local file system. To make this request, you need to have Read access to the target object or the target object allows Public Read.

#### Samples

[//]: # (.cssg-snippet-get-object)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
    Key: 'exampleobject', /*Required*/
}, function(err, data) {
    console.log(err || data.Body);
});
```

Get file content with `Range` specified:

[//]: # (.cssg-snippet-get-object-range)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
    Key: 'exampleobject', /*Required*/
    Range: 'bytes=1-3', /*Optional*/
}, function(err, data) {
    console.log(err || data.Body);
});
```

Download the file to a specified path:

[//]: # (.cssg-snippet-get-object-path)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
    Key: 'exampleobject', /*Required*/
    Output: './exampleobject',
}, function(err, data) {
    console.log(err || data);
});
```

Download the file to a specified write file stream:

[//]: # (.cssg-snippet-get-object-stream)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
    Key: 'exampleobject', /*Required*/
    Output: fs.createWriteStream('./exampleobject'),
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| -------------------------- | ------------------------------------------------------------ | ------------------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Region and Domain Nam Access](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (Object name), the unique identifier of the object in the bucket, see [Object Overview] details(https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| Output | An output file path or a write stream. If this parameter is not passed in, the full content will be written to `data` in the callback function | String/WriteStream | No |
| ResponseContentType | Sets the Content-Type parameter in the response header | String | No |
| ResponseContentLanguage | Sets the Content-Language parameter in the response header | String | No |
| ResponseExpires | Sets the Content-Expires parameter in the response header | String | No |
| ResponseCacheControl | Sets the Cache-Control parameter in the response header | String | No |
| ResponseContentDisposition | Sets the Content-Disposition parameter in the response header | String | No |
| ResponseContentEncoding | Sets the Content-Encoding parameter in the response header | String | No |
| Range | Byte range of the object. The range value must be in the format of bytes=first-last, where both first and last are offsets starting from 0. For example, bytes=0-9 means that you want to copy the first 10 bytes of data of the source object. If this parameter is not specified, the entire object will be read | String | No |
| If-Modified-Since | If the object is modified after the specified time, the object will be returned; otherwise, HTTP status code 304 (Not Modified) will be returned | String | No |
| If-Unmodified-Since | If the object is not modified after the specified time, the object will be returned; otherwise, HTTP status 412 (Precondition Failed) will be returned | String | No |
| IfMatch | The file will be returned only if ETag matches the specified content; otherwise, 412 (precondition failed) will be returned | String | No |
| IfNoneMatch | The file will be returned only if ETag does not match the specified content; otherwise, 304 (not modified) will be returned | String | No |
| VersionId | Specifies the version ID of the object to be downloaded | String | No |
| onProgress | Progress callback function. Attributes of the progress callback response object, `progressData`, are as follows | Function | No |
| - progressData.loaded | Size of the file part that has been downloaded; unit: byte | Number | No |
| - progressData.total | Size of the entire file; unit: byte | Number | No |
| - progressData.speed | File download speed; unit: bytes/s | Number | No |
| - progressData.percent | A decimal representing the file download progress. For example, 0.5 means 50% has been downloaded | Number | No |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| Cache-Control | Cache directives as defined in RFC 2616, which will be returned only if it is contained in the object metadata or specified through the request parameter | string |
| Content-Disposition | Filename as defined in RFC 2616, which will be returned only if it is contained in the object metadata or specified through the request parameter | string |
| Content-Encoding | Encoding format as defined in RFC 2616, which will be returned only if it is contained in the object metadata or specified through the request parameter | string |
| Expires | Cache expiration time as defined in RFC 2616, which will be returned only if it is contained in the object metadata or specified through the request parameter | string |
| x-cos-storage-class | Storage class of the object. Enumerated values: `STANDARD`, `STANDARD_IA`. <br>**Note: If this header is not returned, it means the file storage class is `STANDARD` (standard storage)** | String |
| - x-cos-meta-* | User-defined metadata | String |
| - NotModified | This attribute will be returned if the request carries `IfModifiedSince`. If the file has not been modified, `true` will be returned; otherwise, `false` will be returned | Boolean |
| - ETag | Returns the MD5 checksum of the file. The value of `ETag` can be used to check whether the object gets corrupted during the upload. <br>For example, `"09cba091df696af91549de27b8e7d0f6"`. **Note: Double quotation marks are required at the beginning and the end of the `ETag` value string here** | String |
| - VersionId | Uploads an object in a version control-enabled bucket returns the version ID of the object. This parameter is not returned if the bucket has never been enabled | String |
| - Body | Returned file content, default is Buffer | Buffer |

### Pre-requesting cross-origin configuration

#### Feature

This API (OPTIONS Object) is used to implement a pre-request for cross-origin object access configuration. Before making a real cross-origin resource sharing (CORS) request, you can send an `OPTIONS` request carrying the specific source origin, HTTP method, and header information to COS for it to determine whether a real request can be sent. If there is no CORS configuration, `403 Forbidden` will be returned. **You can enable CORS for a bucket using the `PUT Bucket cors` API**.

#### Samples

[//]: # (.cssg-snippet-option-object)
```js
cos.optionsObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
    Key: 'exampleobject', /*Required*/
    Origin: 'https://www.qq.com', /*Required*/
    AccessControlRequestMethod: 'PUT', /*Required*/
    AccessControlRequestHeaders: 'origin,accept,content-type' /*Optional*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Region and Domain Nam Access](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (Object name), the unique identifier of the object in the bucket, see [Object Overview] details(https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| Origin | Source origin of the simulated cross-origin access request | String | Yes |
| AccessControlRequestMethod | HTTP method of the simulated cross-origin access request | String | Yes |
| AccessControlRequestHeaders | Headers of the simulated cross-origin access request | String | No |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ---------------------------- | ------------------------------------------------------------ | ------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - headers | Header information returned by the request | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - AccessControlAllowOrigin | Source origins of the simulated cross-origin access request separated by commas. This header will not be returned if the origins are not allowed. Example: `*` | String |
| - AccessControlAllowMethods | HTTP methods of the simulated cross-origin access request separated by commas, such as PUT, GET, POST, DELETE, and HEAD. This header will not be returned if the request method is not allowed | String |
| - AccessControlAllowHeaders | Headers of the simulated cross-origin access request separated by commas, such as accept, content-type, origin, and authorization. This request header will not be returned if any of the simulated headers is not allowed | String |
| - AccessControlExposeHeaders | Headers that can be returned by CORS, separated by commas, such as ETag | String |
| - AccessControlMaxAge | Sets the validity period of the `OPTIONS` request result, such as `3600` | String  |
| - OptionsForbidden | Whether the `OPTIONS` request is forbidden, which will be `true` if the returned HTTP status code is `403` | Boolean |

### Replicating Objects

#### Feature

This API (PUT Object-Copy) is used to create a copy of an existing COS object, that is, an object is copied from the source path (object key) to the destination path (object key). During replication, object metadata and access control lists (ACLs) can be modified.
Users can use this API to create a copy, modify object meta attributes (source object and destination file have the same attributes), move or rename the object (copy first, and then call the delete API separately).

> We recommend an object size between 1MB-5GB. For objects greater than 5GB, please use the advanced APIs to copy the object [Slice Copy File](#. E5.A4.8D.E5.88.B6.E5.AF.B9.E8.B1.A12) .

#### Samples

[//]: # (.cssg-snippet-copy-object)
```js
cos.putObjectCopy({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
    Key: 'exampleobject', /*Required*/
    CopySource: 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject', /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Region and Domain Nam Access](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (Object name), the unique identifier of the object in the bucket, see [Object Overview] details(https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| CopySource | URL path to the source object. A historical version can be specified with the URL parameter ?versionId=\<versionId> | String | Yes |
| x-cos-acl | Defines the access control list (ACL) attribute of the object. For the enumerated values such as `default`, `private`, and `public-read`, see the Preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: default <br>**Note:** Currently, there can be up to 1,000 entries in one ACL. If you do not need access control for the object, set `default` for this parameter or simply leave it blank, and the object will inherit the permissions of the bucket | Enum | No |
| GrantReadAcp | Grants the grantee Read access to ACL and policies in the format of `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantWrite | Grants the grantee Write access in the format of `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantFullControl | Grants the grantee Read/Write access in the format of `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| MetadataDirective | Whether to copy the metadata. Enumerated values: `Copy`, `Replaced`. Default value: `Copy`. If its value is `Copy`, the user metadata in the corresponding header will be ignored and the copy will be performed; if its value is `Replaced`, the metadata will be replaced by the information in the corresponding header. **If the destination path is the same as the source path, which means you want to modify the metadata, you must specify this parameter as `Replaced`** | String | No |
| CopySourceIfModifiedSince | If the object is modified after the specified time, the operation will be performed; otherwise, `412` will be returned. **This parameter can be used together with `CopySourceIfNoneMatch`. If it is used together with other conditions, a conflict will be returned** | String | No |
| CopySourceIfUnmodifiedSince | If the object is not modified after the specified time, the operation will be performed; otherwise, `412` will be returned. **This parameter can be used together with `CopySourceIfMatch`. If it is used together with other conditions, a conflict will be returned** | String | No |
| CopySourceIfMatch | If the `Etag` of the object is the same as the specified one, the operation will be performed; otherwise, `412` will be returned. **This parameter can be used together with `CopySourceIfUnmodifiedSince`. If it is used together with other conditions, a conflict will be returned** | String | No |
| CopySourceIfNoneMatch | If the `Etag` of the object is different from the specified one, the operation will be performed; otherwise, `412` will be returned. **This parameter can be used together with `CopySourceIfModifiedSince`. If it is used together with other conditions, a conflict will be returned** | string | No |
| StorageClass | Sets the object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String | No |
| x-cos-meta-* | Other user-defined file headers | String | No |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - ETag | MD5 checksum of the file, such as `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end** | String |
| - LastModified | Describes the last modified time of the object, such as `2017-06-23T12:33:27.000Z` | String |
| - VersionId | Uploads an object in a version control-enabled bucket returns the version ID of the object. This parameter is not returned if the bucket has never been enabled | String |

### Deleting a single object

#### Feature

This API is used to delete an object from a COS bucket. To make this request, you need to have the permission to write to the bucket.

#### Samples

[//]: # (.cssg-snippet-delete-object)
```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
    Key: 'exampleobject' /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Region and Domain Nam Access](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (Object name), the unique identifier of the object in the bucket, see [Object Overview] details(https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| - VersionId | Version ID of the object or the delete marker to be deleted | String | No |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 204, 403, and 404. **If the deletion is successful or the file does not exist, 204 or 200 will be returned; if the specified bucket is not found, 404 will be returned** | Number |
| - headers | Header information returned by the request | Object |

### Deleting multiple objects

#### Feature

This API (DELETE Multiple Objects) is used to delete multiple objects in a single request. You can delete up to 1,000 objects in a single request. For the response, there are two modes for you to choose from: Verbose and Quiet. Verbose mode returns the information on the deletion of each object, whereas Quiet mode only returns the information on objects for which errors are reported.

#### Samples

Deleting multiple files:

[//]: # (.cssg-snippet-delete-multi-object)
```js
cos.deleteMultipleObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
    Objects: [
        Key='exampleobject',
        'Key': 'exampleobject2',
    ]
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ----------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Region and Domain Nam Access](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Quiet | A boolean value which determines whether to enable Quiet mode. If the value is true, Quiet mode is enabled; if it is false, Verbose mode is enabled. The default value is false | Boolean | No |
| Objects | List of files to be deleted | ObjectArray | Yes |
| Key | Object key (Object name), the unique identifier of the object in the bucket, see [Object Overview] details(https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| - VersionId | Version ID of the object or the delete marker to be deleted | String | No |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - Deleted | List of object information indicating successful deletion | ObjectArray |
| Key | Object key (Object name), the unique identifier of the object in the bucket, see [Object Overview] details(https://intl.cloud.tencent.com/document/product/436/13324) for details | String |
| - - VersionId | If the `VersionId` parameter is passed in, it will also be included in the response, indicating the version of the operated object or delete marker | String |
| - - DeleteMarker | If versioning is enabled and the `VersionId` parameter is not specified, the deletion will not actually erase the content of a file; instead, it will only add a new delete marker, indicating that the visible file has been deleted. Enumerated values: `true`, `false` | String |
| - - DeleteMarkerVersionId | If the value of the returned `DeleteMarker` is `true`, this parameter will be returned, representing the `VersionId` of the newly added delete marker | String |
| - Error | List of object information indicating deletion failure | ObjectArray |
| Key | Object key (Object name), the unique identifier of the object in the bucket, see [Object Overview] details(https://intl.cloud.tencent.com/document/product/436/13324) for details | String |
| - - Code | Error code of the deletion failure | String |
| - - Message | Error message of the deletion failure | String |

## Multipart Operations

### Querying multipart upload

#### Feature

This API (List Multiparts Uploads) is used to query the ongoing multipart uploads. A single request operation can list up to 1,000 multipart uploads.

#### Samples

Get the list of unfinshed UploadIds prefixed with exampleobject, for example:

[//]: # (.cssg-snippet-list-multi-upload)
```js
cos.multipartList({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
    Prefix: 'exampleobject', /*Optional*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Region and Domain Nam Access](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Prefix | Matching prefix for object keys, which sets that the response only contains object keys with the specified prefix. Note that when you make a query with the prefix specified, the returned keys will still contain `Prefix` | String | No |
| Delimiter | A delimiter is a separating symbol used to group object keys. It is usually `/`. The identical paths between `Prefix` or, if no `Prefix` is specified, the beginning and the first `delimiter` are grouped and defined as a common prefix. All common prefixes will be listed. | String | No |
| EncodingType | Specifies the encoding method of the return value; value range: url | String | No |
| MaxUploads | Sets the maximum number of entries returned; value range: 1-1,000. Default value: 1,000 | String | No |
| KeyMarker | Used together with `upload-id-marker`. <br> <li>If `upload-id-marker` is not specified: <br>&emsp;- only the multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed. <br><li>If `upload-id-marker` is specified: <br>&emsp;- the multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed; <br>&emsp;- and the multipart uploads whose `ObjectName` is equal to the `key-marker` will also be listed, provided that their `UploadID` is greater than the specified `upload-id-marker` | String | No |
| UploadIdMarker | Used together with `key-marker`. <br><li>If `key-marker` is not specified: <br>&emsp;- `upload-id-marker` will be ignored. <br><li>If `key-marker` is specified: <br>&emsp;- the multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed; <br>&emsp;- and the multipart uploads whose `ObjectName` is equal to the `key-marker` will also be listed, provided that their `UploadID` is greater than the specified `upload-id-marker` | String | No |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| -------------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - Bucket | Destination bucket for the multipart upload | String |
| - Encoding-Type | Specifies the encoding type of the returned values; valid value: `url` | String |
| - KeyMarker | The key value where the entry list starts | String |
| - UploadIdMarker | The `UploadId` value where the entry list starts | String |
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
| - - Initiator | Information on the initiator of this upload | Object |
| - - - DisplayName | Name of the upload initiator | String |
| - - - ID | ID of the upload initiator in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`. <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String |
| - - Owner | Information on the owner of the parts | Object  |
| - - - DisplayName | Part owner name | String |
| - - - ID | Part owner ID in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`.<br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String |
| - - Initiated | Starting time of the multipart upload | String |

### Initializing multipart upload

#### Feature

This API (Initiate Multipart Upload) is used to initialize a multipart upload. After a successful operation, an upload ID will be returned which can be used in the subsequent `Upload Part` requests.

#### Samples

[//]: # (.cssg-snippet-init-multi-upload)
```js
cos.multipartInit({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
    Key: 'exampleobject', /*Required*/
}, function(err, data) {
    console.log(err || data);
    if (data) {
      UploadId=uploadid,
    }
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Region and Domain Nam Access](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (Object name), the unique identifier of the object in the bucket, see [Object Overview] details(https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| CacheControl | Cache policy as defined in RFC 2616, which will be stored in the object metadata | String | No |
| Content-Disposition | Filename as defined in RFC 2616, which will be stored in the object metadata | String | No |
| Content-Encoding | Encoding format as defined in RFC 2616, which will be stored in the object metadata | String | No |
| ContentType | Content type (MIME) as defined in RFC 2616, which will be stored as the object's metadata | String | No |
| Expires | Cache expiration time as defined in RFC 2616, which will be stored in the object metadata | String | No |
| x-cos-acl | Defines the access control list (ACL) attribute of the object. For the enumerated values such as `default`, `private`, and `public-read`, see the Preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: default <br>**Note:** Currently, there can be up to 1,000 entries in one ACL. If you do not need access control for the object, set `default` for this parameter or simply leave it blank, and the object will inherit the permissions of the bucket | Enum | No |
| GrantRead | Grants the grantee Read access in the format of `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantFullControl | Grants the grantee Read/Write access in the format of `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| StorageClass | Sets the object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String | No |
| x-cos-meta-* | Headers that can be defined by users, which will be returned as the object metadata; maximum size: 2 KB | String | No |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
string bucket = "examplebucket-1250000000";Bucket. Format: BucketName-APPID
| Key | Object key (Object name), the unique identifier of the object in the bucket, see [Object Overview] details(https://intl.cloud.tencent.com/document/product/436/13324) for details | String |
| UploadId | ID that can be used in subsequent uploads | String |

### Uploading Parts

#### Feature

This API (Upload Part) is used to upload parts after a multipart upload is initialized. It can upload up to 10,000 parts of 1 MB to 5 GB each in size.
You can obtain an uploadId when you use the API "Initiate Multipart Upload" to initiate multipart upload. This ID exclusively identifies this multipart data, and the relative position of this multipart in the entire file.
2. Every time you request the `Upload Part` API, you need to pass in `partNumber`, the part number, and `uploadId`. You can upload multiple parts out of order.
3. When the `uploadId` and `partNumber` of a new part are the same as those of a previously uploaded part, the old part will be overwritten by the new one. A 404 error, `NoSuchUpload`, will be returned if the `uploadId` does not exist.

#### Samples

[//]: # (.cssg-snippet-upload-part)
```js
const filePath = "temp-file-to-upload" // Local file path
cos.multipartUpload({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
    Key: 'exampleobject', /*Required*/
    ContentLength='123',
    UploadId: 'exampleUploadId',
    'PartNumber': 1
    Body: fs.createReadStream(filePath)
}, function(err, data) {
    console.log(err || data);
    if (data) {
      eTag = data.ETag;
    }
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------------- | ------------------------------------------------------------ | ---------------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Region and Domain Nam Access](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (Object name), the unique identifier of the object in the bucket, see [Object Overview] details(https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| ContentLength | HTTP request length in bytes as defined in RFC 2616 | String | Yes |
| PartNumber | Part number | String | Yes |
| UploadId | The number of this multipart upload task | String | Yes |
| Body | Content of the file part to be uploaded, which can be a string, a File object, or a Blob object | String\File\Blob | Yes |
| Expect | If `Expect: 100-continue` is used, the request content will be sent only after confirmation from the server is received | String | No |
| ContentMD5 | Base64-encoded 128-bit content MD5 checksum as defined in RFC 1864. This header is used to check whether the file content has changed | String | No |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

### Copying Parts

#### Feature

This API (Upload Part - Copy) is used to copy the parts of an object from a source path to a destination path.

>- To upload an object in parts, you must first initialize the multipart upload. A unique descriptor (upload ID) will be returned in the response of multipart upload initialization, which needs to be carried in the multipart upload request.

#### Samples

[//]: # (.cssg-snippet-upload-part-copy)
```js
cos.uploadPartCopy({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
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

#### Parameter Description

| Parameter Name | Description | Type | Required |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Region and Domain Nam Access](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (Object name), the unique identifier of the object in the bucket, see [Object Overview] details(https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| CopySource | URL path to the source object. A historical version can be specified with the URL parameter ?versionId=\<versionId> | String | Yes |
| PartNumber | Part number | String | Yes |
| uploadId | To upload an object in parts, you must first initialize the multipart upload. The response of the multipart upload initialization will return a unique descriptor, an upload ID, which needs to be carried in the multipart upload request | String | Yes |
| CopySourceRange | Byte range of the source object. The range value must be in the format of `bytes=first-last`, where both `first` and `last` are offsets starting from 0. For example, `bytes=0-9` means that you want to copy the first 10 bytes of data of the source object. If this parameter is not specified, the entire object will be copied | String | No |
| CopySourceIfMatch | If the `Etag` of the object is the same as the specified one, the operation will be performed; otherwise, `412` will be returned. This parameter can be used together with `x-cos-copy-source-If-Unmodified-Since`. If it is used together with other conditions, a conflict will be returned | String | No |
| CopySourceIfNoneMatch | If the `Etag` of the object is different from the specified one, the operation will be performed; otherwise, `412` will be returned. This parameter can be used together with `x-cos-copy-source-If-Modified-Since`. If it is used together with other conditions, a conflict will be returned | string | No |
| CopySourceIfUnmodifiedSince | If the object is not modified after the specified time, the operation will be performed; otherwise, `412` will be returned. This parameter can be used together with `x-cos-copy-source-If-Match`. If it is used together with other conditions, a conflict will be returned | String | No |
| CopySourceIfModifiedSince | If the object is modified after the specified time, the operation will be performed; otherwise, `412` will be returned. This parameter can be used together with `x-cos-copy-source-If-None-Match`. If it is used together with other conditions, a conflict will be returned | String | No |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - ETag | MD5 checksum of the file, such as `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end** | String |
| - LastModified | Returns the last modified time of the object in GMT time | String |

### Querying uploaded parts

#### Feature

This API (List Parts) is used to query the uploaded parts in a specified multipart upload, i.e., listing all the successfully uploaded parts in the multipart upload with the specified `UploadId`.

#### Samples

[//]: # (.cssg-snippet-list-parts)
```js
cos.multipartListPart({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
    Key: 'exampleobject', /*Required*/
    UploadId: 'exampleUploadId', /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ---------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Region and Domain Nam Access](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (Object name), the unique identifier of the object in the bucket, see [Object Overview] details(https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| UploadId | ID of this multipart upload. When the `Initiate Multipart Upload` API is used to initialize a multipart upload, an `uploadId` will be returned. The ID uniquely identifies the data of the part and its position in the entire file | String | Yes |
| EncodingType | Specifies the encoding type of the returned value | String | No |
| MaxParts | Maximum number of entries returned at a time. Default value: 1,000 | String | No |
| PartNumberMarker | By default, entries are listed in UTF-8 binary order starting from the marker | String | No |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ---------------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - Bucket | Destination bucket for the multipart upload | String |
| - Encoding-type | Specifies the encoding type of the returned value | String |
| Key | Object key (Object name), the unique identifier of the object in the bucket, see [Object Overview] details(https://intl.cloud.tencent.com/document/product/436/13324) for details | String |
| - UploadId | Identifies the ID of this multipart upload | String |
| - Initiator | Identifies the initiator of this upload | Object |
| - - DisplayName | Name of the upload initiator | String |
| - - ID | ID of the upload initiator in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String |
| - Owner | Information on the owner of the parts | Object  |
| - - - DisplayName | Bucket owner name | String |
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

### Completing multipart upload

#### Feature

This API (Complete Multipart Upload) is used to complete a multipart upload. After all parts are uploaded via the `Upload Part` API, you need to call this API to complete the multipart upload. When using this API, you need to specify the `PartNumber` and `ETag` of each part in the request body for the part information to be verified.
As the parts need to be merged after they are uploaded, and the merge takes several minutes, when the merge starts, COS will immediately return status code 200 and periodically return space information during the merge process to keep the connection active until the merge is completed. After that, COS will return the content of the merged parts in the body.

- If the uploaded part size is below 1 MB, 400 EntityTooSmall will be returned when this API is called.
- If the uploaded part numbers are not continuous, 400 InvalidPart will be returned when this API is called.
- If the part information entries in the request body are not sorted by number in ascending order, 400 InvalidPartOrder will be returned when this API is called.
- If the `UploadId` does not exist, `404 NoSuchUpload` will be returned when this API is called.

>We recommend you either complete or abort a multipart upload as early as possible, as the uploaded parts of an incomplete multipart upload will take up storage capacity and incur storage fees.

#### Samples

[//]: # (.cssg-snippet-complete-multi-upload)
```js
cos.multipartComplete({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
    Key: 'exampleobject', /*Required*/
    UploadId: 'exampleUploadId', /*Required*/
    Parts: [
        {PartNumber: '1', ETag: 'exampleETag'},
    ]
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ----------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Region and Domain Nam Access](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (Object name), the unique identifier of the object in the bucket, see [Object Overview] details(https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| UploadId | Upload task number | String | Yes |
| Parts | List of information on the parts in this multipart upload | ObjectArray | Yes |
| - PartNumber | Part number | String | Yes |
| - ETag | MD5 checksum of each part. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end** | String | Yes |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - Location | Creates an object's access domain name for external network | String |
| - Bucket | Destination bucket for the multipart upload | String |
| Key | Object key (Object name), the unique identifier of the object in the bucket, see [Object Overview] details(https://intl.cloud.tencent.com/document/product/436/13324) for details | String |
| - ETag | Unique ID of the merged file in the format of `"uuid-<part quantity>"`. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`. **Note that double quotation marks are required at the beginning and the end** | String |

### Terminating multipart upload

#### Feature

This API (Abort Multipart Upload) is used to abort a multipart upload and delete the uploaded parts. If you call this API and there is an `Upload Part` request that is using the multipart upload, the request will fail. If the `uploadId` does not exist, `404 NoSuchUpload` will be returned.

>We recommend you either complete or abort a multipart upload as early as possible, as the uploaded parts of an incomplete multipart upload will take up storage capacity and incur storage fees.

#### Samples

[//]: # (.cssg-snippet-abort-multi-upload)
```js
cos.multipartAbort({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
    Key: 'exampleobject', /*Required*/
    UploadId: 'exampleUploadId' /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Region and Domain Nam Access](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (Object name), the unique identifier of the object in the bucket, see [Object Overview] details(https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| UploadId | ID of this multipart upload. When the `Initiate Multipart Upload` API is used to initialize a multipart upload, an `uploadId` will be returned. The ID uniquely identifies the data of the part and its position in the entire file | String | Yes |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

## Other Operations

### Restoring archived object

#### Feature

This API is used to restore an object archived by COS. The restored readable object is temporary, and you can make configuration to keep it readable and set the time when you want it to be deleted. You can use the `Days` parameter to specify the expiration time of the temporary object. If the object expires and you have not initiated any operation to copy the object or extend its validity period before the expiration, the temporary object will be automatically deleted. A temporary object is only a copy of the source archived object and the source object will exist throughout the period.

#### Samples

[//]: # (.cssg-snippet-restore-object)
```js
cos.restoreObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
    Key='exampleobject',
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
| ------------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Region and Domain Nam Access](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (Object name), the unique identifier of the object in the bucket, see [Object Overview] details(https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| RestoreRequest | Container used for data restoration | Object | Yes |
| - Days | Sets the expiration time of a temporary copy | Number | Yes |
| - CASJobParameters | Container of the Cloud Archive Storage job parameters | Object | Yes |
| - - Tier | This parameter can be specified as one of the three data restoration modes supported by CAS: `Standard`, standard mode where a restoration job can be completed in 3-5 hours; `Expedited`, expedited mode where a restoration job can be completed in 15 minutes; and `Bulk`, batch mode where a restoration job can be completed in 5-12 hours | Integer | Yes |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

### Setting object ACL

#### Feature

This API (PUT Object acl) is used to set the access control list (ACL) of an object in a specific bucket.

> The total number of policies associated with bucket ACL, Policy, and CAM under a single root account (i.e., under the same APPID) cannot exceed 1,000. There is no upper limit on the number of object ACL rules. If you do not need access control for an object, do not make the configuration, and the object will inherit the permissions of its bucket.

#### Samples

[//]: # (.cssg-snippet-put-object-acl)
```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
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
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
    Key: 'exampleobject', /*Required*/
    GrantFullControl: 'id="100000000001"' // 100000000001 is the UIN of the root account
}, function(err, data) {
    console.log(err || data);
});
```

Grant an object write permissions via AccessControlPolicy:

[//]: # (.cssg-snippet-put-object-acl-acp)
```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
    Key: 'exampleobject', /*Required*/
    AccessControlPolicy: {
        "Owner": { // `Owner` is required in `AccessControlPolicy`
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

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Region and Domain Nam Access](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (Object name), the unique identifier of the object in the bucket, see [Object Overview] details(https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| x-cos-acl | Defines the access control list (ACL) attribute of the object. For the enumerated values such as `default`, `private`, and `public-read`, see the Preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: default <br>**Note:** Currently, there can be up to 1,000 entries in one ACL. If you do not need access control for the object, set `default` for this parameter or simply leave it blank, and the object will inherit the permissions of the bucket | Enum | No |
| GrantReadAcp | Grants the grantee Read access to ACL and policies in the format of `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantFullControl | Grants the grantee Read/Write access in the format of `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| AccessControlPolicy | Sets an object's access control list (ACL) attributes information | Object | No |
| - Owner | Object owner information | Object | No |
| - - - ID | User ID in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String | No |
| - - - DisplayName | Part owner name | String |
| - Grants | List of information on the grantee and permissions | ObjectArray | No |
| - - Permission | Specifies the permission granted to the grantee. Enumerated values: `READ`, `WRITE`, `READ_ACP`, `WRITE_ACP`, `FULL_CONTROL` | String | No |
| - - Grantee | Grantee Information | Object | No |
| - - - DisplayName | Grantee Name | String | No |
| - - - ID | User ID in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String | No |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

### Querying object ACL

#### Feature

This API is used to get the access permissions on a specified object in a specified bucket. Only the bucket owner has the permission to perform this operation.

#### Samples

[//]: # (.cssg-snippet-get-object-acl)
```js
cos.getObjectAcl({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
    Key: 'exampleobject', /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Region and Domain Nam Access](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (Object name), the unique identifier of the object in the bucket, see [Object Overview] details(https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Parameter Description                                                     | Type |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| x-cos-acl | Defines the access control list (ACL) attribute of the bucket. For the enumerated values such as `private` and `public-read`, see the “Preset ACL for buckets” section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: `private` | Enum | No |
| - Owner | Identifies owner of the resource | Object |
| - - - ID | User ID in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String |
| - - DisplayName | Object owner name | String |
| - Grants | List of information on the grantee and permissions | ObjectArray |
| - - Permission | Specifies the permission granted to the grantee. Enumerated values: `READ`, `WRITE`, `READ_ACP`, `WRITE_ACP`, `FULL_CONTROL` | String | No |
| - - Grantee | Grantee Information | Object |
| - - - DisplayName | User Name | String |
| - - - ID | User ID in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String |

## Advanced APIs (Recommended)

The following methods encapsulate the native methods mentioned above. They can implement the complete process of multipart upload/copy and support concurrent multipart upload/copy, checkpoint restart as well as cancelling, pausing, and restarting upload tasks.

### Uploading objects by parts

#### Feature

This API (Slice Upload File) is used to upload large files in parts.

#### Samples

[//]: # (.cssg-snippet-transfer-upload-object)
```js
const filePath = "temp-file-to-upload" // Local file path
cos.sliceUploadFile({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
    Key: 'exampleobject', /*Required*/
    FilePath: filePath, /*Required*/
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

| Parameter Name | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Region and Domain Nam Access](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (Object name), the unique identifier of the object in the bucket, see [Object Overview] details(https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| FilePath | Path to the file to be uploaded | String | Yes |
| SliceSize | Part size | String | No |
| AsyncLimit | Concurrent number of parts being uploaded | String | No |
| - StorageClass | Object storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE` | String |
| TaskReady | Callback function when an upload task is created. The callback returns a `taskId`, which uniquely identifies the task and can be used to cancel (cancelTask), pause (pauseTask), or restart (restartTask) the task | Function | No |
| - taskId | Upload task number | String | No |
| onHashProgress | Progress callback function for file MD5 value calculation. The callback parameter is the progress object `progressData` | Function | No |
| - progressData.loaded | Size of the file part that has been verified; unit: byte | Number | No |
| - progressData.total | Size of the entire file in bytes | Number | No |
| - progressData.speed | File verification speed; unit: bytes/s | Number | No |
| - progressData.percent | A decimal representing the file verification progress; for example, 0.5 means 50% verified | Number | No |
| onProgress | Progress callback function for file upload. The callback parameter is the progress object `progressData` | Function | No |
| - progressData.loaded | Size of the file part that has been uploaded; unit: byte | Number | No |
| - progressData.total | Size of the entire file in bytes | Number | No |
| - progressData.speed | File upload speed in bytes/s | Number | No |
| - progressData.percent | Percentage of file upload progress in decimal form; for example, 0.5 means 50% downloaded | Number | No |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - Location | Creates an object's access domain name for external network | String |
| - Bucket | Destination bucket for the multipart upload | String |
| Key | Object key (Object name), the unique identifier of the object in the bucket, see [Object Overview] details(https://intl.cloud.tencent.com/document/product/436/13324) for details | String |
| - ETag | Unique ID of the merged file in the format of `"uuid-<part quantity>"`. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`. **Note that double quotation marks are required at the beginning and the end** | String |
| - VersionId | Uploads an object in a version control-enabled bucket returns the version ID of the object. This parameter is not returned if the bucket has never been enabled | String |

### Replicating Objects

#### Feature

This API (Slice Copy File) is used to copy a file from a source path to a destination path through multipart copy. Object metadata and ACL can be modified during the copy process. You can use this API to move, rename, and copy a file or modify its attributes.

#### Method Prototype

Call Slice Copy File:

[//]: # (.cssg-snippet-transfer-copy-object)
```js
cos.sliceCopyFile({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
    Key: 'exampleobject', /*Required*/
    CopySource: 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject', /*Required*/
    onProgress:function (progressData) { /*Optional*/
        console.log(JSON.stringify(progressData));
    }
},function (err,data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Region and Domain Nam Access](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (Object name), the unique identifier of the object in the bucket, see [Object Overview] details(https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| CopySource | URL path to the source object. A historical version can be specified with the URL parameter ?versionId=\<versionId> | String | Yes |
| ChunkSize | Size of the parts in the multipart copy; unit: byte. Default value: 1,048,576 (1 MB) | Number | No |
| SliceSize | Indicates multipart copy will be used when the file size exceeds a value, unit is byte, default value is 5G. If the value is less than or equal to 5G, putObjectCopy will be used for upload, otherwise sliceCopyFile will be used | Number | No | | Number | No |
| onProgress | Progress callback function for file upload. The callback parameter is the progress object `progressData` | Function | No |
| - progressData.loaded | Size of the file part that has been uploaded; unit: byte | Number | No |
| - progressData.total | Size of the entire file in bytes | Number | No |
| - progressData.speed | File upload speed in bytes/s | Number | No |
| - progressData.percent | Percentage of file upload progress in decimal form; for example, 0.5 means 50% downloaded | Number | No |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - Location | Creates an object's access domain name for external network | String |
| - Bucket | Destination bucket for the multipart upload | String |
| Key | Object key (Object name), the unique identifier of the object in the bucket, see [Object Overview] details(https://intl.cloud.tencent.com/document/product/436/13324) for details | String |
| - ETag | MD5 checksum of the merged file. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end** | String |
| - VersionId  | Uploads an object in a version control-enabled bucket returns the version ID of the object. This parameter is not returned if the bucket has never been enabled | String |

### Batch Upload

#### Feature

Method 1:
You can call `putObject` and `sliceUploadFile` multiple times to implement batch uploads. You can instantiate `FileParallelLimit` parameter to limit how many files can be uploaded at the same time, which is 3 by default.

Method 2:
You can call `cos.uploadFiles` to implement batch uploads. The `SliceSize` method parameter can be used to manage the files. Below are instructions on the `uploadFiles` method.

#### Method Prototype

Call the `uploadFiles` operation:

[//]: # (.cssg-snippet-batch-upload-objects)
```js
const filePath1 = "temp-file-to-upload" // Local file path
const filePath2 = "temp-file-to-upload" // Local file path
cos.uploadFiles({
    files: [{
        Bucket: 'examplebucket-1250000000',
        Region: 'COS_REGION',
        Key='exampleobject',
        FilePath: filePath1,
    }, {
        Bucket: 'examplebucket-1250000000',
        Region: 'COS_REGION',
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
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Region and Domain Nam Access](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (Object name), the unique identifier of the object in the bucket, see [Object Overview] details(https://intl.cloud.tencent.com/document/product/436/13324) for details | String | Yes |
| FilePath | Path to the file to be uploaded | String | Yes |
| SliceSize | Specifies the minimum file size in bytes for which multipart upload will be used. If the size of a file is equal to or smaller than this value, the file will be uploaded using `putObject`; otherwise, it will be uploaded using `sliceUploadFile` | Number | Yes |
| onProgress | Upload progress calculated by averaging out the progress of all tasks | String | Yes |
| - progressData.loaded | Size of the file part that has been uploaded; unit: byte | Number | No |
| - progressData.total | Size of the entire file in bytes | Number | No |
| - progressData.speed | File upload speed in bytes/s | Number | No |
| - progressData.percent | Percentage of file upload progress in decimal form; for example, 0.5 means 50% downloaded | Number | No |
| onFileFinish | The completion or error callback for each file | String | Yes |
| - err | Upload error message | Object | No |
| - data | File upload completion information | Object | No |
| - options | Parameter information on the files that have been uploaded | Object | No |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - files | error or data for each file | ObjectArray |
| - - err | Upload error message | Object |
| - - data | File upload completion information | Object |
| - - options | Parameter information on the files that have been uploaded | Object |

### Uploading Queue

The SDK for WeChat Mini Program recorded all the upload tasks initiated with `putObject` and `sliceUploadFile` in an upload queue. You can use the queue in the following ways:

1. Use cos.getTaskList to get the task list.
2. Use cos.pauseTask, cos.restartTask, and cos.cancelTask to perform operations on upload tasks.
3. cos.on('list-update', callback); can listen to the list and progress changes.

For a complete queue use case, see [Queue Demo](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/demo/queue).

#### Canceling an upload task

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

#### Pausing an upload task

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

#### Restarting an upload task

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
