## Overview

This document provides an overview of APIs and SDK code samples related to object downloads.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system. |

#### Description

This API (`GET Object`) is used to get the content, in string format, of a specified file in a bucket.

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

Downloading an object (via getObjectUrl): 

[//]: # (.cssg-snippet-get-presign-download-url-then-fetch)
```js
cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: '1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
    Sign: true
}, function (err, data) {
    if (err) return console.log(err);
    wx.downloadFile({
        url: data.Url, // The “url” domain name needs to be added to the download allowlist
        success (res) {
            console.log(res.statusCode, res.tempFilePath);
        },
        fail: function (err) {
            console.log(err);
        },
    });
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
| - statusCode | HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Headers. | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | Returns an HTTP status code, such as 200, 304, 403, and 404 | Number |
| - headers | Headers. | Object |
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
