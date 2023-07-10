

This document provides an overview of APIs and SDK code samples related to logging.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | -------------------------- |
| [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/17054) | Setting logging | Enables logging for a source bucket |
| [GET Bucket logging](https://intl.cloud.tencent.com/document/product/436/17053) | Querying logging configuration | Queries the logging configuration of a source bucket |

## Setting Logging Configuration

#### Description

This API is used to enable logging for a source bucket and store the access logs in a specified destination bucket.

#### Method prototype

```
public Guzzle\Service\Resource\Model PutBucketLogging(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-logging)
```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

try {
    $result = $cosClient->putBucketLogging(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
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

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| Bucket | Source bucket for which logging is to be enabled, in the format of `BucketName-APPID`. For more information, please see [Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312). | String                                      |
| TargetBucket | Destination bucket to store logs, in the format of `BucketName-APPID`. For more information, please see [Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312). | String                                      |
| TargetPrefix | Path to the directory that stores logs in the destination bucket | String |

## Querying Logging Configuration

#### Description

This API is used to query the logging configuration of a specified bucket.

#### Method prototype

```
public Guzzle\Service\Resource\Model GetBucketLogging(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-logging)
```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
            
try {
    $result = $cosClient->getBucketLogging(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| Bucket | Source bucket in the format of `BucketName-APPID`. For more information, please see [Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312). | String |

#### Sample response

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

#### Response description

| Member Variable | Description | Type |
| ------------ | ------------------------ | ------ |
| TargetBucket | Destination bucket that stores logs     | String |
| TargetPrefix |  Path to the directory that stores logs in the destination bucket |  String |
