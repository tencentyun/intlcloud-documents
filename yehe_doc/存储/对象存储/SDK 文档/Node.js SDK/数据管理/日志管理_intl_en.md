## Overview


This document provides an overview of APIs and SDK code samples related to log management.


| API | Operation | Description |
| --------------------------- | ------------ | -------- |
| [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/17054) | Setting log management | Enables logging for a source bucket |
| [GET Bucket logging](https://intl.cloud.tencent.com/document/product/436/17053) | Querying log management | Queries the logging configuration of a source bucket |


## Setting Log Management

#### Feature

This API (PUT Bucket Logging) is used to enable logging for the source bucket and store its access logs in the specified destination bucket.

> Only the source bucket owner can make this request.

#### Request samples

Sample 1: Configure the source bucket `sourcebucket-1250000000` so that its logs are shipped to the path `bucket-logging-prefix/` under the destination bucket `targetbucket-1250000000`.

```js
cos.putBucketLogging({
    Bucket: 'sourcebucket-1250000000',  /* Required */
    Region: 'ap-beijing',                                  /* Required */
    BucketLoggingStatus: {              /* Required */
        LoggingEnabled: {
            TargetBucket: 'targetbucket-1250000000',
            TargetPrefix: 'bucket-logging-prefix/'
        }
    }
}, function(err, data) {
    console.log(err || data);
});
```

Sample 2. Disable log shipping on the destination bucket `sourcebucket-1250000000`.

```js
cos.putBucketLogging({
    Bucket: 'sourcebucket-1250000000',  /* Required */
    Region: 'ap-beijing',                                  /* Required */
    BucketLoggingStatus: {}             /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket | Bucket for which log management is set. Required format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| BucketLoggingStatus | Indicates the logging status. If it’s null, logging is disabled.                            | Object     | Yes   |
| - LoggingEnabled             | Information about the bucket logging configuration, mainly for the destination bucket                                           | Object      | No   |
| - - TargetBucket             | Destination bucket that stores the logs. It can be the source bucket (not recommended), or a bucket in the same account or region as the source bucket.                                           | String      | No   |
| - - TargetPrefix             | The specified path used to store logs in the destination bucket                                           | String      | No   |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------ |
| err | A returned request error (network error or service error). If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request succeeds. If the request fails, this is null. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

## Querying Log Management

#### Feature

This API (GET Bucket logging) is used to query the logging configuration of the source bucket.

> Only the source bucket owner can make this request.

#### Request samples

```js
cos.getBucketLogging({
    Bucket: 'sourcebucket-1250000000',  /* Required */
    Region: 'ap-beijing',                                  /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Sample Response

```json
{
    "BucketLoggingStatus": {
        "LoggingEnabled": {
            "TargetBucket": "targetbucket-1250000000",
            "TargetPrefix": "bucket-logging-prefix/"
        }
    },
    "statusCode": 200,
    "headers": {}
}
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket for which log management is queried. Required format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   | Required |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ----------- |
| err | A returned request error (network error or service error). If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request succeeds. If the request fails, this is null. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - BucketLoggingStatus                                                        | Indicates the logging status. If it’s null, logging is disabled.  | Object/String      |
| - - LoggingEnabled             | Information about the bucket logging configuration, mainly for the destination bucket                                           | Object      |
| - - - TargetBucket             | Destination bucket that stores the logs. It can be the source bucket (not recommended), or a bucket in the same account or region as the source bucket.                                           | String      |
| - - - TargetPrefix             | The specified path used to store logs in the destination bucket                                           | String      |
