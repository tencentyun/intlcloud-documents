## Overview

This document provides sample code for quickly checking whether a bucket exists.

The sample code actually calls the [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) COS API and is a simplified version of the API.

In addition to checking whether a bucket exists, `HEAD Bucket` also checks whether you have permission to access the bucket. Possible scenarios are as follows:

- If the bucket exists and you have permission to read it, HTTP status code 200 will be returned.
- If you do not have permission to read the bucket, HTTP status code 403 will be returned.
- If the bucket does not exist, HTTP status code 404 will be returned.


## Checking Whether a Bucket Exists

#### Feature description

This API is used to check whether a bucket exists.

#### Method prototype

```php
public Guzzle\Service\Resource\Model doesBucketExist(array $args = array());
```

#### Sample code

[//]: # ".cssg-snippet-object-exist"

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
    $result = $cosClient->doesBucketExist(
        'examplebucket-125000000'// Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
    ); ;
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```
