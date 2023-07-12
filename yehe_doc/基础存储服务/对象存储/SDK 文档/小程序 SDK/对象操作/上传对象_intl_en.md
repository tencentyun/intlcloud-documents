## Feature Overview

This document provides an overview of APIs and SDK code samples related to simple operations and other object operations.

>? For upload FAQs, see [FAQs](https://intl.cloud.tencent.com/document/product/436/38958).
> 

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ---------------------------------------- |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object in whole | Uploads an object to a bucket. |
| [Append Object](https://intl.cloud.tencent.com/document/product/436/7741) | Appending parts | Appends object parts to a bucket.                      |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | Uploading an object using an HTML form | Uploads an object using an HTML form. |

**Multipart operations**

| API | Operation | Description |
| :----------------------------------------------------------- | :------------- | :----------------------------------- |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries in-progress multipart uploads. |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload. |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads an object in multiple parts. |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries the uploaded parts of a specified multipart upload. |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of an object. |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload and deletes the uploaded parts. |


## Simple Operations

### Uploading an object using simple upload

#### Feature description

This API (`PUT Object`) is used to upload an object to a bucket. To call this API, you must have write access to the bucket.

> !
> 1. The Key (filename) cannot end with `/`; otherwise, it will be identified as a folder.
> 2. Uploading the Key (file name) with the same name is identified as an overwritten operation by default. If you have not enabled version control and do not want to overwrite the file on the cloud, ensure that the Key to be uploaded is not duplicated.
> 3. Each root account (`AAPID`) can have up to 1,000 bucket ACLs and an unlimited number of object ACLs. If you do not need an ACL for an object, you can choose not to configure an ACL for the object during upload. In this way, the object will inherit the permissions of its bucket by default.
> 4. After an object is uploaded, you can use the same key to generate a pre-signed URL, which can be shared with other clients for downloading (to download, please use the `GET` method. The detailed API description is shown below). If your file is set to private-read, note that the pre-signed URL will only be valid for a certain period of time.

#### Sample code

Select a file and upload it (by using the `Body` parameter):

[//]: # (.cssg-snippet-put-object-body)
```js
// The image selecting API (wx.chooseImage) is used as an example here. For other APIs, see the official documentation of WeChat Mini Program.
wx.chooseImage({
    count: 1,
    success: function(res) {
        var file = res.tempFiles[0];
        // Get the file manager in the WeChat mini program
        var wxfs = wx.getFileSystemManager();
        wxfs.readFile({
            filePath: file.path,
            success: function (res) {
                cos.putObject({
                    Bucket: config.Bucket,
                    Region: config.Region,
                    Key: file.name,
                    Body: res.data, // Pass in the content of the file to `Body`
                }, function(err, data) {
                    console.log(err || data);
                });
            },
            fail: function(err) {
              console.error(err)
            },
        });
    },
    fail: function(err) {
      console.error(err)
    },
});
```

Select a file and upload it (by using the `FilePath` parameter, for SDK 1.3.0 or later only):

[//]: # (.cssg-snippet-put-object-filepath)
```js
// The image selecting API (wx.chooseImage) is used as an example here. For other APIs, see the official documentation of WeChat Mini Program.
wx.chooseImage({
    count: 1,
    success: function(res) {
        var file = res.tempFiles[0];
        cos.putObject({
            Bucket: config.Bucket,
            Region: config.Region,
            Key: file.name,
            FilePath: file.path,  // Pass in the file path to `FilePath`
        }, function(err, data) {
            console.log(err || data);
        });
    },
    fail: function(err) {
      console.error(err)
    },
});
```

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

>? For more information about the speed limits on object uploads, see [Single-Connection Bandwidth Limit](https://intl.cloud.tencent.com/document/product/436/34072).

[//]: # (.cssg-snippet-put-object-traffic-limit)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /* Required */
    StorageClass: 'STANDARD',
    Body: 'hello!', // Upload the file object (string or selected file)
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
| Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| Body                   | Text content of the created file, which can be a string or an ArrayBuffer                           | String or ArrayBuffer   | Yes  |
| CacheControl | Cache policy as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentDisposition | Filename as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentEncoding | Encoding format as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentLength | HTTP request length (in bytes) as defined in RFC 2616 | String | No |
| ContentType | Content type (MIME) as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| Expires | Expiration time as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| Expect | If `Expect: 100-continue` is used, the request content will be sent only after confirmation from the server is received | String | No |
| ACL   | Defines the access control list (ACL) attribute of the object. For the enumerated values such as `default`, `private`, and `public-read`, see the Preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). <br>**Note:** If you do not need access control for the object, set `default` for this parameter or simply leave it blank, and the object will inherit the permissions of the bucket | String | No |
| GrantRead | Grants a user read permission to the object in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users. <ul  style="margin: 0;"><li>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.</li><li>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.</br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'`</li></ul> | String | No |
| GrantReadAcp | Grants the user read permission to the object's ACL in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.</li><li>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'`</li></ul>| String | No |
| GrantWriteAcp | Grants the user write permission to the object's ACL in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.</li><li>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.</br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'`</li></ul> | String | No |
| GrantFullControl | Grants the user full permission to the object in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users. <ul  style="margin: 0;"><li>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.</li><li>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.</br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'`</li></ul> | String | No |
| StorageClass | Storage class of the object. For the enumerated values, such as `STANDARD` (default), `STANDARD_IA`, and `ARCHIVE`, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String | No |
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
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| - ETag | MD5 checksum of the object. The value of this parameter can be used to check whether the object was corrupted during the upload. <br>Example: `"09cba091df696af91549de27b8e7d0f6"`. **Note that double quotation marks are required at the beginning and the end.** | String |
| - Location | Public network access endpoint of the object | String |
| - VersionId       | Version ID of the uploaded object if versioning is enabled for its bucket. If versioning is not enabled, this parameter is not returned. | String  |

### Appending parts

#### Feature description

This API (`APPEND Object`) is used to append object parts to a bucket.

> !
>- The COS Mini Program SDK version should be or later than v1.1.1.
> - This API can append data only to appendable objects.
> - If an object is uploaded using the `APPEND Object` API for the first time, it will be automatically determined as "appendable".
> - You can use the `GET Object` or `HEAD Object` API to get the `x-cos-object-type` response header to determine the object type.
> 

#### Sample code

Append parts for the first time:

[//]: # (.cssg-snippet-append-object)
```js
cos.appendObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'test.txt',              /* Required */
    Body: fileObject, // Upload the file object.
    Position: 0, // The value is `0` for the first upload.
}, function(err, data) {
    console.log(err || data);
});
```

Check whether parts can be appended to an object in a bucket:

[//]: # (.cssg-snippet-append-object)
```js
cos.headObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'test.txt',              /* Required */
}, function(err, data) {
    if (err) return console.log(err);
    // If `data.headers` does not contain the `x-cos-object-type` field, you need to configure `expose-headers`. For more information, see https://cloud.tencent.com/document/product/436/13318.
    var objectType = data.headers['x-cos-object-type'];
    console.log(objectType === 'appendable');
});
```

Query the position of the object for parts appending and start upload:

[//]: # (.cssg-snippet-append-object)
```js
cos.headObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'test.txt',              /* Required */
}, function(err, data) {
    if (err) return console.log(err);
    // Get the current length (position for upload) of the file to be appended
    var position = data.headers['content-length'];
    cos.appendObject({
        Bucket: 'examplebucket-1250000000', /* Required */
        Region: 'COS_REGION',     /* Bucket region. Required */
        Key: 'test.txt',              /* Required */
        Body: '66666',
        Position: position,
    },
    function(err, data) {
        if (err) return console.log(err);
        // Get the position for the next upload and continue appending parts
        // If `data.headers` does not contain the `x-cos-next-append-position` field, you need to configure `expose-headers`. For more information, see https://cloud.tencent.com/document/product/436/13318.
        var nextPosition = data.headers['x-cos-next-append-position'];
        console.log(nextPosition);
    })
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | ---------------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| Body | Text content of the created file, which can be a string                           | String or ArrayBuffer   | Yes |
| Position | Starting point for the append operation (in bytes). For the first append, the value of this parameter is 0. For subsequent appends, the value is the `content-length` of the current object. | Number | Yes |
| CacheControl | Cache policy as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentDisposition | Filename as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentEncoding | Encoding format as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentLength | HTTP request length (in bytes) as defined in RFC 2616 | String | No |
| ContentType | Content type (MIME) as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| Expires | Expiration time as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| Expect | If `Expect: 100-continue` is used, the request content will be sent only after confirmation from the server is received. | String | No |
| ACL | ACL attribute of the object. For the enumerated values, such as `default`, `private`, and `public-read`, see the **Preset ACL** section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). <br/>**Note: if you do not need access control for the object, set this parameter to `default` or do not specify it, in which case the object will inherit the permissions of the bucket.** | String | No |
| GrantRead              | Grants a user read access to the object in the format of `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.<br/>Example: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul> | String               | No   |
| GrantReadAcp           | Grants a user read access to the object in the format of `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.<br/>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'`</li></ul> | String           | No   |
| GrantWriteAcp          | Grants a user write access to the object in the format of `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.<br/>Example: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul> | String           | No   |
| GrantFullControl       | Grants a user full access in the format of `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/<OwnerUin>:uin/&lt;SubUin&gt;"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code>.<br/>Example: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul> | String | No   |
| StorageClass | Storage class of the object. For the enumerated values, such as `STANDARD` (default), `STANDARD_IA`, `ARCHIVE`, and `DEEP_ARCHIVE`, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String | No |
| x-cos-meta-\* | User-defined headers, which will be saved as the object metadata. The maximum size is 2 KB. | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Error code, which is returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| - RequestId | Unique ID of the request | String |

 

### Uploading an object using an HTML form

This API (POST Object) is used to upload an object selected by the user through `wx.chooseImage` to a specified bucket. To call this API, you need to have permission to write the bucket.

>! `onProgress` depends on the mini program [UploadTask.onProgressUpdate](https://developers.weixin.qq.com/miniprogram/dev/api/network/upload/UploadTask.onProgressUpdate.html). The progress might be inaccurate on some Android models.

#### Sample code

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
| Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| ContentLength | HTTP request length in bytes as defined in RFC 2616 | String | Yes |
| CacheControl | Cache policy as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentDisposition | Filename as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentEncoding | Encoding format as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentType | Content type (MIME) as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| Expires | Expiration time as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| Expect | If `Expect: 100-continue` is used, the request content will be sent only after confirmation from the server is received | String | No |
| ACL | Defines the ACL attribute of the object. For the enumerated values, such as `default`, `private`, and `public-read`, see the **Preset ACL** section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: `default` <br>**Note:** If you do not need access control for the object, set `default` for this parameter or leave it empty. In this way, the object will inherit the permissions of the bucket it is stored in. | String | No |
| StorageClass | Storage class of the object. For the enumerated values, such as `STANDARD` (default), `STANDARD_IA`, and `ARCHIVE`, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String | No |
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
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| - ETag | Returns the MD5 checksum of the object. The value of `ETag` can be used to check whether the object was corrupted during upload. <br>For example, `"09cba091df696af91549de27b8e7d0f6"`. **Note: double quotation marks are required at the beginning and the end of the `ETag` value ** |string   |
| - Location | Creates an object's access domain name for external networks | String |
| - VersionId | The version ID of the returned object in a versioning-enabled bucket | String |


## Multipart Operations

### Querying multipart uploads

#### Feature description

This API (List Multipart Uploads) is used to query ongoing multipart uploads. Up to 1,000 multipart uploads can be listed at a time.

#### Sample code

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
| Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Prefix | Object key prefix to query uploads by. Note that when you query uploads with the prefix specified, the returned object keys will also contain the prefix. | String | No |
| Delimiter | Separating symbol used to group object keys. It is usually `/`. The identical paths between `Prefix` or, if no `Prefix` is specified, the beginning and the first `delimiter` are grouped and defined as a common prefix. All common prefixes will be listed. | String | No |
| EncodingType | Encoding type of the returned value. Valid value: `url` | String | No |
| MaxUploads | Maximum number of entries to return at a time. Valid range: 1-1000 (default) | String | No |
| KeyMarker      | This parameter is used together with `upload-id-marker`.<ul  style="margin: 0;"><li>If `upload-id-marker` is not specified:<br>Only multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed. </li><li>If `upload-id-marker` is specified:<ul  style="margin: 0;"><li>Multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed. </li><li>Multipart uploads whose `ObjectName` is lexicographically equal to the specified `key-marker` and whose `UploadID` is greater than the specified `upload-id-marker` will be listed.</li></ul></li></ul> | String | No   |
| UploadIdMarker | This parameter is used together with `key-marker`.<ul  style="margin: 0;"><li>If `key-marker` is not specified:<br>`upload-id-marker` will be ignored.</li><li>If `key-marker` is specified:<ul  style="margin: 0;"><li>Multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed.</li><li>Multipart uploads whose `ObjectName` is lexicographically equal to the specified `key-marker` and whose `UploadID` is greater than the specified `upload-id-marker` will be listed.</li></ul></li></ul>| String | No   |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| -------------------- | ------------------------------------------------------------ | ----------- |
| err | Error code, which is returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
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
| - MaxUploads | Maximum number of returned entries. Valid value range: 1-1000 | String | 
| - IsTruncated | Whether the returned list is truncated. Valid values: `true`, `false` | String|
| - Prefix | Object key prefix by which uploads are queried | String |
| - Delimiter | Separating symbol used to group object keys, which is usually `/`. Objects with identical paths between `Prefix` or, if no `Prefix` is specified, the beginning of their keys, and the first delimiter are grouped together and defined as common prefixes. All common prefixes are listed. | String |
| - CommonPrefixes | Objects with identical paths between `Prefix` and the delimiter, which are grouped together and defined as common prefixes | ObjectArray |
| - - Prefix | Specific prefixes | String |
| - Upload | Information of the multipart upload | ObjectArray |
| - - Key | Object key, i.e., object name | String |
| - - UploadId | ID of the multipart upload | String |
| - - StorageClass | Storage class of the parts, such as `STANDARD`, `STANDARD_IA`, and `ARCHIVE`. For more information, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String |
| - - Initiator | Initiator of the multipart upload | Object |
| - - - DisplayName | Name of the upload initiator | String |
| - - - ID | ID of the upload initiator in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value. | String |
| - - Owner | Information about the part owner | Object  |
| - - - DisplayName | Name of the part owner | String |
| - - - ID | ID of the parts owner in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`.<br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value. | String |
| - - Initiated | Starting time of the multipart upload | String |

### Initializing a multipart upload

#### Feature description

This API (Initiate Multipart Uploads) is used to initialize a multipart upload. After a successful operation, an upload ID will be returned, which can be used in the subsequent `Upload Part` requests.

#### Sample code

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
| Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| CacheControl | Cache policy as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| Content-Disposition | Filename as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentEncoding | Encoding format as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentType | Content type (MIME) as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| Expires | Cache expiration time as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ACL | ACL attribute of the object. For the enumerated values, such as `default`, `private`, and `public-read`, see the **Preset ACL** section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). <br>**Note**: If you do not need access control for the object, set this parameter to `default` or do not specify it, in which case the object will inherit the permissions of its bucket. | String | No |
| GrantRead | Grants a user read permission to the object in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users. <ul  style="margin: 0;"><li>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.</li><li>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'`</li></ul> | String | No |
| GrantFullControl | Grants the user full permission to the object in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users. <ul  style="margin: 0;"><li>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.</li><li>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'`</li></ul> | String | No |
| StorageClass | Storage class of the object, such as `STANDARD` (default), `STANDARD_IA`, and `ARCHIVE`. For more information, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String | No |
| x-cos-meta-* | User-defined headers, which will be returned as the object metadata. The maximum size is 2 KB. | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| Bucket | Destination bucket for the multipart upload. Format: `BucketName-APPID`. Example: `examplebucket-1250000000` | String |
| Key | Object key (object name), the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| UploadId | Upload ID, which is required for the subsequent upload | String |

### Uploading parts

#### Feature description

This API (`Upload Part`) is used to upload parts after a multipart upload is initialized. It can upload 1-10,000 parts of 1 MB to 5 GB at a time.
<li>When you use the `Initiate Multipart Upload` API to initiate a multipart upload, you can obtain the `uploadId`. This ID uniquely identifies the part and its position in the entire object.</li>
<li>Every time you call the `Upload Part` API, you need to pass `partNumber` (the part number) and `uploadId`. You can upload multiple parts out of order.</li>
<li>When the `uploadId` and `partNumber` of a new part are the same as those of a previously uploaded part, the old part will be overwritten. If the `uploadId` does not exist, the 404 error, "NoSuchUpload", will be returned.</li>

#### Sample code

[//]: # (.cssg-snippet-upload-part)
```js
cos.multipartUpload({
   Bucket: 'examplebucket-1250000000', /* Required */
   Region: 'COS_REGION',     /* Bucket region. Required */
   Key: 'exampleobject', /* Required */
   UploadId: 'exampleUploadId',
   PartNumber: 1,
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
| Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| ContentLength | HTTP request length (in bytes) as defined in RFC 2616 | String | Yes |
| PartNumber    | Part number                                                   | Number           | Yes   |
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
| err | Error code, which is returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |

### Querying uploaded parts

#### Feature description

This API (`List Parts`) is used to query the uploaded parts of a specified multipart upload, i.e., listing all successfully uploaded parts of a multipart upload with the specified `uploadId`.

#### Sample code

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
| Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key     | Object key (object name), which is the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
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
| err | Error code, which is returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| - Bucket | Destination bucket for the multipart upload | String |
| - Encoding-type | Encoding type for the returned value | String |
|  - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| - UploadId | Multipart upload ID obtained from the `Initiate Multipart Upload` API | String      |
| - Initiator | Initiator of the upload | Object |
| - - DisplayName | Name of the upload initiator | String |
| - - ID | ID of the upload initiator in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` <br>For the root account, &lt;OwnerUin> and &lt;SubUin> have the same value. | String |
| - Owner | Information about the part owner | Object  |
| - - DisplayName | Name of the bucket owner | String |
| - - ID | ID of the bucket owner. This parameter is usually the user’s UIN. | String |
| - StorageClass | Storage class of the parts, such as `STANDARD`, `STANDARD_IA`, and `ARCHIVE`. For more information, see [Storage Classes Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String |
| - PartNumberMarker | By default, parts are listed in UTF-8 binary order, starting from the part after the marker. | String |
| NextPartNumberMarker  | The part after which the next returned list begins if the list is truncated.    | String    |
| - MaxParts | Maximum number of entries returned at a time | String |
| - IsTruncated | Whether the returned list is truncated. Valid values: `true`, `false` | String |
| - Part | Part information list | ObjectArray |
| - - PartNumber | Part number | String |
| - - LastModified | Last modified time of a part | String |
| - - ETag | MD5 checksum of a part | String |
| - - Size | Part size, in bytes | String |

### Completing a multipart upload

#### Feature description

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
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
    Key: 'exampleobject', /* Required */
    UploadId: 'exampleUploadId', /*Required*/
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
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key     | Object key (object name), which is the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| UploadId | ID of the upload | String | Yes |
| Parts | A list of information about the parts of the multipart upload | ObjectArray | Yes |
| - PartNumber    | Part number                                                   | Number           | Yes   |
| - ETag | MD5 checksum of each part. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`<br>**Note that double quotation marks are required at the beginning and the end.** | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| - Location | Public network access endpoint of the object | String |
| - Bucket | Destination bucket for the multipart upload | String |
| - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| - ETag | Unique ID of the file after assembly in the format of `"uuid-<part quantity>"`. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`. **Note that double quotation marks are required at the beginning and the end.** | String |

### Aborting a multipart upload

#### Feature description

This API (`Abort Multipart Upload`) is used to abort a multipart upload and delete the uploaded parts. If you call this API and there is an in-progress upload request with the specified `UploadId`, the upload request will fail. If the `uploadId` does not exist, `404` (NoSuchUpload) will be returned.

> !We recommend you either complete or abort a multipart upload as early as possible, as the uploaded parts of an incomplete multipart upload will take up storage capacity and incur storage fees.

#### Sample code

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
| Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key     | Object key (object name), which is the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| UploadId | Multipart upload ID, which is obtained from the response of the `Initiate Multipart Upload` API | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |

## Advanced APIs (Recommended)

The following methods encapsulate the native methods mentioned above. They can implement the complete process of multipart upload and support concurrent multipart upload, checkpoint restart as well as canceling, pausing, and resuming upload tasks.

### Advanced upload

#### Feature description
    
This API is used to implement advanced upload. The `SliceSize` parameter can be used to specify the file size limit (1 MB by default) to determine whether to use multipart upload. If the file size is greater than this threshold, multipart upload will be used; otherwise, simple upload will be used.
    
#### Sample code

[//]: # (.cssg-snippet-transfer-upload-file)
```js
var uploadFile = function(file) {
    cos.uploadFile({
        Bucket: 'examplebucket-1250000000', /* Required */
        Region: 'COS_REGION',     /* Bucket region. Required */
        Key: file.name,              /* Required */
        FilePath: file.path,                /* Required */
        FileSize: file.size,                 /* Required for versions earlier than v1.4.3 and optional for v1.4.3 and later */
        SliceSize: 1024 * 1024 * 5,     /* Threshold (5 MB in this example) to trigger multipart upload. This parameter is optional. You can adjust it as needed. The minimum value of this parameter is 1 MB.*/
        TaskReady: function(taskId) { /*Optional*/
            console.log(taskId);
        },
        onProgress: function (progressData) { /* Optional */
            console.log(JSON.stringify(progressData));
        },
        onFileFinish: function (err, data, options) {   /* Optional */
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
       uploadFile(res.tempFiles[0]);
   }
});
```

#### Parameter description

| Parameter &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type      | Required |
| ------------------------------------------------------------ | ------------------------------------------------------------ | --------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key                                                          | Object key (object name), which is the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String    | Yes   |
| FilePath                                                         | Path to the file to upload           | String | Yes   |
| FileSize                                                         | Size of the file to be uploaded (required for versions earlier than v1.4.3 and optional for v1.4.3 and later)	           | Number | Yes   |
| SliceSize                                                    | File size threshold in bytes, `1048576` (1 MB) by default. If the file size is equal to or smaller than this value, the file will be uploaded using `putObject`; otherwise, it will be uploaded using `sliceUploadFile`.                                                     | Number    | No   |
| AsyncLimit                                                   | Maximum number of concurrently uploaded parts allowed. This parameter is valid only when a multipart upload is triggered.                                           | Number    | No   |
| StorageClass | Storage class of the object, such as `STANDARD`, `STANDARD_IA`, `ARCHIVE`, and `DEEP_ARCHIVE`. For more information, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String | No |
| UploadAddMetaMd5 | Sets x-cos-meta-md5 as the object’s MD5 checksum in the object’s metadata during upload in the format of a 32-bit lowercase string. Example: `4d00d79b6733c9cc066584a02ed03410`. | String | No |
| CacheControl | Cache policy as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentDisposition | Filename as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentEncoding | Encoding format as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentLength | HTTP request length (in bytes) as defined in RFC 2616 | String | No |
| ContentType | Content type (MIME) as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| Expires | Expiration time as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| Expect | If `Expect: 100-continue` is used, the request content will be sent only after confirmation from the server is received. | String | No |
| onTaskReady | Callback function when an upload task is created. The callback returns a `taskId`, which uniquely identifies the task and can be used to cancel (`cancelTask`), pause (`pauseTask`), or resume (`restartTask`) the task. | Function | No |
| - taskId                                                     | ID of the upload task                                              | String    | No  |
| onProgress | Callback for the upload progress, whose parameter is `progressData` | Function | No |
| - progressData.loaded | Size of the uploaded parts, in bytes | Number | No |
| - progressData.total                                         | Size of the entire file, in bytes                      | Number    | No   |
| - progressData.speed                                         | File upload speed, in bytes/s                 | Number    | No   |
| - progressData.percent | File upload progress, in decimal form. For example, 0.5 means 50% has been uploaded. | Number | No |
| onFileFinish           | Callback for file upload success or failure                                       | Function    | No   |
| - err | Upload error message | Object | No |
| - data | Information about the completion of object upload | Object | No |
| - options | Parameter information about the files that have been uploaded | Object | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Error code, which is returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| - Location   | Access address of the uploaded file                                        | String |
| - Bucket     | Destination bucket for the multipart upload. This parameter is returned only when a multipart upload is triggered.                                       | String |
| - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324). This parameter is returned only when multipart upload is triggered. | String |
| - ETag | Unique ID of the file after assembly in the format of `"uuid-<part quantity>"`. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`. **Note that double quotation marks are required at the beginning and the end.** | String |
| - VersionId       | Version ID of the uploaded object if versioning is enabled for its bucket. If versioning is not enabled, this parameter is not returned. | String  |

### Uploading an object using multipart upload (checkpoint restart)
#### Feature description
This API (`Slice Upload File`) is used to upload large files in parts.
#### Sample code
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
| Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| FilePath | Path to the file to upload | String | Yes |
| SliceSize              | Part size                                                     | Number   | No   |
| AsyncLimit                                                   | Maximum number of parts for concurrent upload. This parameter is valid only when multipart upload is triggered.                                           | Number    | No   |
|  StorageClass | Storage class of the object, such as `STANDARD`, `STANDARD_IA` and `ARCHIVE`. For more information, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String | No |
| CacheControl | Cache policy as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentDisposition | Filename as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentEncoding | Encoding format as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| ContentLength | HTTP request length (in bytes) as defined in RFC 2616 | String | No |
| ContentType | Content type (MIME) as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| Expires | Expiration time as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| Expect | If `Expect: 100-continue` is used, the request content will be sent only after confirmation from the server is received. | String | No |
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
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| - Location | Public network access endpoint of the object | String |
| - Bucket | Destination bucket for the multipart upload | String |
| - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| - ETag | Unique ID of the file after assembly in the format of `"uuid-<part quantity>"`. <br>Example: `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`. **Note that double quotation marks are required at the beginning and the end.** | String |
| - VersionId       | Version ID of the uploaded object if versioning is enabled for its bucket. If versioning is not enabled, this parameter is not returned. | String  |

### Batch upload

#### Feature description

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
            FilePath: file.path,                /* Required */
            FileSize: file.size,                 /* Required for versions earlier than v1.4.3 and optional for v1.4.3 and later */
            Bucket: 'examplebucket-1250000000', /* Required */
            Region: 'COS_REGION',     /* Bucket region. Required */
            Key: file.name,              /* Required */
            onTaskReady: function(taskId) {
              /* Based on `taskId`, you can use queue operations to cancel upload `cos.cancelTask(taskId)`, pause upload `cos.pauseTask(taskId)`, and resume upload `cos.restartTask(taskId)` */
              console.log(taskId);
            }
        });
    });
    cos.uploadFiles({
        files: fileList,
        SliceSize: 1024 * 1024 * 10,    /* Threshold (10 MB in this example) to trigger multipart upload. You can adjust it as needed. The minimum value of this parameter is 1 MB. */
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
| - Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| - Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| - FilePath | Path to the file to upload | String | Yes |
| - FileSize                                                         | Size of the file to be uploaded (required for versions earlier than v1.4.3 and optional for v1.4.3 and later)           | Number | Yes   |
| - CacheControl | Cache policy as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| - ContentDisposition | Filename as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| - ContentEncoding | Encoding format as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| - ContentLength | HTTP request length (in bytes) as defined in RFC 2616 | String | No |
| - ContentType | Content type (MIME) as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| - Expires | Expiration time as defined in RFC 2616. It will be stored as the object metadata. | String | No |
| - Expect | If `Expect: 100-continue` is used, the request content will be sent only after confirmation from the server is received. | String | No |
| - onTaskReady | Callback function when an upload task is created. The callback returns a `taskId`, which uniquely identifies the task and can be used to cancel (`cancelTask`), pause (`pauseTask`), or resume (`restartTask`) the task. | Function | No |
| -- taskId                                                     | ID of the upload task                                              | String    | No  |
| SliceSize                                                    | File size threshold in bytes, `1048576` (1 MB) by default. If the file size is equal to or smaller than this value, the file will be uploaded using `putObject`; otherwise, it will be uploaded using `sliceUploadFile`.                                                     | Number    | Yes   |
| onProgress | Upload progress calculated by averaging out the progress of all tasks | String | Yes |
| - progressData.loaded | Size of the uploaded parts, in bytes | Number | No |
| - progressData.total | Size of the entire file, in bytes | Number | No |
| - progressData.speed | File upload speed, in bytes/s | Number | No |
| - progressData.percent | Percentage of the file upload progress, in decimal form. For example, 0.5 means 50% has been uploaded. | Number | No |
| onFileFinish           | Callback for file upload success or failure                                       | Function    | No   |
| - err | Upload error message | Object | No |
| - data | Information about the completion of object upload | Object | No |
| - options | Parameter information about the files that have been uploaded | Object | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ----------- |
| err | Error code, which is returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - files | Error or data for each file | ObjectArray |
| - - error | Upload error message | Object |
| - - data | Information about the completion of object upload | Object |
| - - options | Parameter information about the files that have been uploaded | Object |

### Uploading queue

The Mini Program SDK records all the `putObject` upload tasks in a queue; relevant queue operations are as follows:

1. Use `var taskList = cos.getTaskList()` to get the task list.
2. Use `cos.pauseTask()`, `cos.restartTask()`, and `cos.cancelTask()` to perform operations on upload tasks.
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

