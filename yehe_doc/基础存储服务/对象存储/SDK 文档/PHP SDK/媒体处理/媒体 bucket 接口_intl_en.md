## Overview

This document provides an overview of APIs and SDK code samples for media processing activation status query.

| API | Description |
| ------------- |  ---------------------- |
| Querying media processing activation status | Queries media processing activation status |


## Querying Media Processing Activation Status

#### Feature description

This API is used to query buckets with media processing enabled.

#### Method prototype

```php
public Guzzle\Service\Resource\Model describeMediaBuckets(array $args = array());
```

#### Sample request

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; // Replace it with your real `secretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; // Replace it with your real `secretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; // Replace it with your real region information, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is `http` by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

try {
    $result = $cosClient->describeMediaBuckets(array(
        'Regions' => '', // Optional region information, such as `ap-shanghai` and `ap-beijing`. To specify multiple regions, separate them with commas
        'BucketNames' => '', // Optional bucket name. To specify multiple bucket names, separate them with commas. Exact search is supported.
        'BucketName' => '', // Optional bucket name prefix for prefix search
        'PageNumber' => 1, // Optional page number
        'PageSize' => 20, // Optional number of entries per page
    ));
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

`Request` has the following sub-nodes:

| Name | Description | Type | Required |
| :---------- | :----------------------------------------------------------- | :----- | :------- |
| regions     |  Region information, such as `ap-shanghai` and `ap-beijing`. To specify multiple regions, separate them with commas. For more information, see [Regions and Domain Names](https://intl.cloud.tencent.com/document/product/1045/33423). | string |  No    |
| bucketNames | Bucket name. To specify multiple bucket names, separate them with commas. Exact search is supported. | string | No |
| bucketName  | Bucket name prefix for prefix search.        | string |  No       |
| pageNumber  | Page number.                  |  string | No       |
| pageSize    | Number of entries per page.                | string | No       |

#### Sample response

```php
GuzzleHttp\Command\Result Object
(
    [RequestId] => NjI2MTE5OTlfNzgSxDxIHF0ZF8xZjk0MmQ=
    [ContentType] => application/xml
    [ContentLength] => 4744
    [TotalCount] => 51
    [PageNumber] => 1
    [PageSize] => 5
    [MediaBucketList] => Array
        (
            [0] => Array
                (
                    [BucketId] => examplebucket-1250000000
                    [Name] => examplebucket-1250000000
                    [Region] => ap-guangzhou
                    [CreateTime] => 2022-04-07T22:06:57+0800
                )

            [1] => Array
                (
                    [BucketId] => examplebucket-1250000000
                    [Name] => examplebucket-1250000000
                    [Region] => ap-guangzhou
                    [CreateTime] => 2022-04-07T22:06:57+0800
                )

            [2] => Array
                (
                    [BucketId] => examplebucket-1250000000
                    [Name] => examplebucket-1250000000
                    [Region] => ap-guangzhou
                    [CreateTime] => 2022-04-07T22:06:57+0800
                )

            [3] => Array
                (
                    [BucketId] => examplebucket-1250000000
                    [Name] => examplebucket-1250000000
                    [Region] => ap-guangzhou
                    [CreateTime] => 2022-04-07T22:06:57+0800
                )

            [4] => Array
                (
                    [BucketId] => examplebucket-1250000000
                    [Name] => examplebucket-1250000000
                    [Region] => ap-guangzhou
                    [CreateTime] => 2022-04-07T22:06:57+0800
                )

        )

    [Location] => ci.ap-guangzhou.myqcloud.com/mediabucket
)
```

