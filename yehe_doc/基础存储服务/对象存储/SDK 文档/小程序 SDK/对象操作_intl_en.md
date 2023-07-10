## Overview

This document provides an overview of APIs and SDK code samples related to simple operations and other object operations.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ---------------------------------------- |
| [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying objects | Queries some or all the objects in a bucket. |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object in whole | Uploads an object to a bucket. |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | Uploading an object using an HTML form | Uploads an object using an HTML form. |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object. |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object |
| [OPTIONS Object](https://intl.cloud.tencent.com/document/product/436/8288) | Checking cross-origin resource sharing (CORS) configuration | Sends a preflight request to determine whether an actual CORS request can be sent. |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object | Copies an object to a destination path (object key) |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting an object | Deletes an object from a bucket. |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket. |

**Multipart operations**

| API | Operation | Description |
| :----------------------------------------------------------- | :------------- | :----------------------------------- |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries in-progress multipart uploads. |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload. |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads an object in multiple parts. |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying an object part | Copies a part of an object. |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries the uploaded parts of a specified multipart upload. |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of an object. |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload and deletes the uploaded parts. |


**Other operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access. |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting an object ACL | Sets an ACL for an object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying an object ACL | Queries the ACL of an object |

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

Sample 2. Listing the files in the `a` directory without deep traversal

[//]: # (.cssg-snippet-get-bucket-with-delimiter)
```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',                                  /* Required */
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
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Prefix | Key prefix to query objects by | String | No   |
| Delimiter | A separating symbol (usually `\`) used to group object keys. The identical paths between a prefix or, if no prefix is specified, the beginning and the first `delimiter` are grouped and defined as a common prefix. All common prefixes will be listed. | String | No |
| Marker | Marks the starting object key. Object key entries will be returned in UTF-8 lexicographical order starting from the first object key after the marker | String | No |
| MaxKeys | Maximum number of entries returned in a single response. Defaults to `1000`. | String | No |
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
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - headers | Headers | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - Name | Bucket name in the format of `BucketName-APPID`, such as `examplebucket-1250000000` | String |
| - Prefix          | Key prefix by which objects are queried. Returned objects are listed according to the UTF-8 lexicographical order of their keys after the prefix.   | String      |
| - Marker | Marker for the starting object key. Object key entries will be returned in UTF-8 lexicographical order, starting from the first object key after the marker | String |
| - MaxKeys | Maximum number of entries returned in a single response | String |
| - Delimiter | Delimiter | String |
| - IsTruncated | Whether the returned list is truncated. Valid values: `true`; `false` | String |
| - NextMarker | Key of the object after which the next returned list begins if the list is truncated | String |
| - CommonPrefixes | Objects with identical paths between the specified prefix and the delimiter, which are grouped together and defined as common prefixes | ObjectArray |
| - - Prefix | A common prefix | String |
| - EncodingType | Indicates the encoding method of the returned value, which is effective for `Delimiter`, `Marker`, `Prefix`, `NextMarker`, and `Key` | String |
| - Contents | A list of object metadata | ObjectArray |
| - - Key | Object key, i.e., object name | String |
| - - ETag | MD5 checksum of the object, such as `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end.** | String |
| - - Size | Object size, in bytes | String |
| - - LastModified  | Last modified time of the object, in ISO 8601 format, for example, `2019-05-24T10:56:40Z` | String |
| - - Owner | Information about the object owner | Object |
| - - - ID | Complete ID of the object owner. Format: `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`, such as `qcs::cam::uin/100000000001:uin/100000000001`，where 100000000001 is uin | String |
| - - - DisplayName | Name of the object owner | String |
| - - StorageClass | Sets the object storage class. Enumerated values: `STANDARD`, `STANDARD_IA` and `ARCHIVE`. For more information, see [Storage Class](https://intl.cloud.tencent.com/document/product/436/30925) | String |

### Uploading an object using simple upload

#### Description

This API (`PUT Object`) is used to upload an object to a bucket. To call this API, you must have write access to the bucket.

> !
> 1. The Key (filename) cannot end with `/`; otherwise, it will be identified as a folder.
> 2. Each root account (`AAPID`) can have up to 1,000 bucket ACLs and an unlimited number of object ACLs. If you do not need an ACL for an object, you can choose not to configure an ACL for the object during upload. In this way, the object will inherit the permissions of its bucket by default.
> 3. After an object is uploaded, you can use the same key to generate a pre-signed URL, which can be shared with other clients for downloading (to download, please use the `GET` method. The detailed API description is shown below). If your file is set to private-read, note that the pre-signed URL will only be valid for a certain period of time.

#### Example

Upload a string as the file content:

[//]: # (.cssg-snippet-put-object-string)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',                                  /* Required */
    Key: 'picture.jpg',              /* Required */
    Body: 'hello!',
}, function(err, data) {
    console.log(err || data);
});
```

Creating a directory

[//]: # (.cssg-snippet-put-object-folder)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',                                  /* Required */
    Key: 'a/', /*Required*/
    Body: '',
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
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| Body | Text content of the created file, which can be a string | String | Yes |
| CacheControl | Cache policy as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentDisposition | Filename as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentEncoding | Encoding format as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentLength | HTTP request length (in bytes) as defined in RFC 2616 | String | No |
| ContentType | Content type (MIME) as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| Expires | Expiration time as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| Expect | If `Expect: 100-continue` is used, the request content will be sent only after confirmation from the server is received | String | No |
| ACL   | Defines the access control list (ACL) attribute of the object. For the enumerated values such as `default`, `private`, and `public-read`, see the Preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). <br>**Note:** If you do not need access control for the object, set `default` for this parameter or simply leave it blank, and the object will inherit the permissions of the bucket | String | No |
| GrantRead | Grants the user read permission in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users. <br><li>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br><li>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantReadAcp | Grants the user read permission to the object’s ACL in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<br/><li>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br><li>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantWriteAcp | Grants the user write permission to the object’s ACL in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<br><li>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br><li>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantFullControl | Grants the user full permission in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users. <br><li>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| StorageClass | Storage class of the object. For the enumerated values, such as `STANDARD` (default), `STANDARD_IA`, and `ARCHIVE`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String | No |
| x-cos-meta-* | User-defined headers, which will be returned as the object metadata. The maximum size is 2 KB. | String | No |
| TaskReady | Callback function when an upload task is created. The callback returns a `taskId`, which uniquely identifies the task and can be used to cancel (`cancelTask`), pause (`pauseTask`), or resume (`restartTask`) the task. | Function | No |
| - taskId | ID of the upload task | String | No |
| onProgress | Callback of the progress. Attributes of the response object `progressData` are as follows: | Function | No |
| - progressData.loaded | Size of the uploaded parts, in bytes | Number | No |
| - progressData.total | Size of the entire file, in bytes | Number | No |
| - progressData.speed | File upload speed, in bytes/s | Number | No |
| - progressData.percent | Percentage of the file upload progress in decimal form; for example, 0.5 means 50% downloaded | Number | No |

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

This API (POST Object) is used to upload an object selected by the user through `wx.chooseImage` to a specified bucket. To call this API, you need to have permission to write the bucket.

>! `onProgress` depends on the mini program [UploadTask.onProgressUpdate](https://developers.weixin.qq.com/miniprogram/dev/api/network/upload/UploadTask.onProgressUpdate.html). The progress might be inaccurate on some Android models.

#### Example

Upload a file using simple upload:

[//]: # (.cssg-snippet-post-object)
```js
cos.postObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: filename,
    FilePath: tmpFilePath, // tmpFilePath obtained when you select the file through wx.chooseImage
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function (err, data) {
    console.log(err || data);
});
```

Uploading a file to a specified directory

```js
var folder = 'examplefolder/';
cos.postObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: folder + filename,              /* Required */
    FilePath: tmpFilePath, // tmpFilePath obtained when you select the file through wx.chooseImage
    onProgress: function(progressData) {
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
| ContentLength | HTTP request length in bytes as defined in RFC 2616 | String | Yes |
| CacheControl | Cache policy as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentDisposition | Filename as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentEncoding | Encoding format as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentType | Content type (MIME) as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| Expires | Expiration time as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| Expect | If `Expect: 100-continue` is used, the request content will be sent only after confirmation from the server is received | String | No |
| ACL | Defines the ACL attribute of the object. For the enumerated values, such as `default`, `private`, and `public-read`, please see the **Preset ACL** section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: `default` <br>**Note:** If you do not need access control for the object, set `default` for this parameter or leave it empty. In this way, the object will inherit the permissions of the bucket it is stored in. | String | No |
| StorageClass | Storage class of the object. For the enumerated values, such as `STANDARD` (default), `STANDARD_IA`, and `ARCHIVE`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String | No |
| x-cos-meta-* | User-defined headers, which will be saved as the object metadata. The maximum size is 2 KB. | String | No |
| FilePath | Temporary file path of the file to be uploaded, which can be obtained by selecting the file through `wx.chooseImage` | String | Yes |
| onProgress | Progress callback function. The first parameter in a callback is the `progressData` object. | Function | No |
| - progressData.loaded | Size of the file part that has been downloaded in bytes | Number | No |
| - progressData.total | Size of the entire file, in bytes | Number | No |
| - progressData.speed | File download speed in bytes/s | Number | No |
| - progressData.percent | Percentage of the file download progress in decimal form; for example, 0.5 means 50% downloaded | Number | No |

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
| - ETag | Returns the MD5 checksum of the object. The value of `ETag` can be used to check whether the object was corrupted during upload. <br>For example, `"09cba091df696af91549de27b8e7d0f6"`. **Note: double quotation marks are required at the beginning and the end of the `ETag` value  | String |
| - Location | Creates an object's access domain name for external networks | String |
| - VersionId | The version ID of the returned object in a versioning-enabled bucket | String |

### Querying object metadata

#### Description

This API is used to query the metadata of an object.

#### Example

[//]: # (.cssg-snippet-head-object)
```js
cos.headObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',                                  /* Required */
    Key: 'picture.jpg',               /* Required */
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
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code, such as `200` and `304`. `304` is returned if no modification is made after the specified time. | Number |
| - headers | Headers | Object |
| - x-cos-object-type | Whether an object is appendable. Enumerated values: `normal`, `appendable`. The default value `normal` is not displayed. | String |
| - x-cos-storage-class | Storage class of the object. For the enumerated values, such as `STANDARD` (default), `STANDARD_IA`, and `ARCHIVE`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). Note that `STANDARD` is not displayed if returned. | String  |
| - x-cos-meta-* | User-defined metadata | String |
| - NotModified | Whether an object hasn’t been modified after the specified time | Boolean |
| - ETag | MD5 checksum of the object. The value of `ETag` can be used to check whether the object was corrupted during the upload. <br>Example: `"09cba091df696af91549de27b8e7d0f6"` <br>**Note that double quotation marks are required at the beginning and the end**. | String |
| - VersionId       | Version ID of the uploaded object if versioning is enabled for its bucket. If versioning is not enabled, this parameter is not returned. | String  |

### Download an object

This API (`GET Object`) is used to get the content, in string format, of a specified file in a bucket.

#### Example

[//]: # (.cssg-snippet-get-object)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',                                  /* Required */
    Key: 'picture.jpg',              /* Required */
}, function(err, data) {
    console.log(err || data.Body);
});
```

Getting file content with `Range` specified

[//]: # (.cssg-snippet-get-object-range)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',                                  /* Required */
    Key: 'picture.jpg',              /* Required */
    Range: 'bytes=1-3', /*Optional*/
}, function(err, data) {
    console.log(err || data.Body);
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
| -------------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| ResponseContentType | `Content-Type` parameter in the response header | String | No |
| ResponseContentLanguage | `Content-Language` in the response header | String | No |
| ResponseExpires | `Content-Expires` in the response header | String | No |
| ResponseCacheControl | `Cache-Control` in the response header | String | No |
| ResponseContentDisposition | `Content-Disposition` in the response header | String | No |
| ResponseContentEncoding | `Content-Encoding` in the response header | String | No |
| Range | Byte range of the object as defined in RFC 2616. The range value must be in the format of `bytes=first-last`, where both `first` and `last` are offsets starting from 0. For example, `bytes=0-9` means to download the first 10 bytes of the object. If this parameter is not specified, the entire object will be downloaded. | String | No |
| If-Modified-Since | If the object is modified after the specified time, the corresponding object metadata will be returned; otherwise, "304 (not modified)" will be returned. | String | No |
| If-Unmodified-Since | Required unmodified time. The object is downloaded only if it has not been modified since the specified time. Otherwise, `412` (precondition failed) will be returned. | String | No |
| IfMatch | Returns the object only if the `ETag` matches the specified content; otherwise, an HTTP `412` (Precondition Failed) status code is returned | String | No |
| IfNoneMatch | Returns the object only if the `ETag` does not match the specified content; otherwise, an HTTP `304` (Not Modified) status code is returned | String | No |
| VersionId | Version ID of the object to download | String | No |
| onProgress | Progress callback. The attributes of the response object `progressData` are as follows. | Function | No |
| - progressData.loaded | Size of the downloaded parts, in bytes | Number | No |
| - progressData.total | Size of the entire object, in bytes | Number | No |
| - progressData.speed | Download speed, in bytes/s | Number | No |
| - progressData.percent | Percentage of the file download progress; for example, 0.5 means 50% downloaded | Number | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | Returns an HTTP status code, such as 200, 304, 403, and 404 | Number |
| - headers | Headers | Object |
| - Cache-Control | Cache directives as defined in RFC 2616. It will be returned only if it is contained in the object metadata or specified through the request parameter. | String |
| - Content-Disposition | Filename as defined in RFC 2616. It will be returned only if it is contained in the object metadata or specified through the request parameter. | String |
| - ContentEncoding | Encoding format as defined in RFC 2616. It will be returned only if it is contained in the object metadata or specified through the request parameter. | String |
| - Expires | Cache expiration time as defined in RFC 2616. It will be returned only if it is contained in the object metadata or specified through the request parameter. | string |
| - x-cos-storage-class | Storage class of the object. For the enumerated values, such as `STANDARD` (default), `STANDARD_IA`, and `ARCHIVE`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925).<br>**Note: If this header is not returned, the storage class of the object is `STANDARD`.** | String  |
| - x-cos-meta-* | User-defined metadata | String |
| - NotModified | This attribute will be returned if the request contains `IfModifiedSince`. If the file has been modified, `false` will be returned. If not, `true` will be returned. | Boolean |
| - ETag | MD5 checksum of the object. The value of `ETag` can be used to check whether the object was corrupted during the upload. <br>Example: `"09cba091df696af91549de27b8e7d0f6"` <br>**Note that double quotation marks are required at the beginning and the end**. | String |
| - VersionId       | Version ID of the uploaded object if versioning is enabled for its bucket. If versioning is not enabled, this parameter is not returned. | String  |
| - Body                | Returned file content. Uses the String format by default.        | String  |

### Checking CORS configuration

#### Description

This API (`OPTIONS Object`) is used to send a preflight request to check the CORS configuration of an object. Before making an actual CORS request, you can send an OPTIONS request that includes the source origin, HTTP method, and headers to COS to determine whether an actual CORS request can be sent. If there is no CORS configuration, "403 Forbidden" will be returned. **You can enable CORS for a bucket using the `PUT Bucket cors` API.**

#### Example

[//]: # (.cssg-snippet-option-object)
```js
cos.optionsObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',                                  /* Required */
    Key: 'picture.jpg',              /* Required */
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
| - AccessControlAllowMethods | HTTP methods of the simulated cross-origin access request separated by commas, such as `PUT`, `GET`, `POST`, `DELETE`, and `HEAD`. This header will not be returned if the request method is not allowed | String |
| - AccessControlAllowHeaders | Headers (separated by commas) of the simulated CORS request (for example, `accept,content-type,origin,authorization`). If none of the stimulated request headers is allowed, this header will not be returned. | String |
| - AccessControlExposeHeaders | Response headers supported by CORS, such as `ETag`. The headers are separated by commas | String |
| - AccessControlMaxAge | Validity period of the result of the  `OPTIONS` request, for example, `3600` | String  |
| - OptionsForbidden | Indicates whether the `OPTIONS` request is forbidden. If the returned HTTP status code is 403, this value is `true`. | Boolean |

### Copying objects

#### Description

This API (`PUT Object - Copy`) is used to create a copy of an existing COS object, that is, to copy an object from the source path (object key) to the destination path (object key). During the process, object metadata and ACLs can be modified.
You can use this API to create a copy of an object, modify an object’s metadata (the source object and destination file have the same attributes), and move or rename an object (copy the object first and then call the deletion API).

> !We recommend that you use this API to download an object of 1 MB-5 GB. For objects greater than 5 GB, please use the advanced copy API [Slice Copy File](#.E5.A4.8D.E5.88.B6.E5.AF.B9.E8.B1.A12).



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
| ACL    | Defines the access control list (ACL) attribute of the object. For the enumerated values such as `default`, `private`, and `public-read`, see the Preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). <br>**Note:** If you do not need access control for the object, set `default` for this parameter or simply leave it blank, and the object will inherit the permissions of the bucket | String | No |
| GrantRead | Grants the user read permission in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users. <br><li>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br><li>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantWrite | Grants the user write permission in the format: `id="[OwnerUin]"`.<br>You can use commas (,) to separate multiple users.<br><li>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br><li>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantFullControl | Grants the user full permission in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users. <br><li>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br><li>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| MetadataDirective | Whether to copy the metadata. Enumerated values: `Copy` (default), `Replaced`. If it is set to `Copy`, the metadata of the source object will be copied and the user-defined metadata in the header will be ignored. If it is set to `Replaced`, the metadata of the source object will be replaced with the user-defined metadata in the header. **If the destination and source paths are the same, that is, if you want to modify the metadata, this parameter must be set to `Replaced`.** | String | No |
| CopySourceIfModifiedSince | Required modification time. The object is copied only if it has been modified after the specified time. Otherwise, `412` will be returned. **This parameter can be used together with `CopySourceIfNoneMatch`. Using it together with other conditions may cause a conflict.** | String | No |
| CopySourceIfUnmodifiedSince | Required unmodified time. The object is copied only if it hasn’t been modified since the specified time. Otherwise, `412` will be returned. **This parameter can be used together with `CopySourceIfMatch`. Using it together with other conditions may cause a conflict.** | String | No |
| CopySourceIfMatch | `ETag` that must be matched. The object is copied only if its `ETag` matches the specified value. Otherwise, `412` will be returned. **This parameter can be used together with `CopySourceIfUnmodifiedSince`. Using it together with other conditions may cause a conflict.** | String | No |
| CopySourceIfNoneMatch | `ETag` that cannot be matched. The object is copied only if its `ETag` does not match the specified value. Otherwise, `412` will be returned. **This parameter can be used together with `CopySourceIfModifiedSince`. Using it together with other conditions may cause a conflict**. | string | No |
| StorageClass | Storage class of the object. For the enumerated values, such as `STANDARD` (default) and `STANDARD_IA`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String | No |
| x-cos-meta-* | Other user-defined file headers | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
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
    Region: 'ap-beijing',                                  /* Required */
    Key: 'picture.jpg'                            /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
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
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
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
    Region: 'ap-beijing',                                  /* Required */
    Objects: [
        {Key: 'picture.jpg'},
        {Key: '2.zip'},
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
| Quiet | Whether to use the `Quiet` mode. If it is set to `true`, the `Quiet` mode is enabled. If it is set to `false` (default), the `Verbose` mode is enabled. | Boolean | No |
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



## Multipart Operations

### Querying multipart uploads

#### Description

This API (List Multipart Uploads) is used to query ongoing multipart uploads. Up to 1,000 multipart uploads can be listed at a time.

#### Example

Getting a list of `UploadId` of uploads with the object key prefix `exampleobject`

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
| KeyMarker | Used together with `upload-id-marker`. <br><li>If `upload-id-marker` is not specified: <br>&emsp;- Only multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed. <br><li>If `upload-id-marker` is specified: <br>&emsp;- Multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed; <br>&emsp;- Multipart uploads whose `ObjectName` is lexicographically equal to the specified `key-marker` and the `UploadID` is larger than the `upload-id-marker` will be listed. | String | No |
| UploadIdMarker | Used together with `key-marker`. <br><li>If `key-marker` is not specified: <br>&emsp;- `upload-id-marker` will be ignored. <br><li>If `key-marker` is specified: <br>&emsp;- Multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed; <br>&emsp;- Multipart uploads whose `ObjectName` is equal to the specified `key-marker` and the `UploadID` is greater than the `upload-id-marker` will be listed. | String | No |

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
| Expires | Cache expiration time as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ACL | ACL attribute of the object. For the enumerated values, such as `default`, `private`, and `public-read`, please see the **Preset ACL** section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). <br>**Note**: If you do not need access control for the object, set this parameter to `default` or do not specify it, in which case the object will inherit the permissions of its bucket. | String | No |
| GrantRead | Grants the user read permission in the format of `id="[OwnerUin]"`. You can use commas (,) to separate multiple users. <br><li>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br><li>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantFullControl | Grants the grantee Read/Write access in the format of `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| StorageClass | Storage class of the object. For the enumerated values, such as `STANDARD` (default), `STANDARD_IA` and `ARCHIVE`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String | No |
| x-cos-meta-* | User-defined headers, which will be returned as the object metadata. The maximum size is 2 KB. | String | No |

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

### Uploading parts

#### Description

This API (`Upload Part`) is used to upload parts after a multipart upload is initialized. It can upload 1-10,000 parts of 1 MB to 5 GB at a time.
<li>When you use the `Initiate Multipart Upload` API to initiate a multipart upload, you can obtain the `uploadId`. This ID uniquely identifies the part and its position in the entire object.</li>
<li>Every time you call the `Upload Part` API, you need to pass `partNumber` (the part number) and `uploadId`. You can upload multiple parts out of order.</li>
<li>When the `uploadId` and `partNumber` of a new part are the same as those of a previously uploaded part, the old part will be overwritten. If the `uploadId` does not exist, the 404 error, "NoSuchUpload", will be returned.</li>

#### Example

[//]: # (.cssg-snippet-upload-part)
```js
cos.multipartUpload({
   Bucket: 'examplebucket-1250000000', /* Required */
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
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| ContentLength | HTTP request length (in bytes) as defined in RFC 2616 | String | Yes |
| PartNumber | Part number | String | Yes |
| UploadId | ID of the multipart upload | String | Yes |
| Body          | Content of the uploaded file part, which can be a string or ArrayBuffer object    | String/ArrayBuffer | Yes   |
| Expect | HTTP request length (in bytes) defined in RFC 2616. If `Expect: 100-continue` is used, the request content will be sent only after confirmation from the server is received. | String | No |
| ContentMD5 | Base64-encoded 128-bit MD5 checksum as defined in RFC 1864. This header is used to verify whether the file content has changed. | String | No |

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
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
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
| - Part |Part information list | ObjectArray |
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
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code, such as 200, 403, and 404 | Number |
| - headers    | Returns headers  

## Other Operations

### Restoring an archived object

#### Description

This API is used to restore an object archived by COS. The restored readable object is temporary, and you can configure the object to keep it readable and set the time when you want it to be deleted. You can use the `Days` parameter to specify the expiration time of the temporary object. If the object expires and you have not initiated any operation to copy the object or extend its validity period before it expires, the temporary object will be automatically deleted. A temporary object is only a copy of the source archived object and the source object will exist throughout this period.

#### Example

[//]: # (.cssg-snippet-restore-object)
```js
cos.restoreObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',                                  /* Required */
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

| Parameter   | Description  | Type | Required |
| ------------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| RestoreRequest | A container for data restoration | Object | Yes |
| - Days | Expiration time of the temporary copy | Number | Yes |
| - CASJobParameters | A container for the archive job parameters | Object | Yes |
| - - Tier  | Restoration mode. For ARCHIVE, `Tier` can be set to `Standard` (restores an object within 3-5 hours), `Expedited` (restores an object within 15 minutes), and `Bulk` (restores an object within 5-12 hours). For DEEP ARCHIVE, `Tier` can be set to `Standard` (restores an object within 12-24 hours) and `Bulk` (restores an object within 24-48 hours) | String | Yes |

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

### Setting an object ACL

#### Description

This API (PUT Object acl) is used to set the ACL of an object in a bucket.

> !The total number of policies associated with bucket ACL, Policy, and CAM under a single root account (i.e., under the same `APPID`) cannot exceed 1,000. There is no upper limit on the number of object ACL rules. If you do not need access control for an object, do not make any configuration, and the object will inherit the permissions of its bucket.

#### Example

[//]: # (.cssg-snippet-put-object-acl)
```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',                                  /* Required */
    Key: 'picture.jpg',              /* Required */
    ACL: 'public-read', /*Optional*/
}, function(err, data) {
    console.log(err || data);
});
```

Grant a user all permissions for an object:

[//]: # (.cssg-snippet-put-object-acl-user)
```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',                                  /* Required */
    Key: 'picture.jpg',              /* Required */
    GrantFullControl: 'id="100000000001"' // 100000000001 is the uin of the root account.
}, function(err, data) {
    console.log(err || data);
});
```

Grant the user permission to write the object via `AccessControlPolicy`:

[//]: # (.cssg-snippet-put-object-acl-acp)
```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',                                  /* Required */
    Key: 'picture.jpg',              /* Required */
    AccessControlPolicy: {
        "Owner": { // `Owner` is required in `AccessControlPolicy`.
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

| Parameter | Description | Type | Required |
| ------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket | Bucket name, formatted as `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| ACL | Defines the ACL attribute of the object. For the enumerated values, such as `default`, `private`, and `public-read`, please see the **Preset ACL** section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: `default` <br>**Note:** If you do not need access control for the object, set `default` for this parameter or leave it empty. In this way, the object will inherit the permissions of the bucket it is stored in. | String | No |
| GrantRead | Grants the user read permission in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<br><li>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br><li>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantFullControl | Grants the user full permission in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<br><li>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br><li>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| AccessControlPolicy | Sets the object's ACL attributes. | Object | No |
| - Owner | Information about the object owner | Object | No |
| - - - ID | Object owner ID in the format: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>For root accounts, `&lt;OwnerUin>` and `&lt;SubUin>` have the same value | String | No |
| - - DisplayName | Name of the object owner | String |No |
| - Grants | A list of information about the grantee and granted permissions | ObjectArray | No |
| - - Permission | Permission granted. Enumerated values: `READ`, `WRITE`, `READ_ACP`, `WRITE_ACP`, `FULL_CONTROL` | String | No |
| - - Grantee | Information about the grantee | Object | No |
| - - - DisplayName | Name of the grantee | String | No |
| - - - ID | Authorized user’s ID in the format: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` <br>For root accounts, `&lt;OwnerUin>` and `&lt;SubUin>` have the same value. | String | No |

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
| - statusCode | HTTP status code, such as `200`, `204`, `403`, and `404` | Number |
| - headers | Headers | Object |

### Querying an object ACL

#### Description

This API (GET Object acl) is used to query the access permissions of an object in a bucket. Only the bucket owner has permission to perform this operation.

#### Example

[//]: # (.cssg-snippet-get-object-acl)
```js
cos.getObjectAcl({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',                                  /* Required */
    Key: 'picture.jpg',              /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ----------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| - ACL | Defines the access control list (ACL) attributes of the object. For the enumerated values such as `private` and `public-read`, see the “Preset ACL for buckets” section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: `private` | String |
| - Owner | Owner of the resource | Object |
| - - - ID | Object owner ID in the format: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>For root accounts, `&lt;OwnerUin>` and `&lt;SubUin>` have the same value | String |
| - - DisplayName | Name of the object owner | String |
| - Grants | List of information on the grantee and permissions | ObjectArray |
| - - Permission | Permission granted. Enumerated values: `READ`, `WRITE`, `READ_ACP`, `WRITE_ACP`, `FULL_CONTROL` | String |
| - - Grantee | Authorized user’s information | Object |
| - - - DisplayName | Name of the user | String |
| - - - ID | User ID in the format: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>For root accounts, `&lt;OwnerUin>` and `&lt;SubUin>` have the same value | String |

## Advanced APIs (Recommended)

The following methods encapsulate the native methods mentioned above. They can be used to implement the complete multipart replication process and support concurrent multipart replications, checkpoint restart, as well as canceling, pausing, and restarting replication tasks.

### Advanced upload

#### Description
    
This API is used to implement advanced upload. The `SliceSize` parameter can be used to specify the file size limit (1 MB by default) to determine whether to use multipart upload. If the file size is greater than this threshold, multipart upload will be used; otherwise, simple upload will be used.
    
#### Example

[//]: # (.cssg-snippet-transfer-upload-file)
```js
var uploadFile = function(file) {
    cos.uploadFile({
        Bucket: 'examplebucket-1250000000', /* Required */
        Region: 'COS_REGION',     /* Bucket region. Required */
        Key: file.name,              /* Required */
        FilePath: file.path,                /* Required */
        FileSize: file.size,                /* Required */
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
}

wx.chooseMessageFile({
   count: 10,
   type: 'all',
   success: function(res) {
       uploadFiles(res.tempFiles[0]);
   }
});
```

#### Parameter description

| Parameter  | Description                                                     | Type      | Required |
| ------------------------------------------------------------ | ------------------------------------------------------------ | --------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| FilePath                                                         | Path to the file to upload           | String | Yes   |
| FileSize                                                         | Size of the object to upload    | Number | Yes |
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
[//]: # (.cssg-snippet-transfer-copy-object)
```js
var sliceUploadFile = function (file) {
    var key = file.name;
    cos.sliceUploadFile({
        Bucket: 'examplebucket-1250000000', /* Required */
        Region: 'COS_REGION',/*Required*/
        Key: 'exampleobject',              /* Required */
        FilePath: file.path,                /* Required */
        FileSize: file.size,                        /* Optional */
        CacheControl: 'max-age=7200',               /* Optional */
        Headers: {                                  /* Optional */
            aa: 123,
        },
        Query: {                                     /* Optional */
            bb: 123,
        },
        onTaskReady: function(taskId) {              /* Optional */
            console.log(taskId);
        },
        onHashProgress: function(info) {             /* Optional */
            console.log('check hash', JSON.stringify(info));
        },
        onProgress: function(info) {                 /* Optional */
            console.log(JSON.stringify(info));
        }
    }, requestCallback);
};
wx.chooseMessageFile({
    count: 10,
    type: 'all',
    success: function(res) {
        sliceUploadFile(res.tempFiles[0]);
    }
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
| AsyncLimit                                                   | Maximum number of parts for concurrent upload. This parameter is valid only when multipart upload is triggered.                                           | Number    | No   |
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

This API (Slice Copy File) is used to copy a file from a source path to a destination path through multipart copy. Object metadata and ACL can be modified during the copy process. You can use this API to move, rename, and copy a file or modify its attributes.

#### Method prototype

Calling `Slice Copy File`

[//]: # (.cssg-snippet-transfer-copy-object)
```js
cos.sliceCopyFile({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'ap-beijing',                                  /* Required */
    Key: '1.zip',                                            /* Required */
    CopySource: 'test-1250000000.cos.ap-guangzhou.myqcloud.com/2.zip', /* Required */
    onProgress:function (progressData) {                     /* Optional */
        console.log(JSON.stringify(progressData));
    }
},function (err,data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter                | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| CopySource | URL of the source object. You can specify a previous version using the URL parameter `?versionId=<versionId>`. | String | Yes |
| ChunkSize | Size (in bytes) of each part in the multipart copy. Defaults to `1048576` (1 MB). | Number | No |
| SliceSize | File size threshold in bytes, 5 GB by default. If the file size is equal to or smaller than this value, the file will be uploaded using `putObjectCopy`; otherwise, it will be uploaded using `sliceCopyFile`. | Number | No | 
| onProgress | Callback for the upload progress, whose parameter is `progressData` | Function | No |
| - progressData.loaded | Size of the uploaded parts, in bytes | Number | No |
| - progressData.total | Size of the entire file, in bytes | Number | No |
| - progressData.speed | File upload speed, in bytes/s | Number | No |
| - progressData.percent | Percentage of the file copy progress, in decimal form. For example, 0.5 means 50% has been copied. | Number | No |

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
var uploadFiles = function(files) {
    var fileList = files.map(function(file) {
        return Object.assign(file, {
            FilePath: file.path,
            FileSize: file.size,
            Bucket: 'examplebucket-1250000000',
            Region: 'COS_REGION',
            Key: file.name,
            onTaskReady: function(taskId) {
              /* Based on `taskId`, you can use queue operations to cancel upload `cos.cancelTask(taskId)`, pause upload `cos.pauseTask(taskId)`, and resume upload `cos.restartTask(taskId)` */
              console.log(taskId);
            }
        });
    });
    cos.uploadFiles({
        files: fileList,
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
}
wx.chooseMessageFile({
    count: 10,
    type: 'all',
    success: function(res) {
        uploadFiles(res.tempFiles);
    }
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
| - FileSize             | Size of the object to upload                                 | Number | Yes |
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
| - - options  | Parameter information for the currently completed file   

### Uploading queue

The Mini Program SDK records all the `putObject` upload tasks in a queue; relevant queue operations are as follows:

1. Use `cos.getTaskList` to get the task list.
2. Use `cos.pauseTask`, `cos.restartTask`, and `cos.cancelTask` to perform operations on upload tasks.
3. Use `cos.on('list-update', callback);` to listen for list and progress changes.

For a complete example of queue usage, see the [demo](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/demo/queue).

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
| taskId | ID of an upload task. When `putObject` is called, the `TaskReady` callback will return the `taskId` of the upload task. | String | Yes |

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
| taskId | ID of an upload task. When `putObject` is called, the `TaskReady` callback will return the `taskId` of the upload task. | String | Yes |

#### Resuming an upload task

This API is used to resume an upload task by `taskId`. You can resume tasks that have been manually paused through the `pauseTask` API, or automatically paused due to an upload error.

**Example**

[//]: # (.cssg-snippet-transfer-upload-resume)
```js
var taskId = 'xxxxx';                   /* Required */
cos.restartTask(taskId);
```

**Parameter description**

| Parameter | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | ID of an upload task. When `putObject` is called, the `TaskReady` callback will return the `taskId` of the upload task. | String | Yes |


