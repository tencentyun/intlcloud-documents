## Overview

This document provides an overview of APIs and SDK sample codes related to cross-origin resource sharing (CORS).

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting CORS configuration | Sets the CORS permissions of bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying CORS configuration | Queries the CORS configuration of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting CORS configuration | Deletes the CORS configuration of a bucket |

## Setting CORS Configuration

#### Description

This API is used to set the CORS configuration of a specified bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model putBucketCors(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-cors)

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
    $result = $cosClient->putBucketCors(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'CORSRules' => array(
            array(
                'AllowedHeaders' => array('*',),
                'AllowedMethods' => array('PUT', ),
                'AllowedOrigins' => array('*', ),
                'ExposeHeaders' => array('*', ),
                'MaxAgeSeconds' => 1,
            ),  
            // ... repeated
        )   
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| -------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | Bucket for which CORS configuration is set, in the format of `BucketName-APPID`  | String      | Yes   |
| CORSRules      | Array  | CORS configuration list                                                 | Yes |
| CORSRule     | Array  | CORS configuration                                                | Yes |
| AllowedMethods | String | Allowed HTTP operations. Enumerated values: GET, PUT, HEAD, POST, DELETE       | Yes  |
| AllowedOrigins | String |  Allowed source origins. The wildcard `*` is supported. Format: `Protocol://domain name[:port]`, e.g. `http://www.qq.com` | Yes |
| AllowedHeaders | String | Custom HTTP request headers that can be included in subsequent `OPTIONS` requests sent. The wildcard `*` is supported. | No |
| ExposeHeaders  | String | Custom header information that can be received by the browser from the server | No |
| MaxAgeSeconds  | Int    | Validity period of the `OPTIONS` request result                      | No |
| ID             | String |  Rule ID | Yes |

## Querying CORS Configuration

#### Description

This API is used to query the CORS configuration of a bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model getBucketCors(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-cors)

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
    $result = $cosClient->getBucketCors(array(
        'Bucket' => 'examplebucket-1250000000' // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter | Type | Description | Required |
| -------- | ------ | -------------------------------------------- | -------- |
| Bucket | String | Bucket for which CORS configuration is queried, in the format of `BucketName-APPID` | Yes |

#### Sample response

```php
Guzzle\Service\Resource\Model Object
(
    [data:protected] => Array
        (
            [CORSRules] => Array
                (
                    [0] => Array
                        (
                            [ID] => 1234
                            [AllowedHeaders] => Array
                                (
                                    [0] => *
                                )
                            [AllowedMethods] => Array
                                (
                                    [0] => PUT
                                )
                            [AllowedOrigins] => Array
                                (
                                    [0] => http://www.qq.com
                                )
                        )
                )
            [RequestId] => NWE3YzhkMmRfMTdiMjk0MGFfNTQzZl8xNWUw****
        )
)
```

#### Response description

| Parameter Name | Type | Description | Parent Node | 
| -------------- | ------ | ------------------------------------------------------------ | --------- |
| CORSRules      | Array  | CORS configuration list                                                 |None |
| CORSRule     | Array  | CORS configuration                                                | CORSRules |
| AllowedMethods | String | Allowed HTTP operations. Enumerated values: GET, PUT, HEAD, POST, DELETE       | CORSRule |
| AllowedOrigins | String  | Allowed source origins. The wildcard `*` is supported. Format: `Protocol://domain name[:port]`, e.g. `http://www.qq.com` | CORSRule |
| AllowedHeaders | String | Custom HTTP request headers that can be included in subsequent `OPTIONS` requests sent. The wildcard `*` is supported. | CORSRule |
| ExposeHeaders  | String | Custom header information that can be received by the browser from the server | CORSRule |
| MaxAgeSeconds  | Int    | Validity period of the `OPTIONS` request result                      | CORSRule  |
| ID             | String |  Rule ID | CORSRule |

## Deleting CORS Configuration

#### Description

This API is used to delete the CORS configuration of a bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model deleteBucketCors(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-delete-bucket-cors)

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
    $result = $cosClient->deleteBucketCors(array(
        'Bucket' => 'examplebucket-1250000000' // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter | Type | Description | Required |
| -------- | ------ | ---------------------------------------------- | -------- |
| Bucket | String | Bucket for which CORS configuration is deleted, in the format of `BucketName-APPID` | Yes |
