## Overview

This document provides an overview of APIs and SDK code samples related to restoring an archived object.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access. |

## Restoring an Archived Object 

#### Description

This API (`POST Object restore`) is used to restore an archived object for access.

#### Method prototype

```php
public Guzzle\Service\Resource\Model restoreObject(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-restore-object)

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
    $result = $cosClient->restoreObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'Days' => 10,
        'CASJobParameters' => array(
            'Tier' =>'Expedited'
        )    
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| ---------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key | String | Object key | Yes |
| Days | String | Number of days before the temporary copy expires | Yes |
| CASJobParameters | Array  | Restoration information | Yes |
| Tier | String | Restoration mode. For data in the ARCHIVE storage class, `Tier` can be set to `Expedited`, `Standard`, or `Bulk`. For data in DEEP ARCHIVE, `Tier` can be set to `Standard` or `Bulk`. | Yes |
