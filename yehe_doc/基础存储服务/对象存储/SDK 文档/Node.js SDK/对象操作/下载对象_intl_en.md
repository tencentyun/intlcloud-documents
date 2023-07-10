## Overview

>! This API is used to read object content. To download a file using your browser, you should first get a download URL through the `cos.getObjectUrl` method. For more information, please see [Pre-signed URLs](https://intl.cloud.tencent.com/document/product/436/31540).
>

This document provides an overview of APIs and SDK code samples related to object downloads.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system. |

## Simple Operations

## Downloading a Single Object

#### Description

This API (GET Object) is used to download an object in a COS bucket to a local file system. To call this API, you need to have permission to read the object, or the object is set to `public-read`.

#### Sample code

[//]: # (.cssg-snippet-get-object)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: '1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
}, function(err, data) {
    console.log(err || data.Body);
});
```

Getting file content with `Range` specified

[//]: # (.cssg-snippet-get-object-range)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: '1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
    Range: 'bytes=1-3', /*Optional*/
}, function(err, data) {
    console.log(err || data.Body);
});
```

Download the file to a specified path:

[//]: # (.cssg-snippet-get-object-path)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: '1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
    Output: './exampleobject',
}, function(err, data) {
    console.log(err || data);
});
```

Download the file to a specified write file stream:

[//]: # (.cssg-snippet-get-object-stream)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: '1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
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
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: '1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
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
| - statusCode | HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Headers. | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | Returns an HTTP status code, such as 200, 304, 403, and 404 | Number |
| - headers | Headers. | Object |
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


### Downloading multiple objects

#### Sample code

Download multiple objects with a specified prefix (download objects from a specified directory):

[//]: # (.cssg-snippet-get-objects)
```js
var config = {
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */ 
}

// Example of how to create a directory recursively. You can implement it by yourself.
function mkdirsSync(dirname) {
  if(fs.existsSync(dirname)) {
    return true;
  }else{
    if(mkdirsSync(path.dirname(dirname))) {
      fs.mkdirSync(dirname);
      return true;
    }
  }
}

// Download a single object
function downloadItem(Key, downloadPath) {
    cos.getObject({
      Bucket: config.Bucket,
      Region: config.Region,
      Key: Key,
      Output: fs.createWriteStream(downloadPath),
    },
    function(err, data) {
        console.log(err || data);
    });
}

// Download multiple objects
function batchDownload(marker = undefined) {
  cos.getBucket({
    Bucket: config.Bucket,
    Region: config.Region,
    Prefix: '1',  // Search for all objects with prefix '1'
    Marker:       marker,
    MaxKeys: 1000,
  },
  function (listError, listResult) {
    if (listError) return console.log(listError);
    // Download to the 'download' directory under this directory
    var localPath = 'download';
    listResult.Contents.forEach(function (item) {
      var downloadPath = path.resolve(localPath, item.Key);
      var pathParse = path.parse(item.Key);
      if (pathParse.dir) {
        // If the downloaded object is in a multi-level directory, create a corresponding directory locally.
        // For example, if the Key is a/b/1.png, create a directory structure 'a/b' locally 
        var mkdir = path.resolve(localPath, pathParse.dir);
        mkdirsSync(mkdir);
        downloadItem(item.Key, downloadPath);
      } else {
        downloadItem(item.Key, downloadPath);
      }
    });
  })
}
batchDownload();
```


## Advanced Operations (Recommended)

### Multipart download

#### Description

This API is used to implement multipart download. It supports concurrent part download.(The sdk version is required to be at least v2.9.14)

#### Method prototype

Multipart download sample:

```js
var Key = 'test.zip';
cos.downloadFile({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: Key,
    FilePath: './' + Key, // Local path
    ChunkSize: 1024 * 1024 * 8, // Part size
    ParallelLimit: 5, // Number of concurrent parts
    RetryTimes: 3, // Number of retries for multipart download failures
    TaskId: '123', // TaskId can be automatically generated for canceling the download

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
| err | Error code, which is returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | Returns an HTTP status code, such as 200, 304, 403, and 404 | Number |
| - headers | Headers. | Object |
| - Cache-Control | Cache directives as defined in RFC 2616. It will be returned only if it is contained in the object metadata or specified through the request parameter. | String |
| - Content-Disposition | Filename as defined in RFC 2616. It will be returned only if it is contained in the object metadata or specified through the request parameter. | String |
| - ContentEncoding | Encoding format as defined in RFC 2616. It will be returned only if it is contained in the object metadata or specified through the request parameter. | String |
| - Expires | Cache expiration time as defined in RFC 2616. It will be returned only if it is contained in the object metadata or specified through the request parameter. | string |
| - x-cos-storage-class | Storage class of the object. Enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE` <br>**Note: If this header is not returned, the storage class is automatically set to `STANDARD`** | String |
| - x-cos-meta-* | User-defined metadata | String |
| - NotModified | This attribute will be returned if the request contains `IfModifiedSince`. If the file has been modified, `false` will be returned. If not, `true` will be returned. | Boolean |
| - ETag | MD5 checksum of the object. The value of `ETag` can be used to check whether the object was corrupted during the upload. <br>Example: `"09cba091df696af91549de27b8e7d0f6"` <br>**Note that double quotation marks are required at the beginning and the end**. | String |
| - VersionId       | Version ID of the uploaded object if versioning is enabled for its bucket. If versioning is not enabled, this parameter is not returned. | String  |
