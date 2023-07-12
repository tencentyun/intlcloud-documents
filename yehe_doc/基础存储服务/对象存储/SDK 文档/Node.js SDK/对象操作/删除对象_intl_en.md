## Overview

This document provides an overview of APIs and SDK code samples related to object deletion.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting an object | Deletes an object from a bucket. |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket in a single request |

### Deleting an object

#### Description

This API (`DELETE Object`) is used to delete an object from a COS bucket. To call this API, you must have write access to the bucket.

#### Sample code

[//]: # (.cssg-snippet-delete-object)
```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: '1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
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
| err | Error code, which is returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as `200`, `204`, `403`, and `404`. **If the deletion is successful or the object does not exist, `204` or `200` will be returned. If the specified bucket is not found, `404` will be returned.** | Number |
| - headers | Headers | Object |

### Deleting multiple objects

#### Description

This API (`DELETE Multiple Objects`) is used to delete multiple objects from a bucket. You can delete up to 1,000 objects in a single request. There are two response modes for you to choose from: `Verbose` and `Quiet`. The `Verbose` mode returns the deletion result of each object, whereas the `Quiet` mode returns only information about the objects that fail to be deleted.

#### Sample code

Deleting multiple files

[//]: # (.cssg-snippet-delete-multi-object)
```js
cos.deleteMultipleObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Objects: [
        { Key: '1.jpg' }, /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
        { Key: '2.txt' }, /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
    ]
}, function(err, data) {
    console.log(err || data);
});
```

Deleting multiple objects with a specified prefix (deleting files in the specified `a` directory)

```js
var deleteFiles = function (marker) {
    cos.getBucket({
        Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
        Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
        Prefix: 'a/',
        Marker:       marker,
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
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Quiet | Specifies whether to use the `Quiet` mode. If set to `true`, the `Quiet` mode is enabled. If set to `false` (default), the `Verbose` mode is enabled. | Boolean | No |
| Objects | List of objects to delete. | ObjectArray | Yes |
| - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| - VersionId | Version ID of the object or delete marker to delete. | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | Returns an HTTP status code, such as 200, 204, 403, and 404 | Number |
| - headers | Returns headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | Returns an HTTP status code, such as 200, 204, 403, and 404 | Number |
| - headers | Returns headers | Object |
| - Deleted | A list of objects that are successfully deleted | ObjectArray |
| - - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| - - VersionId | If the `VersionId` parameter is passed in, it will also be included in the response, indicating the version of the object or delete marker. | String |
| - - DeleteMarker | If versioning is enabled and the `VersionId` parameter is not specified, the deletion operation will not actually delete the object; instead, it will only add a delete marker, meaning that the visible object has been deleted. Enumerated values: `true`, `false` | String |
| - - DeleteMarkerVersionId | `VersionId` of the newly added delete marker if `DeleteMarker` is `true`.  | String |
| - Error | A list of objects whose deletion failed | ObjectArray |
| - - Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| - - Code | Error code of the deletion failure | String |
| - - Message | Error messages of the deletion failure | String |
