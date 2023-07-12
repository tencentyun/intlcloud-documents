## Overview

This document provides an overview of advanced APIs and APIs for simple object operations and multipart upload operations, as well as their SDK code samples.
**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ---------------------------------------- |
| [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying objects | Queries some or all the objects in a bucket. |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object in whole | Uploads an object to a bucket. |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | Uploading an object using an HTML form | Uploads an object using an HTML form. |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object. |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system. |
| [OPTIONS Object](https://intl.cloud.tencent.com/document/product/436/8288) | Checking cross-origin resource sharing (CORS) configuration | Sends a preflight request to determine whether an actual CORS request can be sent. |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object | Copies an object to a destination path (object key) |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting an object | Deletes an object from a bucket. |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket. |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access. |


**Multipart operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries in-progress multipart uploads. |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload. |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads an object in multiple parts. |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying an object part | Copies a part of an object. |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries the uploaded parts of a specified multipart upload. |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of an object. |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload and deletes the uploaded parts. |

## Simple Operations

### Query objects

#### Description

This API is used to query some or all the objects in a bucket.

#### Example

Sample 1. Listing all files in the `a` directory

[//]: # (.cssg-snippet-get-bucket)
```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION', /* Required */
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
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
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
var prefix = 'examplefolder/';  /* The directory/prefix of the objects to query*/
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
| Bucket | Bucket name in the format of `BucketName-APPID`. | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Prefix | Key prefix to query objects by | String | No   |
| Delimiter | Separating symbol used to group object keys. It is usually `/`. The identical paths between `Prefix` or, if no `Prefix` is specified, the beginning and the first `delimiter` are grouped and defined as a common prefix. All common prefixes will be listed. | String | No |
| Marker | Indicates where the object key listing begins. Entries are listed starting from the key after the `Marker` in UTF-8 lexicographical order by default. | String | No |
| MaxKeys | Maximum number of entries returned in a single response, which is `1000` (the maximum value allowed) by default | String | No |
| EncodingType | Encoding type of the returned value. Valid value: `url`, meaning that the returned object keys are URL-encoded (percent-encoded) values. For example, "Tencent Cloud" will be encoded to `%E8%85%BE%E8%AE%AF%E4%BA%91`. | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ----------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request succeeds. If the request fails, it will be empty.| Object |
| - headers | Headers | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - Name | Bucket name in the format of `&lt;BucketName-APPID>`, such as `examplebucket-1250000000` | string |
| - Prefix          | Key prefix by which objects are queried. Returned objects are listed according to the UTF-8 lexicographical order of their keys after the prefix.   | String      |
|  - Marker | The marker after which the returned list begins. By default, entries are listed in UTF-8 binary order. | String |
| - MaxKeys | Maximum number of entries returned in a single response | String |
| - Delimiter | Delimiter | String |
| - IsTruncated | Whether the returned list is truncated. Valid values: `true`; `false` | String |
| - NextMarker | Key of the object after which the next returned list begins if the list is truncated | String |
| - CommonPrefixes | Objects with identical paths between the specified prefix and the delimiter, which are grouped together and defined as common prefixes | ObjectArray |
| - - Prefix | A common prefix | String |
| - EncodingType | Encoding type of the returned values. This parameter is applicable to `Delimiter`, `Marker`, `Prefix`, `NextMarker`, and `Key`, | String |
| - Contents | A list of object metadata | ObjectArray |
| - - Key | Object key, i.e., object name | String |
| - - ETag | MD5 checksum of the object, such as `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end.** | String |
| - - Size | Object size, in bytes | String |
| - - LastModified  | Last modified time of the object, in ISO 8601 format, for example, `2019-05-24T10:56:40Z` | String |
| - - Owner | Information about the object owner | Object |
| - - - ID | Complete ID of object owner in the format of `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`, for example, `qcs::cam::uin/100000000001:uin/100000000001`, where `100000000001` is the uin. | String |
| - - - DisplayName | Name of the object owner | String |
| - - StorageClass | Storage class of the object. For the enumerated values, such as `STANDARD`, `STANDARD_IA` and `ARCHIVE`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String |

### Uploading an object in whole

#### Description

This API (PUT Object) is used to upload an object smaller than 5 GB to a specified bucket. To call this API, you need to have permission to write to the bucket. If the object size is larger than 5 GB, please use [Multipart Upload](#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) or [Advanced APIs](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89) for the upload.

> !
> - The key (filename) cannot end with `/`; otherwise, it will be identified as a folder.
> - Each root account (`APPID`) can have up to 1,000 bucket ACLs and an unlimited number of object ACLs. Do not configure ACLs for an object during upload if you don’t need to control access to it. The object will inherit the permissions of its bucket by default.
> - After an object is uploaded, you can use the same key to generate a pre-signed URL, which can be shared with other clients for downloading. To download, please use the `GET` method. The detailed API description is shown below. If your file is set to private-read, note that the pre-signed URL will only be valid for a certain period of time.
> 

#### Example

Uploading a small file

[//]: # (.cssg-snippet-put-object)
```js
const filePath = "temp-file-to-upload" // Local file path
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
    Key: 'exampleobject', /* Required */
    StorageClass: 'STANDARD',
    Body: fs.createReadStream(filePath), // Upload file object
    ContentLength: fs.statSync(filepath).size,  // If the body is the file stream, file size must be specified. Otherwise, onProgress cannot return the progress correctly.
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
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
    Key: 'exampleobject', /* Required */
    Body: Buffer.from('hello!'), /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

Uploading a string

[//]: # (.cssg-snippet-put-object-string)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
    Key: 'exampleobject', /* Required */
    Body: 'hello!',
}, function(err, data) {
    console.log(err || data);
});
```

Upload a Base64-encoded string

[//]: # (.cssg-snippet-put-object-string)
```js
var base64Url = 'data:image/png;base64,iVBORw0KGgo.....';
// Convert to Buffer for upload
var body = Buffer.from(base64Url.split(',')[1] , 'base64');
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
    Key: 'exampleobject.png',              /* Required */
    Body: body,
}, function(err, data) {
    console.log(err || data);
});
```

Creating a directory

[//]: # (.cssg-snippet-put-object-folder)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
    Key: 'a/', /*Required*/
    Body: '',
}, function(err, data) {
    console.log(err || data);
});
```

Uploading a file to a specified directory

```js
var folder = 'examplefolder/';
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Required */
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

Uploading an object (limiting single-URL speed):

>? For more information about the speed limits on object uploads, please see [Single-URL Speed Limits](https://intl.cloud.tencent.com/document/product/436/34072).

[//]: # (.cssg-snippet-put-object-traffic-limit)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /* Required */
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
| ContentLength | HTTP request length (in bytes) as defined in RFC 2616 | String | No |
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
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |
| - ETag | MD5 checksum of the object. The value of this parameter can be used to check whether the object was corrupted during the upload. <br>Example: `"09cba091df696af91549de27b8e7d0f6"`. **Note that double quotation marks are required at the beginning and the end.** | String |
| - Location | Public network access endpoint of the object | String |
| - VersionId       | Version ID of the uploaded object if versioning is enabled for its bucket. If versioning is not enabled, this parameter is not returned. | String  |

### Uploading an object using an HTML form

The SDK for Node.js does not provide a method for the `POST Object` API. If you need to use this API, please see "Solution B: Upload with a Form" in [Practice of Direct Transfer for Web End](https://intl.cloud.tencent.com/document/product/436/9067).

### Querying object metadata

#### Description

This API is used to query the metadata of an object.

#### Example

[//]: # (.cssg-snippet-head-object)
```js
cos.headObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
    Key: 'exampleobject', /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| --------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| IfModifiedSince | If the object is modified after the specified time, the corresponding object metadata will be returned; otherwise, 304 will be returned. | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request succeeds. If the request fails, it will be empty.| Object |
| - statusCode | HTTP status code, such as `200` and `304`. `304` is returned if no modification is made after the specified time. | Number |
| - headers | Headers | Object |
| - x-cos-object-type | Whether an object is appendable. Enumerated values: `normal`, `appendable`. The default value `normal` is not displayed. | String |
| - x-cos-storage-class | Storage class of the object. Enumerated values: `STANDARD` (default), `STANDARD_IA`, `ARCHIVE`. `STANDARD` is not displayed if returned. | String |
| - x-cos-meta-* | User-defined metadata | String |
| - NotModified | Whether an object hasn’t been modified after the specified time | Boolean |
| - ETag | MD5 checksum of the object. The value of `ETag` can be used to check whether the object was corrupted during the upload. <br>Example: `"09cba091df696af91549de27b8e7d0f6"` <br>**Note that double quotation marks are required at the beginning and the end**. | String |
| - VersionId       | Version ID of the uploaded object if versioning is enabled for its bucket. If versioning is not enabled, this parameter is not returned. | String  |

### Download an object

This API (GET Object) is used to download an object in a COS bucket to a local file system. To call this API, you need to have permission to read the object, or the object is set to `public-read`.

#### Example

[//]: # (.cssg-snippet-get-object)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
    Key: 'exampleobject', /* Required */
}, function(err, data) {
    console.log(err || data.Body);
});
```

Getting file content with `Range` specified

[//]: # (.cssg-snippet-get-object-range)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
    Key: 'exampleobject', /* Required */
    Range: 'bytes=1-3', /*Optional*/
}, function(err, data) {
    console.log(err || data.Body);
});
```

Download the file to a specified path:

[//]: # (.cssg-snippet-get-object-path)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
    Key: 'exampleobject', /* Required */
    Output: './exampleobject',
}, function(err, data) {
    console.log(err || data);
});
```

Download the file to a specified write file stream:

[//]: # (.cssg-snippet-get-object-stream)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
    Key: 'exampleobject', /* Required */
    Output: fs.createWriteStream('./exampleobject'),
}, function(err, data) {
    console.log(err || data);
});
```

Downloading an object (limiting single-URL speed):

>?For more information about the speed limits on object downloads, please see [Single-URL Speed Limits](https://intl.cloud.tencent.com/document/product/436/34072).

[//]: # (.cssg-snippet-get-object-traffic-limit)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /* Required */
    Headers: {
      'x-cos-traffic-limit': 819200, // The speed range is 819200 to 838860800, that is 100 KB/s to 100 MB/s. If the value is not within this range, 400 will be returned.
    },
}, function(err, data) {
    console.log(err || data.Body);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------------------- | ------------------------------------------------------------ | ------------------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| Output | An output file path or a write stream. If this parameter is specified, the full content will be written to `data` in the callback function. | String/WriteStream | No |
| ResponseContentType | Sets the `Content-Type` parameter in the response header. | String | No |
| ResponseContentLanguage | Sets the `Content-Language` parameter in the response header. | String | No |
| ResponseExpires | Sets the `Content-Expires` parameter in the response header. | String | No |
| ResponseCacheControl | Sets the `Cache-Control` parameter in the response header. | String | No |
| ResponseContentDisposition | Sets the `Content-Disposition` parameter in the response header. | String | No |
| ResponseContentEncoding | Sets the `Content-Encoding` parameter in the response header. | String | No |
| Range | Byte range of the object as defined in RFC 2616. The range value must be in the format of `bytes=first-last`, where both `first` and `last` are offsets starting from 0. For example, `bytes=0-9` means that you want to copy the first 10 bytes of data of the source object. If this parameter is not specified, the entire object will be downloaded. | String | No |
| If-Modified-Since | If the object is modified after the specified time, the corresponding object metadata will be returned; otherwise, "304 (not modified)" will be returned. | String | No |
| If-Unmodified-Since | If the object is not modified after the specified time, the object will be returned; otherwise, "412 (precondition failed)" will be returned. | String | No |
| IfMatch | The object will be returned only if the value of `ETag` matches the specified content; otherwise, "412 (precondition failed)" will be returned. | String | No |
| IfNoneMatch | The file will be returned only if the value of `ETag` does not match the specified content; otherwise, "304 (not modified)" will be returned. | String | No |
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

| Parameter | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request succeeds. If the request fails, it will be empty.| Object |
| - statusCode | Returns an HTTP status code, such as 200, 304, 403, and 404 | Number |
| - headers | Headers | Object |
| - Cache-Control | Cache directives as defined in RFC 2616. It will be returned only if it is contained in the object metadata or specified through the request parameter. | String |
| - Content-Disposition | Filename as defined in RFC 2616. It will be returned only if it is contained in the object metadata or specified through the request parameter. | String |
| - ContentEncoding | Encoding format as defined in RFC 2616. It will be returned only if it is contained in the object metadata or specified through the request parameter. | String |
| - Expires | Cache expiration time as defined in RFC 2616. It will be returned only if it is contained in the object metadata or specified through the request parameter. | string |
| - x-cos-storage-class | Storage class of the object. Enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE` </br>**Note: If this header is not returned, the storage class is automatically set to `STANDARD`** | String |
| - x-cos-meta-\*                                               | User-defined metadata                                           | String  |
| - NotModified | This attribute will be returned if the request contains `IfModifiedSince`. If the file has been modified, `false` will be returned. If not, `true` will be returned. | Boolean |
| - ETag | MD5 checksum of the object. The value of `ETag` can be used to check whether the object was corrupted during the upload. <br>Example: `"09cba091df696af91549de27b8e7d0f6"` <br>**Note that double quotation marks are required at the beginning and the end**. | String |
| - VersionId       | Version ID of the uploaded object if versioning is enabled for its bucket. If versioning is not enabled, this parameter is not returned. | String  |
| - Body | Content of the returned file. The default form is buffer. | Buffer |

### Checking CORS configuration

#### Description

This API (`OPTIONS Object`) is used to send a preflight request to check the CORS configuration of an object. Before making an actual CORS request, you can send an OPTIONS request that includes the source origin, HTTP method, and headers to COS to determine whether an actual CORS request can be sent. If there is no CORS configuration, "403 Forbidden" will be returned. **You can enable CORS for a bucket using the `PUT Bucket cors` API.**

#### Example

[//]: # (.cssg-snippet-option-object)
```js
cos.optionsObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
    Key: 'exampleobject', /* Required */
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
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| Origin | Origin domain name of the simulated CORS request | String | Yes |
| AccessControlRequestMethod | HTTP method of the simulated CORS request | String | Yes |
| AccessControlRequestHeaders | Headers of the simulated CORS request | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ---------------------------- | ------------------------------------------------------------ | ------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Returns headers | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - headers | Returns headers | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
| - AccessControlAllowOrigin | Source origins (separated by commas) of the simulated CORS request. If the origins are not allowed, this header will not be returned. Example: `*` | String |
| - AccessControlAllowMethods | HTTP methods (separated by commas) of the simulated CORS request (for example, `PUT,GET,POST,DELETE,HEAD`). If the request method is not allowed, this header will not be returned. | String |
| - AccessControlAllowHeaders | Headers (separated by commas) of the simulated CORS request (for example, `accept,content-type,origin,authorization`). If none of the stimulated request headers is allowed, this header will not be returned. | String |
| - AccessControlExposeHeaders | CORS-supported headers (separated by commas) that can be returned, for example, `ETag` | String |
| - AccessControlMaxAge | Validity period of the result of the  `OPTIONS` request, for example, `3600` | String  |
| - OptionsForbidden | Indicates whether the `OPTIONS` request is forbidden. If the returned HTTP status code is 403, this value is `true`. | Boolean |

### Copying objects

#### Description

This API (`PUT Object - Copy`) is used to create a copy of an existing COS object, that is, to copy an object from the source path (object key) to the destination path (object key). During the process, object metadata and ACLs can be modified.
You can use this API to create a copy of an object, modify an object’s metadata (the source object and destination file have the same attributes), and move or rename an object (copy the object first and then call the deletion API).

>! We recommend that you use this API to download an object of 1 MB-5 GB. For objects greater than 5 GB, please use the advanced copy API [Slice Copy File](#.E5.A4.8D.E5.88.B6.E5.AF.B9.E8.B1.A12).
>

#### Example

Copying an object:

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

Modifying the object storage class:

[//]: # (.cssg-snippet-copy-object)
```js
cos.putObjectCopy({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'sourceObject',                                            /* Key must be the same as that in CopySource (required) */
    CopySource: 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject', /*Required*/
    StorageClass: 'ARCHIVE',  /* Set the storage class to ARCHIVE. */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| CopySource | URL of the source object. You can specify a previous version using the URL parameter `?versionId=&lt;versionId>`. | String | Yes |
| ACL | ACL attribute of the object. For the enumerated values, such as `default`, `private`, and `public-read`, please see the **Preset ACL** section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). <br>**Note**: If you do not need access control for the object, set this parameter to `default` or do not specify it, in which case the object will inherit the permissions of its bucket. | String | No |
| GrantRead                   | Grants a user read access in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.<br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'`</li></ul> | String | No   |
| GrantWrite                  | Grants a user write access to the object’s ACL in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.<br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'`</li></ul> | String | No   |
| GrantFullControl       | Grants a user full access in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.</br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` </li></ul> | String               | No   |
| MetadataDirective | Whether to copy the metadata. Enumerated values: `Copy` (default), `Replaced`. If it is set to `Copy`, the metadata of the source object will be copied and the user-defined metadata in the header will be ignored. If it is set to `Replaced`, the metadata of the source object will be replaced with the user-defined metadata in the header. **If the destination and source paths are the same, that is, if you want to modify the metadata, this parameter must be set to `Replaced`.** | String | No |
| CopySourceIfModifiedSince | Required modification time. The object is copied only if it has been modified after the specified time. Otherwise, `412` will be returned. **This parameter can be used together with `CopySourceIfNoneMatch`. Using it together with other conditions may cause a conflict.** | String | No |
| CopySourceIfUnmodifiedSince | Required unmodified time. The object is copied only if it hasn’t been modified since the specified time. Otherwise, `412` will be returned. **This parameter can be used together with `CopySourceIfMatch`. Using it together with other conditions may cause a conflict.** | String | No |
| CopySourceIfMatch | `ETag` that must be matched. The object is copied only if its `ETag` matches the specified value. Otherwise, `412` will be returned. **This parameter can be used together with `CopySourceIfUnmodifiedSince`. Using it together with other conditions may cause a conflict.** | String | No |
| CopySourceIfNoneMatch | `ETag` that cannot be matched. The object is copied only if its `ETag` does not match the specified value. Otherwise, `412` will be returned. **This parameter can be used together with `CopySourceIfModifiedSince`. Using it together with other conditions may cause a conflict**. | string | No |
| StorageClass  | Storage class of the object. For the enumerated values, such as `STANDARD` (default), `STANDARD_IA` and `ARCHIVE`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String | No |
| x-cos-meta-\* | Other user-defined file headers | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |
| - ETag | MD5 checksum of the object, such as `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end.** | String |
| - LastModified | Last modified time of the object, for example, `2017-06-23T12:33:27.000Z` | String |
| - VersionId       | Version ID of the uploaded object if versioning is enabled for its bucket. If versioning is not enabled, this parameter is not returned. | String  | 

### Deleting an object

#### Description

This API (`DELETE Object`) is used to delete an object from a COS bucket. To call this API, you must have write access to the bucket.

#### Example

[//]: # (.cssg-snippet-delete-object)
```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
    Key: 'exampleobject' /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | ObjectKey (object name) is the unique ID of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| VersionId | Version ID of the object or delete marker to delete | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code, such as `200`, `204`, `403`, and `404`. **If the deletion is successful or the object does not exist, `204` or `200` will be returned. If the specified bucket is not found, `404` will be returned.** | Number |
| - headers | Headers | Object |

### Deleting multiple objects

#### Description

This API (DELETE Multiple Objects) is used to delete multiple objects from a bucket in a single request. You can delete up to 1,000 objects in a single request. There are two response modes for you to choose from: `Verbose` and `Quiet`. The `Verbose` mode returns information about the deletion of each object, whereas the `Quiet` mode returns only information about error objects.

#### Example

Deleting multiple files

[//]: # (.cssg-snippet-delete-multi-object)
```js
cos.deleteMultipleObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
    Objects: [
        {Key: 'exampleobject'},
        {Key: 'exampleobject2'},
    ]
}, function(err, data) {
    console.log(err || data);
});
```

Deleting multiple objects with a specified prefix (deleting files in a specified directory)

```js
var bucket: 'examplebucket-1250000000'; /* Required */
var region: 'ap-beijing';     /* Region of the bucket (required) */
var prefix = 'examplefolder/';  /* The directory/prefix of the objects to query*/
var deleteFolder = function (marker) {
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
                if (listResult.IsTruncated === 'true') deleteFolder(nextMarker);
                else console.log('delete complete');
            }
        });
    });
}
deleteFolder();
```

#### Parameter description

| Parameter | Description | Type | Required |
| ----------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Quiet | Specifies whether to use the `Quiet` mode. If set to `true`, the `Quiet` mode is enabled. If set to `false` (default), the `Verbose` mode is enabled. | Boolean | No |
| Objects | List of objects to delete | ObjectArray | Yes |
| - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| - VersionId | Version ID of the object or delete marker to delete | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | Returns an HTTP status code, such as 200, 204, 403, and 404 | Number |
| - headers | Returns headers | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | Returns an HTTP status code, such as 200, 204, 403, and 404 | Number |
| - headers | Returns headers | Object |
| - Deleted | A list of objects that are successfully deleted | ObjectArray |
| - - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| - - VersionId | If the `VersionId` parameter is passed in, it will also be included in the response, indicating the version of the object or delete marker. | String |
| - - DeleteMarker | If versioning is enabled and the `VersionId` parameter is not specified, the deletion operation will not actually delete the object; instead, it will only add a delete marker, meaning that the visible object has been deleted. Enumerated values: `true`, `false` | String |
| - - DeleteMarkerVersionId | `VersionId` of the newly added delete marker if `DeleteMarker` is `true`  | String |
| - Error | A list of objects whose deletion failed | ObjectArray |
| - - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| - - Code | Error code of the deletion failure | String |
| - - Message | Error messages of the deletion failure | String |


### Restoring an archived object

#### Description

This API (POST Object restore) is used to restore an archived COS object. The restored readable object is temporary. You can configure the object to keep it readable and set the time for the object to be deleted. You can use the `Days` parameter to specify the expiration time of the temporary object. If you have not initiated any operation on the object, such as copying it or extending its validity period, before it expires, the temporary object will be automatically deleted. A temporary object is only a copy of the archived object and the source archived object will always exist throughout this period.

#### Example

[//]: # (.cssg-snippet-restore-object)
```js
cos.restoreObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
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
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| RestoreRequest | A container for data restoration | Object | Yes |
| - Days | Expiration time of the temporary copy | Number | Yes |
| - CASJobParameters | A container for the archive job parameters | Object | Yes |
| - - Tier  | Specifies the restoration mode. The following three restoration modes are supported for the ARCHIVE storage class: <ul><li>Standard: restores an object within 3-5 hours.</li><li>Expedited: restores an object within 15 minutes.</li><li>Bulk: restores an object within 5-12 hours.</li></ul>The following two restoration modes are supported for the DEEP ARCHIVE storage class:<ul><li> Standard: restores an object within 12-24 hours.</li><li>Bulk: restores an object within 24-48 hours.</li></ul> | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |



## Multipart Operations

### Querying multipart uploads

#### Description

This API (List Multipart Uploads) is used to query ongoing multipart uploads. Up to 1,000 multipart uploads can be listed at a time.

#### Example

Get the list of unfinished UploadIds prefixed with `exampleobject`. The following is an example:

[//]: # (.cssg-snippet-list-multi-upload)
```js
cos.multipartList({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
    Prefix: 'exampleobject', /*Optional*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
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
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Returns headers | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Returns headers | Object |
| - Bucket | Destination bucket for the multipart upload | String |
| - Encoding-Type | Encoding type for the returned values. Valid value: `url` | String |
| - KeyMarker | Specifies the key where the list starts. | String |
| - UploadIdMarker | Specifies the `UploadId` where the list starts. | String |
| - NextKeyMarker | If the returned list is truncated, the `NextKeyMarker` returned will be the starting point of the subsequent list. | String |
|-  NextUploadIdMarker |  The `UploadId` after which the next returned list begins if the list is truncated | String |
| MaxUploads | Sets the maximum number of entries returned. Value range: 1-1000 | String | 
| - IsTruncated | Indicates whether returned objects are truncated. Valid value: `true` or `false` | String|
| - Prefix | Matching prefix for object keys. This parameter specifies that the response can contain only object keys with the specified prefix. | String |
| - Delimiter | Separating symbol used to group object keys. It is usually `/`. The identical paths between `Prefix` or, if no `Prefix` is specified, the beginning and the first `delimiter` are grouped and defined as a common prefix. All common prefixes will be listed. | String |
| - CommonPrefixes | The identical paths between `prefix` and `delimiter` are grouped and defined as a common prefix. | ObjectArray |
| - - Prefix | Displays specific common prefixes | String |
| - Upload | A set of information about multipart uploads | ObjectArray |
| - - Key | Object key, i.e., object name | String |
| - - UploadId | ID of the multipart upload | String |
| - - StorageClass | Storage class of the parts. For the enumerated values, such as `STANDARD`, `STANDARD_IA` and `ARCHIVE`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String |
| - - Initiator | Information about the upload initiator | Object |
| - - - DisplayName | Name of the upload initiator | String |
| - - - ID | ID of the upload initiator in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`. <br>For the root account, &lt;OwnerUin> and &lt;SubUin> have the same value. | String |
| - - Owner | Information about the part owner | Object  |
| - - - DisplayName | Name of the part owner | String |
| - - - ID | ID of the part owner in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`.<br>For the root account, &lt;OwnerUin> and &lt;SubUin> have the same value. | String |
| - - Initiated | Starting time of the multipart upload | String |

### Initializing a multipart upload

#### Description

This API (Initiate Multipart Uploads) is used to initialize a multipart upload. After a successful operation, an upload ID will be returned, which can be used in the subsequent `Upload Part` requests.

#### Example

[//]: # (.cssg-snippet-init-multi-upload)
```js
cos.multipartInit({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
    Key: 'exampleobject', /* Required */
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
| StorageClass | Storage class of the object. For the enumerated values, such as `STANDARD` (default), `STANDARD_IA` and `ARCHIVE`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String | No |
| x-cos-meta-\* | User-defined headers, which will be returned as the object metadata. The maximum size is 2 KB. | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| Bucket | Destination bucket for the multipart upload in the format of `BucketName-APPID`, for example. `examplebucket-1250000000` | String |
| Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| UploadId | Upload ID, which is required for the subsequent upload | String |

###  Uploading parts

#### Description

This API (`Upload Part`) is used to upload parts after a multipart upload is initialized. It can upload 1-10,000 parts of 1 MB to 5 GB at a time.
<li>When you use the `Initiate Multipart Upload` API to initiate a multipart upload, you can obtain the `uploadId`. This ID uniquely identifies the part and its position in the entire object.</li>
<li>Every time you call the `Upload Part` API, you need to pass `partNumber` (the part number) and `uploadId`. You can upload multiple parts out of order.</li>
<li>When the `uploadId` and `partNumber` of a new part are the same as those of a previously uploaded part, the old part will be overwritten. If the `uploadId` does not exist, the 404 error, "NoSuchUpload", will be returned.</li>

#### Example

[//]: # (.cssg-snippet-upload-part)
```js
const filePath = "temp-file-to-upload" // Local file path
cos.multipartUpload({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
    Key: 'exampleobject', /* Required */
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
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |

### Copying an object part

#### Description

This API (`Upload Part - Copy`) is used to copy a part of an object from the source path to the destination path.

> !To copy an object part, you must first initialize a multipart upload, after which a unique upload ID will be returned. This ID is required in the copy request.

#### Example

[//]: # (.cssg-snippet-upload-part-copy)
```js
cos.uploadPartCopy({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
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
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| CopySource | URL of the source object. You can specify a previous version using the URL parameter `?versionId=&lt;versionId>`. | String | Yes |
| PartNumber | Part number | String | Yes |
| UploadId | To upload an object in parts, you must first initialize the multipart upload. The response of the multipart upload initialization will carry a unique descriptor (an upload ID), which needs to be carried in the multipart upload request. | String | Yes |
| CopySourceRange | Byte range of the source object. The range value must be in the format of `bytes=first-last`, where both `first` and `last` are offsets starting from 0. For example, `bytes=0-9` means to copy the first 10 bytes of the source object. If this parameter is not specified, the entire object will be copied. | String | No |
| CopySourceIfMatch | `Etag` that must be matched. The part will be copied only if its `ETag` matches the specified value. Otherwise, `412` will be returned. This parameter can be used together with `x-cos-copy-source-If-Unmodified-Since`. Using it together with other conditions may cause a conflict. | String | No |
| CopySourceIfNoneMatch | `ETag` that cannot be matched. The part is copied only if its `ETag` does not match the specified value. Otherwise, `412` will be returned. This parameter can be used together with `x-cos-copy-source-If-Modified-Since`. Using it together with other conditions may cause a conflict. | string | No |
| CopySourceIfUnmodifiedSince | Required unmodified time. The object is copied only if it hasn’t been modified since the specified time. Otherwise, `412` will be returned. This parameter can be used together with `x-cos-copy-source-If-Match`. Using it together with other conditions may cause a conflict.  | String | No |
| CopySourceIfModifiedSince | Required modification time. The object is copied only if it has been modified after the specified time. Otherwise, `412` will be returned. This parameter can be used together with `x-cos-copy-source-If-None-Match`. Using it together with other conditions may cause a conflict. | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |
| - ETag | MD5 checksum of the object, such as `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end.** | String |
| - LastModified | Last modified time of the object, in GMT format | String |

### Querying uploaded parts

#### Description

This API (`List Parts`) is used to query the uploaded parts of a specified multipart upload, i.e., listing all successfully uploaded parts of a multipart upload with the specified `uploadId`.

#### Example

[//]: # (.cssg-snippet-list-parts)
```js
cos.multipartListPart({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
    Key: 'exampleobject', /* Required */
    UploadId: 'exampleUploadId', /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
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
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Returns headers | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Returns headers | Object |
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
| - StorageClass |Storage class of the parts. For the enumerated values, such as `STANDARD`, `STANDARD_IA` and `ARCHIVE`, please see [Storage Classes Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String |
| - PartNumberMarker | By default, parts are listed in UTF-8 binary order, starting from the part after the marker. | String |
| NextPartNumberMarker  | The part after which the next returned list begins if the list is truncated    | String    |
| - MaxParts | Maximum number of entries returned at a time | String |
| - IsTruncated | Indicates whether the returned list is truncated. Valid values: `true`, `false` | String |
| - Part | Part information list | ObjectArray |
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

#### Example

[//]: # (.cssg-snippet-complete-multi-upload)
```js
cos.multipartComplete({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
    Key: 'exampleobject', /* Required */
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
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |
| - Location | Public network access endpoint of the object | String |
| - Bucket | Destination bucket for the multipart upload | String |
| - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| - ETag | Unique ID of the file after assembly in the format of `"uuid-<part quantity>"`. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`. **Note that double quotation marks are required at the beginning and the end.** | String |

### Aborting a multipart upload

#### Description

This API (`Abort Multipart Upload`) is used to abort a multipart upload and delete the uploaded parts. If you call this API and there is an in-progress upload request with the specified `UploadId`, the upload request will fail. If the `uploadId` does not exist, `404` (NoSuchUpload) will be returned.

> !We recommend you either complete or abort a multipart upload as early as possible, as the uploaded parts of an incomplete multipart upload will take up storage capacity and incur storage fees.

#### Example

[//]: # (.cssg-snippet-abort-multi-upload)
```js
cos.multipartAbort({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
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
| UploadId | Multipart upload ID, which is obtained from the response of the `Initiate Multipart Upload` API | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |



## Advanced APIs (Recommended)

The following methods encapsulate the native methods mentioned above. They can implement the complete process of multipart upload/copy and support concurrent multipart upload/copy, checkpoint restart as well as canceling, pausing, and resuming upload tasks.

### Advanced upload

#### Description

This API is used to implement advanced upload. The `SliceSize` parameter can be used to specify the file size limit (1 MB by default) to determine whether to use multipart upload. If the file size is greater than this threshold, multipart upload will be used; otherwise, simple upload will be used.

#### Example

[//]: # (.cssg-snippet-transfer-upload-file)
```js
const filePath = "temp-file-to-upload" // Local file path
cos.uploadFile({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /* Required */
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

| Parameter | Description                                                     | Type      | Required |
| ------------------------------------------------------------ | ------------------------------------------------------------ | --------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| FilePath                                                         | Path to the file to upload           | String | Yes   |
| SliceSize                                                    | File size threshold in bytes, `1048576` (1 MB) by default. If the file size is equal to or smaller than this value, the file will be uploaded using `putObject`; otherwise, it will be uploaded using `sliceUploadFile`.                                                     | Number    | No   |
| AsyncLimit                                                   | Maximum number of concurrently uploaded parts allowed. This parameter is valid only when a multipart upload is triggered.                                           | Number    | No   |
| StorageClass | Storage class of the object. For the enumerated values, such as `STANDARD`, `STANDARD_IA`, `ARCHIVE`, and `DEEP_ARCHIVE`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String | No |
| UploadAddMetaMd5 | Sets x-cos-meta-md5 as the object’s MD5 checksum in the object’s metadata during upload in the format of a 32-bit lowercase string. Example: `4d00d79b6733c9cc066584a02ed03410` | String | No |
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
| - statusCode | HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |
| - Location   | Access address of the uploaded file                                        | String |
| - Bucket     | Destination bucket for the multipart upload. This parameter is returned only when a multipart upload is triggered.                                       | String |
| - Key | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324). This parameter is returned only when multipart upload is triggered. | String |
| - ETag | Unique ID of the file after assembly in the format of `"uuid-<part quantity>"`. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`. **Note that double quotation marks are required at the beginning and the end.** | String |
| - VersionId       | Version ID of the uploaded object if versioning is enabled for its bucket. If versioning is not enabled, this parameter is not returned. | String  |

### Multipart upload operations

#### Description

This API (`Slice Upload File`) is used to upload large files in parts.

#### Example

[//]: # (.cssg-snippet-transfer-upload-file)
```js
const filePath = "temp-file-to-upload" // Local file path
cos.sliceUploadFile({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
    Key: 'exampleobject', /* Required */
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
|  StorageClass | Storage class of the object. For the enumerated values, such as `STANDARD`, `STANDARD_IA` and `ARCHIVE`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String | No |
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
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |
| - Location | Public network access endpoint of the object | String |
| - Bucket | Destination bucket for the multipart upload | String |
| - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| - ETag | Unique ID of the file after assembly in the format of `"uuid-<part quantity>"`. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`. **Note that double quotation marks are required at the beginning and the end.** | String |
| - VersionId       | Version ID of the uploaded object if versioning is enabled for its bucket. If versioning is not enabled, this parameter is not returned. | String  |

### Copying objects

#### Description

This API (Slice Copy File) is used to copy an object from the source path to the destination path through multipart copy. During the copy, the object metadata and ACL can be modified. You can use this API to move, rename, and copy a file or modify its attributes.

#### Method prototype

Calling `Slice Copy File`

[//]: # (.cssg-snippet-transfer-copy-object)
```js
cos.sliceCopyFile({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
    Key: 'exampleobject', /*Required*/
    CopySource: 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject', /*Required*/
    onProgress:function (progressData) {                     /* Optional */
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
| CopySource | URL of the source object. You can specify a previous version using the URL parameter `?versionId=<versionId>`. | String | Yes |
| ChunkSize | Size (in bytes) of each part in the multipart copy. Defaults to `1048576` (1 MB). | Number | No |
| SliceSize | Specifies the minimum file size (in bytes) to use multipart copy. The default value is 5 GB. If the file size is equal to or smaller than this value, the file will be uploaded using `putObjectCopy`; otherwise, it will be uploaded using `sliceCopyFile`. | Number | No |
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
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |
| - Location | Public network access endpoint of the object | String |
| - Bucket | Destination bucket for the multipart upload | String |
| - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| - ETag | MD5 checksum of the file after assembly. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end.** | String |
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
        Bucket: 'examplebucket-1250000000',
        Region: 'COS_REGION',
        Key: 'exampleobject',
        FilePath: filePath1,
        onTaskReady: function(taskId) {
          /* Based on `taskId`, you can use queue operations to cancel upload `cos.cancelTask(taskId)`, pause upload `cos.pauseTask(taskId)`, and resume upload `cos.restartTask(taskId)` */
          console.log(taskId);
        }
    }, {
        Bucket: 'examplebucket-1250000000',
        Region: 'COS_REGION',
        Key: '2.jpg',
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
| - Bucket | Bucket name in the format of `BucketName-APPID`. | String | Yes |
| - Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| - FilePath | Path to the file to upload | String | Yes |
| - onTaskReady | Callback function when an upload task is created. The callback returns a `taskId`, which uniquely identifies the task and can be used to cancel (`cancelTask`), pause (`pauseTask`), or resume (`restartTask`) the task. | Function | No |
| -- taskId                                                     | ID of the upload task                                              | String    | No  |
| SliceSize                                                    | Specifies the minimum file size (in bytes) to use multipart upload. The default value is `1048576` (1 MB). If the file size is equal to or smaller than this value, the file will be uploaded using `putObject`; otherwise, it will be uploaded using `sliceUploadFile`.                                                     | Number    | Yes   |
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
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - files | Error or data for each file | ObjectArray |
| - - error | Upload error message | Object |
| - - data | Information about the completion of object upload | Object |
| - - options | Parameter information about the files that have been uploaded | Object |

### Multipart download


#### Description

This API is used to implement multipart download. It supports concurrent part download.

#### Method prototype

Multipart download sample:

```js
var Key = 'test.zip';
cos.downloadFile({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing,
    Key: Key,
    FilePath: './' + Key, // Local path
    ChunkSize: 1024 * 1024 * 8, // Part size
    ParallelLimit: 5, // Number of concurrent parts
    RetryTimes: 3, // Number of retries for multipart download failures
    onTaskReady: function (taskId) {
        console.log(taskId);
    },
    onProgress: function (progressData) {
        console.log(JSON.stringify(progressData));
    },
}, function (err, data) {
    console.log(err || data);
});

// Cancel the download task.
// cos.emit('inner-kill-task', {TaskId: '123'});
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name, formatted as `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| FilePath | Path to store the downloaded file | String | Yes |
| ChunkSize | Part size | Number | No |
| ParallelLimit | Number of parts to download concurrently | Number | No  |
| RetryTimes  | Number of retries for multipart download failures | Number | No  |
| onProgress | Download progress | String | No |
| - progressData.loaded | Size of the uploaded parts, in bytes | Number | No |
| - progressData.total | Size of the entire file, in bytes | Number | No |
| - progressData.speed | File upload speed, in bytes/s | Number | No |
| - progressData.percent | Percentage of the file upload progress, in decimal form. For example, 0.5 means 50% has been uploaded. | Number | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request succeeds. If the request fails, it will be empty.| Object |
| - statusCode | Returns an HTTP status code, such as 200, 304, 403, and 404 | Number |
| - headers | Headers | Object |
| - Cache-Control | Cache directives as defined in RFC 2616. It will be returned only if it is contained in the object metadata or specified through the request parameter. | String |
| - Content-Disposition | Filename as defined in RFC 2616. It will be returned only if it is contained in the object metadata or specified through the request parameter. | String |
| - ContentEncoding | Encoding format as defined in RFC 2616. It will be returned only if it is contained in the object metadata or specified through the request parameter. | String |
| - Expires | Cache expiration time as defined in RFC 2616. It will be returned only if it is contained in the object metadata or specified through the request parameter. | string |
| - x-cos-storage-class | Storage class of the object. Enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE` <br>**Note: If this header is not returned, the storage class is automatically set to `STANDARD`** | String |
| - x-cos-meta-* | User-defined metadata | String |
| - NotModified | This attribute will be returned if the request contains `IfModifiedSince`. If the file has been modified, `false` will be returned. If not, `true` will be returned. | Boolean |
| - ETag | MD5 checksum of the object. The value of `ETag` can be used to check whether the object was corrupted during the upload. <br>Example: `"09cba091df696af91549de27b8e7d0f6"` <br>**Note that double quotation marks are required at the beginning and the end**. | String |
| - VersionId       | Version ID of the uploaded object if versioning is enabled for its bucket. If versioning is not enabled, this parameter is not returned. | String  |

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
