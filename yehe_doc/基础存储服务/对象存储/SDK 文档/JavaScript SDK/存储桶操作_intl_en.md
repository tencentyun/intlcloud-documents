## Overview

This document provides an overview of APIs and SDK code samples related to basic bucket operations.


| API | Operation |  Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Checking a bucket and its permissions | Checks whether a bucket exists and whether you have permission to access it |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket from a specified account |



## Checking a Bucket and Its Permissions

#### Description

This API is used to verify whether a bucket exists and whether you have permission to access it.

- If the bucket exists and you have permission to read it, HTTP status code 200 will be returned.
- If you do not have permission to read the bucket, HTTP status code 403 will be returned.
- If the bucket does not exist, the HTTP status code 404 will be returned.

#### Sample code

Extracting bucket information:

[//]: # (.cssg-snippet-head-bucket)
```js
cos.headBucket({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
}, function(err, data) {
    console.log(err || data);
});
```

Determining whether the bucket exists:

[//]: # (.cssg-snippet-head-bucket)
```js
function doesBucketExist() {
    cos.headBucket({
        Bucket: 'examplebucket-1250000000', /* Required */
        Region: 'COS_REGION',     /* Bucket region. Required */
    }, function(err, data) {
        if (data) {
            console.log('The bucket exists.');

        } else if (err.statusCode == 403) {
            console.log('no permission to read the bucket');
        }
    });
}
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID`. | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------ |
| err | Error code, which is returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |

## Deleting a Bucket

#### Description

This API is used to delete an empty bucket under a specified account. Note that if the deletion is successful, the HTTP status code 200 or 204 will be returned.

> ?Before deleting a bucket, please make sure that all the data and incomplete multipart uploads in the bucket have been cleared; otherwise, the bucket cannot be deleted.

#### Sample code

[//]: # (.cssg-snippet-delete-bucket)
```js
cos.deleteBucket({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID`. | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |

