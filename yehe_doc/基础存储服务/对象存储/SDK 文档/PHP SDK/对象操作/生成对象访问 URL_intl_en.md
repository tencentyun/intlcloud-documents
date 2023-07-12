## Overview

This document provides sample code for getting an object access URL.

## Getting an Object Access URL

#### Description

These code samples are used to obtain an object URL.

>?
> - To make the generated object URL a preview URL instead of a download URL, concatenate the `response-content-disposition=inline` parameter to the end of the obtained URL.
> - To make the generated object URL a download URL instead of a preview URL, concatenate the `response-content-disposition=attachment` parameter to the end of the obtained URL.
> 

#### Sample code

#### Sample 1
```php
// Obtain a signed download URL of an object.
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
    $bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
    $key = "exampleobject";  // Object key, the unique identifier of the object in the bucket
    $signedUrl = $cosClient->getObjectUrl($bucket, $key, '+10 minutes');
    // Request succeeded
    echo $signedUrl;
} catch (\Exception $e) {
    // Request failed
    print_r($e);
}
```

#### Sample 2

```php
// Obtain an unsigned download URL of an object for anonymous downloads or delivery.
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
    $bucket = 'examplebucket-125000000'; // Bucket in the format of BucketName-APPID
    $key = "exampleobject"; // Object key, the unique identifier of the object in the bucket
    $Url = $cosClient -> getObjectUrlWithoutSign($bucket, $key);
    // Request succeeded
    echo $Url;
} catch (\Exception $e) {
    // Request failed
    print_r($e);
}
```

>?For more samples, please see [Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/31544).

#### Parameter description

| Parameter | Description | Type | Required |
| ------- | ------------------------------------------------------------ | ------- | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID`. | String | Yes |
| Key | Object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| Expires | Validity duration of a signature. Default: 1,800 seconds                                  | String  | Yes  |

#### Response description

This method returns the object URL.
