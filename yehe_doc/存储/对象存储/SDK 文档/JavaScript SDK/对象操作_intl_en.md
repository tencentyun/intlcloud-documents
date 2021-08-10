## Overview

This document provides an overview of APIs and SDK code samples related to simple operations, multipart operations, and other object operations.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ---------------------------------------- |
| [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying an object list | Queries some or all objects in a bucket |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploads an object using simple upload | Uploads an object to a bucket |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | Uploading an object using an HTML form | Uploads an object using an HTML form |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |
| [OPTIONS Object](https://intl.cloud.tencent.com/document/product/436/8288) | Configuring a pre-flight request for cross-origin access | Sends a pre-flight request to confirm whether a real cross-origin access request can be sent |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object | Copies an object to the destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes an object from a bucket |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects in a single request |

**Multipart upload operations**

| API          | Operation                   | Description                                       |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries the information about ongoing multipart uploads |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload task |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading a part | Uploads a part in a multipart upload |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Uploads a part by copying data from an existing object as the data source |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries the uploaded parts of a specified multipart upload |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of an entire object |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload operation | Aborts a multipart upload operation and deletes the uploaded parts |

**Other Operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting object ACL | Sets the ACL of a specified object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying object ACL | Queries the ACL of an object |

## Simple operations

### Querying object list

#### API description

This API is used to query some or all objects in a bucket.

#### Samples

Sample 1. Listing all files in the `a` directory

[//]: # (.cssg-snippet-get-bucket)
```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000', /*Required*/
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

Sample 2. Listing the files in the `a` directory without deep traversal

[//]: # (.cssg-snippet-get-bucket-with-delimiter)
```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Prefix: 'a/',              /* Optional */
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

Sample 3. Listing all files in a directory

```js
var bucket = 'examplebucket-1250000000';
var region = 'ap-beijing';
var prefix = 'examplefolder/';  /* A directory/prefix to delete */
var listFolder = function(marker) {
    cos.getBucket({
        Bucket: bucket,
        Region: region,
        Prefix: prefix,
        Marker: marker,
        MaxKeys: 1000,
    }, function(err, data) {
        if (err) {
            return console.log('list error:', err);
        } else {
            console.log('list result:', data.Contents);
            if (data.IsTruncated === 'true') listFolder(data.NextMarker);
            else return console.log('list complete');
        }
    });
};
listFolder();
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Prefix | Matching prefix for object keys. This parameter specifies that the response can contain only object keys with the specified prefix. | String |
| Delimiter | Separating symbol used to group object keys. It is usually `/`. The identical paths between `Prefix` or, if no `Prefix` is specified, the beginning, and the first delimiter` are grouped and defined as a common prefix. All common prefixes will be listed. | String | No |
| Marker | Indicates where the object key listing begins. Entries are listed starting from the key after the `Marker` in UTF-8 lexicographical order by default. | String | No |
| MaxKeys | Maximum number of entries to return in a single response. Defaults to `1000`. | String | No |
| EncodingType | Encoding type of the returned value. Valid value: `url`, meaning that the returned object keys are URL-encoded (percent-encoded) values. For example, "Tencent Cloud" will be encoded to `%E8%85%BE%E8%AE%AF%E4%BA%91`. | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ----------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is left empty. | Object |
| - headers | Header information returned by the request | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - Name | Bucket name in the format of `BucketName-APPID`, such as `examplebucket-1250000000` | String |
| - Prefix | Matching prefix for object keys. Object key entries will be returned in UTF-8 lexicographical order, starting from the key after the marker. | String |
|  - Marker | By default, parts are listed in UTF-8 binary order, starting from the part after the marker. | String |
| - MaxKeys | Maximum number of entries returned in a single response | String |
| - Delimiter | Delimiter | String |
| - IsTruncated | Specifies whether returned entries are truncated. Valid values: `true`, `false` | String |
| - NextMarker | If returned entries are truncated, then `NextMarker` marks where the next listing should begin | String |
| - CommonPrefixes | The identical paths between a specified prefix and the delimiter are grouped and defined as a common prefix. | ObjectArray |
| - - Prefix | A single common prefix | String |
| - EncodingType | Encoding type of the returned values. This parameter is applicable to `Delimiter`, `Marker`, `Prefix`, `NextMarker`, and `Key`, | String |
| - Contents | A list of object metadata | ObjectArray |
| - - Key | Object key, i.e., object name | String |
| - - ETag | MD5 checksum of the object </br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end.** | String |
| - - Size | Object size, in bytes | String |
| - - LastModified  | Last modified time of the object, in ISO 8601 format, for example, `2019-05-24T10:56:40Z` | String |
| - - Owner | Information about the object owner | Object |
| - - - ID | Complete ID of the object owner in the format of `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]` </br>Example: `qcs::cam::uin/100000000001:uin/100000000001`, where 100000000001 is the UIN | String |
| - - - DisplayName | Name of the object owner | String |
| - - StorageClass | Storage class of the object. For the enumerated values, such as `STANDARD`, `STANDARD_IA`, `ARCHIVE`, and `DEEP_ARCHIVE`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String |

### Uploading an object using simple upload

#### API description

This API (PUT Object) is used to upload an object to a bucket. To call this API, you need to have permission to write to the bucket.

> !
> - The key (filename) cannot end with `/`; otherwise, it will be identified as a folder.
> - Each root account (`AAPID`) can have up to 1,000 bucket ACL rules and an unlimited number of object ACL rules. If you do not need an ACL for an object, you can choose not to configure an ACL for the object during upload. In this way, the object will inherit the permissions of its bucket by default.
> - After an object is uploaded, you can use the same key to generate a pre-signed URL, which can be shared with other clients for downloading (to download, please use the `GET` method. The detailed API description is shown below). If your file is set to private-read, note that the pre-signed URL will only be valid for a certain period of time.
> 

#### Sample

Simple upload is suitable for uploading small files.

[//]: # (.cssg-snippet-put-object)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    StorageClass: 'STANDARD',
    Body: fileObject, // Upload the file object.
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

Upload a string as the file content:

[//]: # (.cssg-snippet-put-object-string)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    Body: 'hello!',
}, function(err, data) {
    console.log(err || data);
});
```

Upload a Base64-encoded string as the file content:

[//]: # (.cssg-snippet-put-object-string)
```js
var base64Url = 'data:image/png;base64,iVBORw0KGgo.....';
var dataURLtoBlob = function (dataurl) {
    var arr = dataurl.split(',');
    var mime = arr[0].match(/:(.*?);/)[1];
    var bstr = atob(arr[1]);
    var n = bstr.length;
    var u8arr = new Uint8Array(n);
    while (n--) {
        u8arr[n] = bstr.charCodeAt(n);
    }
    return new Blob([u8arr], { type: mime });
};
// Convert to Blob for upload
var body = dataURLtoBlob(base64Url);
cos.putObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject.png',              /* Required */
    Body: body,
}, function(err, data) {
    console.log(err || data);
});
```

Create a directory:

[//]: # (.cssg-snippet-put-object-folder)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'examplefolder/',              /* Required */
    Body: '',
}, function(err, data) {
    console.log(err || data);
});
```

Upload a file to a specified directory:

```js
var folder = 'examplefolder/';
cos.putObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: folder + 'exampleobject',              /* Required */
    Body: fileObject, // Upload the file object.
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description


| Parameter | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | ---------------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| Body | Content of the file to be uploaded. This parameter can be a File object or a Blob object. | String\File\Blob | Yes |
| CacheControl | Cache policy as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentDisposition | Filename as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentEncoding | Encoding format as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentLength | HTTP request length (in bytes) as defined in RFC 2616 | String | No |
| ContentType | Content type (MIME) as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| Expires | Expiration time as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| Expect | If `Expect: 100-continue` is used, the request content will be sent only after confirmation from the server is received. | String | No |
| ACL | Defines the ACL attribute of the object. For the enumerated values, such as `default`, `private`, and `public-read`, please see the **Preset ACL** section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). <br/>**Note: if you do not need access control for the object, set `default` for this parameter or simply leave it blank. In this way, the object will inherit the permissions of the bucket.** | String | No |
| GrantRead              | Grants a user read permission for an object in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code></li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code><br/>Example: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul> | String               | No   |
| GrantReadAcp           | Grants a user read access to an object's ACL in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.<br/>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'`</li></ul> | String           | No   |
| GrantWriteAcp          | Grants a user write access to an object's ACL in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.<br/>Example: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul> | String           | No   |
| GrantFullControl       | Grants a user full access in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/<OwnerUin>:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.<br/>Example: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul> | String | No   |
| StorageClass | Storage class of the object. For the enumerated values, such as `STANDARD` (default), `STANDARD_IA`, `ARCHIVE`, and `DEEP_ARCHIVE`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String | No |
| x-cos-meta-\* | User-defined headers, which will be returned as the object metadata. The maximum size is 2 KB. | String | No |
| UploadAddMetaMd5 | Sets x-cos-meta-md5 as the object’s MD5 checksum in the object's metadata during upload in the format of a 32-bit lowercase string. Example: `4d00d79b6733c9cc066584a02ed03410` | String | No |
| TaskReady | Callback function when an upload task is created. The callback returns a `taskId`, which uniquely identifies the task and can be used to cancel (cancelTask), pause (pauseTask), or restart (restartTask) the task. | Function | No |
| - taskId | ID of the upload task | String | No |
| onProgress | Callback of the progress. The progress callback response object is `progressData`. | Function | No |
| - progressData.loaded | Size of the uploaded parts, in bytes | Number | No |
| - progressData.total | Size of the entire file, in bytes | Number | No |
| - progressData.speed | File upload speed, in bytes/s | Number | No |
| - progressData.percent | Percentage of the file upload progress, in decimal form. For example, 0.5 means 50% has been uploaded. | Number | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - ETag | MD5 checksum of the object. The value of this parameter can be used to check whether the object was corrupted during the upload. <br>Example: `"09cba091df696af91549de27b8e7d0f6"`. **Note that double quotation marks are required at the beginning and the end.** | String |
| - Location   | Location where the uploaded file can be accessed                                        | String |
| - VersionId       | Returns the version ID for versioning-enabled buckets. For buckets which have never had versioning enabled, this parameter is not returned | String  |

### Uploading an object using a form

The SDK for JS does not provide a method for the `POST Object` API. If you need to use this API, please see "Solution B: Upload with Form" in [Practice of Direct Transfer for Web End](https://intl.cloud.tencent.com/document/product/436/9067).

### Querying object metadata

#### API description

This API is used to query the metadata of an object.

#### Sample

[//]: # (.cssg-snippet-head-object)
```js
cos.headObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| --------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| IfModifiedSince | If the object is modified after the specified time, the corresponding object metadata will be returned; otherwise, 304 will be returned. | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this is left empty. | Object |
| - statusCode | HTTP status code returned by the request, such as 200 and 304. If no modification is made after the specified time, 304 will be returned. | Number |
| - headers | Header information returned by the request | Object |
| - x-cos-object-type | Indicates whether an object is appendable. Enumerated values: `normal`, `appendable`. The default value `normal` is not displayed if returned. | String |
| - x-cos-storage-class | Storage class of the object. For the enumerated values, such as `STANDARD` (default), `STANDARD_IA`, `ARCHIVE`, and `DEEP_ARCHIVE`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). Note that `STANDARD` is not displayed if returned. | String  |
| - x-cos-meta-\* | User-defined metadata | String |
| - NotModified | Indicates whether an object is unmodified after the specified time. | Boolean |
| - ETag | MD5 checksum of the object. The value of this parameter can be used to check whether the object was corrupted during the upload.<br>Example: `"09cba091df696af91549de27b8e7d0f6"`. **Note that double quotation marks are required at the beginning and the end.** | String |
| - VersionId       | Returns the version ID for versioning-enabled buckets. For buckets that have never had versioning enabled, this parameter is not returned. | String  |

### Downloading an object

>! This API is used to read object content. To download a file using your browser, you should first get a download URL through the `cos.getObjectUrl` method. For more information, please see [Pre-signed URLs](https://intl.cloud.tencent.com/document/product/436/31540).
>

#### API description

This API is used to get the content, in string format, of a specified file in a bucket.

#### Sample

[//]: # (.cssg-snippet-get-object)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
}, function(err, data) {
    console.log(err || data.Body);
});
```

Get the file content with `Range` specified:

[//]: # (.cssg-snippet-get-object-range)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    Range: 'bytes=1-3', /*Optional*/
}, function(err, data) {
    console.log(err || data.Body);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| ResponseContentType | Sets the `Content-Type` parameter in the response header. | String | No |
| ResponseContentLanguage | Sets the `Content-Language` parameter in the response header. | String | No |
| ResponseExpires | Sets the `Content-Expires` parameter in the response header. | String | No |
| ResponseCacheControl | Sets the `Cache-Control` parameter in the response header. | String | No |
| ResponseContentDisposition | Sets the `Content-Disposition` parameter in the response header. | String | No |
| ResponseContentEncoding | Sets the `Content-Encoding` parameter in the response header. | String | No |
| Range | Byte range of the object as defined in RFC 2616. The range value must be in the format of `bytes=first-last`, where both `first` and `last` are offsets starting from 0. For example, `bytes=0-9` means that you want to copy the first 10 bytes of data of the source object. If this parameter is not specified, the entire object will be downloaded. | String | No |
| IfModifiedSince | If the object is modified after the specified time, the object will be returned; otherwise, "304 (Not Modified)" will be returned. | String | No |
| If-Unmodified-Since | If the object is not modified after the specified time, the object will be returned; otherwise, "412 (precondition failed)" will be returned. | String | No |
| IfMatch | The object will be returned only if the value of `ETag` matches the specified value; otherwise, "412 (precondition failed)" will be returned. | String | No |
| IfNoneMatch | The object will be returned only if the value of `ETag` does not match the specified value; otherwise, "304 (not modified)" will be returned. | String | No |
| VersionId | Version ID of the object to download | String | No |
| onProgress | Callback of the progress. Attributes of the response object `progressData` are as follows: | Function | No |
| - progressData.loaded | Size of the downloaded parts, in bytes | Number | No |
| - progressData.total | Size of the entire object, in bytes | Number | No |
| - progressData.speed | Download speed, in bytes/s | Number | No |
| - progressData.percent | Percentage of the file download progress, in decimal form. For example, 0.5 means 50% has been downloaded. | Number | No |

#### Callback function description

```
function(err, data) { ... }

```

| Parameter &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Type | 
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Headers returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 304, 403, and 404 | Number |
| - headers | Headers returned by the request | Object |
| - CacheControl  | Cache directives as defined in RFC 2616. This header will be returned only if it is contained in the object metadata or if it is specified in the request parameter. | string |
| - ContentDisposition                                         | File name as defined in RFC 2616, which will be returned only if it is contained in the object metadata or if it is specified in the request parameter | String  |
| - ContentEncoding                                            | Encoding format as defined in RFC 2616, which will be returned only if it is contained in the object metadata or if it is specified in the request parameter | String  |
| - Expires                                                    | Cache expiration time as defined in RFC 2616, which will be returned only if it is contained in the object metadata or if it is specified in the request parameter | String  |
| - x-cos-storage-class | Storage class of the object. For the enumerated values, such as `STANDARD` and `STANDARD_IA`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925).</br>**Note: If this header is not returned, the storage class is `STANDARD`.** | String  |
| - x-cos-meta-\*                                               | User defined metadata                                           | String  |
| - NotModified      | If the request has IfModifiedSince, then the attributes of IfModifiedSince will be returned. If the file has been modified, `false` will be returned. If not, `true` will be returned | Boolean |
| - ETag | MD5 checksum of the object. The value of this parameter can be used to check whether the object was corrupted during the upload. </br>Example: `"09cba091df696af91549de27b8e7d0f6"`. **Note that double quotation marks are required at the beginning and the end.** | String |
| - VersionId       | Returns the version ID for versioning-enabled buckets. For buckets that have never had versioning enabled, this parameter is not returned. | String  |
| - Body                | Returned file content. Uses the String format by default.        | String  |

### Configuring pre-flight requests for cross-origin access

#### API description

This API (OPTIONS Object) is used to send a pre-flight request for the CORS configuration of an object. Before making a real CORS request, you can send an OPTIONS request that includes the source origin, HTTP method, and headers to COS for it to determine whether a real CORS request can be sent. If there is no CORS configuration, "403 Forbidden" will be returned. **You can enable CORS for a bucket using the `PUT Bucket cors` API.**

#### Sample

[//]: # (.cssg-snippet-option-object)
```js
cos.optionsObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
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

| Parameter | Description | Type | Required |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| Origin | Origin domain name of the simulated CORS request | String | Yes |
| AccessControlRequestMethod | HTTP method of the simulated CORS request | String | Yes |
| AccessControlRequestHeaders | Headers of the simulated CORS request | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Type | 
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Headers returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - headers | Headers returned by the request | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - AccessControlAllowOrigin | Source origins (separated by commas) of the simulated CORS request. If the origins are not allowed, this header will not be returned. Example: `*` | String |
| - AccessControlAllowMethods | HTTP methods (separated by commas) of the simulated CORS request (for example, `PUT,GET,POST,DELETE,HEAD`). If the request method is not allowed, this header will not be returned. | String |
| - AccessControlAllowHeaders | Headers (separated by commas) of the simulated CORS request (for example, `accept,content-type,origin,authorization`). If none of the stimulated request headers is allowed, this header will not be returned. | String |
| - AccessControlExposeHeaders | Response headers supported by CORS, such as `ETag`. The headers are separated by commas | String |
| - AccessControlMaxAge | The validity duration of results returned by the OPTIONS request, e.g. `3600` | String  |
| - OptionsForbidden | Indicates whether the `OPTIONS` request is forbidden. It is `true` if HTTP status code 403 is returned | Boolean |

### Setting object replication

#### API description

This API (PUT Object - Copy) is used to create a copy of an existing COS object, that is, an object is copied from the source path (object key) to the destination path (object key). During the copy, object metadata and the ACLs can be modified.
You can use this API to create a copy, modify object metadata (the source object and destination file have the same attributes), and move or rename the object (first copy the object, and then call the deletion API separately).

>! We recommend that you use this API to download an object of 1 MB-5 GB. For objects greater than 5 GB, please use the advanced copy API [Slice Copy File](#.E5.A4.8D.E5.88.B6.E5.AF.B9.E8.B1.A1).
>

#### Sample

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

| Parameter | Description | Type | Required |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| CopySource | URL of the source object. A historical version can be specified using the URL parameter `?versionId=&lt;versionId>`. | String | Yes |
| ACL | Defines the ACL attribute of the object. For the enumerated values, such as `default`, `private`, and `public-read`, please see the **Preset ACL** section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: default <br>**Note**: If you do not need access control for the object, set this parameter to `default` or leave it empty. In this way, the object will inherit the permissions of the bucket it is stored in. | String | No |
| GrantRead              | Grants a user read permission for an object in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.<br>Example: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul> | String | No   |
| GrantWrite                  | Grants a user write permission in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code><br>Example: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul> | String | No   |
| GrantFullControl       | Grants a user full access in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.</br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` </li></ul> | String               | No   |
| MetadataDirective | Indicates whether to copy the metadata. Enumerated values: `Copy` (default), `Replaced`. If set to `Copy`, the metadata of the source object will be copied directly and the user-defined metadata in the header will be ignored. If set to `Replaced`, the metadata of the source object will be replaced with the user-defined metadata in the header. **If the destination and source paths are the same, that is, you want to modify the metadata, this parameter must be set to `Replaced`.** | String | No |
| CopySourceIfModifiedSince | If the object is modified after the specified time, the operation will be performed; otherwise, 412 will be returned. **This parameter can be used together with `CopySourceIfNoneMatch`. If it is used together with other conditions, a conflict will be returned.** | String | No |
| CopySourceIfUnmodifiedSince | If the object is not modified after the specified time, the operation will be performed; otherwise, 412 will be returned. **This parameter can be used together with `CopySourceIfMatch`. If it is used together with other conditions, a conflict will be returned.** | String | No |
| CopySourceIfMatch | If the `ETag` of the object is the same as the specified one, the operation will be performed; otherwise, 412 will be returned. **This parameter can be used together with `CopySourceIfUnmodifiedSince`. If it is used together with other conditions, a conflict will be returned.** | String | No |
| CopySourceIfNoneMatch | If the `Etag` of the object is different from the specified one, the operation will be performed; otherwise, 412 will be returned. **This parameter can be used together with `CopySourceIfModifiedSince`. If it is used together with other conditions, a conflict will be returned.** | string | No |
| StorageClass | Storage class of the object. For the enumerated values, such as `STANDARD` (default) and `STANDARD_IA`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String | No |
| x-cos-meta-\* | Other user-defined file headers | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| - ETag | MD5 checksum of the object, such as `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end.** | String |
| - LastModified | Last modified time of the object, for example, `2017-06-23T12:33:27.000Z` | String |
| - VersionId | Returns the version ID for versioning-enabled buckets. For buckets that have never had versioning enabled, this parameter is not returned. | String  |

### Deleting a single object

#### API description

This API (DELETE Object) is used to delete an object from a COS bucket. To call this API, you need to have permission to write to the bucket.

#### Sample

[//]: # (.cssg-snippet-delete-object)
```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject'        /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| VersionId | Version ID of the object or delete marker to delete | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 204, 403, and 404. **If the deletion is successful or the object does not exist, an HTTP 204 or 200 status code will be returned. If the specified bucket is not found, an HTTP 404 status code will be returned.** | Number |
| - headers | Header information returned by the request | Object |

### Deleting multiple objects

#### API description

This API (DELETE Multiple Objects) is used to delete multiple objects from a bucket in a single request. You can delete up to 1,000 objects in a single request. There are two response modes for you to choose from: `Verbose` and `Quiet`. The `Verbose` mode returns information about the deletion of each object, whereas the `Quiet` mode returns only information about error objects.

#### Sample

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
}, function(err, data) {
    console.log(err || data);
});
```

Deleting multiple objects with a specified prefix (deleting files in a specified directory):

```js
var bucket: 'examplebucket-1250000000'; /* Required */
var region: 'ap-beijing';     /* Region of the bucket (required) */
var prefix = 'examplefolder/';  /* A directory/prefix to delete */
var deleteFiles = function (marker) {
    cos.getBucket({
        Bucket: bucket,
        Region: region,
        Prefix: prefix,
        Marker: marker,
        MaxKeys: 1000,
    }, function (listError, listResult) {
        if (listError) return console.log('list error:', listError);
        var nextMarker = listResult.NextMarker;
        var objects = listResult.Contents.map(function (item) {
            return {Key: item.Key}
        });
        cos.deleteMultipleObject({
            Bucket: bucket,
            Region: region,
            Objects: objects,
        }, function (delError, deleteResult) {
            if (delError) {
                console.log('delete error', delError);
                console.log('delete stop');
            } else {
                console.log('delete result', deleteResult);
                if (listResult.IsTruncated === 'true') deleteFiles(nextMarker);
                else console.log('delete complete');
            }
        });
    });
}
deleteFiles();
```

#### Parameter description

| Parameter | Description | Type | Required |
| ----------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Quiet | Specifies whether to use the `Quiet` mode. If set to `true`, the `Quiet` mode is enabled. If set to `false` (default), the `Verbose` mode is enabled. | Boolean | No |
| Objects | The list of objects to delete | ObjectArray | Yes |
| - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| - VersionId | Version ID of the object or delete marker to delete | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description  | Type |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 204, 403, and 404 | Number |
| - headers | Headers returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 204, 403, and 404 | Number |
| - headers | Headers returned by the request | Object |
| - Deleted | Lists objects deleted successfully | ObjectArray |
| - - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| - - VersionId | If the `VersionId` parameter is passed in, it will also be included in the response, indicating the version of the object or delete marker. | String |
| - - DeleteMarker | If versioning is enabled and the `VersionId` parameter is not specified, the deletion will not actually delete the file; instead, it will only add a new delete marker, indicating that the visible file has been deleted. Enumerated values: `true`, `false` | String |
| - - DeleteMarkerVersionId | Returns the VersionId of the newly added delete marker if `DeleteMarker` is `true`  | String |
| - Error | Lists objects whose deletion failed | ObjectArray |
| - - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| - - Code                                                     | Deletion failure error codes                                             | String      |
| - - Message                                                  | Deletion failure error messages                                      | String      |

## Multipart Upload Operations

### Querying multipart upload operations

#### API description

This API (List Multipart Uploads) is used to query the ongoing multipart uploads. Up to 1,000 multipart uploads can be listed at a time.

#### Sample

Get the list of unfinished UploadIds prefixed with `exampleobject`. The following is an example:

[//]: # (.cssg-snippet-list-multi-upload)
```js
cos.multipartList({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Prefix: 'exampleobject', /*Optional*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Prefix | Matching prefix for object keys. This parameter specifies that the response can contain only object keys with the specified prefix. Note that when you query with the prefix specified, the returned object keys will still contain the prefix. | String | No |
| Delimiter | Separating symbol used to group object keys. It is usually `/`. The identical paths between `Prefix` or, if no `Prefix` is specified, the beginning and the first `delimiter` are grouped and defined as a common prefix. All common prefixes will be listed. | String | No |
| EncodingType | Encoding type of the returned value. Valid value: `url` | String | No |
| MaxUploads | Maximum number of entries that can be returned at a time. Valid range: 1-1000. Defaults to `1000`. | String | No |
| KeyMarker      | Used together with `upload-id-marker`.<ul  style="margin: 0;">If `upload-id-marker` is not specified:</br>&emsp;- Only multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed. </li><li>If `upload-id-marker` is specified:</br>&emsp;- Multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed;</br>&emsp;- Multipart uploads whose `ObjectName` is lexicographically equal to the specified `key-marker` and the `UploadID` is greater than the `upload-id-marker` will be listed.</li></ul> | String | No   |
| UploadIdMarker | Used together with `key-marker`.<ul  style="margin: 0;"><li>If `key-marker` is not specified:</br>&emsp;- `upload-id-marker` will be ignored.</li><li>If `key-marker` is specified:</br>&emsp;- Multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed;</br>&emsp;- Multipart uploads whose `ObjectName` is lexicographically equal to the specified `key-marker` and the `UploadID` is greater than the `upload-id-marker` will be listed.</li></ul> | String | No   |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Type |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Headers returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Headers returned by the request | Object |
| - Bucket | Destination bucket for the multipart upload | String |
| - Encoding-Type | Encoding type of the returned value. Valid value: `url`  | String |
| - KeyMarker | Marks the key after which the entry listing starts  | String |
| - UploadIdMarker | Marks the UploadId after which the entry listing starts | String |
| - NextKeyMarker | If the returned list is truncated, the `NextKeyMarker` returned will be the starting point of the subsequent list | String |
|-  NextUploadIdMarker |  If the returned list is truncated, the `UploadId` returned will be the starting point of the subsequent list | String |
| - MaxUploads                                                 | The maximum number of returned entries. Valid value range: 1 - 1000                  | String      |
| - IsTruncated   |  Indicates whether returned objects are truncated. Valid value: `true` or `false` | String |
|  - Prefix  | Matching prefix for object keys. This parameter specifies that the response can contain only object keys with the specified prefix | String | 
| - Delimiter | Separating symbol used to group object keys. It is usually `/`. The identical paths between `Prefix` or, if no `Prefix` is specified, the beginning and the first `delimiter` are grouped and defined as a common prefix. All common prefixes will be listed | String |
| - CommonPrefixs                                              | The identical paths between `Prefix` and `Delimiter` are grouped and defined as a common prefix | ObjectArray |
| - - Prefix | Displays specific common prefixes | String |
| - Upload                                                     | A collection of multipart upload information                                  | ObjectArray |
| - - Key                                                      | Name of the object, i.e. object key                                         | String      |
| - - UploadId           | ID of the current multipart upload                                    | String      |
| - - StorageClass | Storage class of the parts. For the enumerated values, such as `STANDARD`, `STANDARD_IA`, `ARCHIVE`, and `DEEP_ARCHIVE`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String |
| - - Initiator                        | Initiator of the current multipart upload                                    | Object      |
| - - - DisplayName | Name of the upload initiator | String |
|- - - ID | ID of the upload initiator in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value. | String |
| - - Owner                 | Owner of the parts                                    | Object      |
| - - - DisplayName | Name of the part owner | String |
| - - - ID | Parts owner ID in the format: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`.<br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value. | String |
| - - Initiated                               | Start time of the multipart upload                                        | String      |

### Initializing a multipart upload

#### API description

This API (Initiate Multipart Upload) is used to initialize a multipart upload. After a successful operation, an upload ID will be returned, which can be used in the subsequent `Upload Part` requests.

#### Sample

[//]: # (.cssg-snippet-init-multi-upload)
```js
cos.multipartInit({
    Bucket: 'examplebucket-1250000000', /*Required*/
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

| Parameter | Description | Type | Required |
| ------------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| CacheControl | Cache policy as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| Content-Disposition | Filename as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentEncoding | Encoding format as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentType | Content type (MIME) as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| Expires | Cache expiration time as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ACL | Defines the ACL attribute of the object. For the enumerated values, such as `default`, `private`, and `public-read`, please see the **Preset ACL** section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: `default` <br>**Note:** If you do not need access control for the object, set `default` for this parameter or leave it empty. In this way, the object will inherit the permissions of the bucket it is stored in. | String | No |
| GrantRead              | Grants a user read permission for an object in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.<br>Example: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code> </li></ul> | String | No   |
| GrantFullControl       | Grants a user full access in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.</br>Example: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul> | String | No   |
| StorageClass | Storage class of the object. For the enumerated values, such as `STANDARD` (default), `STANDARD_IA`, `ARCHIVE`, and `DEEP_ARCHIVE`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String | No |
| x-cos-meta-\* | User-defined headers, which will be returned as the object metadata. The maximum size is 2 KB. | String | No |
| UploadAddMetaMd5 | Sets x-cos-meta-md5 as the object’s MD5 checksum in the object’s metadata during upload in the format of a 32-bit lowercase string. Example: `4d00d79b6733c9cc066584a02ed03410` | String | No   |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| Bucket | Name of the destination bucket for the multipart upload. The value is formed by connecting a user-defined string and the system-generated `APPID` with a hyphen, for example, `examplebucket-1250000000`. | string |
| Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| UploadId | ID that can be used in subsequent uploads | String |

### Uploading parts

#### API description

This API (Upload Part) is used to upload parts after a multipart upload is initialized. It can upload up to 10,000 parts of 1 MB to 5 GB for a multipart upload.
- When you use the `Initiate Multipart Upload` API to initiate a multipart upload, you can obtain the `uploadId`. This ID uniquely identifies the part and its position in the entire object.
- Every time you call the `Upload Part` API, you need to pass `partNumber` (the part number) and `uploadId`. You can upload multiple parts out of order.
- When the `uploadId` and `partNumber` of a new part are the same as those of a previously uploaded part, the old part will be overwritten. If the `uploadId` does not exist, the 404 error, "NoSuchUpload", will be returned.

#### Sample

[//]: # (.cssg-snippet-upload-part)
```js
cos.multipartUpload({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /* Required */
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

| Parameter | Description | Type | Required |
| ------------- | ------------------------------------------------------------ | ---------------- | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| ContentLength | HTTP request length (in bytes) as defined in RFC 2616 | String | Yes |
| PartNumber | Part number | String | Yes |
| UploadId | ID of the multipart upload task | String | Yes |
| Body | Content of the file part to be uploaded. This parameter can be a File object or a Blob object. | String\File\Blob | Yes |
| Expect | HTTP request content length (in bytes) as defined in RFC 2616. If `Expect: 100-continue` is used, the request content will be sent only after confirmation from the server is received. | String | No |
| ContentMD5 | Base64-encoded 128-bit MD5 checksum as defined in RFC 1864. This header is used to verify whether the file content has changed. | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

### Copying parts

#### API description

This API (Upload Part - Copy) is used to copy the parts of an object from the source path to the destination path.

> !To upload an object in parts, you must first initialize the multipart upload. A unique descriptor (upload ID) will be returned in the response of the multipart upload initialization. This ID needs to be carried in the multipart upload request.

#### Sample

[//]: # (.cssg-snippet-upload-part-copy)
```js
cos.uploadPartCopy({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /* Required */
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

| Parameter | Description | Type | Required |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| CopySource | URL path of the source object. A historical version can be specified using the URL parameter `?versionId=&lt;versionId>`. | String | Yes |
| PartNumber | Part number | String | Yes |
| uploadId | To upload an object in parts, you must first initialize the multipart upload. The response of the multipart upload initialization will carry a unique descriptor (an upload ID), which needs to be carried in the multipart upload request. | String | Yes |
| CopySourceRange | Byte range of the source object. The range value must be in the format of `bytes=first-last`, where both `first` and `last` are offsets starting from 0. For example, `bytes=0-9` means that you want to copy the first 10 bytes of data of the source object. If this parameter is not specified, the entire object will be copied. | String | No |
| CopySourceIfMatch | If the `Etag` of the object is the same as the specified one, the operation will be performed; otherwise, 412 will be returned. This parameter can be used together with `x-cos-copy-source-If-Unmodified-Since`. If it is used together with other conditions, a conflict will be returned. | String | No |
| CopySourceIfNoneMatch | If the `ETag` of the object is different from the specified one, the operation will be performed; otherwise, 412 will be returned. This parameter can be used together with `x-cos-copy-source-If-Modified-Since`. If it is used together with other conditions, a conflict will be returned. | string | No |
| CopySourceIfUnmodifiedSince | If the object is not modified after the specified time, the operation will be performed; otherwise, 412 will be returned. This parameter can be used together with `x-cos-copy-source-If-Match`. If it is used together with other conditions, a conflict will be returned. | String | No |
| CopySourceIfModifiedSince | If the object is modified after the specified time, the operation will be performed; otherwise, 412 will be returned. This parameter can be used together with `x-cos-copy-source-If-None-Match`. If it is used together with other conditions, a conflict will be returned. | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| - ETag | MD5 checksum of the object, such as `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end.** | String |
| - LastModified | Last modified time of the object, in GMT format | String |

### Querying uploaded parts

#### API description

This API (List Parts) is used to query the uploaded parts of a specified multipart upload, i.e., listing all successfully uploaded parts of a multipart upload with a specified `uploadId`.

#### Sample

[//]: # (.cssg-snippet-list-parts)
```js
cos.multipartListPart({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    UploadId: 'exampleUploadId', /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| UploadId | Multipart upload ID obtained from the `Initiate Multipart Upload` API | String | Yes |
| EncodingType | Encoding type of the returned value | String | No |
| max-parts | Maximum number of parts to return at a time. Defaults to `1000`. | string | No |
| PartNumberMarker | By default, parts are listed in UTF-8 binary order, starting from the part after the marker. | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Type |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Headers returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Headers returned by the request | Object |
| - Bucket | Destination bucket for the multipart upload | String |
| EncodingType | Encoding type of the returned value | String |
|  - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| - UploadId | ID of the current multipart upload  | String  |
| - Initiator | Initiator of the current multipart upload | Object      |
| - - DisplayName | Name of the upload initiator | String |
| - - - ID | ID of the upload initiator in the format: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`. <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value. | String |
| - Owner | Owner of the parts  | Object      |
| - - DisplayName                                              | Name of the bucket owner | String      |
| - - ID                      | Bucket owner ID, generally the user's UIN                         | String      |
| - StorageClass |Storage class of the parts. For the enumerated values, such as `STANDARD`, `STANDARD_IA`, `ARCHIVE`, and `DEEP_ARCHIVE`, please see [Storage Classes Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String |
| - PartNumberMarker      | By default, entries are listed in UTF-8 binary order, starting from the part after the marker.  | String    |
| NextPartNumberMarker  | If the returned list is truncated, the `NextMarker` returned will be the starting point of the subsequent list   | String    |
| - MaxUploads                                                 | The maximum number of entries returned in a single request                 | String      |
| - IsTruncated   |  Indicates whether returned objects are truncated. Valid value: `true` or `false` | String |
| - Part                                  | Parts information list                                                 | ObjectArray |
| - - PartNumber                                               | Part number                                                    | String      |
| - - LastModified                 | Last modified time of the part                                           | String      |
| - - ETag                                 | MD5 algorithm checksum of the part                                          | String      |
| - - Size          | Part size, in bytes                                            | String      |

### Completing a multipart upload

#### API description

This API is used to complete a multipart upload operation. After all parts are uploaded via the `Upload Part` API, you need to call this API to complete the multipart upload. When using this API, you need to specify the `PartNumber` and `ETag` of each part in the request body for the part information to be verified.
As the parts need to be merged after they are uploaded, and the merge takes several minutes, when the merge starts, COS will immediately return status code "200" and periodically return space information during the merge process to keep the connection active until the merge is completed. After that, COS will return the content of the merged parts in the body.

- If any uploaded part is less than 1 MB in size, `400 EntityTooSmall` will be returned when this API is called.
- If the uploaded part numbers are not continuous, "400 InvalidPart" will be returned when this API is called.
- If the part information entries in the request body are not sorted by number in ascending order, "400 InvalidPartOrder" will be returned when this API is called.
- If the `uploadId` does not exist, "404 NoSuchUpload" will be returned when this API is called.

> !We recommend you either complete or abort a multipart upload as early as possible, as the uploaded parts of an incomplete multipart upload will take up storage capacity and incur storage fees.

#### Sample

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
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ----------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| UploadId | ID of the upload task | String | Yes |
| Parts | A list of information about the parts of the multipart upload | ObjectArray | Yes |
| - PartNumber | Part number | String | Yes |
| - ETag | MD5 checksum of each part. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`<br>**Note that double quotation marks are required at the beginning and the end.** | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - Location   | Location where the uploaded file can be accessed                                        | String |
| - Bucket | Destination bucket for the multipart upload | String |
| - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| - ETag | Unique ID of the merged file in the format of `"uuid-<part quantity>"`. </br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`. **Note that double quotation marks are required at the beginning and the end.** | String |

### Aborting a multipart upload

#### API description

This API (Abort Multipart Upload) is used to abort a multipart upload and delete the uploaded parts. If you call this API and there is an `Upload Part` request that is using the multipart upload, the request will fail. If the `uploadId` does not exist, "404 NoSuchUpload" will be returned.

> !We recommend you either complete or abort a multipart upload as early as possible, as the uploaded parts of an incomplete multipart upload will take up storage capacity and incur storage fees.

#### Sample

[//]: # (.cssg-snippet-abort-multi-upload)
```js
cos.multipartAbort({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    UploadId: 'exampleUploadId' /*Required*/
}, function(err, data) {
    console.log(err || data);
});

```

#### Parameter description

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name, formatted as `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| UploadId | Multipart upload ID obtained from the `Initiate Multipart Upload` API | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

## Other Operations

### Restoring an archived object

#### API description

This API (POST Object restore) is used to restore an archived COS object. The restored readable object is temporary. You can configure the object to keep it readable and set the time for the object to be deleted. You can use the `Days` parameter to specify the expiration time of the temporary object. If you have not initiated any operation on the object, such as copying it or extending its validity period, before it expires, the temporary object will be automatically deleted. A temporary object is only a copy of the archived object and the source archived object will always exist throughout this period.

#### Sample

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
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| RestoreRequest | A container for data restoration | Object | Yes |
| - Days | Sets the expiration time of the temporary copy. | Number | Yes |
| - CASJobParameters | A container for the archive job parameters | Object | Yes |
| - - Tier | Specifies one of the three data restoration modes supported by COS: `Standard`, which completes a restoration job in 3-5 hours; `Expedited`, which completes a restoration job in 15 minutes; and `Bulk`, which completes multiple restoration jobs in 5-12 hours. | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

### Setting an object ACL

#### API description

This API (PUT Object acl) is used to set the ACL of an object in a bucket.

> !The total number of policies associated with bucket ACL, Policy, and CAM under a single root account (i.e., under the same `APPID`) cannot exceed 1,000. There is no upper limit on the number of object ACL rules. If you do not need access control for an object, do not make any configuration, and the object will inherit the permissions of its bucket.

#### Sample

[//]: # (.cssg-snippet-put-object-acl)
```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    ACL: 'public-read', /*Optional*/
}, function(err, data) {
    console.log(err || data);
});
```

Grant a user all permissions for an object:

[//]: # (.cssg-snippet-put-object-acl-user)
```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    GrantFullControl: 'id="100000000001"' // 100000000001 is the uin of the root account.
}, function(err, data) {
    console.log(err || data);
});
```

Grant the user permission to write the object via `AccessControlPolicy`:

[//]: # (.cssg-snippet-put-object-acl-acp)
```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    AccessControlPolicy: {
        "Owner": { // `Owner` is required in `AccessControlPolicy`.
            "ID": 'qcs::cam::uin/100000000001:uin/100000000001' // 100000000001 is the UIN of the bucket owner
        },
        "Grants": [{
            "Grantee": {
                "ID": "qcs::cam::uin/100000000011:uin/100000000011", // 100000000011 is the UIN of the sub-account of the bucket owner
            },
            "Permission": "WRITE"
        }]
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket | Bucket name, formatted as `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| ACL | Defines the ACL attribute of the object. For the enumerated values, such as `default`, `private`, and `public-read`, please see the **Preset ACL** section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: `default` <br>**Note:** If you do not need access control for the object, set `default` for this parameter or leave it empty. In this way, the object will inherit the permissions of the bucket it is stored in. | String | No |
| GrantRead              | Grants a user read permission for an object in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.<br><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.<br>Example: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul> | String | No   |
| GrantFullControl       | Grants a user full access in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.<br>Example: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul> | String | No   |
| AccessControlPolicy | Sets the object's ACL attributes. | Object | No |
| - Owner | Information about the object owner | Object | No |
| - - ID | ID of the object owner in the format: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value. | String | No |
| - - DisplayName | Name of the object owner | String |
| - Grants | A list of information about the grantee and granted permissions | ObjectArray | No |
| - - Permission | Permission granted. Enumerated values: `READ`, `WRITE`, `READ_ACP`, `WRITE_ACP`, `FULL_CONTROL` | String | No |
| - - Grantee | Information about the grantee | Object | No |
| - - - DisplayName | Name of the grantee | String | No |
| - - - ID | ID of the authorized user in the format: `qcs::cam::uin/<OwnerUin>:uin/<;SubUin>` <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value. | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code returned by the request, such as "200", "204", "403", and "404" | Number |
| - headers | Header information returned by the request | Object |

### Querying object ACL

#### API description

The API is used to query the ACL of an object. Only the owner of the bucket has the permission to use this API.

#### Sample

[//]: # (.cssg-snippet-get-object-acl)
```js
cos.getObjectAcl({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name, formatted as `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ----------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is left empty. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - ACL | Defines the ACL attribute of the object. For the enumerated values, such as `default`, `private`, and `public-read`, please see the **Preset ACL** section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: `default` <br>**Note:** If you do not need access control for the object, set `default` for this parameter or leave it empty. In this way, the object will inherit the permissions of the bucket it is stored in. | String | No |
| - Owner | Owner of the resource | Object |
| - - ID | Object owner ID in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value. | String |
| - - DisplayName | Name of the object owner | String |
| - Grants | List of information on the grantee and permissions | ObjectArray |
| - - Permission | Permission granted. Enumerated values: `READ`, `READ_ACP`, `WRITE_ACP`, `FULL_CONTROL` | String |
| - - Grantee | Grantee information | Object |
| - - - DisplayName | Name of the user | String |
| - - - ID | User ID in the format: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`</br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value. | String |

## Advanced APIs (Recommended)

The following methods encapsulate the native methods mentioned above. They can implement the complete process of multipart upload/copy and support concurrent multipart upload/copy, checkpoint restart as well as canceling, pausing, and restarting upload tasks.

### Uploading an object in parts

#### API description

This API is used to upload large files in parts.

>?
>- If the browser is not closed, you can suspend, restart, or cancel the upload job.
>- If you upload the same file to the same bucket path after refreshing the browser, the file content will be verified based on `UploadId` and the upload will proceed if the verification is passed.

#### Sample

[//]: # (.cssg-snippet-transfer-upload-file)
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
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type      | Required |
| ------------------------------------------------------------ | ------------------------------------------------------------ | --------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| Body | Content of the file part to be uploaded, which can be a File object or a Blob object | File\Blob | Yes |
| SliceSize | Part size | String | No |
| AsyncLimit | Maximum number of parts for concurrent upload | String | No |
| StorageClass | Storage class of the object. For the enumerated values, such as `STANDARD`, `STANDARD_IA`, `ARCHIVE`, and `DEEP_ARCHIVE`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String | No |
| UploadAddMetaMd5 | Sets x-cos-meta-md5 as the object’s MD5 checksum in the object’s metadata during upload in the format of a 32-bit lowercase string. Example: `4d00d79b6733c9cc066584a02ed03410` | String | No |
| TaskReady | Callback function when an upload task is created. The callback returns a `taskId`, which uniquely identifies the task and can be used to cancel (cancelTask), pause (pauseTask), or restart (restartTask) the task. | Function | No |
| - taskId                                                     | Upload task number                                              | String    | No  |
| onHashProgress | Progress callback function for file MD5 checksum calculation. The callback parameter is the progress object `progressData` | Function | No |
| - progressData.loaded | Size of the verified parts, in bytes | Number | No |
| - progressData.total                                         | Size of the entire file, in bytes                      | Number    | No   |
| - progressData.speed                                         | File verification speed in bytes/s                 | Number    | No   |
| - progressData.percent | Percentage of the file verification progress, in decimal form. For example, 0.5 means 50% has been verified. | Number | No |
| onProgress | File upload progress callback function. The callback parameter is the object in progress `progressData` | Function | No |
| - progressData.loaded | Size of the uploaded parts, in bytes | Number | No |
| - progressData.total                                         | Size of the entire file, in bytes                      | Number    | No   |
| - progressData.speed                                         | File upload speed in bytes/s                 | Number    | No   |
| - progressData.percent | Percentage of the file upload progress, in decimal form. For example, 0.5 means 50% has been uploaded. | Number | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - Location   | Location where the uploaded file can be accessed                                        | String |
| - Bucket | Destination bucket for the multipart upload | String |
| - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| - ETag | Unique ID of the merged file in the format of `"uuid-<part quantity>"`. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`. **Note that double quotation marks are required at the beginning and the end.** | String |
| - VersionId       | Returns the version ID for versioning-enabled buckets. For buckets that have never had versioning enabled, this parameter is not returned. | String  |

### Copying an object

#### API description

This API (Slice Copy File) is used to copy an object from the source path to the destination path through multipart copy. During the copy, the object metadata and ACL can be modified. You can use this API to move, rename, and copy a file or modify its attributes.

#### Method prototype

Call `Slice Copy File`:

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

| Parameter | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| CopySource | URL of the source object. A historical version can be specified using the URL parameter `?versionId=&lt;versionId>`. | String | Yes |
| ChunkSize | Size (in bytes) of each part in the multipart copy. Defaults to `1048576` (1 MB). | Number | No |
| SliceSize | Specifies the minimum file size (in bytes) to use multipart copy. The default value is 5 GB. If the file size is equal to or smaller than this value, the file will be uploaded using `putObjectCopy`; otherwise, it will be uploaded using `sliceCopyFile`. | Number | No | | Number | No |
| onProgress | Callback of the upload progress. The callback parameter is the progress object `progressData`. | Function | No |
| - progressData.loaded | Size of the uploaded parts, in bytes | Number | No |
| - progressData.total | Size of the entire file, in bytes | Number    | No   |
| - progressData.speed | File upload speed, in bytes/s | Number | No |
| - progressData.percent | Percentage of the file upload progress, in decimal form. For example, 0.5 means 50% has been uploaded. | Number | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - Location   | Location where the uploaded file can be accessed                                        | String |
| - Bucket | Destination bucket for the multipart upload | String |
| - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| - ETag | MD5 checksum of the merged file. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end.** | String |
| - VersionId       | Returns the version ID for versioning-enabled buckets. For buckets that have never had versioning enabled, this parameter is not returned. | String  |

### Batch upload

#### API description

Method 1:
You can call `putObject` and `sliceUploadFile` multiple times to implement batch uploads. You can instantiate the `FileParallelLimit` parameter to limit how many objects (default value: 3) can be uploaded at the same time.

Method 2:
You can call `cos.uploadFiles` to implement batch uploads. The `SliceSize` parameter can be used to set a size limit to determine whether `sliceUploadFile` is used. The following describes how to use the `uploadFiles` method:

#### Method prototype

Call `uploadFiles`:

[//]: # (.cssg-snippet-transfer-batch-upload-objects)
```js
cos.uploadFiles({
    files: [{
        Bucket: 'examplebucket-1250000000', // Format: BucketName-APPID
        Region: 'COS_REGION',     /* Bucket region. Required */
        Key: 'exampleobject',
        Body: fileObject1,
    }, {
        Bucket: 'examplebucket-1250000000', // Format: BucketName-APPID
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

| Parameter | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | --------- | ---- |
| files | File list. Each item is a parameter object to be passed to `putObject` and `sliceUploadFile`. | Object | Yes |
| - Bucket | Bucket name in the format of `BucketName-APPID`. | String | Yes |
| - Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| - Body | Content of the file part to be uploaded. This parameter can be a File object, or a Blob object. | File\Blob | Yes |
| SliceSize | Specifies the minimum file size (in bytes) to use multipart upload. If the file size is equal to or smaller than this value, the file will be uploaded using `putObject`; otherwise, it will be uploaded using `sliceUploadFile`. | Number | Yes |
| onProgress | Upload progress calculated by averaging out the progress of all tasks | String | Yes |
| - progressData.loaded | Size of the uploaded parts, in bytes | Number | No |
| - progressData.total | Size of the entire file, in bytes | Number | No |
| - progressData.speed | File upload speed, in bytes/s | Number | No |
| - progressData.percent | Percentage of the file upload progress, in decimal form. For example, 0.5 means 50% has been uploaded. | Number | No |
| onFileFinish | Completion or error callback for each file | String | Yes |
| - err | Upload error message | Object | No |
| - data | Information about the completion of object upload | Object | No |
| - options | Parameter information about the files that have been uploaded | Object | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - files | The error or data for each file | ObjectArray |
| - - error | Upload error message | Object |
| - - data | Information about the object upload completion | Object |
| - - options | Parameter information about files that have been uploaded | Object |

### Uploading queue

The SDK for JavaScript records all the upload tasks initiated with `putObject` and `sliceUploadFile` in an upload queue. You can use the queue in the following ways:

1. Use `cos.getTaskList` to get the task list.
2. Use `cos.pauseTask`, `cos.restartTask`, and `cos.cancelTask` to perform operations on upload tasks.
3. cos.on('list-update', callback); can listen to the list and progress changes.

For a complete sample of how to use the upload queue, please see [Queue Demo](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/demo/queue).

#### Canceling an upload task

This API cancels an upload task by `taskId`.

**Sample**

[//]: # (.cssg-snippet-transfer-upload-cancel)
```js
var taskId = 'xxxxx';                   /* Required */
cos.cancelTask(taskId);
```

**Parameter description**

| Parameter | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | ID of the upload task. When `sliceUploadFile` is called, `TaskReady` in the callback will return the `taskId` of the upload task. | String | Yes |

#### Pausing an upload task

This API is used to suspend an upload task by `taskId`.

**Sample**

[//]: # (.cssg-snippet-transfer-upload-pause)
```js
var taskId = 'xxxxx';                   /* Required */
cos.pauseTask(taskId);
```

**Parameter description**

| Parameter | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | ID of the upload task. When `sliceUploadFile` is called, `TaskReady` in the callback will return the `taskId` of the upload task. | String | Yes |

#### Restarting an upload task

This API is used to restart an upload task by `taskId`. You can restart tasks that have been manually suspended through the `pauseTask` API, or automatically suspended due to an upload error.

**Sample**

[//]: # (.cssg-snippet-transfer-upload-resume)
```js
var taskId = 'xxxxx';                   /* Required */
cos.restartTask(taskId);
```

**Parameter description**

<table>
	<tr><th>Parameter</th><th>Description</th><th>Type</th><th>Required</th></tr>
	<tr><td>taskId</td><td>ID of the upload task. When `sliceUploadFile` is called, `TaskReady` in the callback will return the `taskId` of the upload task.</td><td>String</td><td>Yes</td></tr>
</table>
