

## Overview

This document provides an overview of APIs and SDK code samples related to log management.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | -------------------------- |
| [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/17054) | Setting log management | Enables logging for the source bucket |
| [GET Bucket logging](https://intl.cloud.tencent.com/document/product/436/17053) | Querying log management | Queries the logging configuration information of the source bucket |

## Setting Log Management

#### Feature description

This API (PUT Bucket logging) is used to enable logging for the source bucket and store its access logs in a specified destination bucket.

#### Method prototype

```
put_bucket_logging(Bucket, BucketLoggingStatus={}, **kwargs):
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-logging)
```
response = client.put_bucket_logging(
    Bucket='examplebucket-1250000000',
    BucketLoggingStatus={
        'LoggingEnabled': {
            'TargetBucket': 'logging-bucket-1250000000',
            'TargetPrefix': 'string'
        }
    }
)
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ------ | -------- |
| Bucket            | Source bucket for which to enable the logging feature in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String | Yes |
| TargetBucket | Destination bucket where to store logs in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String | Yes |
| TargetPrefix | Specified path prefix in the destination bucket for storing logs | String | Yes |

#### Returned result description

The returned value of this method is None.

## Querying Log Management

#### Feature description

This API (GET Bucket logging) is used to query the log configuration information of a specified bucket.

#### Method prototype

```
get_bucket_logging(Bucket, **kwargs):
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-logging)
```
response = client.get_bucket_logging(
    Bucket='examplebucket-1250000000'
)
```

#### Parameter description                      

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket   | Destination bucket where to store logs in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String | Yes |

#### Returned result description

Log management configuration of the bucket in dict type.

```
{
    'LoggingEnabled': {
        'TargetBucket': 'logging-bucket-1250000000',
        'TargetPrefix': 'string'
    }
}
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| TargetBucket | Destination bucket where to store logs in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| TargetPrefix | Specified path prefix in the destination bucket for storing logs | String |
