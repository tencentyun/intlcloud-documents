## Overview

>! This API is used to read object content. To download a file using your browser, you should first get a download URL through the `cos.getObjectUrl` method. For more information, see [Pre-signed URLs](https://intl.cloud.tencent.com/document/product/436/31540).
>

This document provides an overview of APIs and SDK code samples for downloading an object.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |

#### Feature description

This API (`GET Object`) is used to get the content, in string format, of a specified file in a bucket.
To download files to your local system, see [Generating Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/31540#.E4.B8.8B.E8.BD.BD.E8.AF.B7.E6.B1.82.E7.A4.BA.E4.BE.8B).

### Downloading a single object

#### Sample code

[//]: # (.cssg-snippet-get-object)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region (required), such as ap-beijing */
    Key: '1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
    onProgress: function (progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data.Body);
});
```

Getting file content with `Range` specified

[//]: # (.cssg-snippet-get-object-range)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region (required), such as ap-beijing */
    Key: '1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
    Range: 'bytes=1-3', /*Optional*/
    onProgress: function (progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data.Body);
});
```

Object content in BLOB format is returned.

[//]: # (.cssg-snippet-get-object-data-type)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /* Required */
    DataType: 'blob',        /* Optional */
    onProgress: function (progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data.Body);
});
```

Downloading an object (limiting single-URL speed):

>?For more information about the speed limits on object downloads, see [Single-Connection Bandwidth Limit](https://intl.cloud.tencent.com/document/product/436/34072).

[//]: # (.cssg-snippet-get-object-traffic-limit)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region (required), such as ap-beijing */
    Key: '1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
    Headers: {
      'x-cos-traffic-limit': 819200, // The speed range is 819200 to 838860800, that is 100 KB/s to 100 MB/s. If the value is not within this range, 400 will be returned.
    },
    onProgress: function (progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data.Body);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| DataType                     | Format of the object content returned. Enumerated values: `string` (default), `blob`, `arraybuffer` | String   | No  |
| ResponseContentType | `Content-Type` parameter in the response header | String | No |
| ResponseContentLanguage | `Content-Language` in the response header | String | No |
| ResponseExpires | `Content-Expires` in the response header | String | No |
| ResponseCacheControl | `Cache-Control` in the response header | String | No |
| ResponseContentDisposition | `Content-Disposition` in the response header | String | No |
| ResponseContentEncoding | `Content-Encoding` in the response header | String | No |
| Range | Byte range of the object as defined in RFC 2616. The range value must be in the format of `bytes=first-last`, where both `first` and `last` are offsets starting from 0. For example, `bytes=0-9` means to download the first 10 bytes of the object. If this parameter is not specified, the entire object will be downloaded. | String | No |
| IfModifiedSince | Required modification time. The object is downloaded only if it has been modified after the specified time. Otherwise, `304` (not modified) will be returned. | String | No |
| If-Unmodified-Since | Required unmodified time. The object is downloaded only if it has not been modified since the specified time. Otherwise, `412` (precondition failed) will be returned. | String | No |
| IfMatch | `ETag` that must be matched. The object is downloaded only if its `ETag` matches the specified value. Otherwise, `412` (precondition failed) will be returned. | String | No |
| IfNoneMatch | `ETag` that cannot be matched. The object is downloaded only if its `ETag` does not match the specified value. Otherwise, `304` (not modified) will be returned. | String | No |
| VersionId | Version ID of the object to download | String | No |
| onProgress | Progress callback. The attributes of the response object `progressData` are as follows. | Function | No |
| - progressData.loaded | Size of the downloaded parts, in bytes | Number | No |
| - progressData.total | Size of the entire object, in bytes | Number | No |
| - progressData.speed | Download speed, in bytes/s | Number | No |
| - progressData.percent | File download progress, in decimal form. For example, 0.5 means 50% has been downloaded. | Number | No |

#### Callback function description

```
function(err, data) { ... }

```

| Parameter &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Type |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------- |
| err | Error code, which is returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as `200`, `304`, `403`, and `404` | Number |
| - headers | Headers | Object |
| - CacheControl  | Cache directives as defined in RFC 2616, which will be returned only if it is contained in the object metadata or if it is specified in the request parameter. | string |
| - ContentDisposition                                         | Filename as defined in RFC 2616, which will be returned only if it is contained in the object metadata or if it is specified in the request parameter | String  |
| - ContentEncoding                                            | Encoding format as defined in RFC 2616, which will be returned only if it is contained in the object metadata or if it is specified in the request parameter | String  |
| - Expires                                                    | Cache expiration time as defined in RFC 2616, which will be returned only if it is contained in the object metadata or if it is specified in the request parameter | String  |
| - x-cos-storage-class | Storage class of the object. For the enumerated values, such as `STANDARD` and `STANDARD_IA`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925).</br>**Note: If this header is not returned, the storage class is `STANDARD`.** | String  |
| - x-cos-meta-\*                                               | User defined metadata                                           | String  |
| - NotModified      | This field is returned if the request has `IfModifiedSince`. If the file hasn’t been modified after the specified time, `true` is returned. If not, `false` is returned. | Boolean |
| - ETag | MD5 checksum of the object. The value of this parameter can be used to check whether the object was corrupted during the upload. </br>Example: `"09cba091df696af91549de27b8e7d0f6"`. **Note that double quotation marks are required at the beginning and the end of the value.** | String |
| - VersionId       | Version ID of the uploaded object if versioning is enabled for its bucket. If versioning is not enabled, this parameter is not returned. | String  | 
| - Body                | Returned file content, in string format by default        | String  |


### Downloading multiple objects

This is not recommended as you cannot use code to control the start or stop after triggering a download with browser. When too many objects need to be downloaded, it may cause a poor experience.


#### Sample code

Downloading multiple objects with a specified prefix (downloading files in a specified directory):

[//]: # (.cssg-snippet-get-objects)
```js
var getObjects = function (marker) {
    cos.getBucket({
        Bucket: config.Bucket,
        Region: config.Region,
        Prefix: 'abc', /* A directory/prefix to download */
        Marker:       marker,
        MaxKeys: 1000,
    }, function (listError, listResult) {
        if (listError) return console.log('list error:', listError);
        var nextMarker = listResult.NextMarker;
        listResult.Contents.forEach(function (item) {
            cos.getObjectUrl({
              Bucket: config.Bucket,
              Region: config.Region,
              Key: item.Key,
            }, function(err, data) {
              if (err) return console.log(err);
              setTimeout(() => {
                var downloadUrl = data.Url + (data.Url.indexOf('?') > -1 ? '&' : '?') + 'response-content-disposition=attachment'; // Add the parameter for a forced download
                window.open(downloadUrl); // This opens the URL in a new window. If you need to open the URL in the current window, you can use the hidden iframe for download, or use the <a> tag download attribute.
              }, 500);
            });
        });
        // If processing is not finished, continue to query the object list on the next page
        if (listResult.IsTruncated === 'true') getMultipleObjects(nextMarker);
    });
}
getObjects();
```
