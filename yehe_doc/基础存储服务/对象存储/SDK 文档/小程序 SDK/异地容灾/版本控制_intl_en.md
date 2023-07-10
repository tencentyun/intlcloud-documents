## Overview

This document provides an overview of APIs and SDK code samples related to versioning.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets versioning configuration of a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning configuration of a bucket |

## Setting versioning

#### Feature description

This API is used to enable or suspend versioning for a bucket.

>
> 1. If you have never enabled versioning for the bucket, GET Bucket versioning will not return a versioning status.
> 2. Once enabled, versioning can only be suspended but cannot be disabled.
> 3. Set the versioning state value to `Enabled` or `Suspended` to enable or suspend versioning, respectively.
> 4. To set versioning for a bucket, you need to have write permission for the bucket.

#### Sample request

[//]: # (.cssg-snippet-put-bucket-versioning)
```js
cos.putBucketVersioning({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    VersioningConfiguration: {
        Status: "Enabled"
    }
}, function (err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ----------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket                           | Bucket for which versioning is enabled or suspended in the format: `BucketName-APPID`  | String      | Yes   |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| VersioningConfiguration | Defines the versioning configuration of the bucket | Object | Yes |
| - Status | Versioning status; enumerated values: `Enabled`, `Suspended` | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |

## Querying versioning

#### Feature description

This API is used to query the versioning configuration of a bucket.

#### Sample request

[//]: # (.cssg-snippet-get-bucket-versioning)
```js
cos.getBucketVersioning({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
}, function (err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket for which versioning is queried in the format: `BucketName-APPID`  | String      | Yes   |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Type |
| ------------------------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - VersioningConfiguration | Versioning configuration of the bucket | Object |
| - - Status | Versioning status; enumerated values: `Enabled`, `Suspended` | String |
