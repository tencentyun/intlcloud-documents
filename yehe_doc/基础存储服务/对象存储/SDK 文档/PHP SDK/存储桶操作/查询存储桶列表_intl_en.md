## Overview

This document provides an overview of APIs and SDK code samples for querying a bucket list.

| API | Operation |  Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service (List Buckets)](https://intl.cloud.tencent.com/document/product/436/8291) | Querying a bucket list | Queries the list of all buckets under a specified account |

## Querying a Bucket List

#### Feature description

This API (`GET Service (List Buckets)`) is used to query the list of all buckets under a specified account.

#### Method prototype

```php
public Guzzle\Service\Resource\Model listBuckets();
```

#### Sample code

[//]: # (.cssg-snippet-get-service)

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual `region`, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

try {
    $result = $cosClient->listBuckets();
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample response

```php
Array
(
    [data:protected] => Array
        (
            [Owner] => Array
                (
                    [ID] => qcs::cam::uin/100000000001:uin/100000000001
                    [DisplayName] => 100000000001
                )

            [Buckets] => Array
                (
                    [0] => Array
                        (
                            [Name] => examplebucket-1250000000
                            [Location] => ap-beijing
                            [CreationDate] => 2016-07-29T03:09:54Z
                        )

                    [1] => Array
                        (
                            [Name] => examplebucket2-1250000000
                            [Location] => ap-beijing
                            [CreationDate] => 2017-08-02T04:00:24Z
                        )

                )

            [RequestId] => NWE3YzgxZmFfYWZhYzM1MGFfMzc3MF9iOGY5OQ==
        )

)
```

#### Response description

| Parameter | Parent Node | Description | Type | 
| ------------ | ------- | ---------------------- | ------ |
| Owner        | None      | Bucket owner information       | Array  |
| ID           | Owner   | Bucket owner ID      | String |
| DisplayName  | Owner   | Bucket owner name | String |
| Buckets      | None      | Bucket list             | Array  |
| Bucket       | Buckets | Bucket information             | Array  |
| Name        | Bucket  | Bucket name | String |
| Location   | Bucket  | Name of bucket region | String |                                     
| CreationDate | Bucket  |  Time of Bucket creation | String |
