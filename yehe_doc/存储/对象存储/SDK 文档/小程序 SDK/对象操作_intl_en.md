## Overview

This document provides an overview of APIs and SDK code samples related to simple operations and other object operations.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ---------------------------------------- |
| [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying an object list | Queries some or all objects in a bucket |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploads an object using simple upload | Uploads an object to a bucket |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | Uploading an object using an HTML form | Uploads an object using an HTML form |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object |
| [OPTIONS Object](https://intl.cloud.tencent.com/document/product/436/8288) | Configuring pre-flight requests for cross-origin access | Sends a pre-flight request to confirm whether a real cross-origin access request can be sent |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object | Copies an object to a destination path (object key) |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes a specified object from a bucket |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket in a single request |

**Other operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access |
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
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'ap-beijing',     /* Required */
    Prefix: 'a/',           /* Optional */
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
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'ap-beijing',    /* Required */
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
| Prefix | Matching prefix for object keys. This parameter limits the response to contain only object keys with the specified prefix. | String | No |
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
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Headers returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - headers | Headers returned by the request | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - Name | Bucket name in the format of `BucketName-APPID`, such as `examplebucket-1250000000` | String |
| - Prefix | Matching prefix for object keys. Object key entries will be returned in UTF-8 lexicographical order starting from the first object key after the prefix | String |
| - Marker | Marks for the starting object key. Object key entries will be returned in UTF-8 lexicographical order starting from the first object key after the marker | String |
| - MaxKeys | Maximum number of entries returned in a single response | String |
| - Delimiter | Delimiter | String |
| - IsTruncated | Indicates whether the returned request entries are truncated. Valid values: `true`, `false` | String |
| - NextMarker | If returned entries are truncated, then `NextMarker` marks where the next listing should begin | String |
| - CommonPrefixes | The identical paths between a specified prefix and the delimiter are grouped and defined as a common prefix. | ObjectArray |
| - - Prefix | A single common prefix | String |
| - EncodingType | Indicates the encoding method of the returned value, which is effective for `Delimiter`, `Marker`, `Prefix`, `NextMarker`, and `Key` | String |
| - Contents | A list of object metadata | ObjectArray |
| - - Key | Object name, i.e., object key | String |
| - - ETag | MD5 checksum of the object, such as `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end**. | String |
| - - Size | Part size, in bytes | String |
| - - LastModified  | Last modified time of the object, in ISO 8601 format, for example, `2019-05-24T10:56:40Z` | String |
| - - Owner | Information about the object owner | Object |
| - - - ID | Complete ID of the object owner. Format: `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`, such as `qcs::cam::uin/100000000001:uin/100000000001`，where 100000000001 is uin | String |
| - - - DisplayName | Name of the part owner | String |
| - - StorageClass | Sets the object storage class. Enumerated values: `STANDARD`, `STANDARD_IA` and `ARCHIVE`. For more information, see [Storage Class](https://intl.cloud.tencent.com/document/product/436/30925) | String |

### Uploading an object using simple upload

#### API description

This API (PUT Object) is used to upload an object to a bucket. To call this API, you need to have permission to write the bucket.

> !
> 1. The Key (filename) cannot end with `/`; otherwise, it will be identified as a folder.
> 2. Each root account (`AAPID`) can have up to 1,000 bucket ACLs and an unlimited number of object ACLs. If you do not need an ACL for an object, you can choose not to configure an ACL for the object during upload. In this way, the object will inherit the permissions of its bucket by default.
> 3. After an object is uploaded, you can use the same key to generate a pre-signed URL, which can be shared with other clients for downloading (to download, please use the `GET` method. The detailed API description is shown below). If your file is set to private-read, note that the pre-signed URL will only be valid for a certain period of time.

#### Use case

Upload a string as the file content:

[//]: # (.cssg-snippet-put-object-string)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
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
    Region: 'ap-beijing',    /* Required */
    Key: 'a/',              /* Required */
    Body: '',
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | ObjectKey (object name) is the unique ID of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
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
| TaskReady | Callback function when an upload task is created. The callback returns a `taskId`, which uniquely identifies the task and can be used to cancel (cancelTask), pause (pauseTask), or restart (restartTask) the task. | Function | No |
| - taskId                                                     | Upload task number                                              | String    | No  |
| onProgress | Callback of the progress. Attributes of the response object `progressData` are as follows: | Function | No |
| - progressData.loaded | Size of the file part that has been uploaded in bytes | Number | No |
| - progressData.total | Size of the entire object, in bytes | Number    | No   |
| - progressData.speed                                         | File upload speed in bytes/s                 | Number    | No   |
| - progressData.percent | Percentage of the file upload progress in decimal form; for example, 0.5 means 50% downloaded | Number | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as "200", "403", and "404" | Number |
| - headers | Headers returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code returned by the request, such as "200", "403", and "404" | Number |
| - headers | Headers returned by the request | Object |
| - ETag | MD5 checksum of the object. The value of `ETag` can be used to check whether the object was corrupted during the upload. <br>Example: `"09cba091df696af91549de27b8e7d0f6"` <br> **Note that double quotation marks are required at the beginning and the end**. | String |
| - Location | Public network access endpoint of the object | String |
| - VersionId | Returns the version ID for versioning-enabled buckets. For buckets that have never had versioning enabled, this parameter is not returned. | String  |

### Uploading an object using a form

This API (POST Object) is used to upload an object selected by the user through `wx.chooseImage` to a specified bucket. To call this API, you need to have permission to write the bucket.

>! `onProgress` depends on the mini program [UploadTask.onProgressUpdate](https://developers.weixin.qq.com/miniprogram/dev/api/network/upload/UploadTask.onProgressUpdate.html). The progress might be inaccurate on some Android models.

#### Use case 

Upload a file using simple upload

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

Uploading an object to a specified directory:

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
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
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
| x-cos-meta-* | User-defined headers, which will be returned as the object metadata. The maximum size is 2 KB. | String | No |
| FilePath | Temporary file path of the file to be uploaded, which can be obtained by selecting the file through `wx.chooseImage` | String | Yes |
| onProgress | Progress callback function. The first parameter in a callback is the `progressData` object. | Function | No |
| - progressData.loaded | Size of the file part that has been downloaded in bytes | Number | No |
| - progressData.total | Size of the entire file; unit: byte | Number | No |
| - progressData.speed | File download speed in bytes/s | Number | No |
| - progressData.percent | Percentage of the file download progress in decimal form; for example, 0.5 means 50% downloaded | Number | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as "200", "403", and "404" | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code returned by the request, such as "200", "403", and "404" | Number |
| - headers | Headers returned by the request | Object |
| - ETag | Returns the MD5 checksum of the object. The value of `ETag` can be used to check whether the object was corrupted during upload. <br>For example, `"09cba091df696af91549de27b8e7d0f6"`. **Note: double quotation marks are required at the beginning and the end of the `ETag` value ** | String |
| - Location | Creates an object's access domain name for external networks | String |
| - VersionId | The version ID of the returned object in a versioning-enabled bucket | String |

### Querying object metadata

#### API description

This API is used to query the metadata of an object.

#### Use case 

[//]: # (.cssg-snippet-head-object)
```js
cos.headObject({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',               /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| --------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | ObjectKey (object name) is the unique ID of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| IfModifiedSince | If the object is modified after the specified time, the corresponding object metadata will be returned; otherwise, 304 will be returned. | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this is null. | Object |
| - statusCode | HTTP status code returned by the request, such as 200 and 304. If no modification is made after the specified time, 304 will be returned. | Number |
| - headers | Headers returned by the request | Object |
| - x-cos-object-type | Indicates whether an object is appendable. Enumerated values: `normal`, `appendable`. The default value `normal` is not displayed if returned. | String |
| - x-cos-storage-class | Storage class of the object. For the enumerated values, such as `STANDARD` (default), `STANDARD_IA`, and `ARCHIVE`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). Note that `STANDARD` is not displayed if returned. | String  |
| - x-cos-meta-* | User-defined metadata | String |
| - NotModified | Indicates whether an object is unmodified after the specified time. | Boolean |
| - ETag | MD5 checksum of the object. The value can be used to check whether the object was corrupted during the upload.<br>Example: `"09cba091df696af91549de27b8e7d0f6"` <br>**Note that double quotation marks are required at the beginning and the end**. | String |
| - VersionId | Returns the version ID for versioning-enabled buckets. For buckets that have never had versioning enabled, this parameter is not returned. | String  |

### Downloading an object

This API is used to get the content, in string format, of a specified file in a bucket.

#### Use case 

[//]: # (.cssg-snippet-get-object)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
}, function(err, data) {
    console.log(err || data.Body);
});
```

Get the file content with `Range` specified:

[//]: # (.cssg-snippet-get-object-range)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
    Range: 'bytes=1-3',        /* Optional */
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
| Range | Byte range of the object as defined in RFC 2616. This value must be in the format of bytes=first-last, where both first and last are offsets starting from 0. For example, bytes=0-9 means that you want to download the first 10 bytes of data of the source object. If this parameter is not specified, the entire object will be downloaded | String | No |
| If-Modified-Since | If the object is modified after the specified time, the corresponding object metadata will be returned; otherwise, "304 (not modified)" will be returned. | String | No |
| IfUnmodifiedSince    | Returns the object if the object is not modified after the specified time; otherwise, an HTTP `412` (Precondition Failed) status code is returned | String | No |
| IfMatch | Returns the object only if the `ETag` matches the specified content; otherwise, an HTTP `412` (Precondition Failed) status code is returned | String | No |
| IfNoneMatch | Returns the object only if the `ETag` does not match the specified content; otherwise, an HTTP `304` (Not Modified) status code is returned | String | No |
| VersionId | Version ID of the object to be downloaded | String | No |
| onProgress | Callback of the progress. Attributes of the response object `progressData` are as follows: | Function | No |
| - progressData.loaded | Size of the downloaded parts, in bytes | Number | No |
| - progressData.total | Size of the entire object, in bytes | Number | No |
| - progressData.speed | Object download speed in bytes/s | Number | No |
| - progressData.percent | Percentage of the file download progress; for example, 0.5 means 50% downloaded | Number | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this is null. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 304, 403, and 404 | Number |
| - headers | Headers returned by the request | Object |
| Cache-Control | Cache directives as defined in RFC 2616. It will be returned only if it is contained in the object metadata or specified through the request parameter. | string |
| Content-Disposition | Filename as defined in RFC 2616. It will be returned only if it is contained in the object metadata or specified through the request parameter. | string |
| - ContentEncoding | Encoding format as defined in RFC 2616. It will be returned only if it is contained in the object metadata or specified through the request parameter. | string |
| Expires | Cache expiration time as defined in RFC 2616. It will be returned only if it is contained in the object metadata or specified through the request parameter. | string |
| - x-cos-storage-class | Storage class of the object. For the enumerated values, such as `STANDARD` (default), `STANDARD_IA`, and `ARCHIVE`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925).<br>**Note: If this header is not returned, the storage class of the object is `STANDARD`.** | String  |
| - x-cos-meta-* | User-defined metadata | String |
| - NotModified | This attribute will be returned if the request contains `IfModifiedSince`. If the file has been modified, `false` will be returned. If not, `true` will be returned. | Boolean |
| - ETag | MD5 checksum of the object. The value of `ETag` can be used to check whether the object was corrupted during the upload. <br>Example: `"09cba091df696af91549de27b8e7d0f6"` <br>**Note that double quotation marks are required at the beginning and the end**. | String |
| - VersionId | Returns the version ID for versioning-enabled buckets. For buckets that have never had versioning enabled, this parameter is not returned. | String  |
| - Body                | Returned file content. Uses the String format by default.        | String  |

### Configuring pre-flight requests for cross-origin access

#### API description

This API (OPTIONS Object) is used to send a pre-flight request for the CORS configuration of an object. Before making a real CORS request, you can send an OPTIONS request that includes the source origin, HTTP method, and headers to COS for it to determine whether a real CORS request can be sent. If there is no CORS configuration, "403 Forbidden" will be returned. **You can enable CORS for a bucket using the `PUT Bucket cors` API**.

#### Use case 

[//]: # (.cssg-snippet-option-object)
```js
cos.optionsObject({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
    Origin: 'https://www.qq.com',      /* Required */
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

| Parameter | Description | Type |
| ---------------------------- | ------------------------------------------------------------ | ------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - headers | Headers returned by the request | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - AccessControlAllowOrigin | Source origins (separated by commas) of the simulated CORS request. If the origins are not allowed, this header will not be returned. Example: `*` | String |
| - AccessControlAllowMethods | HTTP methods of the simulated cross-origin access request separated by commas, such as `PUT`, `GET`, `POST`, `DELETE`, and `HEAD`. This header will not be returned if the request method is not allowed | String |
| - AccessControlAllowHeaders | Headers of the simulated cross-origin access request separated by commas, such as `accept`, `content-type`, `origin`, and `authorization`. This request header will not be returned if any of the simulated headers is not allowed | String |
| - AccessControlExposeHeaders | Response headers supported by CORS, such as `ETag`. The headers are separated by commas | String |
| - AccessControlMaxAge | Sets the validity period of the `OPTIONS` request result, such as `3600` | String  |
| - OptionsForbidden | Indicates whether the `OPTIONS` request is forbidden. If the returned HTTP status code is 403, this value is `true`. | Boolean |

### Copying an object

#### API description

This API (PUT Object - Copy) is used to create a copy of an existing COS object, that is, an object is copied from the source path (object key) to the destination path (object key). During the copy, object metadata and the ACLs can be modified.
Users can use this API to create a copy, modify object metadata (the source object and destination file have the same attributes), and move or rename the object (first copy the object, and then call the delete API separately).

> !We recommend that you use this API to download an object of 1 MB-5 GB. For objects greater than 5 GB, please use the advanced copy API [Slice Copy File](#.E5.A4.8D.E5.88.B6.E5.AF.B9.E8.B1.A12).



#### Use case 

[//]: # (.cssg-snippet-copy-object)
```js
cos.putObjectCopy({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'ap-beijing',                                  /* Required */
    Key: 'picture.jpg',                                            /* Required */
    CopySource: 'test-1250000000.cos.ap-guangzhou.myqcloud.com/2.jpg', /* Required */
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
| CopySource | URL path to the source object. A past object version can be specified with the URL parameter `?versionId=&lt;versionId>` | String | Yes |
| ACL    | Defines the access control list (ACL) attribute of the object. For the enumerated values such as `default`, `private`, and `public-read`, see the Preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). <br>**Note:** If you do not need access control for the object, set `default` for this parameter or simply leave it blank, and the object will inherit the permissions of the bucket | String | No |
| GrantRead | Grants the user read permission in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users. <br><li>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br><li>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantWrite | Grants the user write permission in the format: `id="[OwnerUin]"`.<br>You can use commas (,) to separate multiple users.<br><li>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br><li>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantFullControl | Grants the user full permission in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users. <br><li>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br><li>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| MetadataDirective | Indicates whether to copy the metadata. Enumerated values: `Copy`, `Replaced`. Default value: `Copy`. If you specify this parameter as `Copy`, the user metadata in the corresponding header will be ignored and the copy operation will be performed; if you specify this parameter as `Replaced`, the metadata will be replaced by the information in the corresponding header. **If the destination path is the same as the source path, which means you want to modify the metadata, you must specify this parameter as `Replaced`** | String | No |
| CopySourceIfModifiedSince | If the object is modified after the specified time, the operation will be performed; otherwise, 412 will be returned. **This parameter can be used together with `CopySourceIfNoneMatch`. If it is used together with other conditions, a conflict will be returned**. | String | No |
| CopySourceIfUnmodifiedSince | If the object is not modified after the specified time, the operation will be performed; otherwise, 412 will be returned. **This parameter can be used together with `CopySourceIfMatch`. If it is used together with other conditions, a conflict will be returned**. | String | No |
| CopySourceIfMatch | If the `ETag` of the object is the same as the specified one, the operation will be performed; otherwise, 412 will be returned. **This parameter can be used together with `CopySourceIfUnmodifiedSince`. If it is used together with other conditions, a conflict will be returned**. | String | No |
| CopySourceIfNoneMatch | If the `Etag` of the object is different from the specified one, the operation will be performed; otherwise, 412 will be returned. **This parameter can be used together with `CopySourceIfModifiedSince`. If it is used together with other conditions, a conflict will be returned**. | string | No |
| StorageClass | Storage class of the object. For the enumerated values, such as `STANDARD` (default) and `STANDARD_IA`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String | No |
| x-cos-meta-* | Other user-defined file headers | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Headers returned by the request | Object |
| - ETag | MD5 checksum of the object, such as `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end**. | String |
| - LastModified | Last modified time of the object, for example, `2017-06-23T12:33:27.000Z` | String |
| - VersionId | Returns the version ID for versioning-enabled buckets. For buckets that have never had versioning enabled, this parameter is not returned. | String  |

### Deleting a single object

#### API description

This API (DELETE Object) is used to delete an object from a COS bucket. To call this API, you need to have permission to write the bucket.

#### Use case 

[//]: # (.cssg-snippet-delete-object)
```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg'                            /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| VersionId | Version ID of the object or delete marker to delete | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 204, 403, and 404. **If the deletion is successful or the object does not exist, an HTTP 204 or 200 status code will be returned. If the specified bucket is not found, an HTTP 404 status code will be returned**. | Number |
| - headers | Headers returned by the request | Object |

### Deleting multiple objects

#### API description

This API (DELETE Multiple Objects) is used to delete multiple objects from a bucket in a single request. You can delete up to 1,000 objects in a single request. There are two response modes you to choose from: `Verbose` and `Quiet`. The `Verbose` mode returns information about the deletion of each object, whereas the `Quiet` mode returns only information about error objects.

#### Use case

Deleting multiple files:

[//]: # (.cssg-snippet-delete-multi-object)
```js
cos.deleteMultipleObject({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'ap-beijing',    /* Required */
    Objects: [
        {Key: 'picture.jpg'},
        {Key: '2.zip'},
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
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Quiet | Specifies whether to use the `Quiet` mode. If set to `true`, the `Quiet` mode is enabled. If set to `false` (default), the `Verbose` mode is enabled. | Boolean | No |
| Objects | The list of objects to delete | ObjectArray | Yes |
| - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| - VersionId | Version ID of the object or delete marker to delete | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 204, 403, and 404 | Number |
| - headers | Headers returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 204, 403, and 404 | Number |
| - headers | Headers returned by the request | Object |
| - Deleted | A list of objects that are successfully deleted | ObjectArray |
| - - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| - - VersionId | If the `VersionId` parameter is passed in, it will also be included in the response, indicating the version of the object or delete marker. | String |
| - - DeleteMarker | If versioning is enabled and the `VersionId` parameter is not specified, the deletion operation will not actually delete the object; instead, it will only add a delete marker, meaning that the visible object has been deleted. Enumerated values: `true`, `false` | String |
| - - DeleteMarkerVersionId | Returns the `VersionId` of the generated delete marker if `DeleteMarker` is set to `true`. | String |
| - Error | A list of objects whose deletion failed | ObjectArray |
| - - Key | ObjectKey (object name) is the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| - - Code                                                     | Deletion failure error codes                                             | String      |
| - - Message                                                  | Deletion failure error messages                                      | String      |

## Other Operations

### Restoring an archived object

#### API description

This API is used to restore an object archived by COS. The restored readable object is temporary, and you can configure the object to keep it readable and set the time when you want it to be deleted. You can use the `Days` parameter to specify the expiration time of the temporary object. If the object expires and you have not initiated any operation to copy the object or extend its validity period before it expires, the temporary object will be automatically deleted. A temporary object is only a copy of the source archived object and the source object will exist throughout this period.

#### Use case 

[//]: # (.cssg-snippet-restore-object)
```js
cos.restoreObject({
    Bucket: 'examplebucket-1250000000',                               /* Required */
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

| Parameter   | Description  | Type | Required |
| ------------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | ObjectKey (object name) is the unique ID of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| RestoreRequest | A container for data restoration | Object | Yes |
| - Days | Sets the expiration time of the temporary copy. | Number | Yes |
| - CASJobParameters | A container for the archive job parameters | Object | Yes |
| - - Tier  | Restoration mode. For ARCHIVE, `Tier` can be set to `Standard` (restores an object within 3-5 hours), `Expedited` (restores an object within 15 minutes), and `Bulk` (restores an object within 5-12 hours). For DEEP ARCHIVE, `Tier` can be set to `Standard` (restores an object within 12-24 hours) and `Bulk` (restores an object within 24-48 hours) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as "200", "403", and "404" | Number |
| - headers | Headers returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code returned by the request, such as "200", "403", and "404" | Number |
| - headers | Headers returned by the request | Object |

### Setting an object ACL

#### API description

This API (PUT Object acl) is used to set the ACL of an object in a bucket.

> !The total number of policies associated with bucket ACL, Policy, and CAM under a single root account (i.e., under the same `APPID`) cannot exceed 1,000. There is no upper limit on the number of object ACL rules. If you do not need access control for an object, do not make any configuration, and the object will inherit the permissions of its bucket.

#### Use case 

[//]: # (.cssg-snippet-put-object-acl)
```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
    ACL: 'public-read',        /* Optional */
}, function(err, data) {
    console.log(err || data);
});
```

Grant a user all permissions for an object:

[//]: # (.cssg-snippet-put-object-acl-user)
```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
    GrantFullControl: 'id="100000000001"' // 100000000001 is the UIN of the root account
}, function(err, data) {
    console.log(err || data);
});
```

Grant the user permission to write the object via `AccessControlPolicy`:

[//]: # (.cssg-snippet-put-object-acl-acp)
```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
    AccessControlPolicy: {
        "Owner": { // There must be an owner in AccessControlPolicy
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
| Key | ObjectKey (object name) is the unique ID of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| ACL | Defines the ACL attribute of the object. For the enumerated values, such as `default`, `private`, and `public-read`, please see the **Preset ACL** section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: `default` <br>**Note:** If you do not need access control for the object, set `default` for this parameter or leave it empty. In this way, the object will inherit the permissions of the bucket it is stored in. | String | No |
| GrantRead | Grants the user read permission in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<br><li>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br><li>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantFullControl | Grants the user full permission in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<br><li>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br><li>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| AccessControlPolicy | Sets an object's ACL attributes | Object | No |
| - Owner | Information about the object owner | Object | No |
| - - - ID | Object owner ID in the format: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>For root accounts, `&lt;OwnerUin>` and `&lt;SubUin>` have the same value | String | No |
| - - DisplayName | Name of the object owner | String | No |
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
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as "200", "403", and "404" | Number |
| - headers | Headers returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 204, 403, and 404 | Number |
| - headers | Headers returned by the request | Object |

### Querying object ACL

#### API description

This API (GET Object acl) is used to query the access permissions of an object in a bucket. Only the bucket owner has permission to perform this operation.

#### Use case 

[//]: # (.cssg-snippet-get-object-acl)
```js
cos.getObjectAcl({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
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
| - headers | Headers returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Headers returned by the request | Object |
| - ACL | Defines the access control list (ACL) attributes of the object. For the enumerated values such as `private` and `public-read`, see the “Preset ACL for buckets” section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: `private` | String |
| - Owner | Identifies the owner of the resource | Object |
| - - - ID | Object owner ID in the format: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>For root accounts, `&lt;OwnerUin>` and `&lt;SubUin>` have the same value | String |
| - - DisplayName | Object owner name | String |
| - Grants | List of information on the grantee and permissions | ObjectArray |
| - - Permission | Specifies the permission granted to the authorized user. Enumerated values: `READ`, `WRITE`, `READ_ACP`, `WRITE_ACP`, `FULL_CONTROL` | String |
| - - Grantee | Authorized user’s information | Object |
| - - - DisplayName | Name of the user | String |
| - - - ID | User ID in the format: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>For root accounts, `&lt;OwnerUin>` and `&lt;SubUin>` have the same value | String |

## Advanced APIs (Recommended)

The following methods encapsulate the native methods mentioned above. They can be used to implement the complete multipart replication process and support concurrent multipart replications, checkpoint restart, as well as canceling, pausing, and restarting replication tasks.

### Copying an object

#### API description

This API (Slice Copy File) is used to copy a file from a source path to a destination path through multipart copy. Object metadata and ACL can be modified during the copy process. You can use this API to move, rename, and copy a file or modify its attributes.

#### Method prototype

Call `Slice Copy File`:

[//]: # (.cssg-snippet-transfer-copy-object)
```js
cos.sliceCopyFile({
    Bucket: 'examplebucket-1250000000',                               /* Required */
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

| Parameter                 | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| CopySource | URL path to the source object. A past object version can be specified with the URL parameter `?versionId=\<versionId>` | String | Yes |
| ChunkSize | Size (in bytes) of each part in the multipart copy. Defaults to `1048576` (1 MB). | Number | No |
| SliceSize | Specifies the minimum file size (in bytes) to use multipart copy. The default value is 5 GB. If the file size is equal to or smaller than this value, the file will be uploaded using `putObjectCopy`; otherwise, it will be uploaded using `sliceCopyFile`. | Number | No |
| onProgress | Callback of the upload progress. The callback parameter is the progress object `progressData`. | Function | No |
| - progressData.loaded | Size of the uploaded parts, in bytes | Number | No |
| - progressData.total | Size of the entire object, in bytes | Number    | No   |
| - progressData.speed | Upload speed, in bytes/s | Number | No |
| - progressData.percent | Percentage of the file copy progress, in decimal form. For example, 0.5 means 50% has been copied. | Number | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as "200", "403", and "404" | Number |
| - headers | Headers returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code returned by the request, such as "200", "403", and "404" | Number |
| - headers | Headers returned by the request | Object |
| - Location | Public network access endpoint of the object | String |
| - Bucket | Destination bucket for the multipart upload | String |
| - Key  | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| - ETag | MD5 checksum of the merged file. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880"` <br>**Note that double quotation marks are required at the beginning and the end**. | String |
| - VersionId  | The version ID will be returned for buckets that have enabled versioning. If the bucket has never enabled versioning, no value will be returned | String |

### Uploading queue

The SDK for Wechat Mini Programs records all the `putObject` upload tasks in a queue; relevant queue operations are as follows:

1. Use `cos.getTaskList` to get the task list.
2. Use `cos.pauseTask`, `cos.restartTask`, and `cos.cancelTask` to perform operations on upload tasks.
3. Use `cos.on('list-update', callback);` to monitor changes in the list and the upload progress.

For a complete example of queue usage, see the [demo](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/demo/queue).

#### Canceling an upload task

This API cancels an upload task by `taskId`.

**Use case**

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

This API is used to suspend an upload task by `taskId`.

**Use case**

[//]: # (.cssg-snippet-transfer-upload-pause)
```js
var taskId = 'xxxxx';                   /* Required */
cos.pauseTask(taskId);
```

**Parameter description**

| Parameter | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | ID of an upload task. When `putObject` is called, the `TaskReady` callback will return the `taskId` of the upload task. | String | Yes |

#### Restarting an upload task

This API is used to restart an upload task by `taskId`. You can restart tasks that have been manually suspended through the `pauseTask` API, or automatically suspended due to an upload error.

**Use case**

[//]: # (.cssg-snippet-transfer-upload-resume)
```js
var taskId = 'xxxxx';                   /* Required */
cos.restartTask(taskId);
```

**Parameter description**

| Parameter | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | ID of an upload task. When `putObject` is called, the `TaskReady` callback will return the `taskId` of the upload task. | String | Yes |
