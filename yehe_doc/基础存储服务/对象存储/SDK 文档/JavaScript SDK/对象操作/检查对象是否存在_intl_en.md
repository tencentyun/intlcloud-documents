## Overview

This document provides an overview of the API and sample code for quickly checking whether an object exists in a bucket. The sample code actually calls the [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) COS API and is a simplified version of the API.

In addition to checking whether an object exists, `HEAD Object` returns object metadata. To view the SDK API that contains the full functionality of `HEAD Object`, please see [Querying Object Metadata](https://intl.cloud.tencent.com/document/product/436/37688).

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object. |

#### Description

The API is used to check whether an object exists in a bucket, which can be implemented by encapsulating the `cos.headObject` method.

#### Sample code

[//]: # (.cssg-snippet-head-object)
```js

function doesObjectExist() {
    cos.headObject({
        Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
        Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
        Key: '1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
    }, function(err, data) {
        if (data) {
            console.log('The object exists.');
        } else if (err.statusCode == 404) {
            console.log('The object does not exist.');
        } else if (err.statusCode == 403) {
            console.log('no permission to read the object');
        }
    });
}
```

#### Parameter description

| Parameter | Description | Type | Required |
| --------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID`. | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| IfModifiedSince | Required modification time. Metadata is returned only if the object has been modified after the specified time. Otherwise, `304` is returned. | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------- |
| err | Error code, which is returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404`. | Number |
| - headers | Headers. | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as `200` and `304`. `304` is returned if no modification is made after the specified time. | Number |
| - headers | Headers. | Object |
| - x-cos-object-type | Whether an object is appendable. Enumerated values: `normal`, `appendable`. The default value `normal` is not displayed. | String |
| - x-cos-storage-class | Storage class of the object, such as `STANDARD` (default), `STANDARD_IA`, `ARCHIVE`, and `DEEP_ARCHIVE`. For more information, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). Note that `STANDARD` is not displayed if returned. | String  |
| - x-cos-meta-\* | User-defined metadata. | String |
| - NotModified | Whether an object hasn’t been modified after the specified time. | Boolean |
| - ETag | MD5 checksum of the object. The value of `ETag` can be used to check whether the object was corrupted during the upload. <br>Example: `"09cba091df696af91549de27b8e7d0f6"` <br>**Note that double quotation marks are required at the beginning and the end**. | String |
| - VersionId       | Version ID of the uploaded object if versioning is enabled for its bucket. If versioning is not enabled, this parameter is not returned. | String  |
