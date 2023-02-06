## Overview

This document provides an overview of APIs and SDK code samples for querying the file preview feature status.

| API | Description |
| ------------------------------------------------------------ | ------------------------------------- |
|  [Querying file preview feature status](https://intl.cloud.tencent.com/document/product/436/46919)  | Queries whether the file preview feature is enabled for a bucket.  |


## Querying File Preview Feature Status

#### Feature description

This API is used to query the buckets with the file preview feature enabled.

#### Method prototype

```php
public Guzzle\Service\Resource\Model describeDocProcessBuckets(array $args = array());
```

#### Sample request

```php
<?php

require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual `region`, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //Protocol header, which is http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

try {
    // Query the file preview feature status. For more information, visit https://cloud.tencent.com/document/product/460/46945.
    $result = $cosClient->describeDocProcessBuckets(array(
        'Regions' => '', // Optional region information, such as `ap-shanghai` and `ap-beijing`. To specify multiple regions, separate them with commas
        'BucketNames' => '', // Bucket name (optional). To specify multiple bucket names, separate them by comma. Exact search is supported.
        'BucketName' => '', // Optional bucket name prefix for prefix search
        'PageNumber' => 1, // Optional page number
        'PageSize' => 20, // Optional number of entries per page
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Name | Description | Type | Required |
| :---------- | :----------------------------------------------------------- | :----- | :------- |
| Regions     | Region. Separate multiple regions by comma. Valid values: `All`, `ap-shanghai`, `ap-beijing`. | string | No       |
| BucketNames | Bucket name. Separate multiple bucket names by comma. Exact search is supported. | string | No |
| BucketName  | Bucket name prefix. Prefix search is supported.        | string | No |
| PageNumber  | Page number                  |  string | No       |
| PageSize  | Number of entries per page                 | string |No|

#### Sample response

```php
GuzzleHttp\Command\Result Object
(
    [RequestId] => NjMxMDcwZDlfAHDKAJHSDKJASHDKY3
    [ContentType] => application/xml
    [ContentLength] => 4600
    [TotalCount] => 59
    [PageNumber] => 1
    [PageSize] => 3
    [DocBucketList] => Array
        (
            [0] => Array
                (
                    [BucketId] => xxx-123
                    [Name] => xxx-123
                    [Region] => ap-chongqing
                    [CreateTime] => 2022-08-30T10:41:31+0800
                    [AliasBucketId] => 
                )

            [1] => Array
                (
                    [BucketId] => xxx-123
                    [Name] => xxx-123
                    [Region] => ap-chongqing
                    [CreateTime] => 2022-08-30T10:41:31+0800
                    [AliasBucketId] => 
                )

            [2] => Array
                (
                    [BucketId] => xxx-123
                    [Name] => xxx-123
                    [Region] => ap-chongqing
                    [CreateTime] => 2022-08-30T10:41:31+0800
                    [AliasBucketId] => 
                )

        )

    [Location] => ci.ap-guangzhou.myqcloud.com/docbucket
)
```



