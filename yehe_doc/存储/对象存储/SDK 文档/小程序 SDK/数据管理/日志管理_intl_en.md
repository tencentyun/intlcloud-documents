## Overview


This document provides an overview of APIs and SDK code samples related to logging.


| API | Operation | Description |
| --------------------------- | ------------ | -------- |
| [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/17054) | Setting logging configuration | Enables logging for a source bucket |
| [GET Bucket logging](https://intl.cloud.tencent.com/document/product/436/17053) | Querying logging configuration | Queries the logging configuration of a source bucket |


## Setting Logging Configuration

#### API description

This API is used to enable logging for a source bucket and store its access logs in the specified destination bucket.

>!Only the source bucket owner can request this operation.

#### Sample request 

Sample 1: configure the source bucket `sourcebucket-1250000000` so that its logs are delivered to the path `bucket-logging-prefix/` under the destination bucket `targetbucket-1250000000`.

[//]: # (.cssg-snippet-put-bucket-logging)
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

Sample 2: disable log delivery to the destination bucket `sourcebucket-1250000000`.

[//]: # (.cssg-snippet-put-bucket-logging-disable)
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
| Bucket | The name of the bucket for which to enable logging in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| BucketLoggingStatus | Indicates the logging status. If it is empty, logging is disabled.                            | Object     | Yes   |
| - LoggingEnabled             | Specifies information on the logging configuration, mainly for the destination bucket                                           | Object      | No   |
| - - TargetBucket             | Destination bucket that stores logs. It can be the source bucket itself (although this is not recommended), or a bucket in the same account or region as the source bucket.                                           | String      | No   |
| - - TargetPrefix             | The specified path prefix used to store logs in the destination bucket                                           | String      | No   |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------ |
| err | Returns a network or service error when the request fails. If the request is successful, this is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Returns headers | Object |
| data | Returns data when the request is successful. If the request fails, this is empty. | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Returns headers | Object |

## Querying Logging Configuration

#### API description

This API is used to query the logging configuration of a source bucket.

>!Only the source bucket owner can request this operation.

#### Sample request 

[//]: # (.cssg-snippet-get-bucket-logging)
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
| Bucket | The name of the bucket for which to query logging configuration in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ----------- |
| err | Returns a network or service error when the request fails. If the request is successful, this is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Returns headers | Object |
| data | Returns data when the request is successful. If the request fails, this is empty. | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Returns headers | Object |
| - BucketLoggingStatus | Indicates the logging status. If it is empty, logging is disabled.                            | Object     |
| - - LoggingEnabled             | Specifies information on the logging configuration, mainly for the destination bucket                                           | Object      |
| - - - TargetBucket             | Destination bucket that stores logs. It can be the source bucket itself (although this is not recommended), or a bucket in the same account or region as the source bucket.                                           | String      |
| - - - TargetPrefix             | The specified path prefix used to store logs in the destination bucket                                           | String      |
