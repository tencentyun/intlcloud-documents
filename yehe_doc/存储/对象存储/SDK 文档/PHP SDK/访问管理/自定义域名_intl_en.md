
## Overview

This document provides an overview of APIs and SDK code samples related to custom domains.

| API | Operation | Description |
| ----------------- | -------------- | -------------------------- |
| PUT Bucket domain    | Setting a custom domain | Sets a custom domain for a bucket |
| GET Bucket domain    | Querying a custom domain | Queries the custom domain of a bucket |

## Setting Custom Domains

#### Description

This API is used to set a custom domain for a bucket.

#### Method prototype

```
public Guzzle\Service\Resource\Model PutBucketDomain(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-domain)
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
    $result = $cosClient->putBucketDomain(array( 
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket 
        'DomainRules' => array( 
            array( 
                'Name' => 'www.qq.com', 
                'Status' => 'ENABLED', 
                'Type' => 'REST', 
                'ForcedReplacement' => 'CNAME', 
            ),  
            // ... repeated 
        ),  
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
| ----------------- | ------------------------------------------------------------ | ------ |
| Bucket | Bucket for custom domain name configuration, in the format of `BucketName-APPID`. For more information, please see [Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| Name    | Custom domain name                                                                           | String      |
| Status | Status of the domain name. Valid values: `ENABLED`, `DISABLED` | String |
| Type    | Type of the origin server to bind. Valid values: `REST`, `WEBSITE`                                                             | String      |
| ForcedReplacement | Replaces existing configurations. Valid values: `CNAME`, `TXT`                    | String |

#### Error codes

The following describes some common errors that may occur when you call this API:

| Status Code | Description |
| -------------------------------------- | ------------------------------------------------------------ |
| HTTP 409 Conflict | The domain record already exists, and forced overwrite is not specified in the request; OR the domain record does not exist, and forced overwrite is specified in the request |
| HTTP 451 Unavailable For Legal Reasons | The domain does not have an ICP filing in the Chinese mainland                          |

## Querying a Custom Domain

#### Description

This API is used to query the custom domain set for a bucket.

#### Method prototype

```
public Guzzle\Service\Resource\Model GetBucketDomain(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-domain)
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
    $result = $cosClient->getBucketDomain(array( 
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
| Bucket | Bucket for custom domain name query, in the format of `BucketName-APPID`. For more information, please see [Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312). | String |

#### Sample response

```php
GuzzleHttp\Command\Result Object
(
    [DomainRules] => Array
        (
            [0] => Array
                (
                    [Status] => ENABLED
                    [Name] => www.qq.com
                    [Type] => REST
                )

        )
    [DomainTxtVerification] => tencent-cloud-cos-verification=9d2258433b1f38c7dd4b29fe272d2128
)
```

#### Response description

| Parameter | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------ |
| Name    | Custom domain name                                                                           | String      |
| Status | Status of the domain name. Valid values: `ENABLED`, `DISABLED` | String |
| Type    | Type of the origin server to bind. Valid values: `REST`, `WEBSITE`                                                             | String      |
| ForcedReplacement | Replaces existing configurations. Valid values: `CNAME`, `TXT`                    | String |
| DomainTXTVerification | Endpoint verification information. This field is an MD5 checksum of a character string in the format: <br>`cos[Region][BucketName-APPID][BucketCreateTime]`, where `Region` is the bucket region and `BucketCreateTime` is the time the bucket was created in GMT format | String |
