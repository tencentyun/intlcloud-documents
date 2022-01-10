## Overview

This document provides an overview of advanced APIs and APIs for simple object operations and multipart upload operations, as well as their SDK code samples.
**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ---------------------------------------- |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object in whole | Uploads an object to a bucket. |
| [Append Object](https://intl.cloud.tencent.com/document/product/436/7741) | Appending parts | Appends object parts to a bucket.                      |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | Uploading an object using an HTML form | Uploads an object using an HTML form. |

**Multipart operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries in-progress multipart uploads. |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload. |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads an object in multiple parts. |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries the uploaded parts of a specified multipart upload. |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of an object. |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload and deletes the uploaded parts. |


## Simple Operations

### Uploading an object using simple upload

#### Description

This API (PUT Object) is used to upload an object smaller than 5 GB to a specified bucket. To call this API, you need to have permission to write to the bucket. If the object size is larger than 5 GB, please use [Multipart Upload](#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) or [Advanced APIs](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89) for the upload.

> !
> - The key (filename) cannot end with `/`; otherwise, it will be identified as a folder.
> - Each root account (`APPID`) can have up to 1,000 bucket ACLs and an unlimited number of object ACLs. Do not configure ACLs for an object during upload if you don’t need to control access to it. The object will inherit the permissions of its bucket by default.
> - After an object is uploaded, you can use the same key to generate a pre-signed URL, which can be shared with other clients for downloading. To download, please use the `GET` method. The detailed API description is shown below. If your file is set to private-read, note that the pre-signed URL will only be valid for a certain period of time.
> 

#### Sample code

Uploading a small file

[//]: # (.cssg-snippet-put-object)
```js
const filePath = "temp-file-to-upload" // Local file path
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: '1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
    StorageClass: 'STANDARD',
    /* If the body type is stream, ContentLength must be passed in. Otherwise, onProgress cannot return the progress correctly. */
    Body: fs.createReadStream(filePath), // Upload file object
    ContentLength: fs.statSync(filepath).size,
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

Upload the buffer as the file content:

[//]: # (.cssg-snippet-put-object-bytes)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: '1.txt',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
    Body: Buffer.from('hello!'), /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

Upload a string:

[//]: # (.cssg-snippet-put-object-string)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: '1.txt', /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
    Body: 'hello!',
}, function(err, data) {
    console.log(err || data);
});
```

Upload a Base64-encoded string:

[//]: # (.cssg-snippet-put-object-string)
```js
var base64Url = 'data:image/png;base64,iVBORw0KGgo.....';
// Convert to Buffer for upload
var body = Buffer.from(base64Url.split(',')[1] , 'base64');
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
    Key: '1.png',              /* Required */
    Body: body,
}, function(err, data) {
    console.log(err || data);
});
```

Create directory a:

[//]: # (.cssg-snippet-put-object-folder)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: 'a/',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
    Body: '',
}, function(err, data) {
    console.log(err || data);
});
```

Upload objects to directory a/b:

```js
var folder = 'examplefolder/';
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: 'a/b/1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
    Body: fileObject, // Upload the file object.
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

Uploading an object (limiting single-URL speed):

>? For more information about the speed limits on object uploads, please see [Single-URL Speed Limits](https://intl.cloud.tencent.com/document/product/436/34072).

[//]: # (.cssg-snippet-put-object-traffic-limit)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: '1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
    StorageClass: 'STANDARD',
    Body: fileObject, // Upload the file object.
    Headers: {
      'x-cos-traffic-limit': 819200, // The speed range is 819200 to 838860800, that is 100 KB/s to 100 MB/s. If the value is not within this range, 400 will be returned.
    },
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| Body | Content of the file to be uploaded. This parameter can be file stream, buffer, or a string. | Stream/Buffer/String | Yes |
| CacheControl | Cache policy as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentDisposition | Filename as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentEncoding | Encoding format as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentLength          | HTTP request content length (in bytes) defined in RFC 2616. If the body type is stream, ContentLength is required.                   | String               | No   |
| ContentType | Content type (MIME) as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| Expires | Expiration time as defined in RFC 2616. It will be stored as the object metadata. Expiration only invalidates the cache, and the file will not be deleted. | String | No |
| Expect | If `Expect: 100-continue` is used, the request content will be sent only after confirmation from the server is received. | String | No |
| ACL | Defines the access control list (ACL) attribute of the object. For the enumerated values, such as `default`, `private`, and `public-read`, please see the **Preset ACL** section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). </br>**Note:** if you do not need access control for the object, set `default` for this parameter or simply leave it blank. In this way, the object will inherit the permissions of the bucket. | String | No |
| GrantRead              | Grants a user read permission for an object in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.<br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` </li></ul> | String               | No   |
| GrantReadAcp           | Grants a user read access to the object’s ACL in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<br><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.<br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'`</li></ul> | String               | No   |
| GrantWriteAcp          | Grants a user write access to the object’s ACL in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.<br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` </li></ul>| String               | No   |
| GrantFullControl       | Grants a user full access in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.</br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'`</li></ul> | String               | No   |
| StorageClass | Storage class of the object. For the enumerated values, such as `STANDARD` (default), `STANDARD_IA` and `ARCHIVE`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String | No |
| x-cos-meta-\* | User-defined headers, which will be saved as the object metadata. The maximum size is 2 KB. | String | No |
| onTaskReady | Callback function when an upload task is created. The callback returns a `taskId`, which uniquely identifies the task and can be used to cancel (cancelTask), pause (pauseTask), or restart (restartTask) the task. | Function | No |
| - taskId | ID of the upload task | String | No |
| onProgress | Callback of the progress. Attributes of the response object `progressData` are as follows: | Function | No |
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
| err | Error code, which is returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| - ETag | MD5 checksum of the object. The value of this parameter can be used to check whether the object was corrupted during the upload. <br>Example: `"09cba091df696af91549de27b8e7d0f6"`. **Note that double quotation marks are required at the beginning and the end.** | String |
| - Location | Public network access endpoint of the object | String |
| - VersionId       | Version ID of the uploaded object if versioning is enabled for its bucket. If versioning is not enabled, this parameter is not returned. | String  |

### Appending parts

#### Description

This API (`APPEND Object`) is used to append object parts to a bucket.

> !
> - The COS NodeJS SDK version should be v2.11.2 or higher.
> - This API only allows appending data to appendable objects.
> - If an object is uploaded using the `APPEND Object` API for the first time, it will be automatically determined as "appendable".
> - You can use the `GET Object` or `HEAD Object` API to get the `x-cos-object-type` response header to determine the object type.
> 

#### Sample code

Append parts for the first time:

[//]: # (.cssg-snippet-append-object)
```js
cos.appendObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: 'test.txt',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
    Body: fileObject, // Upload the file object.
    Position: 0, // The value is `0` for the first upload.
}, function(err, data) {
    console.log(err || data);
});
```

Check whether parts can be appended for an object in a bucket:

[//]: # (.cssg-snippet-append-object)
```js
cos.headObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: 'test.txt', /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
}, function(err, data) {
    if (err) return console.log(err);
    // If `data.headers` does not contain the `x-cos-object-type` field, you need to configure `expose-headers`. For more information, please see https://cloud.tencent.com/document/product/436/13318.
    var objectType = data.headers['x-cos-object-type'];
    console.log(objectType === 'appendable');
});
```

Query the position of the object for parts appending and start upload:

[//]: # (.cssg-snippet-append-object)
```js
cos.headObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: 'test.txt', /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
}, function(err, data) {
    if (err) return console.log(err);
    // Get the current length (position for upload) of the file to be appended
    var position = data.headers['content-length'];
    cos.appendObject({
        Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
        Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
        Key: 'test.txt',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
        Body: '66666',
        Position: position,
    },
    function(err, data) {
        if (err) return console.log(err);
        // Get the position for the next upload and continue appending parts
        // If `data.headers` does not contain the `x-cos-next-append-position` field, you need to configure `expose-headers`. For more information, please see https://cloud.tencent.com/document/product/436/13318.
        var nextPosition = data.headers['x-cos-next-append-position'];
        console.log(nextPosition);
    })
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | ---------------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| Body | Content of the file to be uploaded. This parameter can be file stream, buffer, or a string. | Stream/Buffer/String | Yes |
| Position | Starting point for the append operation (in bytes). For the first append, the value of this parameter is 0. For subsequent appends, the value is the `content-length` of the current object. | Number | Yes |
| CacheControl | Cache policy as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentDisposition | Filename as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentEncoding | Encoding format as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentLength | HTTP request length (in bytes) as defined in RFC 2616 | String | No |
| ContentType | Content type (MIME) as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| Expires | Expiration time as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| Expect | If `Expect: 100-continue` is used, the request content will be sent only after confirmation from the server is received. | String | No |
| ACL | ACL attribute of the object. For the enumerated values, such as `default`, `private`, and `public-read`, please see the **Preset ACL** section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). <br/>**Note: if you do not need access control for the object, set this parameter to `default` or do not specify it, in which case the object will inherit the permissions of the bucket.** | String | No |
| GrantRead              | Grants a user read access to the object in the format of `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.<br/>Example: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul> | String               | No   |
| GrantReadAcp           | Grants a user read access to the object in the format of `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.<br/>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'`</li></ul> | String           | No   |
| GrantWriteAcp          | Grants a user write access to the object in the format of `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.<br/>Example: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul> | String           | No   |
| GrantFullControl       | Grants a user full access in the format of `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/<OwnerUin>:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.<br/>Example: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul> | String | No   |
| StorageClass | Storage class of the object. For the enumerated values, such as `STANDARD` (default), `STANDARD_IA`, `ARCHIVE`, and `DEEP_ARCHIVE`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String | No |
| x-cos-meta-\* | User-defined headers, which will be saved as the object metadata. The maximum size is 2 KB. | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Error code, which is returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| - RequestId | Unique ID of the request | String |

  

### Uploading an object using an HTML form

The SDK for Node.js does not provide a method for the `POST Object` API. If you need to use this API, please see "Solution B: Upload with a Form" in [Practice of Direct Transfer for Web End](https://intl.cloud.tencent.com/document/product/436/9067).


## Multipart Operations

### Querying multipart uploads

#### Description

This API (List Multipart Uploads) is used to query ongoing multipart uploads. Up to 1,000 multipart uploads can be listed at a time.

#### Sample code

Get the list of incomplete multipart uploads whose `UploadId` is prefixed with `a`:

[//]: # (.cssg-snippet-list-multi-upload)
```js
cos.multipartList({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Prefix: 'a',              /* Optional */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID`. | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Prefix | Object key prefix to query uploads by. Note that when you query uploads with the prefix specified, the returned object keys will also contain the prefix. | String | No |
| Delimiter | Separating symbol used to group object keys. It is usually `/`. The identical paths between `Prefix` or, if no `Prefix` is specified, the beginning and the first `delimiter` are grouped and defined as a common prefix. All common prefixes will be listed. | String | No |
| EncodingType | Encoding type of the returned value. Valid value: `url` | String | No |
| MaxUploads | Maximum number of entries to return at a time. Valid range: 1-1000 (default) | String | No |
| KeyMarker | Used together with `upload-id-marker`. <br><li>If `upload-id-marker` is not specified: <br>&emsp;- Only multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed. </br><li>If `upload-id-marker` is specified: <br>&emsp;- Multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed; </br>&emsp;- Multipart uploads whose `ObjectName` is lexicographically equal to the specified `key-marker` and the `UploadID` is larger than the `upload-id-marker` will be listed. | String | No |
| UploadIdMarker | Used together with `key-marker`. </br><li>If `key-marker` is not specified: </br>&emsp;- `upload-id-marker` will be ignored. </br><li>If `key-marker` is specified: <br>&emsp;- Multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed; </br>&emsp;- Multipart uploads whose `ObjectName` is equal to the specified `key-marker` and the `UploadID` is greater than the `upload-id-marker` will be listed. | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| -------------------- | ------------------------------------------------------------ | ----------- |
| err | Error code, which is returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| - Bucket | Destination bucket for the multipart upload | String |
| - Encoding-Type | Encoding type for the returned values. Valid value: `url` | String |
| - KeyMarker | Key after which the returned listing begins | String |
| - UploadIdMarker | `UploadId` after which the returned list begins | String |
| - NextKeyMarker | Key after which the next returned list begins if the list is truncated | String |
| - NextUploadIdMarker | `UploadId` after which the next returned list begins if the list is truncated | String |
| - MaxUploads | Maximum number of returned entries. Valid value range: 1-1000 | String | No |
| - IsTruncated | Whether the returned list is truncated. Valid value: `true`; `false` | String|
| - Prefix | Object key prefix by which uploads are queried | String |
| - Delimiter | Separating symbol used to group object keys, which is usually `/`. Objects with identical paths between `Prefix` or, if no `Prefix` is specified, the beginning of their keys, and the first delimiter are grouped together and defined as common prefixes. All common prefixes are listed. | String |
| - CommonPrefixes | Objects with identical paths between `Prefix` and the delimiter, which are grouped together and defined as common prefixes | ObjectArray |
| - - Prefix | Specific prefixes | String |
| - Upload | Information of the multipart upload | ObjectArray |
| - - Key | Object key, i.e., object name | String |
| - - UploadId | ID of the multipart upload | String |
| - - StorageClass | Storage class of the parts, such as `STANDARD`, `STANDARD_IA`, and `ARCHIVE`. For more information, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String |
| - - Initiator | Initiator of the multipart upload | Object |
| - - - DisplayName | Name of the upload initiator | String |
| - - - ID | ID of the upload initiator in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value. | String |
| - - Owner | Information about the part owner | Object  |
| - - - DisplayName | Name of the part owner | String |
| - - - ID | ID of the parts owner in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`.<br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value. | String |
| - - Initiated | Starting time of the multipart upload | String |

### Initializing a multipart upload

#### Description

This API (Initiate Multipart Uploads) is used to initialize a multipart upload. After a successful operation, an upload ID will be returned, which can be used in the subsequent `Upload Part` requests.

#### Sample code

[//]: # (.cssg-snippet-init-multi-upload)
```js
cos.multipartInit({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: '1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
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
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| CacheControl | Cache policy as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| Content-Disposition | Filename as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentEncoding | Encoding format as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentType | Content type (MIME) as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| Expires | Expiration time as defined in RFC 2616. It will be stored as the object metadata. Expiration only invalidates the cache, and the file will not be deleted. | String | No |
| ACL | ACL attribute of the object. For the enumerated values, such as `default`, `private`, and `public-read`, please see the **Preset ACL** section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). <br>**Note**: If you do not need access control for the object, set this parameter to `default` or do not specify it, in which case the object will inherit the permissions of its bucket. | String | No |
| GrantRead              | Grants a user read permission for an object in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.</br>Example: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul> | String               | No   |
| GrantFullControl       | Grants a user full access in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.</br>Example: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul> | String | No   |
| StorageClass | Storage class of the object, such as `STANDARD` (default), `STANDARD_IA`, and `ARCHIVE`. For more information, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String | No |
| x-cos-meta-\* | User-defined headers, which will be returned as the object metadata. The maximum size is 2 KB. | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| err | Error code, which is returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| Bucket | Destination bucket for the multipart upload. Format: `BucketName-APPID`. Example: `examplebucket-1250000000` | String |
| Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| UploadId | Upload ID, which is required for the subsequent upload | String |

### Uploading parts

#### Description

This API (`Upload Part`) is used to upload parts after a multipart upload is initialized. It can upload 1-10,000 parts of 1 MB to 5 GB at a time.
<li>When you use the `Initiate Multipart Upload` API to initiate a multipart upload, you can obtain the `uploadId`. This ID uniquely identifies the part and its position in the entire object.</li>
<li>Every time you call the `Upload Part` API, you need to pass `partNumber` (the part number) and `uploadId`. You can upload multiple parts out of order.</li>
<li>When the `uploadId` and `partNumber` of a new part are the same as those of a previously uploaded part, the old part will be overwritten. If the `uploadId` does not exist, the 404 error, "NoSuchUpload", will be returned.</li>

#### Sample code

[//]: # (.cssg-snippet-upload-part)
```js
const filePath = "temp-file-to-upload" // Local file path
cos.multipartUpload({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: '1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
    ContentLength: '1024',
    UploadId: 'exampleUploadId',
    PartNumber: '1',
    Body: fs.createReadStream(filePath)
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
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| ContentLength | HTTP request length (in bytes) as defined in RFC 2616 | String | Yes |
| PartNumber | Part number | String | Yes |
| UploadId | ID of the multipart upload | String | Yes |
| Body | Content of the part to upload This parameter can be a file or a BLOB. | String\File\Blob | Yes |
| Expect | If `Expect: 100-continue` is used, the request content will be sent only after confirmation from the server is received. | String | No |
| ContentMD5 | Base64-encoded 128-bit MD5 checksum as defined in RFC 1864. This header is used to verify whether the file content has changed. | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Error code, which is returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |

### Querying uploaded parts

#### Description

This API (`List Parts`) is used to query the uploaded parts of a specified multipart upload, i.e., listing all successfully uploaded parts of a multipart upload with the specified `uploadId`.

#### Sample code

[//]: # (.cssg-snippet-list-parts)
```js
cos.multipartListPart({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: '1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
    UploadId: 'exampleUploadId', /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| UploadId | Multipart upload ID, which is obtained from the response of the `Initiate Multipart Upload` API | String | Yes |
| EncodingType | Encoding type of the returned value | String | No |
| MaxParts | Maximum number of parts to return at a time. Defaults to `1000`. | String | No |
| PartNumberMarker | The marker after which the returned list begins. By default, entries are listed in UTF-8 binary order. | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ---------------------- | ------------------------------------------------------------ | ----------- |
| err | Error code, which is returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| - Bucket | Destination bucket for the multipart upload | String |
| - Encoding-type | Encoding type for the returned value | String |
|  - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| - UploadId | Multipart upload ID obtained from the `Initiate Multipart Upload` API | String      |
| - Initiator | Initiator of the upload | Object |
| - - DisplayName | Name of the upload initiator | String |
| - - ID | ID of the upload initiator in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` <br>For the root account, &lt;OwnerUin> and &lt;SubUin> have the same value. | String |
| - Owner | Information about the part owner | Object  |
| - - DisplayName | Name of the bucket owner | String |
| - - ID | ID of the bucket owner. This parameter is usually the user’s UIN. | String |
| - StorageClass | Storage class of the parts, such as `STANDARD`, `STANDARD_IA`, and `ARCHIVE`. For more information, please see [Storage Classes Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String |
| - PartNumberMarker | By default, parts are listed in UTF-8 binary order, starting from the part after the marker. | String |
| NextPartNumberMarker  | The part after which the next returned list begins if the list is truncated.    | String    |
| - MaxParts | Maximum number of entries returned at a time | String |
| - IsTruncated | Whether the returned list is truncated. Valid values: `true`; `false` | String |
| - Part | Array | Part information list | ObjectArray |
| - - PartNumber | Part number | String |
| - - LastModified | Last modified time of a part | String |
| - - ETag | MD5 checksum of a part | String |
| - - Size | Part size, in bytes | String |

### Completing a multipart upload

#### Description

This API (Complete Multipart Upload) is used to complete a multipart upload. After all parts are uploaded via the `Upload Part` API, you need to call this API to complete the multipart upload. When using this API, you need to specify the `PartNumber` and `ETag` of each part in the request body for the part information to be verified.
The parts need to be reassembled after they are uploaded, which takes several minutes. When the assembly starts, COS will immediately return the status code `200` and will periodically return spaces during the process to keep the connection active until the assembly is completed. After that, COS will return the assembled result in the body.

- If the uploaded part size is below 1 MB, "400 EntityTooSmall" will be returned when this API is called.
- If the uploaded part numbers are not continuous, "400 InvalidPart" will be returned when this API is called.
- If the part information entries in the request body are not sorted by number in ascending order, "400 InvalidPartOrder" will be returned when this API is called.
- If the `UploadId` does not exist, "404 NoSuchUpload" will be returned when this API is called.

> !We recommend you either complete or abort a multipart upload as early as possible, as the uploaded parts of an incomplete multipart upload will take up storage capacity and incur storage fees.

#### Sample code

[//]: # (.cssg-snippet-complete-multi-upload)
```js
cos.multipartComplete({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: '1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
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
| UploadId | ID of the upload | String | Yes |
| Parts | A list of information about the parts of the multipart upload | ObjectArray | Yes |
| - PartNumber | Part number | String | Yes |
| - ETag | MD5 checksum of each part. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`<br>**Note that double quotation marks are required at the beginning and the end.** | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Error code, which is returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| - Location | Public network access endpoint of the object | String |
| - Bucket | Destination bucket for the multipart upload | String |
| - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| - ETag | Unique ID of the file after assembly in the format of `"uuid-<part quantity>"`. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`. **Note that double quotation marks are required at the beginning and the end.** | String |

### Aborting a multipart upload

#### Description

This API (`Abort Multipart Upload`) is used to abort a multipart upload and delete the uploaded parts. If you call this API and there is an in-progress upload request with the specified `UploadId`, the upload request will fail. If the `uploadId` does not exist, `404` (NoSuchUpload) will be returned.

> !We recommend you either complete or abort a multipart upload as early as possible, as the uploaded parts of an incomplete multipart upload will take up storage capacity and incur storage fees.

#### Sample code

[//]: # (.cssg-snippet-abort-multi-upload)
```js
cos.multipartAbort({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: '1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
    UploadId: 'exampleUploadId' /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| UploadId | Multipart upload ID, which is obtained from the response of the `Initiate Multipart Upload` API | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Error code, which is returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |



## Advanced APIs (Recommended)

The following methods encapsulate the native methods mentioned above. They can implement the complete process of multipart upload and support concurrent multipart upload, checkpoint restart as well as canceling, pausing, and resuming upload tasks.

### Advanced upload

#### Description

This API is used to implement advanced upload. The `SliceSize` parameter can be used to specify the file size limit (1 MB by default) to determine whether to use multipart upload. If the file size is greater than this threshold, multipart upload will be used; otherwise, simple upload will be used.

#### Sample code

[//]: # (.cssg-snippet-transfer-upload-file)
```js
const filePath = "temp-file-to-upload" // Local file path
cos.uploadFile({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: '1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
    FilePath: filePath, /*Required*/
    SliceSize: 1024 * 1024 * 5,     /* Threshold (5 MB in this example) to trigger multipart upload. Optional */
    TaskReady: function(taskId) { /*Optional*/
        console.log(taskId);
    },
    onProgress: function (progressData) { /* Optional */
        console.log(JSON.stringify(progressData));
    },
    onFileFinish: function (err, data, options) {
       console.log(options.Key + 'upload' + (err ? 'failed' : 'completed'));
    },
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
| FilePath                                                         | Path to the file to upload           | String | Yes   |
| SliceSize                                                    | File size threshold in bytes, `1048576` (1 MB) by default. If the file size is equal to or smaller than this value, the file will be uploaded using `putObject`; otherwise, it will be uploaded using `sliceUploadFile`.                                                     | Number    | No   |
| AsyncLimit                                                   | Maximum number of concurrently uploaded parts allowed. This parameter is valid only when a multipart upload is triggered.                                           | Number    | No   |
| StorageClass | Storage class of the object, such as `STANDARD`, `STANDARD_IA`, `ARCHIVE`, and `DEEP_ARCHIVE`. For more information, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String | No |
| UploadAddMetaMd5 | Sets x-cos-meta-md5 as the object’s MD5 checksum in the object’s metadata during upload in the format of a 32-bit lowercase string. Example: `4d00d79b6733c9cc066584a02ed03410`. | String | No |
| onTaskReady | Callback function when an upload task is created. The callback returns a `taskId`, which uniquely identifies the task and can be used to cancel (`cancelTask`), pause (`pauseTask`), or resume (`restartTask`) the task. | Function | No |
| - taskId                                                     | ID of the upload task                                              | String    | No  |
| onProgress | Callback for the upload progress, whose parameter is `progressData` | Function | No |
| - progressData.loaded | Size of the uploaded parts, in bytes | Number | No |
| - progressData.total                                         | Size of the entire file, in bytes                      | Number    | No   |
| - progressData.speed                                         | File upload speed, in bytes/s                 | Number    | No   |
| - progressData.percent | File upload progress, in decimal form. For example, 0.5 means 50% has been uploaded. | Number | No |
| onFileFinish | Completion or error callback for each file | String | Yes |
| - err | Upload error message | Object | No |
| - data | Information about the completion of object upload | Object | No |
| - options | Parameter information about the files that have been uploaded | Object | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Error code, which is returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| - Location   | Access address of the uploaded file.                                        | String |
| - Bucket     | Destination bucket for the multipart upload. This parameter is returned only when a multipart upload is triggered.                                       | String |
| - Key | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324). This parameter is returned only when multipart upload is triggered. | String |
| - ETag | Unique ID of the file after assembly in the format of `"uuid-<part quantity>"`. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`. **Note that double quotation marks are required at the beginning and the end.** | String |
| - VersionId       | Version ID of the uploaded object if versioning is enabled for its bucket. If versioning is not enabled, this parameter is not returned. | String  |

### Uploading an object using multipart upload (checkpoint restart)

#### Description

This API (`Slice Upload File`) is used to upload large files in parts.

#### Sample code

[//]: # (.cssg-snippet-transfer-upload-file)
```js
const filePath = "temp-file-to-upload" // Local file path
cos.sliceUploadFile({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: '1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
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

#### Parameter description

| Parameter | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| FilePath | Path to the file to upload | String | Yes |
| SliceSize              | Part size                                                     | Number   | No   |
| AsyncLimit | Maximum number of parts for concurrent upload | Number | No |
|  StorageClass | Storage class of the object, such as `STANDARD`, `STANDARD_IA` and `ARCHIVE`. For more information, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String | No |
| TaskReady | Callback function when an upload task is created. The callback returns a `taskId`, which uniquely identifies the task and can be used to cancel (`cancelTask`), pause (`pauseTask`), or resume (`restartTask`) the task. | Function | No |
| - taskId | ID of the upload task | String | No |
| onHashProgress | Progress callback function for the MD5 checksum of the object. The callback parameter is the progress object `progressData`. | Function | No |
| - progressData.loaded | Size of the verified parts, in bytes | Number | No |
| - progressData.total | Size of the entire file, in bytes | Number | No |
| - progressData.speed | File verification speed, in bytes/s | Number | No |
| - progressData.percent | Percentage of the file verification progress, in decimal form. For example, 0.5 means 50% has been verified. | Number | No |
| onProgress | Callback for the upload progress, whose parameter is `progressData` | Function | No |
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
| err | Error code, which is returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| - Location | Public network access endpoint of the object | String |
| - Bucket | Destination bucket for the multipart upload | String |
| - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| - ETag | Unique ID of the file after assembly in the format of `"uuid-<part quantity>"`. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`. **Note that double quotation marks are required at the beginning and the end.** | String |
| - VersionId       | Version ID of the uploaded object if versioning is enabled for its bucket. If versioning is not enabled, this parameter is not returned. | String  |

### Batch upload

#### Description

Method 1:
You can call `putObject` or `sliceUploadFile` multiple times to implement batch uploads. Instantiate the `FileParallelLimit` parameter to limit the maximum number (default value: 3) of concurrently uploaded files allowed.

Method 2:
You can call `cos.uploadFiles` to implement batch uploads. The `SliceSize` parameter can be used to set a size limit to determine whether multipart upload is used. The following describes how to use the `uploadFiles` method:

#### Method prototype

Calling `uploadFiles`

[//]: # (.cssg-snippet-transfer-batch-upload-objects)
```js
const filePath1 = "temp-file-to-upload" // Local file path
const filePath2 = "temp-file-to-upload" // Local file path
cos.uploadFiles({
    files: [{
        Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
        Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
        Key: '1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
        FilePath: filePath1,
        onTaskReady: function(taskId) {
          /* Based on `taskId`, you can use queue operations to cancel upload `cos.cancelTask(taskId)`, pause upload `cos.pauseTask(taskId)`, and resume upload `cos.restartTask(taskId)` */
          console.log(taskId);
        }
    }, {
       Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
        Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
        Key: '2.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
        FilePath: filePath2,
        onTaskReady: function(taskId) {
          /* Based on `taskId`, you can use queue operations to cancel upload `cos.cancelTask(taskId)`, pause upload `cos.pauseTask(taskId)`, and resume upload `cos.restartTask(taskId)` */
          console.log(taskId);
        }
    }],
    SliceSize: 1024 * 1024 * 10,    /* Set the file size threshold to trigger a multipart upload to 10 MB */
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
| ---------------------- | ------------------------------------------------------------ | ------ | ---- |
| files | File list. Each item is a parameter object to be passed to `putObject` and `sliceUploadFile`. | Object | Yes |
| - Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| - Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| - FilePath | Path to the file to upload | String | Yes |
| - onTaskReady | Callback function when an upload task is created. The callback returns a `taskId`, which uniquely identifies the task and can be used to cancel (`cancelTask`), pause (`pauseTask`), or resume (`restartTask`) the task. | Function | No |
| -- taskId                                                     | ID of the upload task                                              | String    | No  |
| SliceSize                                                    | File size threshold in bytes, `1048576` (1 MB) by default. If the file size is equal to or smaller than this value, the file will be uploaded using `putObject`; otherwise, it will be uploaded using `sliceUploadFile`.                                                     | Number    | Yes   |
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
| err | Error code, which is returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - files | Error or data for each file | ObjectArray |
| - - error | Upload error message | Object |
| - - data | Information about the completion of object upload | Object |
| - - options | Parameter information about the files that have been uploaded | Object |


### Uploading queue

The SDK for Node.js records all the upload tasks initiated with `putObject` and `sliceUploadFile` in an upload queue. You can use the queue in the following ways:

1. Use `cos.getTaskList` to get the task list.
2. Use `cos.pauseTask`, `cos.restartTask`, and `cos.cancelTask` to perform operations on upload tasks.
3. Use `cos.on('list-update', callback);` to listen for list and progress changes.

For detailed instructions on how to use the upload queue, please see [Queue Demo](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/demo/queue).

#### Canceling an upload task

This API is used to cancel an upload task by `taskId`.

**Example**

[//]: # (.cssg-snippet-transfer-upload-cancel)
```js
var taskId = 'xxxxx';                   /* Required */
cos.cancelTask(taskId);
```

**Parameter description**

| Parameter | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | ID of the upload task. When `sliceUploadFile` is called, the `taskId` is returned via the `TaskReady`callback. | String | Yes |

#### Suspending an upload task

This API is used to pause an upload task by `taskId`.

**Example**

[//]: # (.cssg-snippet-transfer-upload-pause)
```js
var taskId = 'xxxxx';                   /* Required */
cos.pauseTask(taskId);
```

**Parameter description**

| Parameter | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | ID of the upload task. When `sliceUploadFile` is called, the `taskId` is returned via the `TaskReady`callback. | String | Yes |

#### Resuming an upload task

This API is used to resume an upload task by `taskId`. You can resume tasks that have been manually paused through the `pauseTask` API, or automatically paused due to an upload error.

**Example**

[//]: # (.cssg-snippet-transfer-upload-resume)
```js
var taskId = 'xxxxx';                   /* Required */
cos.restartTask(taskId);
```

**Parameter description**

<table>
	<tr><th>Parameter</th><th>Description</th><th>Type</th><th>Required</th></tr>
	<tr><td>taskId</td><td>ID of the upload task. When `sliceUploadFile` is called, the `taskId` is returned via the `TaskReady` callback.</td><td>String</td><td>Yes</td></tr>
</table>
