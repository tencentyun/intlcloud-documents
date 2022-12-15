## Overview

This document provides an overview of APIs and SDK code samples for simple operations and multipart operations.

>? For more information on how to troubleshoot common upload errors, see [FAQs](https://intl.cloud.tencent.com/document/product/436/40775).
>

**Simple operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | ---------------------------------------- |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object in whole | Uploads an object to a bucket. |
| [Append Object](https://intl.cloud.tencent.com/document/product/436/7741) | Appending parts | Appends object parts to a bucket.                      |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | Uploading an object by using an HTML form | Uploads an object by using an HTML form. |


**Multipart operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries ongoing multipart uploads. |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload operation | Initializes a multipart upload task. |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads an object in parts. |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries the uploaded parts in a multipart upload. |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of an object. |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload and deletes the uploaded parts. |


## Simple Operations

### Uploading object by using simple upload

#### Feature description

This API (`PUT Object`) is used to upload an object to a bucket. To call this API, you must have write access to the bucket.

> !
> - The key (filename) cannot end with `/`; otherwise, it will be identified as a folder.
> - The uploaded file will overwrite the existing file in the cloud with the same key (filename). If you don't want to overwrite the existing file when versioning is not enabled, make sure that the uploaded file has a different key.
> - Each root account (`APPID`) can have up to 1,000 bucket ACLs and an unlimited number of object ACLs. Do not configure ACLs for an object during upload if you don't need to control the access to it, in which case the object will inherit the permissions of its bucket by default.
> - After an object is uploaded, you can use the same key to generate a pre-signed URL, which can be shared with other clients for downloading. To download the object, use the `GET` method. The detailed API description is as follows. If your file is set to private-read, note that the pre-signed URL will only be valid for a certain period of time.
> - The upload progress `onProgress` depends on the native `xhr.upload.onprogress` method. If you find that the upload progress is inaccurate, check whether a library (such as nuysoft/Mock) that intercepts XHR methods is referenced in your project.
> 

#### Sample code

Upload a small file:

[//]: # (.cssg-snippet-put-object)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket (required) */
    Region: 'COS_REGION',  /* Bucket region (required), such as ap-beijing */
    Key: '1.jpg',  /* Object key stored in the bucket (required), such as `1.jpg` and `a/b/test.txt`. */
    Body: fileObject, /* The file object to be uploaded (required). It can be the file object obtained after the `input[type="file"]` tag is used to select a local file. */
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
    Bucket: 'examplebucket-1250000000', /* Your bucket (required) */
    Region: 'COS_REGION',  /* Bucket region (required), such as ap-beijing */
    Key: '1.txt',  /* Object key stored in the bucket (required), such as `1.jpg` and `a/b/test.txt`. */
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
// Convert to BLOB for upload
var body = dataURLtoBlob(base64Url);
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket (required) */
    Region: 'COS_REGION',  /* Bucket region (required), such as ap-beijing */
    Key: '1.png',  /* Object key stored in the bucket, such as `1.jpg` and `a/b/test.txt` (required) */
    Body: body,
}, function(err, data) {
    console.log(err || data);
});
```

Create directory a:

[//]: # (.cssg-snippet-put-object-folder)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket (required) */
    Region: 'COS_REGION',  /* Bucket region (required), such as ap-beijing */
    Key: 'a/',  /* Object key stored in the bucket, such as `1.jpg` and `a/b/test.txt` (required) */
    Body: '',
}, function(err, data) {
    console.log(err || data);
});
```

Upload objects to directory a/b:

```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket (required) */
    Region: 'COS_REGION',  /* Bucket region (required), such as ap-beijing */
    Key: 'a/b/1.jpg',  /* Object key stored in the bucket, such as `1.jpg` and `a/b/test.txt` (required) */
    Body: fileObject, /* The file object to be uploaded (required). It can be the file object obtained after the `input[type="file"]` tag is used to select a local file. */
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

Upload an object (limit the single-URL speed):

>?For more information on the speed limits on object uploads, see [Single-Connection Bandwidth Limit](https://intl.cloud.tencent.com/document/product/436/34072).

[//]: # (.cssg-snippet-put-object-traffic-limit)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket (required) */
    Region: 'COS_REGION',  /* Bucket region (required), such as ap-beijing */
    Key: '1.jpg',  /* Object key stored in the bucket (required), such as `1.jpg` and `a/b/test.txt`. */
    Body: fileObject, /* The file object to be uploaded (required). It can be the file object obtained after the `input[type="file"]` tag is used to select a local file. */
    Headers: {
      'x-cos-traffic-limit': 819200, // The speed range is 819200–838860800, i.e., 100 KB/s to 100 MB/s. If a value is not within this range, 400 will be returned.
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
| ---------------------- | ------------------------------------------------------------ | ---------------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID`. | String  | Yes   |
| Region  | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key     | Object key (object name), which is the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| Body | Content of the file to be uploaded, which can be a string, file, or `BLOB` object. | String/File/Blob/ArrayBuffer | Yes |
| CacheControl           | The cache policy as defined in RFC 2616, which is saved as part of the object metadata.             | String   | No   |
| ContentDisposition     | The filename as defined in RFC 2616, which is saved as part of the object metadata.             | String   | No   |
| ContentEncoding        | The encoding format as defined in RFC 2616, which is saved as part of the object metadata.              | String   | No   |
| ContentLength          | The length of the content of an HTTP request in bytes as defined in RFC 2616                   | String           | No   |
| ContentType | The content type (MIME) as defined in RFC 2616, which is saved as part of the object metadata. | String | No |
| Expires                | The expiration time as defined in RFC 2616, which is saved as part of the object metadata.             | String           | No   |
| Expect | If `Expect: 100-continue` is used, the request content will be sent only after the confirmation from the server is received. | String | No |
| ACL | ACL attribute of the object. For enumerated values, such as `default`, `private`, and `public-read`, see the **Preset ACL** section in [ACL](https://intl.cloud.tencent.com/document/product/436/30583). <br/>**Note: If you don't need access control for the object, set this parameter to `default` or leave it empty, in which case the object will inherit the permissions of its bucket.** | String | No |
| GrantRead       | Grants a user read access to an object in the format of `id="[OwnerUin]"`. You can separate multiple users by comma.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.<br/>Example: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul> | String               | No   |
| GrantReadAcp       | Grants a user read access to an object ACL in the format of `id="[OwnerUin]"`. You can separate multiple users by comma.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.<br/>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'`</li></ul> | String               | No   |
| GrantWriteAcp       | Grants a user write access to an object ACL in the format of `id="[OwnerUin]"`. You can separate multiple users by comma.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.<br/>Example: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul> | String               | No   |
| GrantFullControl       | Grants a user full access to an object in the format of `id="[OwnerUin]"`. You can separate multiple users by comma.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/<OwnerUin>:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.<br/>Example: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul> | String               | No   |
| StorageClass | Storage class of the object. Enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`, `DEEP_ARCHIVE`. Default value: `STANDARD`. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String     | No |
| x-cos-meta-\* | User-defined header of up to 2 KB in size, which is saved as part of the object metadata. | String | No |
| UploadAddMetaMd5 | Sets `x-cos-meta-md5` as the object's MD5 checksum in the object's metadata during upload in the format of a 32-bit lowercase string, such as `4d00d79b6733c9cc066584a02ed03410`. | String | No |
| onTaskReady | Callback for upload task creation. A `taskId` is returned, which uniquely identifies the task and can be used to cancel (cancelTask), pause (pauseTask), or restart (restartTask) the task. | Function | No |
| - taskId | ID of the upload task | String | No |
| onProgress | Callback for the progress. The response object is `progressData`. | Function | No |
| - progressData.loaded | Size of the uploaded parts in bytes | Number | No |
| - progressData.total | Size of the entire file in bytes                      | Number    | No   |
| - progressData.speed | File upload speed in bytes/s | Number | No |
| - progressData.percent | Percentage of the file upload progress in decimal form; for example, 0.5 means 50% uploaded. | Number | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter  | Description                                               | Type             |
| ------------ | ------------------------------------------------------------ | ------ |
| err    | The object returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | Returned HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Returned headers | Object |
| data         | The object returned when the request is successful. If an error occurs with the request, this parameter is empty.               | Object |
| - statusCode | Returned HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Returned headers | Object |
| - ETag | MD5 checksum of the object. The value of this parameter can be used to check whether the object was corrupted during the upload. <br>Example: `"09cba091df696af91549de27b8e7d0f6"`. **Note that double quotation marks are required at the beginning and the end of the value.** | String |
| - Location   | Access address of the uploaded file                                        | String |
| - VersionId       | Version ID of the uploaded object if versioning is enabled for its bucket. If versioning is not enabled, this parameter will not be returned. The `VersionId` field needs to be set in `Expose-Headers`. For more information, see [Setting CORS](https://intl.cloud.tencent.com/document/product/436/13318). | String  |

### Appending parts

#### Feature description

This API (`APPEND Object`) is used to upload an object to a bucket by appending parts.

> !
> - The COS JavaScript SDK version must be at least v1.3.1.
> - This API can append data only to appendable objects.
> - If an object is uploaded by using the `APPEND Object` API for the first time, it will be automatically determined as "appendable".
> - You can use the `GET Object` or `HEAD Object` API to get the `x-cos-object-type` response header to determine the object type.
> 

#### Sample code

Append parts for the first time:

[//]: # (.cssg-snippet-append-object)
```js
cos.appendObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket (required) */
    Region: 'COS_REGION',  /* Bucket region (required), such as ap-beijing */
    Key: 'test.txt',  /* Object key stored in the bucket, such as `1.jpg` and `a/b/test.txt` (required) */
    Body: fileObject, /* The file object to be uploaded (required). It can be the file object obtained after the `input[type="file"]` tag is used to select a local file. */
    Position: 0, // The value is `0` for the first upload.
}, function(err, data) {
    console.log(err || data);
});
```

Check whether parts can be appended to an object in a bucket:

[//]: # (.cssg-snippet-append-object)
```js
cos.headObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket (required) */
    Region: 'COS_REGION',  /* Bucket region (required), such as ap-beijing */
    Key: 'test.txt',  /* Object key stored in the bucket, such as `1.jpg` and `a/b/test.txt` (required) */
}, function(err, data) {
    if (err) return console.log(err);
    // If `data.headers` does not contain the `x-cos-object-type` field, you need to configure `expose-headers`. For more information, visit https://intl.cloud.tencent.com/document/product/436/13318.
    var objectType = data.headers['x-cos-object-type'];
    console.log(objectType === 'appendable');
});
```

Query the position of the object for parts appending and start upload:

[//]: # (.cssg-snippet-append-object)
```js
cos.headObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket (required) */
    Region: 'COS_REGION',  /* Bucket region (required), such as ap-beijing */
    Key: 'test.txt',  /* Object key stored in the bucket, such as `1.jpg` and `a/b/test.txt` (required) */
}, function(err, data) {
    if (err) return console.log(err);
    // Get the current length (position for upload) of the file to be appended
    var position = data.headers['content-length'];
    cos.appendObject({
        Bucket: 'examplebucket-1250000000', /* Your bucket (required) */
        Region: 'COS_REGION',  /* Bucket region (required), such as ap-beijing */
        Key: 'test.txt',  /* Object key stored in the bucket, such as `1.jpg` and `a/b/test.txt` (required) */
        Body: '66666',
        Position: position,
    },
    function(err, data) {
        if (err) return console.log(err);
        // Get the position for the next upload and continue appending parts
        // If `data.headers` does not contain the `x-cos-next-append-position` field, you need to configure `expose-headers`. For more information, visit https://intl.cloud.tencent.com/document/product/436/13318.
        var nextPosition = data.headers['x-cos-next-append-position'];
        console.log(nextPosition);
    })
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | ---------------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID`. | String  | Yes   |
| Region  | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key     | Object key (object name), which is the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| Body | Content of the file to be uploaded, which can be a string, file, or `BLOB` object. | String/File/Blob/ArrayBuffer | Yes |
| Position | Starting point for the append operation (in bytes). For the first append, the value of this parameter is `0`. For subsequent appends, the value is the `content-length` of the current object. | Number | Yes |
| CacheControl           | The cache policy as defined in RFC 2616, which is saved as part of the object metadata.             | String   | No   |
| ContentDisposition     | The filename as defined in RFC 2616, which is saved as part of the object metadata.             | String   | No   |
| ContentEncoding        | The encoding format as defined in RFC 2616, which is saved as part of the object metadata.              | String   | No   |
| ContentLength          | The length of the content of an HTTP request in bytes as defined in RFC 2616                   | String           | No   |
| ContentType | The content type (MIME) as defined in RFC 2616, which is saved as part of the object metadata. | String | No |
| Expires                | The expiration time as defined in RFC 2616, which is saved as part of the object metadata.             | String           | No   |
| Expect | If `Expect: 100-continue` is used, the request content will be sent only after the confirmation from the server is received. | String | No |
| ACL | ACL attribute of the object. For enumerated values, such as `default`, `private`, and `public-read`, see the **Preset ACL** section in [ACL](https://intl.cloud.tencent.com/document/product/436/30583). <br/>**Note: If you don't need access control for the object, set this parameter to `default` or leave it empty, in which case the object will inherit the permissions of its bucket.** | String | No |
| GrantRead       | Grants a user read access to an object in the format of `id="[OwnerUin]"`. You can separate multiple users by comma.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.<br/>Example: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul> | String               | No   |
| GrantReadAcp       | Grants a user read access to an object ACL in the format of `id="[OwnerUin]"`. You can separate multiple users by comma.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.<br/>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'`</li></ul> | String               | No   |
| GrantWriteAcp       | Grants a user write access to an object ACL in the format of `id="[OwnerUin]"`. You can separate multiple users by comma.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.<br/>Example: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul> | String               | No   |
| GrantFullControl       | Grants a user full access to an object in the format of `id="[OwnerUin]"`. You can separate multiple users by comma.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/<OwnerUin>:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.<br/>Example: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul> | String               | No   |
| StorageClass | Storage class of the object. Enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`, `DEEP_ARCHIVE`. Default value: `STANDARD`. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String     | No |
| x-cos-meta-\* | User-defined header of up to 2 KB in size, which is saved as part of the object metadata. | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter  | Description                                               | Type             |
| ------------ | ------------------------------------------------------------ | ------ |
| err    | The object returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | Returned HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Returned headers | Object |
| data         | The object returned when the request is successful. If an error occurs with the request, this parameter is empty.               | Object |
| - statusCode | Returned HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Returned headers | Object |
| - RequestId | Unique ID of the request. | String |

  
### Uploading object by using HTML form

The JavaScript SDK does not provide a method for the `POST Object` API. If you need to use this API, see "Solution B: Upload with a form" in [Practice of Direct Transfer for Web End](https://intl.cloud.tencent.com/document/product/436/9067).


## Multipart Operations

>?Generally, you don't need to care about these methods. `sliceUploadFile` has encapsulated the following multipart operations, which can be called directly. We recommend you use the advanced upload method `uploadFile`.

### Querying multipart uploads

#### Feature description

This API (`List Multipart Uploads`) is used to query ongoing multipart uploads. Up to 1,000 multipart uploads can be listed at a time.

#### Sample code

Get the list of incomplete multipart uploads with `UploadId` prefixed with `a`:

[//]: # (.cssg-snippet-list-multi-upload)
```js
cos.multipartList({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',     /* Bucket region (required) */
    Prefix: 'a',                        /* Optional */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID`. | String  | Yes   |
| Region  | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Prefix | The object key prefix by which uploads are queried. Note that when you query uploads with the specified prefix, the returned object keys will also contain `Prefix`. | String | No |
| Delimiter | The separating symbol used to group object keys, which is usually `/`. Objects with identical paths between `Prefix` or the beginning of their keys if no `Prefix` is specified and the first delimiter are grouped together and defined as a common prefix. All common prefixes are listed. | String | No |
| encodingType | Encoding type of the returned value. Valid value: `url`. | String | No |
| - MaxUploads | Maximum number of entries to be returned. Value range: 1–1000. Default value: `1000`. | String | No |
| KeyMarker | This parameter is used together with `upload-id-marker`: <ul  style="margin: 0;">If `upload-id-marker` is not specified: </br>&emsp;- Uploads with `ObjectName` lexicographically greater than `key-marker` will be listed.</li><li>If `upload-id-marker` is specified: </br>&emsp;- Uploads with `ObjectName` lexicographically greater than `key-marker` will be listed. </br>&emsp;- Uploads with `ObjectName` lexicographically equal to `key-marker` and `UploadID` greater than `upload-id-marker` will be listed.</li></ul> | string | No |
| UploadIdMarker | This parameter is used together with `key-marker`: <ul  style="margin: 0;"><li>If `key-marker` is not specified: </br>&emsp;- `upload-id-marker` will be ignored. </li><li>If `key-marker` is specified: </br>&emsp;- Uploads with `ObjectName` lexicographically greater than `key-marker` will be listed. </br>&emsp;- Uploads with `ObjectName` lexicographically equal to `key-marker` and `UploadID` greater than `upload-id-marker` will be listed.</li></ul> | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ----------- |
| err    | The object returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | Returned HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Returned headers | Object |
| data         | The object returned when the request is successful. If an error occurs with the request, this parameter is empty.               | Object |
| - statusCode | Returned HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Returned headers | Object |
| - Bucket | Destination bucket for the multipart upload | String |
| - Encoding-Type | Encoding type for the returned values. Valid value: `url`. | String |
| - KeyMarker | The key after which the returned list begins. | String |
| - UploadIdMarker | The `UploadId` after which the returned list begins. | String |
| - NextKeyMarker | The key after which the next returned list begins if the list is truncated. | String |
| - NextUploadIdMarker | The `UploadId` after which the next returned list begins if the list is truncated. | String |
| - MaxUploads | Maximum number of entries to be returned. Value range: 1–1000. | String |
| - IsTruncated | Whether the returned list is truncated. Valid values: `true`, `false`. | String |
| - Prefix | The object key prefix by which uploads are queried. | String |
| - Delimiter | The separating symbol used to group object keys, which is usually `/`. Objects with identical paths between `Prefix` or the beginning of their keys if no `Prefix` is specified and the first delimiter are grouped together and defined as a common prefix. All common prefixes are listed. | String |
| - CommonPrefixes | Objects with identical paths between `Prefix` and the delimiter are grouped together and defined as a common prefix. | ObjectArray |
| - - Prefix | Specific common prefixes | String |
| - Upload | Information of the multipart upload | ObjectArray |
| - - Key | Object key, i.e., object name | String |
| - - UploadId | ID of the multipart upload | String |
| - - StorageClass | Storage class of the parts, such as `STANDARD`, `STANDARD_IA`, `ARCHIVE`, and `DEEP_ARCHIVE`. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String |
| - - Initiator | Initiator of the upload | Object |
| - - - DisplayName | Name of the upload initiator | String |
| - - - ID | ID of the upload initiator in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`. <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value. | String |
| - - Owner | Information of the part owner | Object  |
| - - - DisplayName | Name of the part owner | String |
| - - - ID | ID of the parts owner in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`. <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value. | String |
| - - Initiated        | Start time of the multipart upload                                           | String      |

### Initializing multipart upload

#### Feature description

This API (`Initiate Multipart Upload`) is used to initialize a multipart upload. After successful initialization, an upload ID will be returned, which can be used in subsequent `Upload Part` requests.

#### Sample code

[//]: # (.cssg-snippet-init-multi-upload)
```js
cos.multipartInit({
    Bucket: 'examplebucket-1250000000', /* Your bucket (required) */
    Region: 'COS_REGION',  /* Bucket region (required), such as ap-beijing */
    Key: '1.jpg',  /* Object key stored in the bucket (required), such as `1.jpg` and `a/b/test.txt`. */
    Body: fileObject, /* The file object to be uploaded (required). It can be the file object obtained after the `input[type="file"]` tag is used to select a local file. */
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
| Bucket | Bucket name in the format of `BucketName-APPID`. | String  | Yes   |
| Region  | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key     | Object key (object name), which is the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| CacheControl           | The cache policy as defined in RFC 2616, which is saved as part of the object metadata.             | String   | No   |
| ContentDisposition     | The filename as defined in RFC 2616, which is saved as part of the object metadata.             | String   | No   |
| ContentEncoding        | The encoding format as defined in RFC 2616, which is saved as part of the object metadata.              | String   | No   |
| ContentType | The content type (MIME) as defined in RFC 2616, which is saved as part of the object metadata. | String | No |
| Expires                | The expiration time as defined in RFC 2616, which is saved as part of the object metadata.             | String           | No   |
| ACL | ACL attribute of the object. For enumerated values, such as `default`, `private`, and `public-read`, see the **Preset ACL** section in [ACL](https://intl.cloud.tencent.com/document/product/436/30583). <br>**Note: If you don't need access control for the object, set this parameter to `default` or leave it empty, in which case the object will inherit the permissions of its bucket.** | String | No |
| GrantRead       | Grants a user read access to an object in the format of `id="[OwnerUin]"`. You can separate multiple users by comma.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.<br>Example: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code> </li></ul> | String               | No   |
| GrantFullControl       | Grants a user full access to an object in the format of `id="[OwnerUin]"`. You can separate multiple users by comma.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.</br>Example: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul> | String               | No   |
| StorageClass | Storage class of the object. Enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`, `DEEP_ARCHIVE`. Default value: `STANDARD`. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String     | No |
| x-cos-meta-\* | User-defined header of up to 2 KB in size, which is returned as part of the object metadata. | String | No |
| UploadAddMetaMd5 | Sets `x-cos-meta-md5` as the object's MD5 checksum in the object's metadata during upload in the format of a 32-bit lowercase string, such as `4d00d79b6733c9cc066584a02ed03410`. | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| err    | The object returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| data         | The object returned when the request is successful. If an error occurs with the request, this parameter is empty.               | Object |
| Bucket | Destination bucket for the multipart upload in the format of `BucketName-APPID`, such as `examplebucket-1250000000`. | String |
| Key     | Object key (object name), which is the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| UploadId | Upload ID, which is required for the subsequent upload. | String |

### Uploading parts

#### Feature description

This API (`Upload Part`) is used to upload parts after a multipart upload is initialized. It can upload 1–10,000 parts of 1 MB–5 GB at a time.
- After calling the `Initiate Multipart Upload` API to initialize a multipart upload, you will get an `uploadId`. This ID uniquely identifies the part and marks its position in the object.
- Every time you call the `Upload Part` API, you need to pass in `partNumber` (the part number) and `uploadId`. You can upload multiple parts out of order.
- If the `uploadId` and `partNumber` of a new part are the same as those of a previously uploaded part, the old part will be overwritten. If the `uploadId` does not exist, `404` (NoSuchUpload) will be returned.

#### Sample code

[//]: # (.cssg-snippet-upload-part)
```js
cos.multipartUpload({
    Bucket: 'examplebucket-1250000000', /* Your bucket (required) */
    Region: 'COS_REGION',  /* Bucket region (required), such as ap-beijing */
    Key: '1.jpg',  /* Object key stored in the bucket (required), such as `1.jpg` and `a/b/test.txt`. */
    UploadId: 'exampleUploadId',
    PartNumber: 1,
    Body: fileObject, /* The file object to be uploaded (required). It can be the file object obtained after the `input[type="file"]` tag is used to select a local file. */
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
| Bucket | Bucket name in the format of `BucketName-APPID`. | String  | Yes   |
| Region  | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key     | Object key (object name), which is the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| ContentLength          | The length of the content of an HTTP request in bytes as defined in RFC 2616                   | String           | Yes   |
| PartNumber    | Part number                                                   | Number           | Yes   |
| UploadId      | ID of the current multipart upload task                                       | String           | Yes   |
| Body | Content of the file to be uploaded, which can be a string, file, or `BLOB` object. | String/File/Blob/ArrayBuffer | Yes |
| Expect | The length of the content of an HTTP request in bytes as defined in RFC 2616. If `Expect: 100-continue` is used, the request content will be sent only after the confirmation from the server is received. | String | No |
| ContentMD5     | The Base64-encoded 128-bit MD5 checksum as defined in RFC 1864. This header is used to verify whether the file content has changed. | String | No   |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter  | Description                                               | Type             |
| ------------ | ------------------------------------------------------------ | ------ |
| err    | The object returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | Returned HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Returned headers | Object |
| data         | The object returned when the request is successful. If an error occurs with the request, this parameter is empty.               | Object |
| - statusCode | Returned HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Returned headers | Object |

### Querying uploaded parts

#### Feature description

This API (`List Parts`) is used to query the uploaded parts in a specified multipart upload, i.e., listing all successfully uploaded parts in a multipart upload with the specified `uploadId`.

#### Sample code

[//]: # (.cssg-snippet-list-parts)
```js
cos.multipartListPart({
    Bucket: 'examplebucket-1250000000', /* Your bucket (required) */
    Region: 'COS_REGION',  /* Bucket region (required), such as ap-beijing */
    Key: '1.jpg',  /* Object key stored in the bucket (required), such as `1.jpg` and `a/b/test.txt`. */
    UploadId: 'exampleUploadId',    /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID`. | String  | Yes   |
| Region  | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key     | Object key (object name), which is the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| UploadId | Multipart upload ID, which is obtained from the response of the `Initiate Multipart Upload` API. | String | Yes |
| EncodingType | Encoding type of the returned value. | String | No |
| max-parts | Maximum number of entries to be returned at a time. Default value: `1000`. | String | No |
| PartNumberMarker | The marker after which the returned list begins. By default, entries are listed in UTF-8 binary order. | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ----------- |
| err    | The object returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | Returned HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Returned headers | Object |
| data         | The object returned when the request is successful. If an error occurs with the request, this parameter is empty.               | Object |
| - statusCode | Returned HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Returned headers | Object |
| - Bucket | Destination bucket for the multipart upload | String |
| - Encoding-type        | Encoding type of the returned value                                         | String      |
| - Key     | Object key (object name), which is the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| - UploadId | ID of the multipart upload | String |
| - Initiator | Initiator of the upload | Object |
| - - DisplayName | Name of the upload initiator | String |
| - - ID | ID of the upload initiator in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`. <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value. | String |
| - Owner | Information of the part owner | Object  |
| - - DisplayName | Name of the bucket owner | String |
| - - ID | ID of the bucket owner., which is usually the UIN. | String |
| - StorageClass | Storage class of the parts, such as `STANDARD`, `STANDARD_IA`, `ARCHIVE`, and `DEEP_ARCHIVE`. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String |
| - PartNumberMarker | The marker after which the returned list begins. By default, entries are listed in UTF-8 binary order. | String |
| - NextPartNumberMarker | The `NextMarker` after which the next returned list begins if the list is truncated. | String |
| - MaxParts             | Maximum number of entries to be returned at a time                                       | String      |
| - IsTruncated | Whether the returned list is truncated. Valid values: `true`, `false`. | String |
| - Part | Part information list | ObjectArray |
| - - PartNumber | Part number | String |
| - - LastModified | Last modified time of a part | String |
| - - ETag | MD5 checksum of a part | String |
| - - Size | Part size in bytes | String |

### Completing multipart upload

#### Feature description

This API (`Complete Multipart Upload`) is used to complete a multipart upload. After all parts are uploaded via the `Upload Parts` API, you need to call this API to complete the multipart upload. When using this API, you need to specify the `PartNumber` and `ETag` of each part in the request body for the part information to be verified.
The parts need to be reassembled after they are uploaded, which takes several minutes. When the assembly starts, COS will immediately return the status code `200` and will periodically return spaces during the process to keep the connection active until the assembly is completed. After that, COS will return the assembled result in the body.

- If the uploaded part size is below 1 MB, `400 EntityTooSmall` will be returned when this API is called.
- If the uploaded part numbers are not continuous, `400 InvalidPart` will be returned when this API is called.
- If the part information entries in the request body are not sorted by number in ascending order, `400 InvalidPartOrder` will be returned when this API is called.
- If the `UploadId` does not exist, `404 NoSuchUpload` will be returned when this API is called.

>! We recommend you either complete or abort a multipart upload as early as possible, as the uploaded parts of an incomplete multipart upload will take up storage capacity and incur storage fees.

#### Sample code

[//]: # (.cssg-snippet-complete-multi-upload)
```js
cos.multipartComplete({
    Bucket: 'examplebucket-1250000000', /* Your bucket (required) */
    Region: 'COS_REGION',  /* Bucket region (required), such as ap-beijing */
    Key: '1.jpg',  /* Object key stored in the bucket (required), such as `1.jpg` and `a/b/test.txt`. */
    UploadId: 'exampleUploadId', /* Required */
    Parts: [
        {PartNumber: 1, ETag: 'exampleETag'},
    ]
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ----------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID`. | String  | Yes   |
| Region  | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key     | Object key (object name), which is the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| UploadId | ID of the upload | String | Yes |
| Parts | The list of information of parts in the multipart upload | ObjectArray | Yes |
| - PartNumber    | Part number                                                   | Number           | Yes   |
| - ETag | MD5 checksum of each part, such as `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. <br>**Note that double quotation marks are required at the beginning and the end of the value.** | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter  | Description                                               | Type             |
| ------------ | ------------------------------------------------------------ | ------ |
| err    | The object returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | Returned HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Returned headers | Object |
| data         | The object returned when the request is successful. If an error occurs with the request, this parameter is empty.               | Object |
| - statusCode | Returned HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Returned headers | Object |
| - Location   | Access address of the uploaded file                                        | String |
| - Bucket | Destination bucket for the multipart upload | String |
| - Key     | Object key (object name), which is the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| - ETag | Unique ID of the file after assembly in the format of `"uuid-<part quantity>"`, such as `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`. **Note that double quotation marks are required at the beginning and the end of the value.** | String |

### Aborting multipart upload

#### Feature description

This API (`Abort Multipart Upload`) is used to abort a multipart upload and delete the uploaded parts. If you call this API and there is an ongoing upload request with the specified `UploadId`, the upload request will fail. If the `uploadId` does not exist, `404` (NoSuchUpload) will be returned.

>! We recommend you either complete or abort a multipart upload as early as possible, as the uploaded parts of an incomplete multipart upload will take up storage capacity and incur storage fees.

#### Sample code

[//]: # (.cssg-snippet-abort-multi-upload)
```js
cos.multipartAbort({
    Bucket: 'examplebucket-1250000000', /* Your bucket (required) */
    Region: 'COS_REGION',  /* Bucket region (required), such as ap-beijing */
    Key: '1.jpg',  /* Object key stored in the bucket (required), such as `1.jpg` and `a/b/test.txt`. */
    UploadId: 'exampleUploadId'    /* Required */
}, function(err, data) {
    console.log(err || data);
});

```

#### Parameter description

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID`. | String  | Yes   |
| Region  | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key     | Object key (object name), which is the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| UploadId | Multipart upload ID, which is obtained from the response of the `Initiate Multipart Upload` API. | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter  | Description                                               | Type             |
| ------------ | ------------------------------------------------------------ | ------ |
| err    | The object returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | Returned HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Returned headers | Object |
| data         | The object returned when the request is successful. If an error occurs with the request, this parameter is empty.               | Object |
| - statusCode | Returned HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Returned headers | Object |


## Advanced APIs (Recommended)

We strongly recommend you use advanced APIs, which encapsulate the native methods mentioned above. They can implement the complete process of multipart upload and support concurrent multipart upload, checkpoint restart, as well as canceling, pausing, and resuming upload tasks.

### Advanced upload

#### Feature description
This API (`Upload File`) is used to implement an advanced upload. You can use the `SliceSize` parameter to specify a file size threshold (1 MB by default). If a file is larger than this threshold, it will be uploaded in parts (sliceUploadFile); otherwise, it will be uploaded in whole (putObject).
#### Sample code

[//]: # (.cssg-snippet-transfer-upload-file)
```js
cos.uploadFile({
    Bucket: 'examplebucket-1250000000', /* Your bucket (required) */
    Region: 'COS_REGION',  /* Bucket region (required), such as ap-beijing */
    Key: '1.jpg',  /* Object key stored in the bucket (required), such as `1.jpg` and `a/b/test.txt`. */
    Body: fileObject, /* The file object to be uploaded (required). It can be the file object obtained after the `input[type="file"]` tag is used to select a local file. */
    SliceSize: 1024 * 1024 * 5,     /* The threshold (5 MB in this example) to trigger multipart upload (optional) */
    onTaskReady: function(taskId) {                   /* Optional */
        console.log(taskId);
    },
    onProgress: function (progressData) {           /* Optional */
        console.log(JSON.stringify(progressData));
    },
    onFileFinish: function (err, data, options) {   /* Optional */
       console.log(options.Key + 'upload' + (err ? 'failed' : 'completed'));
    },
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------------------------------------------------------------ | ------------------------------------------------------------ | --------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID`. | String  | Yes   |
| Region  | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key     | Object key (object name), which is the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| Body | Content of the file to be uploaded, which can be a file or `BLOB` object. | File/Blob | Yes |
| SliceSize                                                    | File size threshold in bytes, which is `1048576` (1 MB) by default. If the file size is equal to or smaller than this value, the file will be uploaded through `putObject`; otherwise, it will be uploaded through `sliceUploadFile`.                                                     | Number    | No   |
| AsyncLimit                                                   | Maximum number of concurrently uploaded parts allowed. This parameter is valid only when a multipart upload is triggered.                                           | Number    | No   |
| StorageClass | Storage class of the object, such as `STANDARD`, `STANDARD_IA`, `ARCHIVE`, and `DEEP_ARCHIVE`. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String | No |
| UploadAddMetaMd5 | Sets `x-cos-meta-md5` as the object's MD5 checksum in the object's metadata during upload in the format of a 32-bit lowercase string, such as `4d00d79b6733c9cc066584a02ed03410`. | String | No |
| CacheControl           | The cache policy as defined in RFC 2616, which is saved as part of the object metadata.             | String   | No   |
| ContentDisposition     | The filename as defined in RFC 2616, which is saved as part of the object metadata.             | String   | No   |
| ContentEncoding        | The encoding format as defined in RFC 2616, which is saved as part of the object metadata.              | String   | No   |
| ContentLength          | The length of the content of an HTTP request in bytes as defined in RFC 2616                   | String           | No   |
| ContentType | The content type (MIME) as defined in RFC 2616, which is saved as part of the object metadata. | String | No |
| Expires                | The expiration time as defined in RFC 2616, which is saved as part of the object metadata.             | String           | No   |
| Expect | If `Expect: 100-continue` is used, the request content will be sent only after the confirmation from the server is received. | String | No |
| onTaskReady | Callback for upload task creation. A `taskId` is returned, which uniquely identifies the task and can be used to cancel (cancelTask), pause (pauseTask), or restart (restartTask) the task. | Function | No |
| - taskId | ID of the upload task | String | No |
| onProgress | Callback for the upload progress. The callback parameter is `progressData`. | Function | No |
| - progressData.loaded | Size of the uploaded parts in bytes | Number | No |
| - progressData.total | Size of the entire file in bytes                      | Number    | No   |
| - progressData.speed | File upload speed in bytes/s | Number | No |
| - progressData.percent | Percentage of the file upload progress in decimal form; for example, 0.5 means 50% uploaded. | Number | No |
| onFileFinish           | Callback for file upload success or failure                                       | Function    | No   |
| - err | Upload error message | Object | No |
| - data | Information of the completion of object upload | Object | No |
| - options | Parameter information of the files that have been uploaded | Object | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter  | Description                                               | Type             |
| ------------ | ------------------------------------------------------------ | ------ |
| err    | The object returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | Returned HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Returned headers | Object |
| data         | The object returned when the request is successful. If an error occurs with the request, this parameter is empty.               | Object |
| - statusCode | Returned HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Returned headers | Object |
| - Location   | Access address of the uploaded file                                        | String |
| - Bucket     | Destination bucket for the multipart upload. This parameter will be returned only when a multipart upload is triggered.                                       | String |
| - Key     | Object key (object name), which is the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). This parameter will be returned only when a multipart upload is triggered. | String |
| - ETag | Unique ID of the file after assembly in the format of `"uuid-<part quantity>"`, such as `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`. **Note that double quotation marks are required at the beginning and the end of the value.** | String |
| - VersionId       | Version ID of the uploaded object if versioning is enabled for its bucket. If versioning is not enabled, this parameter will not be returned. The `VersionId` field needs to be set in `Expose-Headers`. For more information, see [Setting CORS](https://intl.cloud.tencent.com/document/product/436/13318). | String  |

### Uploading object by using multipart upload (checkpoint restart)

#### Feature description

This API (`Slice Upload File`) is used to upload a large file in parts.

>?
>- If the browser is not closed, you can pause, resume, or cancel the upload.
>- If you upload the same file to the same bucket path after refreshing the browser, the file content will be verified based on `UploadId`, and the upload will resume from where left off if the verification is passed.

#### Sample code

[//]: # (.cssg-snippet-transfer-upload-file)
```js
cos.sliceUploadFile({
    Bucket: 'examplebucket-1250000000', /* Your bucket (required) */
    Region: 'COS_REGION',  /* Bucket region (required), such as ap-beijing */
    Key: '1.jpg',  /* Object key stored in the bucket (required), such as `1.jpg` and `a/b/test.txt`. */
    Body: fileObject, /* The file object to be uploaded (required). It can be the file object obtained after the `input[type="file"]` tag is used to select a local file. */
    onTaskReady: function(taskId) {                   /* Optional */
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

#### Parameter description

| Parameter | Description | Type | Required |
| ------------------------------------------------------------ | ------------------------------------------------------------ | --------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID`. | String  | Yes   |
| Region  | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key     | Object key (object name), which is the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| Body | Content of the file to be uploaded, which can be a file or `BLOB` object. | File/Blob | Yes |
| SliceSize              | Part size                                                     | Number   | No   |
| AsyncLimit | Maximum number of concurrently uploaded parts allowed | Number | No |
| StorageClass | Storage class of the object, such as `STANDARD`, `STANDARD_IA`, `ARCHIVE`, and `DEEP_ARCHIVE`. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String | No |
| UploadAddMetaMd5 | Sets `x-cos-meta-md5` as the object's MD5 checksum in the object's metadata during upload in the format of a 32-bit lowercase string, such as `4d00d79b6733c9cc066584a02ed03410`. | String | No |
| CacheControl           | The cache policy as defined in RFC 2616, which is saved as part of the object metadata.             | String   | No   |
| ContentDisposition     | The filename as defined in RFC 2616, which is saved as part of the object metadata.             | String   | No   |
| ContentEncoding        | The encoding format as defined in RFC 2616, which is saved as part of the object metadata.              | String   | No   |
| ContentLength          | The length of the content of an HTTP request in bytes as defined in RFC 2616                   | String           | No   |
| ContentType | The content type (MIME) as defined in RFC 2616, which is saved as part of the object metadata. | String | No |
| Expires                | The expiration time as defined in RFC 2616, which is saved as part of the object metadata.             | String           | No   |
| Expect | If `Expect: 100-continue` is used, the request content will be sent only after the confirmation from the server is received. | String | No |
| onTaskReady | Callback for upload task creation. A `taskId` is returned, which uniquely identifies the task and can be used to cancel (cancelTask), pause (pauseTask), or restart (restartTask) the task. | Function | No |
| - taskId | ID of the upload task | String | No |
| onHashProgress | Callback for the progress of MD5 checksum calculation. The callback parameter is `progressData`. | Function | No |
| - progressData.loaded | Size of the verified parts in bytes | Number | No |
| - progressData.total | Size of the entire file in bytes                      | Number    | No   |
| - progressData.speed | File verification speed in bytes/s | Number | No |
| - progressData.percent | Percentage of the file verification progress in decimal form; for example, 0.5 means 50% verified. | Number | No |
| onProgress | Callback for the upload progress. The callback parameter is `progressData`. | Function | No |
| - progressData.loaded | Size of the uploaded parts in bytes | Number | No |
| - progressData.total | Size of the entire file in bytes                      | Number    | No   |
| - progressData.speed | File upload speed in bytes/s | Number | No |
| - progressData.percent | Percentage of the file upload progress in decimal form; for example, 0.5 means 50% uploaded. | Number | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter  | Description                                               | Type             |
| ------------ | ------------------------------------------------------------ | ------ |
| err    | The object returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | Returned HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Returned headers | Object |
| data         | The object returned when the request is successful. If an error occurs with the request, this parameter is empty.               | Object |
| - statusCode | Returned HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Returned headers | Object |
| - Location   | Access address of the uploaded file                                        | String |
| - Bucket | Destination bucket for the multipart upload | String |
| - Key     | Object key (object name), which is the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| - ETag | Unique ID of the file after assembly in the format of `"uuid-<part quantity>"`, such as `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`. **Note that double quotation marks are required at the beginning and the end of the value.** | String |
| - VersionId       | Version ID of the uploaded object if versioning is enabled for its bucket. If versioning is not enabled, this parameter will not be returned. The `VersionId` field needs to be set in `Expose-Headers`. For more information, see [Setting CORS](https://intl.cloud.tencent.com/document/product/436/13318). | String  |


### Batch upload

#### Feature description

Option 1:
You can call `putObject` or `sliceUploadFile` multiple times to implement batch uploads. Instantiate the `FileParallelLimit` parameter to limit the maximum number of concurrently uploaded files allowed, which is 3 by default.

Option 2:
You can call `cos.uploadFiles` to implement batch uploads. The `SliceSize` parameter can be used to control the file. The following describes how to use the `uploadFiles` method:

#### Method prototype

Call `uploadFiles`:

[//]: # (.cssg-snippet-transfer-batch-upload-objects)
```js
cos.uploadFiles({
    files: [{
        Bucket: 'examplebucket-1250000000', /* Your bucket (required) */
        Region: 'COS_REGION',  /* Bucket region (required), such as ap-beijing */
        Key: '1.jpg',  /* Object key stored in the bucket (required), such as `1.jpg` and `a/b/test.txt`. */
        Body: fileObject1, /* The file object to be uploaded (required). It can be the file object obtained after the `input[type="file"]` tag is used to select a local file. */
        onTaskReady: function(taskId) {
          /* Based on `taskId`, you can use queue operations to cancel (`cos.cancelTask(taskId)`), pause (`cos.pauseTask(taskId)`), or resume (`cos.restartTask(taskId)`) the upload. */
          console.log(taskId);
        }
    }, {
        Bucket: 'examplebucket-1250000000', /* Your bucket (required) */
        Region: 'COS_REGION',  /* Bucket region (required), such as ap-beijing */
        Key: '2.jpg',  /* Object key stored in the bucket (required), such as `1.jpg` and `a/b/test.txt`. */
        Body: fileObject2, /* The file object to be uploaded (required). It can be the file object obtained after the `input[type="file"]` tag is used to select a local file. */
        onTaskReady: function(taskId) {
        /* Based on `taskId`, you can use queue operations to cancel (`cos.cancelTask(taskId)`), pause (`cos.pauseTask(taskId)`), or resume (`cos.restartTask(taskId)`) the upload. */
        console.log(taskId);
      }
    }],
    SliceSize: 1024 * 1024 * 10,    /* Set the file size threshold to trigger a multipart upload to 10 MB. */
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
| - Bucket | Bucket name in the format of `BucketName-APPID`. | String  | Yes   |
| - Region  | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| - Key     | Object key (object name), which is the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| - Body | Content of the file to be uploaded, which can be a file or `BLOB` object. | File/Blob | Yes |
| - CacheControl           | The cache policy as defined in RFC 2616, which is saved as part of the object metadata.             | String   | No   |
| - ContentDisposition     | The filename as defined in RFC 2616, which is saved as part of the object metadata.             | String   | No   |
| - ContentEncoding        | The encoding format as defined in RFC 2616, which is saved as part of the object metadata.              | String   | No   |
| - ContentLength          | The length of the content of an HTTP request in bytes as defined in RFC 2616                   | String           | No   |
| - ContentType | The content type (MIME) as defined in RFC 2616, which is saved as part of the object metadata. | String | No |
| - Expires                | The expiration time as defined in RFC 2616, which is saved as part of the object metadata.             | String           | No   |
| - Expect | If `Expect: 100-continue` is used, the request content will be sent only after the confirmation from the server is received. | String | No |
| - onTaskReady | The callback for upload task creation. A `taskId` is returned, which uniquely identifies the task and can be used to cancel (cancelTask), pause (pauseTask), or restart (restartTask) the task. | Function | No |
| taskId                                                     | ID of the upload task                                              | String    | No  |
| SliceSize | File size threshold in bytes, which is `1048576` (1 MB) by default. If the file size is equal to or smaller than this value, the file will be uploaded through `putObject`; otherwise, it will be uploaded through `sliceUploadFile`.                                                     | Number    | Yes   |
| AsyncLimit                                                   | Maximum number of concurrently uploaded parts allowed. This parameter is valid only when a multipart upload is triggered.                                           | Number    | No   |
| onProgress | Upload progress calculated by aggregating the progress of all tasks | String | Yes |
| - progressData.loaded | Size of the uploaded parts in bytes | Number | No |
| - progressData.total | Size of the entire file in bytes                      | Number    | No   |
| - progressData.speed | File upload speed in bytes/s | Number | No |
| - progressData.percent | Percentage of the file upload progress in decimal form; for example, 0.5 means 50% uploaded. | Number | No |
| onFileFinish           | Callback for file upload success or failure                                       | Function    | No   |
| - err | Upload error message | Object | No |
| - data | Information of the completion of object upload | Object | No |
| - options | Parameter information of the files that have been uploaded | Object | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ----------- |
| err    | The object returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | Returned HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Returned headers | Object |
| data         | The object returned when the request is successful. If an error occurs with the request, this parameter is empty.               | Object |
| - files | Error or data for each file | ObjectArray |
| - - error    | Upload error message                                               | Object      |
| - - data | Information of the completion of object upload | Object |
| - - options | Parameter information of the files that have been uploaded | Object |

### Upload queue

The JavaScript SDK records all the `putObject` and `sliceUploadFile` upload tasks in a queue. Relevant queue operations are as follows:

1. Use `var taskList = cos.getTaskList()` to get the task list.
2. Use `cos.pauseTask()`, `cos.restartTask()`, or `cos.cancelTask()` to manage the task.
3. Use `cos.on('list-update', callback);` to listen for list and progress changes.

For detailed instructions on how to use the upload queue, see the queue demo at [GitHub](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/demo/queue).

#### Canceling upload task

This API is used to cancel an upload task by `taskId`.

**Sample**

[//]: # (.cssg-snippet-transfer-upload-cancel)
```js
var taskId = 'xxxxx';                   /* Required */
cos.cancelTask(taskId);
```

**Parameter description**

| Parameter | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | ID of the upload task. When `sliceUploadFile` is called, the `taskId` will be returned through the `TaskReady`callback. | String | Yes |

#### Pausing upload task

This API is used to pause an upload task by `taskId`.

**Sample**

[//]: # (.cssg-snippet-transfer-upload-pause)
```js
var taskId = 'xxxxx';                   /* Required */
cos.pauseTask(taskId);
```

**Parameter description**

| Parameter | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | ID of the upload task. When `sliceUploadFile` is called, the `taskId` will be returned through the `TaskReady`callback. | String | Yes |

#### Resuming upload task

This API is used to resume an upload task by `taskId`. You can resume tasks that have been manually paused through the `pauseTask` API or automatically paused due to an upload error.

**Sample**

[//]: # (.cssg-snippet-transfer-upload-resume)
```js
var taskId = 'xxxxx';                   /* Required */
cos.restartTask(taskId);
```

**Parameter description**

<table>
	<tr><th>Parameter</th><th>Description</th><th>Type</th><th>Required</th></tr>
	<tr><td>taskId</td><td>ID of the upload task. When `sliceUploadFile` is called, the `taskId` will be returned through the `TaskReady`callback.</td><td>String</td><td>Yes</td></tr>
</table>
