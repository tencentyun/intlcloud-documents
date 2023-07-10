## Overview


This document provides an overview of APIs and SDK code samples related to log management.


| API | Operation | Description |
| --------------------------- | ------------ | -------- |
| [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/17054) | Setting log management | Enables logging for a source bucket |
| [GET Bucket logging](https://intl.cloud.tencent.com/document/product/436/17053) | Querying log management | Queries the logging configuration of a source bucket |


## Setting log management

#### Feature description

This API is used to enable logging for a source bucket and store its access logs in the specified destination bucket.

> Only the source bucket owner can make this request.

#### Sample request

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
| Bucket | Bucket for which log management is set in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| BucketLoggingStatus | Indicates the logging status. If it is null, logging is disabled.                            | Object     | Yes   |
| - LoggingEnabled             | Specific information on the bucket logging configuration, mainly for the destination bucket                                           | Object      | No   |
| - - TargetBucket             | Destination bucket that stores the logs. It can be the source bucket itself (although this is not recommended), or a bucket in the same account or region as the source bucket.                                           | String      | No   |
| - - TargetPrefix             | The specified path used to store logs in the destination bucket                                           | String      | No   |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description                                                     | Type   |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this is null. | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |

## Querying log management

#### Feature description

This API is used to query the logging configuration of a source bucket.

> Only the source bucket owner can make this request.

#### Sample request

```js
cos.getBucketLogging({
    Bucket: 'sourcebucket-1250000000',  /* Required */
    Region: 'ap-beijing',                                  /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Sample response

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
| Bucket | Bucket for which log management is queried in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```


| Parameter Name        | Description                                                  | Type          |
| --------------------- | ------------------------------------------------------------ | ------------- | 
| err                   | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object        |          
| - statusCode          | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number        |
| - headers             | Header information returned by the request                   | Object        |
| data                  | Data returned when the request is successful. If the request fails, this is null. | Object        |
| - statusCode          | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number        |
| - headers             | Header information returned by the request                   | Object        |
| - BucketLoggingStatus | Indicates the logging status. If it is null, logging is disabled. | Object/String |
| - - LoggingEnabled    | Specific information on the bucket logging configuration, mainly for the destination bucket | Object        |
| - - - TargetBucket    | Destination bucket that stores the logs. It can be the source bucket itself (although this is not recommended), or a bucket in the same account or region as the source bucket. | String        |
| - - - TargetPrefix    | The specified path used to store logs in the destination bucket | String        |

