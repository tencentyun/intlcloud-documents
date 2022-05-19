## Overview

This document provides sample code for quickly checking whether an object exists in a bucket. 

The sample code actually calls the [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) COS API and is a simplified version of the API.

In addition to checking whether an object exists, `HeadObject` returns object metadata. To view the SDK API that contains the full functionality of `HeadObject`, see [Querying Object Metadata](https://intl.cloud.tencent.com/document/product/436/37688).


## Querying Object Metadata

#### Feature description

This API is used to check whether an object exists in a bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model doesObjectExist(array $args = array());
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
    $result = $cosClient->doesObjectExist(
        'examplebucket-125000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'exampleobject' // Object name
    );
    // Request succeeded
    print_r($result);// Return boolean
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

