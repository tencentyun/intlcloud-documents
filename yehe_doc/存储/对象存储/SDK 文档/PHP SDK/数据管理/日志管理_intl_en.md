

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
public Guzzle\Service\Resource\Model PutBucketLogging(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-logging)
```php
try {
    $result = $cosClient->putBucketLogging(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'LoggingEnabled' => array(
            'TargetBucket' => 'examplebucket2-1250000000',
            'TargetPrefix' => '', 
        )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| Bucket            | Source bucket for which to enable the logging feature in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String                                      |
| TargetBucket | Destination bucket where to store logs in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String                                      |
| TargetPrefix | Specified path in the destination bucket for storing logs | String|

## Querying Log Management

#### Feature description

This API (GET Bucket logging) is used to query the log configuration information of a specified bucket.

#### Method prototype

```
public Guzzle\Service\Resource\Model GetBucketLogging(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-logging)
```php
try {
    $result = $cosClient->getBucketLogging(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| Bucket            | Source bucket in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String                                      |

#### Sample return result

```php
GuzzleHttp\Command\Result Object
(
    [LoggingEnabled] => Array
        (
            [TargetBucket] => examplebucket2-1250000000
            [TargetPrefix] => 
        )

    [RequestId] => NWRmMWJjOThfMjZiMjU4NjRfODY4X2ExMjcy****
)
```

#### Returned result description

| Member Variable | Description | Type |
| ------------ | ------------------------ | ------ |
| TargetBucket | Destination bucket for storing logs | String |
| TargetPrefix | Path in the destination bucket for storing logs | String |
