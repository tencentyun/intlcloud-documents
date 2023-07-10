## Overview

This document provides an overview of APIs and SDK code samples for checking a bucket.


| API | Operation |  Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Checking a bucket and its permissions | Checks whether a bucket exists and whether you have permission to access it |


## Checking a Bucket and Its Permissions

#### Feature description

This API (`HEAD Bucket`) is used to verify whether a bucket exists and whether you have permission to access it.

- If the bucket exists and you have permission to read it, HTTP status code 200 will be returned.
- If you do not have permission to read the bucket, HTTP status code 403 will be returned.
- If the bucket does not exist, HTTP status code 404 will be returned.

#### Method prototype

```php
public Guzzle\Service\Resource\Model headBucket(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-head-bucket)

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `secretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual `region`, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    $result = $cosClient->headBucket(array(
        'Bucket' => 'examplebucket-125000000' // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {

    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter | Parent Node | Description | Type | 
| -------- | ------ | ---------------------------------- | ------ |
| Bucket | None | Bucket name in the format of `BucketName-APPID` | String |