This document provides an overview of APIs and SDK code samples related to lifecycles.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle configuration | Sets lifecycle for a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying a lifecycle configuration | Queries the lifecycle configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting a lifecycle configuration | Deletes the lifecycle configuration of a bucket |

## Setting a Lifecycle Configuration

#### Description

This API (PUT Bucket lifecycle) is used to set the lifecycle configuration for a bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model putBucketLifecycle(array $args = array());
```

#### Sample request

#### Sample 1: Delete all objects with a lifecycle of 1 day

[//]: # (.cssg-snippet-put-bucket-lifecycle)

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
    $result = $cosClient->putBucketLifecycle(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Rules' => array(
            array(
                'Expiration' => array(
                    'Days' => 1,
                ),
                'ID' => 'rule01',
                'Filter' => array(
                    'Prefix' => ''
                ),
                'Status' => 'Enabled',
            ),
        )
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}
```

#### Sample 2: Transition a prefixed object with a lifecycle of 1 day to ARCHIVE

[//]: # (.cssg-snippet-put-bucket-lifecycle-archive)

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
    $result = $cosClient->putBucketLifecycle(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Rules' => array(
            array(
                'ID' => 'rule01',
                'Filter' => array(
                    'Prefix' => 'prefix01/'
                ),  
                'Status' => 'Enabled',
                'Transitions' => array(
                    array(
                        'Days' => 1,
                        'StorageClass' => 'Archive'
                    ),
                ),  
            ),
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

| Parameter | Type | Description | Required |
| --------------------------- | ------------ | ------------------------------------------------------------ | ---- |
| Bucket                      | String       | Bucket for which the lifecycle is configured, in the format of `BucketName-APPID`                 | Yes   |
| Rules        | Array        | Lifecycle information list                                             | Yes |
| Rules        | Array        | Lifecycle configuration                                            | Yes |
| Expiration   | Array        | Object expiration rule. You can specify an expiration date (`Date`) or the number of days before the object expires (`Days`). | No |
| Transition   | Array        | Object storage class transitioning rule                               | No |
| NoncurrentVersionExpiration   | Array        | Expiration rule for historical objects   | No                    |
| NoncurrentVersionTransition | Array | Storage class transitioning rule for historica    | No        |
| Filter       | Array        | Objects to which the rule applies                               | Yes |
| Prefix | String | Prefix used to filter objects | Yes |
| Status | String | Whether to enable `Rule`. Valid values: `Enabled`, `Disabled` | Yes |
| ID             | String |  Rule ID | Yes |
| Days                        | Int          | Number of valid days before the rule takes effect                                                | No   |
| Date                        | Int / String | Date on which the rule takes effect                                               | No   |
| NoncurrentDays | Int | Number of valid days for a single-version object | No |
| StorageClass | String | Storage class to be transitioned to. Valid values: `STANDARD` (default), `STANDARD_IA`, `ARCHIVE`| Yes |

## Querying a Lifecycle Configuration

#### Description

This API (GET Bucket lifecycle) is used to query the lifecycle configuration of a bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model getBucketLifecycle(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-lifecycle)

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
    $result = $cosClient->getBucketLifecycle(array(
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
| Bucket   | String | Bucket for which the lifecycle is queried, in the format of `BucketName-APPID` | Yes       |

#### Sample response

```php
Guzzle\Service\Resource\Model Object
(
    [data:protected] => Array
        (
            [Rules] => Array
                (
                    [0] => Array
                        (
                            [ID] => id1
                            [Filter] => Array
                                (
                                    [Prefix] => documents/
                                )
                            [Status] => Enabled
                            [Transition] => Array
                                (
                                    [Days] => 200
                                    [StorageClass] => Standard_IA
                                )
                            [Expiration] => Array
                                (
                                    [Days] => 1000
                                )
                        )
                )
            [RequestId] => NWE3YzhlZjNfY2FhMzNiMGFfNDVkNF8yZDIxODE=
        )
)
```

#### Response description

| Parameter Name | Type | Description | Parent Node | 
| ------------ | ------------ | ------------------------------------------------------------ | ----------------------- |
| Rules        | Array        | Lifecycle configuration list                                             |None |
| Rules        | Array        | Lifecycle configuration                                          | Rules |
| Expiration   | Array        | Expiration rule for an object. You can specify an expiration date (`Date`) or the number of days before the object expires (`Days`). | Rule|
| Transition   | Array        | Object storage class transitioning rule                               | Rule |
| Filter       | Array        | Objects to which the rule applies                               | Rule |
| Prefix | String | Prefix used to filter objects | Filter |
| Status | String | Whether to enable `Rule`. Valid values: `Enabled`, `Disabled` | Rule |
| ID             | String |  Rule ID | Rule |
| Days         | Int          | Number of days before the rule takes effect                                              | Expiration / Transition |
| Date         | Int / String  |  Date on which the rule takes effect                                              | Expiration / Transition |
| StorageClass | String | Storage class to be transitioned to. Valid values: `STANDARD` (default), `STANDARD_IA`, `ARCHIVE`  | Transition |



## Deleting a Lifecycle Configuration

#### Description

This API is used to delete the lifecycle configuration of a bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model deleteBucketLifecycle(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-delete-bucket-lifecycle)

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
    $result = $cosClient->deleteBucketLifecycle(array(
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
| -------- | ------ | -------------------------------------------------- | -------- |
| Bucket   | String | Bucket for which the lifecycle configuration is deleted, in the format of `BucketName-APPID` | Yes       |
