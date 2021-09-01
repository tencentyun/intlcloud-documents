## Overview

This document provides an overview of APIs and SDK code samples related to basic bucket operations.


| API | Operation |  Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Checking a bucket and its permissions | Checks whether a bucket exists and whether you have permission to access it |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket from a specified account |



## Extracting a Bucket and its Permission

#### API description

This API (HEAD Bucket) is used to verify whether a bucket exists and whether you have permission to access it.

- If the bucket exists and you have permission to read it, HTTP status code 200 will be returned.
- If you do not have permission to read the bucket, HTTP status code 403 will be returned.
- If the bucket does not exist, HTTP status code 404 will be returned.

#### Use case

[//]: # (.cssg-snippet-head-bucket)
```js
cos.headBucket({
    Bucket: 'examplebucket-1250000000',                               /* Required */
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

| Parameter Name | Description                                                     | Type   |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |

## Deleting a Bucket

#### API description

This API (DELETE Bucket) is used to delete an empty bucket under a specified account. Note that if the deletion is successful, the HTTP status code "200" or "204" will be returned.

> ?Before deleting a bucket, please make sure that all the data and incomplete multipart uploads in the bucket have been cleared; otherwise, the bucket cannot be deleted.

#### Use case

[//]: # (.cssg-snippet-delete-bucket)
```js
cos.deleteBucket({
    Bucket: 'examplebucket-1250000000',                               /* Required */
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

| Parameter Name | Description                                                     | Type   |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Headers | Object |

